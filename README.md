# Multi-AZ Nginx Orchestration with Ansible

A high-availability web architecture deployed on AWS using Ansible for automated configuration management.

## 🏗️ Architecture
- **Infrastructure:** Custom AWS VPC across 2 Availability Zones (AZs) for fault tolerance.
- **Load Balancer:** 1 Ubuntu EC2 instance running Nginx as a Reverse Proxy.
- **Web Tier:** 2 Ubuntu EC2 instances serving unique content to verify load distribution.
- **Automation:** Ansible playbooks for zero-touch deployment and configuration.

## 🚀 Key Features
- **High Availability:** Distributed nodes across multiple AZs.
- **Security:** Layered Security Groups (LB accepts HTTP/SSH; App Nodes only accept traffic from LB).
- **Idempotent Automation:** Ansible logic ensures the environment stays in the desired state.

## 🛠️ Tech Stack
- **Cloud:** AWS (EC2, VPC, IGW, Subnets)
- **Configuration Management:** Ansible
- **Web Server:** Nginx
- **OS:** Ubuntu 24.04 LTS
