# Lab 24 Multi-branch Pipeline with Shared Library & K8s Deployment

## 📌 Project Overview

This project demonstrates a professional **CI/CD Multibranch Pipeline** implementation using Jenkins. It automates the process of discovering multiple branches, building Java applications, containerizing them, and deploying each environment into a dedicated **Kubernetes Namespace**.

## 🏗 System Architecture

* **Source Control:** GitHub (Multibranch repository structure).
* **Orchestration:** Jenkins (Master-Slave architecture).
* **Build Slave:** Dedicated **Linux Agent Node** configured with multiple executors for parallel processing.
* **Standardization:** **Jenkins Shared Library** used to centralize pipeline logic.
* **Registry:** Docker Hub for storing branch-specific images.
* **Deployment:** Kubernetes (Minikube) using dynamic namespaces.

## 🚀 Key Features

### 1. Dynamic Environment Provisioning

The pipeline identifies the branch name and maps it to a specific Kubernetes Namespace.

* **Main Branch:** Deployed to `main` namespace.
* **Dev Branch:** Deployed to `dev` namespace.
* **Staging Branch:** Deployed to `stag` namespace.
* **Production Branch:** Deployed to `prod` namespace.
  
### 2. Scalable Build Infrastructure (Agent & Executors)

* Configured a **Linux Slave Node** to handle all build workloads.
* Enabled **Parallel Execution** by increasing the number of executors, allowing multiple branches to build and deploy simultaneously without queuing.

### 3. Reusable Shared Library in Repository: https://github.com/noura-abdelnabi/SahredLibrary-NTI.git

* Implemented a custom Groovy library to maintain a "DRY" (Don't Repeat Yourself) Jenkinsfile.
* Centralized stages: **Checkout**, **Maven Build**, **Docker Build/Push**, and **K8s Deploy**.

### 4. Advanced Troubleshooting & Optimization

* **GitHub API Management:** Successfully implemented **Secret Text PAT** to resolve rate-limiting issues, increasing quota from 60 to 5000 requests.
* **Docker Service Management:** Optimized Docker socket and service stability on the agent node for high-concurrency builds.

---

## 📸 Proof of Implementation (Screenshots)

### 1. The Multibranch Dashboard

>
> <img width="1617" height="364" alt="PIPELINES SUCCESS" src="https://github.com/user-attachments/assets/c5e0c796-761e-4299-bf70-420a196b2a64" />


### 2. Shared Library & Agent Config

>
> <img width="1646" height="762" alt="SHARED LIBRARY CONFIGURATION" src="https://github.com/user-attachments/assets/c38d1840-8db6-46d8-ad6b-281ec1ea043a" />
>
> <img width="775" height="436" alt="LINUX AGENT" src="https://github.com/user-attachments/assets/a9802aa2-aa2c-4dd7-9ba1-5afb4239cba6" />


### 3. Docker Hub Registry

>
> <img width="952" height="816" alt="DOCKER HUB IMAGE WITH TAGS" src="https://github.com/user-attachments/assets/fa2b2230-8980-4801-a547-688de5781735" />


### 4. Kubernetes Resources

>
> <img width="836" height="390" alt="PODS IN NAMESPACES" src="https://github.com/user-attachments/assets/8dd7b605-c91d-41fc-b9b1-7055928a3eb3" />


---

## 🛠 How to Use

1. **Define Library:** Add the Shared Library in Jenkins System settings.
2. **Setup Credentials:** Add Docker Hub (User/Pass), GitHub (Secret Text), and Kubeconfig (Secret File).
3. **Scan Repository:** Run the Multibranch Scan to discover branches and trigger builds.
