# DevOps-Supervision Project

## Overview

This project provides a complete, automated supervision and monitoring solution using Ansible for deployment, Jenkins for CI/CD, Prometheus for monitoring, Grafana for dashboards, and Node Exporter for system metrics. The infrastructure is designed to be modular, scalable, and suitable for multi-VM environments.

---

## Features

- **Automated Deployments:** Use Ansible roles to install and configure all components.
- **CI/CD Integration:** Jenkins automates deployments and testing.
- **Monitoring & Metrics:** Prometheus scrapes and stores metrics; Node Exporter collects system metrics.
- **Dashboards:** Grafana visualizes all collected metrics.
- **Documentation:** Includes architecture diagrams, role documentation, and operational guides.

---

## Architecture

```
+-------------------+         +---------------------------+
|   Jenkins +       |  SSH    |      Grafana +            |
|   Ansible  (VM1)  +<------->+   Prometheus  (VM2)       |
+-------------------+         +---------------------------+
         |                                |
         | SSH                            | Prometheus scrape
         |                                |
         |________________________________|
                          |
            +--------------------------+
            |   Server B, C, D, ...    |
            |   (Node Exporter)        |
            +--------------------------+


```

---

## Requirements

- **OS:** Ubuntu 22.04 LTS (recommended)
- **Jenkins:** 2.x
- **Ansible:** 2.9+
- **Prometheus:** 2.40+
- **Grafana:** 9.x
- **Node Exporter:** 1.x
- **Python3** (for Ansible)
- **Git** (for version control)
- **SSH key authentication** between Jenkins/Ansible and managed VMs

---

## Repository Structure

```
DevOps-supervision/
├── ansible/
│   ├── inventories/
│   │   └── hosts
│   ├── roles/
│   │   ├── jenkins/
│   │   ├── prometheus/
│   │   ├── grafana/
│   │   └── node_exporter/
│   ├── playbooks/
│   │   └── site.yml
│   └── group_vars/
├── jenkins/
│   └── Jenkinsfile
├── docs/
│   ├── architecture.png
│   └── installation.md
├── scripts/
│   └── custom-scripts.sh
├── README.md
└── .gitignore
```

---

## Installation & Usage

### 1. Clone the repository
```bash
git clone git@github.com:your-org/DevOps-supervision.git
cd DevOps-supervision
```

### 2. Configure Inventory
Edit `ansible/inventories/hosts` to add your servers and VMs.

### 3. Setup SSH Keys
Ensure the Ansible/Jenkins VM has SSH access to the target servers.

### 4. Run Ansible Playbook
```bash
cd ansible
ansible-playbook -i inventories/hosts playbooks/site.yml
```

### 5. Jenkins CI/CD
- Configure Jenkins to use the included `Jenkinsfile`.
- Set up credentials and job triggers as needed.

---

## Documentation

- **[docs/architecture.png]**: Architecture diagram
- **[docs/installation.md]**: Step-by-step install instructions
- **[ansible/roles/***]:** Each role includes a README describing its purpose and usage.

---

## Contribution

1. Fork the repo and create your feature branch.
2. Commit your changes and push to your branch.
3. Create a Pull Request with details.

---

## License

This project is licensed under the MIT License.

---

## Maintainers

- [HALOUANE Mounir](mailto:mounir.halouane@abil-it.fr)
- [BOUAFIF Zied](mailto:zied.bouafif@abil-it.fr)

