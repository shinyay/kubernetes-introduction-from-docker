# Chapter 1: Creating Docker Containers

In this chapter, we’ll dive into the basics of Docker, the foundation of modern containerized applications. You'll learn how to create, manage, and run Docker containers, which are essential building blocks for Kubernetes.

---

## Chapter Objectives

- Understand the core concepts of Docker and containers
- Learn how to write a `Dockerfile` to containerize an application
- Build and run Docker containers locally
- Manage Docker images and containers effectively

---

## Cartoon Introduction 🎨

**Illustration:**
Captain Kube holding a small box labeled "Container," explaining to our protagonist that it contains everything needed to run their application.

---

## 1-1. What is Docker?

Docker is a platform that simplifies the process of building, running, and managing containers. Containers package applications and their dependencies into a single unit that can run reliably across different computing environments.

### Key Features:
- Lightweight and fast
- Portable and consistent across environments
- Secure by isolating applications

**Illustration:**
Captain Kube showcasing a "containerized" app that runs seamlessly on different machines.

---

## 1-2. Writing Your First Dockerfile

A `Dockerfile` is a script of instructions that tells Docker how to build an image. Here's a simple example:

```dockerfile
# Use a lightweight base image
FROM node:14

# Set the working directory
WORKDIR /app

# Copy application files
COPY package*.json ./
RUN npm install
COPY . .

# Expose the application port
EXPOSE 3000

# Command to run the application
CMD ["node", "app.js"]
```

**Illustration:**
Captain Kube writing a `Dockerfile` with a checklist of instructions.

---

## 1-3. Building and Running Docker Containers

### Steps:

1. Build the Docker image:
   ```bash
   docker build -t my-app .
   ```

2. Run the container:
   ```bash
   docker run -p 3000:3000 my-app
   ```

3. Stop and remove the container:
   ```bash
   docker ps
   docker stop <container-id>
   docker rm <container-id>
   ```

**Illustration:**
Captain Kube starting a container and showing it running with a happy green light.

---

## 1-4. Managing Docker Images and Containers

### Docker Commands:

- List images:
  ```bash
  docker images
  ```
- Remove an image:
  ```bash
  docker rmi <image-id>
  ```
- List running containers:
  ```bash
  docker ps
  ```
- List all containers:
  ```bash
  docker ps -a
  ```

**Illustration:**
Captain Kube organizing a shelf of labeled "images" and "containers."

---

## Chapter Summary & Key Takeaways

- Docker simplifies the process of building and running containers.
- A `Dockerfile` defines the steps to build a Docker image.
- Containers are portable and consistent across environments.
- Docker commands help manage images and containers efficiently.

**Illustration:**
Captain Kube awarding a "Docker Basics" badge to the protagonist.

---

**Quiz Yourself 🤔**
- What is the purpose of a `Dockerfile`?
- How do you expose a port in a Docker container?
- Which command lists all running containers?

---

Congratulations! 🎉 You’ve successfully completed Chapter 1. Next, we’ll explore how to create a Kubernetes cluster in Chapter 2.
