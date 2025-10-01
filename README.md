# 🚀 Docker Multi-Stage Build Example

With **multi-stage builds**, you can separate the **build environment** from the **runtime environment**, enabling you to compile and package your application in one stage and then copy the resulting artifacts into a lightweight runtime image in another stage.

---

## 🔹 What is a Multi-Stage Build?

- **Stage 1 (Build stage):**  
  Installs dependencies, copies source code, and builds the application.

- **Stage 2 (Runtime stage):**  
  Uses a lightweight image for the runtime environment. It copies the built artifacts from the build stage and installs only production dependencies.  

---

## 🍕 Pizza Analogy

Think of Docker multi-stage builds like making pizza:

- **Build Stage (Kitchen):**  
  - Set up a full kitchen with tools & ingredients  
  - Prepare dough & toppings (compile the application)  
  - Output: A ready-to-bake pizza (compiled binary)

- **Runtime Stage (Pizza Box):**  
  - Use a clean, minimal pizza box (lightweight base image)  
  - Place the prepared pizza in the box (copy the compiled binary)  
  - Set instructions for serving the pizza (define entrypoint)

👉 Final result: A lightweight image containing only what’s needed (like a pizza delivered in a clean box without the kitchen mess).

---

## ⚡ How to Try It

### 1. Build without Multi-Stage
```bash
cd dockerfile-without-multistage
docker build -t without_calc .
```
### 2. Build with Multi-Stage
```bash
cd dockerfile-with-multistage
docker build -t with_calc .
```
### docker images 
<img width="1027" height="145" alt="Untitled-2024-08-12-0305" src="https://github.com/user-attachments/assets/11a27f36-3250-4c0e-ad20-c52f0d60bc6b" />

### There you see the difference. It is almost a 99.7% reduction in the size of the docker image, proving its efficiency.



---


# 📦 Docker Volumes and Data Persistence

## Why Do We Need Volumes?

👉 All the log data of your application is stored in the container. If the container goes down, you lose all the crucial log data.  

👉 Example: Imagine, Github hosted its **front-end** on one container and the **back-end(DB)** on another container. The data in the **back-end(codes)** is served to the **front-end** for the user to access and read it. Now, if the **back-end** container goes down, viewers on Github will not be able to see the their codes.

❌ **No company would afford to lose such data.**  
✅ That’s why it’s important to store the data **outside the container’s lifecycle** using **Docker Volumes**.

---

## 🔑 Docker Volumes vs Bind Mounts

### **Docker Volumes**
- **Managed by Docker**: Easy to create, manage, and back up.
- **Persistent Storage**: Data survives even after the container stops or is deleted.
- **Efficient & Fast**: Better performance compared to bind mounts.
- **Recommended for Production**: Best choice for scalable and reliable data persistence.

👉 Example: Now, Github can store all the code in a **DB container with Docker volumes attached**.  
Even if the container stops or restarts, the data will remain safe and available.

---

## ⚙️ Docker Volume Commands

### Show all available options
```bash
docker volume --help
```
## ⚙️ Basic Docker Volume Commands
### 1. Create a Docker Volume
```bash
docker volume create <volume_name>
```
### 2. Run a Container with a Volume (Method 1: -v flag) / (Method 2: --mount)
```bash
docker run -it -v <volume_name>:<container_path>[:options] <image>
docker run -it --mount source=<volume_name>,target=<container_path>[,options] <image>
```
While creating the volume, Docker creates the volume path by default. The -v flag mounts the volume to a directory inside the container. This ensures that the container’s data is stored in the Docker volume.

### 3. Inspect a Volume
```bash
docker volume inspect <volume_name>
```


- Containers are temporary, but Volumes are permanent.
- Volumes ensure that important data (like logs, DB files, blogs, etc.) is not lost when a container crashes.
- Always use Volumes in production for databases and persistent storage needs.
