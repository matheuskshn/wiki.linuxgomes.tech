---
title: Planejamento de Capacidade
description: Tópico 200 - Planejamento de Capacidade
published: true
date: 2022-11-26T21:32:55.734Z
tags: 
editor: markdown
dateCreated: 2022-11-26T20:43:40.845Z
---

# 200.1 - Medir e solucionar problemas de uso de recursos
## iostat
O comando iostat faz parte do pacote sysstat.
O iostat exibe estatísticas de uso de CPU e disco.
É possível verificar com o comando iostat:
- A quantidade de CPU da máquina.
- Média de uso da CPU:
> avg-cpu: 
>
> - %user: Porcentagem de uso de CPU do usuário.
>
> - %nice: Porcentagem de uso de CPU de processos com opção de nice modificada.
>
> - %system: Porcentagem de uso de CPU do sistema operacional (kernel).
>
> - %iowait: Porcentagem de tempo em que a CPU teve que aguardar solicitações de E/S de disco pendentes.
>
> - %steal: 
- Média de uso de discos:

## uptime