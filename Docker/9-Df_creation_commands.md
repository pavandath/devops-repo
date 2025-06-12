- FROM - It defines the starting point for the new image, typically an operating system or a pre-configured environment.
- RUN - Used to run any packages
- CMD - Specify default commands.
- COPY - Copy files from source to destination
- LABEL - Tells who is the owner, simply metadata
- ENV - if you want to give values dynamically during the run time 
    - LABEL developer="pavan"
      LABEL owner = "pavan"
      docker image inspect lavel:v1
        "Labels": {
                "dev": "pavan",
                "for": "practice",
                "org.opencontainers.image.ref.name": "ubuntu",
                "org.opencontainers.image.version": "18.04"
            },
- ARG - It can be used to change the arguments during the image creation
    - FROM ubuntu:18.04
      RUN apt update -y && apt install openjdk-8-jdk -y && apt install wget -y
      ARG SRC_DIR=/tmp/java
      RUN mkdir -p $SRC_DIR
      WORKDIR $SRC_DIR
      ADD https://storage.googleapis.com/sivak8dpublicrepo/spring-petclinic-2.4.5.jar $SRC_DIR/spring-petclinic.jar 
      EXPOSE 8080
      CMD ["java", "-jar", "spring-petclinic.jar"]
    - docker build -t arg:v1 --build-arg SRC_DIR=/opt .

- WORKDIR - Change working directory



## Diff between ADD and COPY
- Both are same but add does some more functionalities those are:
    - if we copy a .tar file copy only copies it but add will untar it too
    - ADD will also download remote files

-  for deploying something like node applications or to reduce size of the docker file there is a concept called multi-stage docker file 
- here in first stage we keep something known as builder and from that build application in second stage we use that build to run 

# 🐳 Multi-Stage Dockerfile

When deploying applications like Node.js, Java, or Go, you often want to:

- Build the app (e.g., compile TypeScript or install dev dependencies).
- Then **deploy only the necessary artifacts** (like the `dist/` folder or built binary) in a smaller runtime image.

This is where **multi-stage builds** come in handy.

---

## 🔧 Why Multi-Stage Builds?

- 🚀 Reduce Docker image size.
- 🔐 Exclude development dependencies and sensitive files.
- 🧹 Keep final images clean, fast, and secure.

---

## 🧱 Example: Node.js Application

### Step-by-step Dockerfile:

```dockerfile
# === Stage 1: Builder ===
FROM node:18 AS builder
WORKDIR /app

# Copy and install all dependencies
COPY package*.json ./
RUN npm install

# Copy the rest of the code and build
COPY . .
RUN npm run build

# === Stage 2: Runtime ===
FROM node:18-slim
WORKDIR /app

# Only copy built files and production dependencies
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/package*.json ./

RUN npm install --only=production

CMD ["node", "dist/index.js"]


# 🐳 Docker ENTRYPOINT: Shell Form vs Exec Form

## 📌 Overview

Docker provides two ways to define the `ENTRYPOINT` in a Dockerfile:

| Feature                  | Shell Form                            | Exec Form                                        |
|--------------------------|----------------------------------------|--------------------------------------------------|
| Syntax                   | `ENTRYPOINT echo "Hello $name"`        | `ENTRYPOINT ["/bin/bash", "-c", "echo Hello $name"]` |
| Shell involved           | Yes (`/bin/sh -c`)                    | Optional (you must specify shell if needed)      |
| Env Variable Expansion   | ✅ Yes                                 | ✅ Yes (only if shell like bash is invoked)      |
| Signal Handling          | ❌ Poor (PID 1)                        | ✅ Better (PID 1 receives signals directly)       |
| Runtime Argument Override| ❌ Hard                               | ✅ Easy                                           |
| Simplicity               | ✅ Simple                             | ⚠️ Slightly verbose                              |

---

## 🧪 Shell Form Example

```dockerfile
# Dockerfile
FROM ubuntu
ENV name=ShellForm
ENTRYPOINT echo "Hello $name"

#Behavior:
#Docker interprets this as:
#/bin/sh -c 'echo "Hello $name"'

#$name will be expanded correctly.
#But signal handling is not ideal.
# Dockerfile Exec form
FROM ubuntu
ENV name=ExecForm
ENTRYPOINT ["/bin/bash", "-c", "echo Hello $name"]
$name is expanded because bash is invoked.

Signal handling is clean.

Preferred in production Dockerfiles.

#incorrect exec form

# Dockerfile
FROM ubuntu
ENV name=BrokenForm
ENTRYPOINT ["echo", "Hello $name"]
Behavior:
$name is not expanded.

Output: Hello $name (literal string)

Because echo is not run in a shell that understands $name.




# 🚀 CMD vs ENTRYPOINT in Docker

## 🔍 Overview

| Feature                    | CMD                                        | ENTRYPOINT                                  |
|----------------------------|--------------------------------------------|---------------------------------------------|
| Purpose                    | Provides default arguments for the container | Defines the main command to run             |
| Overridable by `docker run`| ✅ Yes (fully)                             | ⚠️ Only arguments (if in exec form)         |
| Use Case                  | Provide defaults that users can override    | Force a command to always run               |
| Typical Use               | Set default arguments or scripts            | Set the core executable of the container    |

---

## 🧪 Example 1: CMD only

```dockerfile
FROM ubuntu
CMD ["echo", "Hello from CMD"]
```

### Run:

```bash
docker build -t cmd-example .
docker run cmd-example
# Output: Hello from CMD

docker run cmd-example echo "Overridden!"
# Output: Overridden!
```

✅ **CMD can be completely overridden at runtime**

---

## ⚙️ Example 2: ENTRYPOINT only

```dockerfile
FROM ubuntu
ENTRYPOINT ["echo", "Hello from ENTRYPOINT"]
```

### Run:

```bash
docker build -t entrypoint-example .
docker run entrypoint-example
# Output: Hello from ENTRYPOINT

docker run entrypoint-example "Overridden!"
# Output: Hello from ENTRYPOINT Overridden!
```

✅ **ENTRYPOINT is fixed**, args are appended

---

## 🔁 Example 3: ENTRYPOINT + CMD

```dockerfile
FROM ubuntu
ENTRYPOINT ["echo"]
CMD ["Hello from both"]
```

### Run:

```bash
docker build -t combo-example .
docker run combo-example
# Output: Hello from both

docker run combo-example "Overridden CMD"
# Output: Overridden CMD
```

✅ **ENTRYPOINT runs always**, `CMD` acts as default arguments

---

## 🧠 Key Differences

| Question                                | CMD                              | ENTRYPOINT                         |
|-----------------------------------------|----------------------------------|------------------------------------|
| Can I override it with `docker run`?    | ✅ Yes, completely                | ⚠️ Only CMD part (arguments)       |
| Is it used as the main process?         | ❌ No, unless ENTRYPOINT is unset| ✅ Yes                             |
| Common Use Case                         | Set default args, shell scripts  | Run apps like `nginx`, `java -jar`|

---

## ✅ Best Practices

- Use `CMD` when you want to provide **default args**.
- Use `ENTRYPOINT` when your container has **one main job** (e.g., run a server or executable).
- Combine both for **flexibility + control**.

```dockerfile
ENTRYPOINT ["java", "-jar"]
CMD ["app.jar"]
```

---

- If we have multiple cmds then third one will execute which is last one has highest priority
FROM ubuntu

CMD echo "First"
CMD echo "Second"
CMD echo "Third"
```

### Output on container run:
```
Third
