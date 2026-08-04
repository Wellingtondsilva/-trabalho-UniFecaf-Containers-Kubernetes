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

## 🛠️ 3. Comandos para Executar a Aplicação
Siga as etapas abaixo no terminal (a partir da raiz do projeto) para construir as imagens, realizar a implantação no Kubernetes e expor as portas para validação local:

Step 1: Construir as Imagens Docker Localmente
Bash
# Gerar a imagem do servidor Nginx
docker build -t websolutions-nginx:1.0 ./nginx

# Gerar a imagem do servidor Apache HTTPD
docker build -t websolutions-apache:1.0 ./apache
Step 2: Implantar os Manifestos no Cluster Kubernetes
Bash
# Aplicar todos os Deployments e Services localizados na pasta k8s/
kubectl apply -f k8s/
Step 3: Verificar o Status dos Pods e Serviços
Bash
# Verificar se os Pods estão em execução (STATUS: Running)
kubectl get pods

# Consultar os serviços ativos no cluster
kubectl get svc
Step 4: Redirecionamento de Portas (Port-Forwarding)
Abra dois terminais no seu ambiente de desenvolvimento para manter o encaminhamento de portas ativo:

Terminal 1 — Servidor Nginx (Porta 8080):
kubectl port-forward service/nginx-service 8080:80

Terminal 2 — Servidor Apache HTTPD (Porta 8081):
kubectl port-forward service/apache-service 8081:80

Step 5: Acessar no Navegador Web
Com o port-forwarding rodando nos terminais, abra o navegador e acesse:

🟢 Nginx: http://localhost:8080

🔵 Apache HTTPD: http://localhost:8081

⚙️ 4. Arquitetura da Solução YAML
Deployments: Mantêm replicas: 2 para cada aplicação, assegurando alta disponibilidade e recuperação automática caso um container falhe.

Services: Abstraem o roteamento de rede via NodePort.

Política de Imagem: Configurada com imagePullPolicy: IfNotPresent para garantir o rápido provisionamento em ambiente local.