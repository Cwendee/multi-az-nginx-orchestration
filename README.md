# Multi-AZ Nginx Orchestration
Moving from manual configurations to automated orchestration with Ansible on AWS.

## 🏗️ System Architecture
This project demonstrates a high-availability Nginx orchestration across multiple AWS Availability Zones.

![Multi-AZ Architecture](images/load-balancer-architecture.png)

## 🎯 Project Goals
* **Automate** the installation of Nginx across multiple zones.
* **Orchestrate** configurations to ensure high availability.
* **Ensure Idempotency** across the entire infrastructure.

## 🛠 Tech Stack
* **Configuration Management:** Ansible
* **Infrastructure:** AWS EC2
* **Web Server:** Nginx
* **Version Control:** Git

## 🚀 Execution & Verification
The following terminal output demonstrates the Ansible playbook running across the inventory. Notice the "changed" status, indicating the successful application of the desired state.

### Live Service Verification
Once the orchestration was complete, I verified the deployment by accessing the public DNS of the managed nodes. 

## 💡 Key Learning Moments
1. **SSH Key Management:** Secure communication between cloud instances.
2. **Regex Implementation:** Handle case-insensitive text replacement.
3. **Security Best Practices:** Redacted sensitive IP addresses.
