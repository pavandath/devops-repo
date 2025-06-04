# Building and packaging Maven code

## What is Maven?
- Maven is a OpenSource java based build tool
- Initially it is been developed by Sun MicroSystems, later acquired by Oracle.

### Introduction:
- Developers write code, but that code must be converted into a packaged format before delivering it to customers or deploying it to servers.
- In this section, we’ll understand how to build and package Java code.

### Basic Java Code Compilation:
- Java code is written in `.java` files and compiled into `.class` files using the `javac` command:

  - **Sample Java Program (HelloWorld.java):**
  ```java
  class HelloWorld {
      public static void main(String[] args) {
          System.out.println("Hello, World!");
      }
  }
  ```
  ```bash
  javac HelloWorld.java
  ```
  - This generates the `.class` file (bytecode).

  ```bash
  java HelloWorld
  ```
  - The bytecode is then executed using the `java` command:


- **Challenges in Enterprise Projects:**
  - In larger projects with multiple Java files, managing compilation and building `.jar` files manually becomes complex.

---

# Introduction to Maven

### What is Maven?
- Maven is a powerful build automation tool primarily used for Java projects.
- It simplifies project management by automating the process of:
  - Project builds
  - Dependency management
  - Documentation
  - Reporting

### Why Use Maven?
- **Automation**: It handles the build process, from compilation to packaging and deployment.
- **Dependency Management**: Automatically manages third-party libraries and dependencies.
- **Standardized Structure**: Enforces a consistent project directory structure.
- **Lifecycle Management**: Provides a structured lifecycle for managing the build, testing, and deployment phases.

---

# Various Build Tools

### A quick overview of popular build tools used in the industry:
- **Apache ANT**: XML-based build automation.
- **Gradle**: Flexible build system, supporting Java, Kotlin, and more.
- **Apache Maven**: The tool we will focus on in this course.

---

# Apache Maven: A Software Project Management Tool

### Introduction to Maven (continued):
- Maven is a tool that follows the principle of **Convention over Configuration**.
- It automates the building, packaging, and dependency management of projects, making it easier to manage complex projects.

### Types of Applications and Their Packaging:
- **Standalone Applications**:
- If you have only compilation files
  - Packaged as `.jar` files.
  - A `.jar` file contains compiled `.class` files and a manifest file.
- **Web Applications**:
- If you have ui files
  - Packaged as `.war` files.
  - Includes `.jar` files along with web content like HTML, CSS, JavaScript, and images.
- **Enterprise Applications**:
  - Packaged as `.ear` files.
  - Combines multiple `.jar` and `.war` files along with additional resource files.

- These jar war and ear are called as artificats and these are deployed where ever we want


### Maven in Action:
  ```bash
  javac HelloWorld.java
  java HelloWorld
  ```
  - **Concepts:**
    - **Source Code** → `helloworld.java`
    - **Byte Code** → `helloworld.class`
    - **JVM (Java Virtual Machine)** → Executes the bytecode.

---

### Both Java and Docker build, package and deploy application then what is the difference:
- Docker simply says tp build , share, run and test 
- Where as, maven says that in local there will be source code and build this using maven commands it will generate .jar this can be placed in centralized location or artifacts registry and deploy this in the server
- In docker we create image and this goes to registry 
- java code is running in local machine not in server may be there are no dependencies so we need to install dependencies in server required by .jar file
- where as in docker we create .jar + dependecies into a image and run it as container
- so simply in docker artifact is an image
- whereas in Maven artifact is .jar and .war
- but in image will also have jar and war but along with dependencies
