# CI/CD Agents – Jenkins & Docker

![Docker](https://img.shields.io/badge/docker-ready-blue)
![License](https://img.shields.io/badge/license-MIT-green)
![Status](https://img.shields.io/badge/status-in--development-yellow)

> A collection of hands-on labs focused on setting up and managing Jenkins CI/CD agents using Docker and SSH-based communication.

---

## Overview

This repository contains multiple practical setups that demonstrate how to configure and operate Jenkins agents in containerized environments. These labs are designed to help DevOps engineers understand the inner workings of CI/CD infrastructure, secure agent communication, and pipeline automation.

---

## Technologies Used

- Docker
- Docker Compose
- Jenkins
- OpenSSH
- Bash scripting

---

## Repository Structure

```bash
CI-CD-Agents/
├── agent-base/                # Base image for custom Jenkins agents
│   ├── Dockerfile
│
├── ansible-agent/             # Jenkins agent with Ansible installed
│   ├── Dockerfile
│   └── keys/
│       ├── ansible_id_rsa
│       └── ansible_id_rsa.pub
│
├── docker-agent/              # Jenkins agent with Docker CLI
│   ├── Dockerfile
│   └── keys/
│       ├── docker_id_rsa
│       └── docker_id_rsa.pub
│
├── jenkins-orchestrator/      # Jenkins controller configured via JCasC
│   ├── Dockerfile
│   ├── plugins.txt
│   └── config-as-code/
│       └── jenkins.yaml
│
├── terraform-agent/           # Jenkins agent with Terraform pre-installed
│   ├── Dockerfile
│   └── keys/
│       ├── terraform_id_rsa
│       └── terraform_id_rsa.pub
│
├── test-agent/                # Lightweight agent for unit and security testing
│   ├── Dockerfile
│   └── keys/
│       ├── test_id_rsa
│       └── test_id_rsa.pub
│
└── README.md                  # This file
```

---

## Usage

Each agent is designed to be built independently using:

```bash
docker build -t <agent-name> ./<agent-folder>
```

You can use these custom agents inside Jenkins pipelines or as services in a Jenkins controller with JCasC.

---

## Notes

- The Jenkins controller supports configuration-as-code via the `jenkins.yaml` file.
- Agents can be extended to include specific tooling (e.g., Helm, AWS CLI).

---

## License

This project is licensed under the MIT License.

---

## Author

Developed by GoViz93
