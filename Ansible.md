---
title: Instalando o Ansible
description: Instalando o Ansible
published: true
date: 2023-01-22T00:04:09.251Z
tags: 
editor: markdown
dateCreated: 2023-01-21T23:48:04.793Z
---

# Instalando o Ansible
Your content here

## Centos 8

### Instalando o Pip para Python 3
Pip é um gerenciador de pacotes para a linguagem de programação Python. O Pip facilita a instalação de plug-ins e outros pacotes de software para Python.

#### Passo 1 - Atualizar os pacotes intalados no sistema
```shell
dnf update -y
```
```shell
[root@ansible ~]# dnf update -y
Extra Packages for Enterprise Linux 8 - x86_64                                                         5.0 MB/s |  13 MB     00:02
Extra Packages for Enterprise Linux Modular 8 - x86_64                                                 1.1 MB/s | 733 kB     00:00
Last metadata expiration check: 0:00:02 ago on Sat 21 Jan 2023 09:51:05 PM GMT.
Dependencies resolved.
=======================================================================================================================================
 Package                                    Architecture         Version                                 Repository               Size
=======================================================================================================================================
Installing:
 kernel                                     x86_64               4.18.0-448.el8                          baseos                  9.2 M
Upgrading:
 NetworkManager                             x86_64               1:1.40.10-1.el8                         baseos                  2.3 M
...
```
#### Passo 2 - Instalar o python3
```shell
dnf –y install python3
```

#### Passo 3 - Instalar o pip para o python3
```shell
dnf –y install python3-pip
```

#### Passo 4 - Verifique a versão do pip instalada
```shell
pip -v
```
```shell
pip -v
```