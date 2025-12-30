# Multi-AZ Nginx Orchestration with Ansible

A high-availability web architecture deployed on AWS using Ansible for automated configuration management. This project demonstrates the ability to design, provision, and orchestrate a distributed system that remains resilient and secure.

## 🏗️ Architecture
- **Infrastructure:** Custom AWS VPC across 2 Availability Zones (AZs) for fault tolerance.
- **Load Balancer:** 1 Ubuntu EC2 instance running Nginx as a Reverse Proxy.
- **Web Tier:** 2 Ubuntu EC2 instances serving unique content to verify load distribution.
- **Automation:** Ansible playbooks for zero-touch deployment and configuration.



## 🚀 Key Features
- **High Availability:** Distributed nodes across multiple AZs to prevent single points of failure.
- **Security:** Layered Security Groups (LB accepts public HTTP/SSH; App Nodes are restricted to internal traffic).
- **Idempotent Automation:** Ansible logic ensures the environment stays in the desired state across all nodes.

## 🛠️ Tech Stack
- **Cloud:** AWS (EC2, VPC, IGW, Route Tables)
- **Configuration Management:** Ansible
- **Web Server:** Nginx (Reverse Proxy + Web)
- **OS:** Ubuntu 24.04 LTS

---

### 🔍 Verification & Traffic Distribution
The following screenshots demonstrate the Load Balancer in action. By accessing a single entry point (**18.214.23.84**), the traffic is distributed across different backend nodes in separate Availability Zones.

| Request 1 (Server 01) | Request 2 (Server 02) |
|---|---|
| ![App Server 01](images/server-01.png) | ![App Server 02](images/server-02.png) |
| *Served from us-east-1a* | *Served from us-east-1b* |

### 🌐 Load Balancer Verification
The screenshots below demonstrate the Nginx Load Balancer successfully distributing traffic across both Availability Zones. Note that the IP address in the browser remains constant while the backend server toggles.

| App Server 01 (AZ: us-east-1a) | App Server 02 (AZ: us-east-1b) |
|---|---|
| ![Server 01](server-01.png) | ![Server 02](server-02.png) |

---

## 🛠️ Troubleshooting & Engineering Insights

In a production-like environment, things rarely go perfectly. Below are the technical challenges encountered during this build and how they were resolved.

### 1. The 504 Gateway Timeout (Connectivity "Wall")
**Issue:** After initial configuration, the Load Balancer returned a `504 Gateway Timeout`.
**Diagnosis:** I used `curl` and browser tests to identify that while the LB was alive, it couldn't "see" the app servers. I traced this to a **Security Group mismatch**—the web nodes were blocking traffic on Port 80.
**Resolution:** Updated the Web Tier Security Group to allow Inbound HTTP traffic (Port 80) specifically from the Load Balancer's Security Group, restoring the flow of traffic while maintaining a "Least Privilege" security posture.
![LB Timeout Error](images/troubleshooting-lb-timeout.png)

### 2. Ansible Connection Timeout (SSH Locking)
**Issue:** During the final UI deployment, the terminal reported `UNREACHABLE` for the Load Balancer node (`lb01`).
**Diagnosis:** This was a classic "Control Plane" vs. "Data Plane" issue. My local ISP had rotated my Public IP, and since the AWS Security Group was (correctly) locked down to "My IP" for SSH, Ansible was blocked.
**Engineering Takeaway:** I chose to document this error rather than hide it. It highlights a successful security implementation—the "gate" was locked exactly as intended. I updated the Security Group rule to my new IP to regain management access, while the **Data Plane** (the website itself) remained 100% available to users throughout the lockout.
![AWS Console Setup](images/aws-console-setup.png)

---

## 📈 Future Game Plan
- **Project 3:** Implement real-time monitoring using **Prometheus and Grafana** to visualize traffic distribution.
- **Project 4:** Refactor the entire infrastructure using **Terraform** for full Infrastructure as Code (IaC) compliance.