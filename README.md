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

## There you see the difference. It is almost a 99.7% reduction in the size of the docker image, proving its efficiency.
