---
title: 200 - Planejamento de Capacidade
description: Linux - LPIC-2 - Exame 201 - Tópico 200 - Planejamento de Capacidade
published: true
date: 2022-12-01T02:02:46.003Z
tags: 
editor: markdown
dateCreated: 2022-11-26T20:43:40.845Z
---

# 200.1 - Medir e solucionar problemas de uso de recursos
## iostat
O iostat faz parte do pacote sysstat, o comando exibe estatísticas de uso de CPU e disco. Server para identificar gargalos de CPU ou disco.

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
> - %iowait: Porcentagem de tempo em que a CPU teve que aguardar solicitações de E/S de disco.
>
> - %steal: Porcentagem de uso de CPU por máquinas virtuais (roubo de CPU).

- Média de uso de discos:

## uptime