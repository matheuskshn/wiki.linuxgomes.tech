---
title: 200 - Planejamento de Capacidade
description: Linux - LPIC-2 - Exame 201 - Tópico 200 - Planejamento de Capacidade
published: true
date: 2023-01-05T11:26:21.209Z
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

A documentação do sar traz todas as informações do comando, para consultar: `man sar`

## free
o `free` Exibe informações sobre o uso da memória RAM.
```shell
[root@localhost ~]# free 
               total        used        free      shared  buff/cache   available
Mem:         3722260     1386388     1821420       21996      774516     2335872
Swap:        2097148           0     2097148
[root@localhost ~]# 
```

`free -h`
Exibe as informações "humanamente" legíveis.
```shell
[root@localhost ~]# free -h
               total        used        free      shared  buff/cache   available
Mem:           3,5Gi       1,3Gi       1,7Gi        21Mi       756Mi       2,2Gi
Swap:          2,0Gi          0B       2,0Gi
```

## vmstat
O `vmstat` também exibe informações de uso de memória RAM, porém mais detalhado.
```shell
[root@localhost ~]# vmstat 
procs -----------memory---------- ---swap-- -----io---- -system-- ------cpu-----
 r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st
 0  0      0 1797108   3820 770808    0    0   628    85  186  284  3  4 93  0  0
```
> procs: 
>
> - **r**: Número de processos executáveis (em execução ou aguardando o tempo de execução).
> - **b**: O número de processos bloqueados aguardando a conclusão da E/S.
>
> memory: 
>
> - **swpd**: Quantidade de memória swap usada.
> - **free**: Quantidade de memória ociosa.
> - **buff**: Quantidade de memória usada como buffers.
> - **cache**: Quantidade de memória usada como cache.
>
> swap: 
>
> - **si**: Quantidade de memória trocada do disco (/s).
> - **so**: Quantidade de memória trocada para disco (/s).
>
> io: 
>
> - **bi**: Blocos recebidos de um dispositivo de bloco (blocos/s).
> - **bo**: Blocos enviados para um dispositivo de bloco (blocos/s).
>
> system: 
>
> - **in**: O número de interrupções por segundo, incluindo o clock.
> - **cs**: O número de trocas de contexto por segundo.
>
> CPU: 
>
> - **us**: Tempo gasto executando código não-kernel. (tempo do usuário, incluindo tempo agradável).
> - **sy**: Tempo gasto executando o código do kernel. (hora do sistema).
> - **id**: Tempo gasto ocioso.
> - **wa**: Tempo gasto esperando por IO.
> - **st**: Tempo roubado de uma máquina virtual.

Documentação:
`man vmstat`