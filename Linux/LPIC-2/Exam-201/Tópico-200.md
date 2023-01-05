---
title: 200 - Planejamento de Capacidade
description: Linux - LPIC-2 - Exame 201 - Tópico 200 - Planejamento de Capacidade
published: true
date: 2023-01-05T03:21:11.751Z
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

`iostat -d`
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

Quando instalado e habilitado roda como um serviço do sistema e grava as estatísticas nos logs em /var/log/sa/ em um arquivo binário que pode ser lido pelo comando sar.

`sar`
Se utilizado sem parâmetros, exibe estatísticas de utilização de CPU a cada 10 minutos.
```shell
[root@localhost ~]# sar
Linux 5.14.0-202.el9.x86_64 (localhost) 	04/01/2023 	_x86_64_	(3 CPU)

23:27:45     LINUX RESTART	(3 CPU)

23:30:01        CPU     %user     %nice   %system   %iowait    %steal     %idle
23:30:17        all      0,21      0,00      1,85      0,04      0,00     97,90
Média:         all      0,21      0,00      1,85      0,04      0,00     97,90


```
`sar -d `
Exibe estatísticas de uso de discos. 
```shell
[root@localhost ~]# sar -d
Linux 5.14.0-202.el9.x86_64 (localhost) 	04/01/2023 	_x86_64_	(3 CPU)

23:27:45     LINUX RESTART	(3 CPU)

23:30:01          DEV       tps     rkB/s     wkB/s     dkB/s   areq-sz    aqu-sz     await     %util
23:30:17      nvme0n1      0,25      0,00      0,99      0,00      4,00      0,00      1,25      0,04
23:30:17          sr0      0,00      0,00      0,00      0,00      0,00      0,00      0,00      0,00
23:30:17         dm-0      0,25      0,00      0,99      0,00      4,00      0,00      1,75      0,04
23:30:17         dm-1      0,00      0,00      0,00      0,00      0,00      0,00      0,00      0,00
Média:       nvme0n1      0,25      0,00      0,99      0,00      4,00      0,00      1,25      0,04
Média:           sr0      0,00      0,00      0,00      0,00      0,00      0,00      0,00      0,00
Média:          dm-0      0,25      0,00      0,99      0,00      4,00      0,00      1,75      0,04
Média:          dm-1      0,00      0,00      0,00      0,00      0,00      0,00      0,00      0,00

```
`sar -r`
Exibe estatísticas de uso de memória RAM.
```shell
[root@localhost ~]# sar -r
Linux 5.14.0-202.el9.x86_64 (localhost) 	04/01/2023 	_x86_64_	(3 CPU)

23:27:45     LINUX RESTART	(3 CPU)

23:30:01    kbmemfree   kbavail kbmemused  %memused kbbuffers  kbcached  kbcommit   %commit  kbactive   kbinact   kbdirty
23:30:17      1955184   2439056    941180     25,28      3820    680936   3251160     55,87    340524   1042064         0
Média:       1955184   2439056    941180     25,28      3820    680936   3251160     55,87    340524   1042064         0

23:42:18     LINUX RESTART	(2 CPU)

23:50:01    kbmemfree   kbavail kbmemused  %memused kbbuffers  kbcached  kbcommit   %commit  kbactive   kbinact   kbdirty
23:50:01      2382992   3385380   1003496     21,19      2780   1204244   3278232     47,97    355744   1628224      4176
Média:       2382992   3385380   1003496     21,19      2780   1204244   3278232     47,97    355744   1628224      4176
```
`sar -w`
Exibe o percentual de criação de processos por segundo (**proc/s**) e de mudança de estados (**cswch/s**) quando a CPU alterna entre um processo e outro.
```shell
root@localhost ~]# sar -w
Linux 5.14.0-202.el9.x86_64 (localhost) 	05/01/2023 	_x86_64_	(4 CPU)

00:07:15     LINUX RESTART	(4 CPU)

00:10:00       proc/s   cswch/s
00:10:01         1,82   1120,91
Média:          1,82   1120,91

```
`sar -n DEV`
Exibe estatísticas dos dispositivos de rede.
```shell
[root@localhost ~]# sar -n DEV
Linux 5.14.0-202.el9.x86_64 (localhost) 	05/01/2023 	_x86_64_	(4 CPU)

00:07:15     LINUX RESTART	(4 CPU)

00:10:00        IFACE   rxpck/s   txpck/s    rxkB/s    txkB/s   rxcmp/s   txcmp/s  rxmcst/s   %ifutil
00:10:01           lo      0,00      0,00      0,00      0,00      0,00      0,00      0,00      0,00
00:10:01       ens160      0,00      0,00      0,00      0,00      0,00      0,00      0,00      0,00
Média:            lo      0,00      0,00      0,00      0,00      0,00      0,00      0,00      0,00
Média:        ens160      0,00      0,00      0,00      0,00      0,00      0,00      0,00      0,00

```

`sar -a`
Exibe todas estatísticas que podem ser consultadas com o comando `sar`.