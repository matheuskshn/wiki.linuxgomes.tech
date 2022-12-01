---
title: 200 - Planejamento de Capacidade
description: Linux - LPIC-2 - Exame 201 - Tópico 200 - Planejamento de Capacidade
published: true
date: 2022-12-01T03:09:19.499Z
tags: 
editor: markdown
dateCreated: 2022-11-26T20:43:40.845Z
---

# 200.1 - Medir e solucionar problemas de uso de recursos
## iostat
O iostat faz parte do pacote sysstat, o comando exibe estatísticas de uso de CPU e disco. Geralmente usado para identificar gargalos de CPU ou disco.

`iostat`
```shell
[root@localhost ~]# iostat
Linux 5.14.0-202.el9.x86_64 (localhost.localdomain) 	30/11/2022 	_x86_64_	(3 CPU)

avg-cpu:  %user   %nice %system %iowait  %steal   %idle
           9,99    0,25    8,74    0,20    0,00   80,82

Device             tps    kB_read/s    kB_wrtn/s    kB_dscd/s    kB_read    kB_wrtn    kB_dscd
dm-0             54,02      1548,15       505,58         0,00     799822     261197          0
dm-1              0,19         4,54         0,00         0,00       2348          0          0
nvme0n1          54,06      1603,43       572,15         0,00     828382     295590          0
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
Mostra também o horário atual, quantos usuários estão conectados no momento e uma média de uso de CPU (load average: 1min, 5min, 15min,).

`uptime`
```shell
[root@localhost ~]# uptime
23:55:00 up 9 min,  1 user,  load average: 0,04, 0,34, 0,29
```
## sar
O sar faz parte do pacote sysstat, ele mostra relatório de atividades do sistema.
Usado para monitorar os recursos do sistema, como uso da CPU, memória, consumo de dispositivos de E/S, monitoramento de rede, disco, alocação de processos e threads, desempenho da bateria, dispositivos plug and play, desempenho do processador, sistema de arquivos e muito mais.

`sar`
Se utilizado sem parâmetros, exibe estatísticas de utilização de CPU a cada 10 minutos.
```shell

```