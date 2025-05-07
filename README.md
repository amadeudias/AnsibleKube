# Provisionamento de Pacotes Kubernetes com Ansible + AWS EC2 + SSM

Este repositório contém um playbook Ansible que automatiza a instalação dos pacotes essenciais do Kubernetes (`kubeadm`, `kubelet`, `kubectl`) em instâncias EC2 na AWS, utilizando o AWS Systems Manager (SSM) para acesso seguro.

## Estrutura do Projeto

```
.
├── inventory/
│   └── production.aws_ec2.yml
├── playbooks/
│   └── site.yml
├── roles/
│   ├── dependency-packages/
│   │   └── tasks/main.yml
│   └── kube-packages/
│       └── tasks/
│           ├── main.yml
│           ├── repository.yml
│           ├── install.yml
│           └── hold.yml
```

## Requisitos

- Ansible
- Python 3 com boto3 e botocore instalados
- AWS CLI configurado (com permissões de EC2 e SSM)
- Coleção Ansible `amazon.aws` instalada:

```bash
ansible-galaxy collection install amazon.aws
```

## Como usar

1. Edite o arquivo `inventory/production.aws_ec2.yml` com seu filtro de tags ou IDs das instâncias EC2.

2. Execute o playbook:

```bash
ansible-playbook -i inventory/production.aws_ec2.yml playbooks/site.yml
```

> Obs.: As instâncias devem estar com o SSM Agent ativo e possuir a IAM Role adequada para o AWS Systems Manager.

## O que é feito

- Instala dependências como `curl`, `gpg`, etc
- Adiciona o repositório oficial do Kubernetes
- Instala `kubectl`, `kubeadm`, `kubelet`
- Ativa o `kubelet`
- Coloca os pacotes em hold para evitar atualizações automáticas indesejadas

## Objetivo

Este projeto tem como objetivo ajudar profissionais de infraestrutura e DevOps a automatizar com confiabilidade a preparação de instâncias EC2 para uso com Kubernetes, de forma simples, segura e reutilizável.

---

Contribuições são bem-vindas! 


> Criado com propósito educacional e comunitário. Compartilhe e ajude mais pessoas 

