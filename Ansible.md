---
title: Instalando o Ansible
description: Instalando o Ansible
published: true
date: 2023-01-22T03:53:46.636Z
tags: 
editor: markdown
dateCreated: 2023-01-21T23:48:04.793Z
---

# Instalando o Ansible 7.1.0 no Ubuntu 22.04
Ansible é uma ferramenta de automação de código aberto escrito em Python. Ele pode configurar sistemas, implantar software e orquestrar fluxos de trabalho avançados para oferecer suporte à implantação de aplicativos, atualizações do sistema e muito mais.

Os principais pontos fortes do Ansible são a simplicidade e a facilidade de uso. Ele também tem um forte foco em segurança e confiabilidade, apresentando peças móveis mínimas. Ele usa o OpenSSH para transporte (com outros transportes e modos pull como alternativas) e usa uma linguagem legível por humanos projetada para começar rapidamente sem muito treinamento.

## Passo 1 - Atualizar o repositório de pacotes do sistema.
```shell
apt update -y
```
```shell
root@ansible-ubuntu22:~# apt update -y
Hit:1 http://us-sanjose-1-ad-1.clouds.archive.ubuntu.com/ubuntu jammy InRelease
Get:2 http://security.ubuntu.com/ubuntu jammy-security InRelease [110 kB]
Get:3 http://us-sanjose-1-ad-1.clouds.archive.ubuntu.com/ubuntu jammy-updates InRelease [114 kB]
Get:4 http://us-sanjose-1-ad-1.clouds.archive.ubuntu.com/ubuntu jammy-backports InRelease [99.8 kB]
Fetched 324 kB in 1s (257 kB/s)
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
0 package can be upgraded.
```
## Passo 2 - Instalar o python3.10
```shell
add-apt-repository ppa:deadsnakes/ppa
apt install python3.11
```
Definindo o **python3.11** como padrão do sistema:
```shell
update-alternatives --install /usr/bin/python python /usr/bin/python3.11 1
update-alternatives --set python /usr/bin/python3.11
```
Verificando a versão do python:
```shell
python --version
```
## Passo 3 - Instalar o pip para o python3
Pip é um gerenciador de pacotes para a linguagem de programação Python. O Pip facilita a instalação de plug-ins e outros pacotes de software para Python.
```shell
apt install pip
pip install --upgrade pip
```
Verificando a versão do pip instalada:
```shell
pip --version
```
#### Passo 4 - Instalando o Ansible
```shell
pip install ansible
```
Verificando a versão do pip instalada:
```shell
ansible --version
```