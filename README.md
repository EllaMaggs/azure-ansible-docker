# Azure VM Web Server Deployment with Terraform, Ansible, and Docker

[![Terraform](https://img.shields.io/badge/Terraform-%23623CE4.svg?logo=terraform&logoColor=white)](https://www.terraform.io)
[![Ansible](https://img.shields.io/badge/Ansible-%231A1918.svg?logo=ansible&logoColor=white)](https://www.ansible.com)
[![Docker](https://img.shields.io/badge/Docker-%232496ED.svg?logo=docker&logoColor=white)](https://www.docker.com)

This project uses Terraform, Ansible, and Docker to deploy a containerized Apache HTTPD web server on an Azure VM. Terraform provisions the VM and networking resources declaratively, Ansible automates Docker installation and container setup via SSH, and Docker runs the web server in a consistent, isolated environment. The pipeline enables automated, repeatable, and scalable infrastructure deployment.

## Project Structure

```
azure-ansible-docker/
├── ansible/                    # Ansible configuration and playbooks
│   ├── inventory.ini.template # Template for Ansible inventory
│   ├── inventory.ini         # Your configured inventory file (gitignored)
│   ├── playbooks/            # Ansible playbooks
│   │   ├── main.yml         # Main playbook for Docker setup
│   │   └── test.yml         # Test playbook for verification
│   ├── files/               # Files to be deployed
│   │   └── index.html      # Custom web page
│   └── host_vars/          # Host-specific variables
│       ├── servervars.yml.template  # Template for server variables
│       └── servervars.yml          # Your configured variables (gitignored)
├── terraform/               # Terraform configuration
│   ├── main.tf             # Main Terraform configuration
│   ├── variables.tf        # Input variables for Terraform
│   ├── output.tf           # Output values from Terraform
└── README.md               # Project documentation
```

## What currently get deployed

1 VM → 1 Container → 1 Website

### 💻 Infrastructure
- [x] **Azure VM**: Ubuntu 18.04 LTS instance
- [x] **Network Security Group**: Restricted ports (22/8080)
- [x] **Virtual Network**: Isolated subnet configuration

### 🐳 Application Stack
- [x] **Docker**: Container runtime installed
- [x] **Apache HTTPD**: Containerized web server
- [x] **Static Website**: Served on port 8080
- [x] **Persistent Storage**: Volume-mounted web content

### 🔒 Security Features
- [x] **SSH Access**: Key-based auth only (port 22)
- [x] **Network Policies**: HTTP restricted to port 8080
- [x] **Container Isolation**: Process sandboxing
- [x] **Self-Healing**: Auto-restart policy

## What scalability could look like

10 VMs → Multiple Containers per VM → Microservices (Web, DB Cache) → Load Balanced Website

### 📈 Elastic Scaling
- [ ] **Horizontal**: VM Scale Sets + Azure Load Balancer  
- [ ] **Vertical**: Upgrade to Dv3-series VMs with tuned memory limits  
- [ ] **Hybrid**: Auto-scaling based on CPU/memory metrics  

### 🧩 Architecture Evolution
- [ ] **Static Assets**: Azure Blob Storage + CDN
- [ ] **Reverse Proxy**: Nginx/Traefik for routing
- [ ] **Microservices**: Decoupled DB/cache layers

### 🚀 Orchestration
- [ ] **Container Management**: Docker Swarm/AKS
- [ ] **Auto-Scaling**: Pod/node autoscaling
- [ ] **CI/CD Pipeline**: Automated rolling updates

## Troubleshooting

- **Check Docker Installation**
  ```bash
  ssh adminuser@your-vm-ip 'docker --version'
- **Verify Apache Container status**
   ```bash
   ssh adminuser@your-vm-ip 'docker ps -a'
- **Confirm that port 8080 is open in the Network Security Group (NSG):**

   Check Docker status
   ```bash
   az network nsg rule list -g your-resource-group --nsg-name your-nsg-name
   ```
   View container logs
   ```bash
   ssh adminuser@your-vm-ip 'docker logs apache-httpd'
   ```

## Roadmap

### 🐳 Custom Docker Image & Nginx Reverse Proxy
- [ ] Create optimized custom Docker image for Apache
- [ ] Implement Nginx as reverse proxy
- [ ] Configure SSL/TLS with Let's Encrypt
- [ ] Set up proper caching and compression

### 📊 Monitoring & Visibility
- [ ] Implement Azure Monitor integration
- [ ] Set up centralized logging with Log Analytics
- [ ] Add application performance monitoring
- [ ] Configure alerting for critical metrics

### 🔐 Security Enhancements
- [ ] Implement Azure Key Vault for secrets
- [ ] Configure Azure Security Center
- [ ] Add network security rules
- [ ] Implement regular security scanning

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request
