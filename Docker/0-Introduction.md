# Introduction to Generations of Application Deployment

## Gen 1 - Bare Metal Servers
- In Gen 1, one physical machine (e.g., 8 CPUs, 32 GB RAM) was used to run **a single application**.
- There was **no virtualization**, and system resources were underutilized.

## Gen 2 - Virtual Machines (VMs)
- A **hypervisor** (like VMware, KVM, or Hyper-V) runs on a single physical server.
- It can host **multiple guest VMs**, each with its **own OS** and dependencies.
- Each VM consumes significant resources, even if the application (like a Java `.jar`) doesn't need much.

## Gen 3 - Containers
- A **Container Runtime (CRT)** (like Docker Engine, containerd) runs directly on the host OS.
- Containers are lightweight and share the **host OS kernel**.
- You can run **multiple containerized applications** efficiently using fewer resources.

---

## What is a Container?

- A Docker container is a standardized, executable software package that includes everything an application needs to run, such as code, runtime, system tools, libraries, and configuration files.
- Containers are a technology that allows you to run softwares on a variety of systems, starting from developers systems to production systems 
- Containers are all about portable softwares

- **Benefits:**
  - Portability (runs the same on any system)
  - Lightweight (does not include a full OS)
  - Scalable (easy to replicate and manage)

---

## What is Docker?

- Docker is a platform that allows you to **build, share, run, and manage containers**.
- It simplifies application deployment without worrying about system setup.

## Docker Objects?
- images
- containers
- registry
- network
- volume


### Docker Workflow:
```text
Dockerfile 
   ↓ Build
Docker Image (artifact)
   ↓ Push
Docker Registry (Docker Hub or private)
   ↓ Pull
Container Runtime
   ↓ Run
Docker Container


