# Orquestração de Containers com Kubernetes: Desafios e Soluções no Mundo Real
**Instituição:** UniFECAF  
**Projeto:** Prova de Conceito - Conteinerização e Orquestração Web (Nginx & Apache HTTPD)  
**Ambiente:** Windows 11 | VS Code | Docker Desktop | Kubernetes (`kubectl`) | GitHub  

---

## 📌 1. Visão Geral do Projeto

A **Web Solutions Ltda.** enfrentava gargalos em sua infraestrutura tradicional baseada em máquinas virtuais dedicadas. Com o aumento da demanda, a alocação de recursos tornou-se inflexível, as atualizações eram manuais/lentas e os conflitos de dependências impactavam a disponibilidade dos serviços.

Esta Prova de Conceito (PoC) demonstra a modernização da infraestrutura através da conteinerização (Docker) e da orquestração de microsserviços (Kubernetes). A solução garante a coexistência independente, resiliente e escalável de dois servidores web distintos em um único cluster local:
- **Nginx**: Exposto e acessível via porta **8080**
- **Apache HTTPD**: Exposto e acessível via porta **8081**

---

## 📁 2. Estrutura do Repositório

```text
trabalho-UniFecaf-Containers & Kubernetes/
├── nginx/
│   ├── Dockerfile
│   └── index.html
├── apache/
│   ├── Dockerfile
│   └── index.html
├── k8s/
│   ├── nginx-deployment.yaml
│   └── apache-deployment.yaml
└── README.md