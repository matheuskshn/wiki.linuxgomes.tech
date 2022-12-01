---
title: 200 - Planejamento de Capacidade
description: Linux - LPIC-2 - Exame 201 - Tópico 200 - Planejamento de Capacidade
published: true
date: 2022-12-01T02:40:59.742Z
tags: 
editor: markdown
dateCreated: 2022-11-26T20:43:40.845Z
---

# 200.1 - Medir e solucionar problemas de uso de recursos
## iostat
O iostat faz parte do pacote sysstat, o comando exibe estatísticas de uso de CPU e disco. Geralmente usado para identificar gargalos de CPU ou disco.

`iostat`
```shell

```

É possível verificar com o comando iostat:
- A quantidade de CPU da máquina.
- Média de uso da CPU:
> avg-cpu: 
>
> - **%user**: Porcentagem de uso de CPU do usuário.
>
> - **%nice**: Porcentagem de uso de CPU de processos com opção de nice modificada.
>
> - **%system**: Porcentagem de uso de CPU do sistema operacional (kernel).
>
> - **%iowait**: Porcentagem de tempo em que a CPU teve que aguardar solicitações de E/S de disco.
>
> - **%steal**: Porcentagem de tempo de uso de CPU por máquinas virtuais (roubo de CPU).
>
> - **%idle**: Porcentagem de tempo livre de CPU.

- Média de uso de discos:
> - **Device**: Dispositivos de discos.
>
> - **tps**: Transações por segundo.
>
> - **kB_read/s**: Kilobytes lidos por segundo.
>
> - **kB_wrtn/s**: Kilobytes gravados por segundo.
>
> - **kB_read**: Kilobytes lidos desde a última reinicialização do S.O.
>
> - **kB_wrtn**: Kilobytes gravados desde a última reinicialização do S.O.

`iostat -c`
Traz somente informações de CPU.

`iostat -c`
Traz somente informações de Disco.

`iostat -c 2 5`
Atualiza as informações CPU de 2 em 2 segundos 5 vezes.

`iostat -d 2 4`
Atualiza as informações disco de 2 em 2 segundos 4 vezes.
## uptime
O uptime mostra a quanto tempo o servidor está ligado. 
Mostra também o horário atual, quantos usuários estão conectados no momento e uma média de uso de CPU (load average: 1min 5min 15min).

`uptime`
```shell

```
## sar
Relatório de atividades do sistema.
Ele pode ser usado para monitorar os recursos do sistema Linux, como uso da CPU, memória, consumo de dispositivos de E/S, monitoramento de rede, disco, alocação de processos e threads, desempenho da bateria, dispositivos plug and play, desempenho do processador, sistema de arquivos e muito mais.
