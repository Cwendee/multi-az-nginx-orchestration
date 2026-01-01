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
The following screenshots illustrate the availability of both servers upon request through the Load Balancer. By accessing a single entry point (**18.214.23.84**), the traffic is seamlessly distributed.

| Request 1 (via LB) | Request 2 (via LB) |
|---|---|
| ![Traffic 01](images/lb-traffic-01.png) | ![Traffic 02](images/lb-traffic-02.png) |
| *Traffic routed to AZ us-east-1a* | *Traffic routed to AZ us-east-1b* |

### 🌐 Web Application Verification
The individual web pages below are displayed to illustrate High Availability (HA) across separate Availability Zones.

| App Server 01 (AZ: us-east-1a) | App Server 02 (AZ: us-east-1b) |
|---|---|
| ![Server 01](images/server-01.png) | ![Server 02](images/server-02.png) |

---

## 🛠️ Troubleshooting & Engineering Insights

### 1. The 504 Gateway Timeout (Connectivity "Wall")
**Issue:** After initial configuration, the Load Balancer returned a `504 Gateway Timeout`.
![LB Timeout Error](images/troubleshooting-lb-timeout.png)

### 2. Ansible Connection Timeout (SSH Locking)
**Issue:** During the final UI deployment, the terminal reported `UNREACHABLE` for the Load Balancer node (`lb01`).
![AWS Console Setup](images/aws-console-setup.png)

---

## 📈 Future Game Plan
- **Project 3:** Implement real-time monitoring using **Prometheus and Grafana**.
- **Project 4:** Refactor the entire infrastructure using **Terraform**.

## 🏗️ System Architecture
This project demonstrates a high-availability Nginx orchestration across multiple AWS Availability Zones.

![Multi-AZ Architecture](images/load-balancer-architecture.png)
