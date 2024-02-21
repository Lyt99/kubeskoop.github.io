# 探针，指标和事件

本篇文档将会介绍KubeSkoop exporter所支持的探针，以及它们的指标和事件。

## 探针

以下是KubeSkoop exporter所支持的探针。

| 探针名称       | 说明                     | 探针类型   | 数据源  | 开销 |
| -------------- | ------------------------ | ---------- | ------- | ---- |
| conntrack      | conntrack统计            | 指标       | netlink | 低   |
| qdisc          | tc qdisc统计             | 指标       | netlink | 低   |
| fd             | 文件与socket描述符统计   | 指标       | procfs  | 中   |
| io             | 进程IO统计               | 指标       | procfs  | 低   |
| ipvs           | IPVS统计                 | 指标       | procfs  | 低   |
| netdev         | 网络设备统计             | 指标       | procfs  | 低   |
| tcpext         | TCPExt统计               | 指标       | procfs  | 低   |
| tcp            | snmp中的TCP统计          | 指标       | profcs  | 低   |
| udp            | UDP统计                  | 指标       | profcs  | 低   |
| ip             | IP统计                   | 指标       | profcs  | 低   |
| sock           | socket统计               | 指标       | procfs  | 低   |
| softnet        | 网络设备发包和丢包数统计 | 指标       | procfs  | 低   |
| tcpsummary     | TCP队列和连接状态统计    | 指标       | procfs  | 中   |
| netiftxlatency | 发包网络延迟跟踪         | 指标、事件 | eBPF    | 高   |
| biolatency     | Block IO延迟跟踪         | 事件       | eBPF    | 中   |
| kernellatency  | 内核延迟跟踪             | 指标、事件 | eBPF    | 高   |
| packetloss     | 丢包事件追踪             | 指标、事件 | eBPF    | 中   |
| socketlatency  | socket延迟追踪           | 指标、事件 | eBPF    | 高   |
| tcpreset       | TCP reset追踪            | 事件       | eBPF    | 低   |
| virtcmdlatency | virtio设备延迟追踪       | 指标、事件 | eBPF    | 高   |
| net_softirq    | 软中断延迟追踪           | 指标、事件 | eBPF    | 高   |

## 指标

### 标签

在所有的指标上都存在以下标签。

| 标签名称         | 说明                       |
| ---------------- | -------------------------- |
| target_pod       | Pod名称，或hostNetwork     |
| target_namespace | Pod命名空间，或hostNetwork |
| target_node      | Node名称                   |

### 指标列表

| 指标名称                                     | 探针名称       | 说明                                                         |
| -------------------------------------------- | -------------- | ------------------------------------------------------------ |
| inspector_pod_conntrackfound                 | conntrack      | conntrack统计计数"found"                                     |
| inspector_pod_conntrackinvalid               | conntrack      | conntrack统计计数"invalid"                                   |
| inspector_pod_conntrackignore                | conntrack      | conntrack统计计数"ignore"                                    |
| inspector_pod_conntrackinsert                | conntrack      | conntrack统计计数"insert"                                    |
| inspector_pod_conntrackinsertfailed          | conntrack      | conntrack统计计数"insert_failed"                             |
| inspector_pod_conntrackdrop                  | conntrack      | conntrack统计计数"drop"                                      |
| inspector_pod_conntrackearlydrop             | conntrack      | conntrack统计计数"early_drop"                                |
| inspector_pod_conntrackerror                 | conntrack      | conntrack统计计数"error"                                     |
| inspector_pod_conntracksearchrestart         | conntrack      | conntrack统计计数"search_restart"                            |
| inspector_pod_conntrackentries               | conntrack      | conntrack全局计数"entries"                                   |
| inspector_pod_conntrackmaxentries            | conntrack      | conntrack全局计数"max_entries"                               |
| inspector_pod_qdiscbytes                     | qdisc          | tc qdisc统计计数"bytes"                                      |
| inspector_pod_qdiscpackets                   | qdisc          | tc qdisc统计计数"packets"                                    |
| inspector_pod_qdiscdrops                     | qdisc          | tc qdisc统计计数"drops"                                      |
| inspector_pod_qdiscqlen                      | qdisc          | tc qdisc统计计数"qlen"                                       |
| inspector_pod_qdiscbacklog                   | qdisc          | tc qdisc统计计数"backlog"                                    |
| inspector_pod_qdiscoverlimits                | qdisc          | tc qdisc统计计数"overlimits"                                 |
| inspector_pod_fdopenfd                       | fd             | pod中打开fd数                                                |
| inspector_pod_fdopensocket                   | fd             | pod中打开socket数                                            |
| inspector_pod_ioioreadsyscall                | io             | pod中读系统调用数                                            |
| inspector_pod_ioiowritesyscall               | io             | pod中写系统调用数                                            |
| inspector_pod_ioioreadbytes                  | io             | pod中读字节数                                                |
| inspector_pod_ioiowritebytes                 | io             | pod中写字节数                                                |
| inspector_pod_ipvsconnections                | ipvs           | pod中IPVS连接数                                              |
| inspector_pod_ipvsincomingpackets            | ipvs           | pod中IPVS入数据包数                                          |
| inspector_pod_ipvsoutgoingbytes              | ipvs           | pod中IPVS出数据包数                                          |
| inspector_pod_ipvsincomingbytes              | ipvs           | pod中IPVS入字节数                                            |
| inspector_pod_ipvsoutgoingpackets            | ipvs           | pod中IPVS出字节数                                            |
| inspector_pod_netdevrxbytes                  | netdev         | pod中所有网络设备的接收字节数                                |
| inspector_pod_netdevrxerrors                 | netdev         | pod中所有网络设备的接收错误数                                |
| inspector_pod_netdevtxbytes                  | netdev         | pod中所有网络设备的发送字节数                                |
| inspector_pod_netdevtxerrors                 | netdev         | pod中所有网络设备的发送错误数                                |
| inspector_pod_netdevrxpackets                | netdev         | pod中所有网络设备的接收数据包数                              |
| inspector_pod_netdevrxdropped                | netdev         | pod中所有网络设备的接收丢弃数据包数                          |
| inspector_pod_netdevtxpackets                | netdev         | pod中所有网络设备的发送数据包数                              |
| inspector_pod_netdevtxdropped                | netdev         | pod中所有网络设备的发送丢弃数据包数                          |
| inspector_pod_tcpextlistendrops              | tcpext         | TCPExt中的ListenDrops                                        |
| inspector_pod_tcpextlistenoverflows          | tcpext         | TCPExt中的ListenOverflow                                     |
| inspector_pod_tcpexttcpsynretrans            | tcpext         | TCPExt中的TCPSynRetrans                                      |
| inspector_pod_tcpexttcpfastretrans           | tcpext         | TCPExt中的TCPFastRetrans                                     |
| inspector_pod_tcpexttcpretransfail           | tcpext         | TCPExt中的TCPRetransFail                                     |
| inspector_pod_tcpexttcptimeouts              | tcpext         | TCPExt中的TCPTimeouts                                        |
| inspector_pod_tcpexttcpabortonclose          | tcpext         | TCPExt中的TCPAbortOnClose                                    |
| inspector_pod_tcpexttcpabortonmemory         | tcpext         | TCPExt中的TCPAbortOnMemory                                   |
| inspector_pod_tcpexttcpabortontimeout        | tcpext         | TCPExt中的TCPAbortOnTimeout                                  |
| inspector_pod_tcpexttcpabortonlinger         | tcpext         | TCPExt中的TCPAbortOnLinger                                   |
| inspector_pod_tcpexttcpabortondata           | tcpext         | TCPExt中的TCPAbortOnData                                     |
| inspector_pod_tcpexttcpabortfailed           | tcpext         | TCPExt中的TCPAbortFailed                                     |
| inspector_pod_tcpexttcpackskippedsynrecv     | tcpext         | TCPExt中的TCPACKSkippedSynRecv                               |
| inspector_pod_tcpexttcpackskippedpaws        | tcpext         | TCPExt中的TCPACKSkippedPAWS                                  |
| inspector_pod_tcpexttcpackskippedseq         | tcpext         | TCPExt中的TCPACKSkippedSeq                                   |
| inspector_pod_tcpexttcpackskippedfinwait2    | tcpext         | TCPExt中的TCPACKSkippedFinWait2                              |
| inspector_pod_tcpexttcpackskippedtimewait    | tcpext         | TCPExt中的TCPACKSkippedTimeWait                              |
| inspector_pod_tcpexttcpackskippedchallenge   | tcpext         | TCPExt中的TCPACKSkippedChallenge                             |
| inspector_pod_tcpexttcprcvqdrop              | tcpext         | TCPExt中的TCPRcvQDrop                                        |
| inspector_pod_tcpexttcpmemorypressures       | tcpext         | TCPExt中的TCPMemoryPressures                                 |
| inspector_pod_tcpexttcpmemorypressureschrono | tcpext         | TCPExt中的TCPMemoryPressuresChrono                           |
| inspector_pod_tcpextpawsactive               | tcpext         | TCPExt中的PAWSActive                                         |
| inspector_pod_tcpextpawsestab                | tcpext         | TCPExt中的PAWSEstab                                          |
| inspector_pod_tcpextembryonicrsts            | tcpext         | TCPExt中的EmbryonicRsts                                      |
| inspector_pod_tcpexttcpwinprobe              | tcpext         | TCPExt中的TCPWinProbe                                        |
| inspector_pod_tcpexttcpkeepalive             | tcpext         | TCPExt中的TCPKeepAlive                                       |
| inspector_pod_tcpexttcpmtupfail              | tcpext         | TCPExt中的TCPMTUPFail                                        |
| inspector_pod_tcpexttcpmtupsuccess           | tcpext         | TCPExt中的TCPMTUPSuccess                                     |
| inspector_pod_tcpexttcpzerowindowdrop        | tcpext         | TCPExt中的TCPZeroWindowDrop                                  |
| inspector_pod_tcpexttcpbacklogdrop           | tcpext         | TCPExt中的TCPBacklogDrop                                     |
| inspector_pod_tcpextpfmemallocdrop           | tcpext         | TCPExt中的PFMemallocDrop                                     |
| inspector_pod_tcpexttcpwqueuetoobig          | tcpext         | TCPExt中的TCPWqueueTooBig                                    |
| inspector_pod_tcpactiveopens                 | tcp            | TCP中的ActiveOpens                                           |
| inspector_pod_tcppassiveopens                | tcp            | TCP中的PassiveOpens                                          |
| inspector_pod_tcpretranssegs                 | tcp            | TCP中的RetransSegs                                           |
| inspector_pod_tcpattemptfails                | tcp            | TCP中的AttemptFails                                          |
| inspector_pod_tcpestabresets                 | tcp            | TCP中的EstabResets                                           |
| inspector_pod_tcpcurrestab                   | tcp            | TCP中的CurrEstab                                             |
| inspector_pod_tcpinsegs                      | tcp            | TCP中的InSegs                                                |
| inspector_pod_tcpoutsegs                     | tcp            | TCP中的OutSegs                                               |
| inspector_pod_tcpinerrs                      | tcp            | TCP中的InErrs                                                |
| inspector_pod_tcpoutrsts                     | tcp            | TCP中的OutRsts                                               |
| inspector_pod_udpindatagrams                 | udp            | UDP中的InDatagrams                                           |
| inspector_pod_udpnoports                     | udp            | UDP中的NoPorts                                               |
| inspector_pod_udpinerrors                    | udp            | UDP中的InErrors                                              |
| inspector_pod_udpoutdatagrams                | udp            | UDP中的OutDatagrams                                          |
| inspector_pod_udprcvbuferrors                | udp            | UDP中的RcvbufErrors                                          |
| inspector_pod_udpsndbuferrors                | udp            | UDP中的SndbufErrors                                          |
| inspector_pod_udpincsumerrors                | udp            | UDP中的InCsumErrors                                          |
| inspector_pod_udpignoredmulti                | udp            | UDP中的IgnoredMulti                                          |
| inspector_pod_ipinnoroutes                   | ip             | IP中的InNoRoutes                                             |
| inspector_pod_ipintruncatedpkts              | ip             | IP中的InTruncatedPkts                                        |
| inspector_pod_sockinuse                      | sock           | sock中的Inuse                                                |
| inspector_pod_sockorphan                     | sock           | sock中的Orphan                                               |
| inspector_pod_socktw                         | sock           | sock中的TW                                                   |
| inspector_pod_sockalloc                      | sock           | Alloc of sock                                                |
| inspector_pod_sockmem                        | sock           | Mem of sock                                                  |
| inspector_pod_softnetprocessed               | softnet        | Processed of softnet                                         |
| inspector_pod_softnetdropped                 | softnet        | Dropped of softnet                                           |
| inspector_pod_tcpsummarytcpestablishedconn   | tcpsummary     | ESTABLISHED connection count                                 |
| inspector_pod_tcpsummarytcptimewaitconn      | tcpsummary     | TIME_WAIT connection count                                   |
| inspector_pod_tcpsummarytcptxqueue           | tcpsummary     | tx queue length of all TCP connections                       |
| inspector_pod_tcpsummarytcprxqueue           | tcpsummary     | rx queue length of all TCP connections                       |
| inspector_pod_netiftxlat_qdiscslow100ms      | netiftxlatency | qdisc latency exceeds 100ms during transmission              |
| inspector_pod_netiftxlat_netdevslow100ms     | netiftxlatency | netdev transmit latency exceeds 100ms during transmission    |
| inspector_pod_kernellatency_rxslow           | kernellatency  | Kernel packet receiving slow                                 |
| inspector_pod_kernellatency_rxslow100ms      | kernellatency  | Kernel packet receiving latency exceeds 100ms                |
| inspector_pod_kernellatency_txslow           | kernellatency  | Kernel packet transmitting slow                              |
| inspector_pod_kernellatency_txslow100ms      | kernellatency  | Kernel packet transmitting latency exceeds 100ms             |
| inspector_pod_packetloss_tcphandle           | packetloss     | Packet dropped count in `tcp_v4_do_rcv()`                    |
| inspector_pod_packetloss_tcprcv              | packetloss     | Packet dropped cont in `tcp_rcv()`                           |
| inspector_pod_packetloss_abnormal            | packetloss     | Packet dropped count in other functions                      |
| inspector_pod_packetloss_total               | packetloss     | Packet dropped total count                                   |
| inspector_pod_packetloss_netfilter           | packetloss     | Packet dropped in `nf_hook_slow()`                           |
| inspector_pod_packetloss_tcpstatm            | packetloss     | Packet dropped in `tcp_rcv_state_process()`                  |
| inspector_pod_socketlatencyread100ms         | socketlatency  | Socket read latency exceeds 100ms                            |
| inspector_pod_socketlatencyread1ms           | socketlatency  | Socket read latency exceeds 1ms                              |
| inspector_pod_socketlatencywrite100ms        | socketlatency  | Socket write latency exceeds 100ms                           |
| inspector_pod_socketlatencywrite1ms          | socketlatency  | Socket write latency exceeds 1ms                             |
| inspector_pod_virtcmdlatency100ms            | virtcmdlatency | Virtio send command latency exceeds 100ms                    |
| inspector_pod_virtcmdlatency                 | virtcmdlatency | Virtio send command slow                                     |
| inspector_pod_net_softirq_schedslow          | net_softirq    | Softirq sched slow (from `softirq_raise()` to `softirq_entry()`) |
| inspector_pod_net_softirq_schedslow100ms     | net_softirq    | Softirq sched latency exceeds 100ms                          |
| inspector_pod_net_softirq_excuteslow         | net_softirq    | Softirq execute slow (from `softirq_entry()` to `softirq_exit()`) |
| inspector_pod_net_softirq_excuteslow100ms    | net_softirq    | Softirq execute latency exceeds 100ms                        |

## Events

### Event List

Event supported by KubeSkoop exporter are listed below.

| Event Name              | Probe Name     | Description                                                  | Event Body                                                   |
| ----------------------- | -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| TXLAT_QDISC_100MS       | netiftxlatency | qdisc latency exceeds 100ms during transmission              | 5-tuple(protocol, saddr, sport, daddr, dport), latency       |
| TXLAT_NETDEV_100MS      | netiftxlatency | netdev transmit latency exceeds 100ms during transmission    | 5-tuple(protocol, saddr, sport, daddr, dport), latency       |
| BIOLAT_10MS             | biolatency     | Block IO latency exceeds 10ms                                | process name, pid, latency                                   |
| BIOLAT_100MS            | biolatency     | Block IO latency exceeds 100ms                               | process name, pid, latency                                   |
| RXKERNEL_SLOW           | kernellatency  | Kernel packet receiving latency exceeds 100ms                | 5-tuple(protocol, saddr, sport, daddr, dport), latency in different locations |
| TXKERNEL_SLOW           | kernellatency  | Kernel packet transmitting latency exceeds 100ms             | 5-tuple(protocol, saddr, sport, daddr, dport), latency in different locations |
| PACKETLOSS              | packetloss     | Packet dropped                                               | 5-tuple(protocol, saddr, sport, daddr, dport), stacktrace    |
| SOCKETLAT_READSLOW      | socketlatency  | Socket read slow                                             | 5-tuple(protocol, saddr, sport, daddr, dport), latency       |
| SOCKETLAT_SENDSLOW      | socketlatency  | Socket send slow                                             | 5-tuple(protocol, saddr, sport, daddr, dport), latency       |
| TCPRESET_NOSOCK         | tcpreset       | TCP connection sent RST because of no socket                 | 5-tuple(protocol, saddr, sport, daddr, dport), socket state  |
| TCPRESET_ACTIVE         | tcpreset       | TCP connection sent active RST because of close() syscall or linger, etc. | 5-tuple(protocol, saddr, sport, daddr, dport), socket state  |
| TCPRESET_PROCESS        | tcpreset       | TCP connection sent RST because of  exception in handshaking, etc. | 5-tuple(protocol, saddr, sport, daddr, dport), socket state  |
| TCPRESET_RECEIVE        | tcpreset       | TCP connection received RST                                  | 5-tuple(protocol, saddr, sport, daddr, dport), socket state  |
| VIRTCMDEXCUTE           | virtcmdlatency | Virtio send command slow                                     | cpu, pid, latency                                            |
| NETSOFTIRQ_SCHED_SLOW   | net_softirq    | Softirq sched slow (from `softirq_raise()` to `softirq_entry()`) | cpu, pid, latency                                            |
| NETSOFTIRQ_SCHED_100MS  | net_softirq    | Softirq sched latency exceeds 100ms                          | cpu, pid, latency                                            |
| NETSOFTIRQ_EXCUTE_SLOW  | net_softirq    | Softirq execute slow (from `softirq_entry()` to `softirq_exit()`) | cpu, pid, latency                                            |
| NETSOFTIRQ_EXCUTE_100MS | net_softirq    | Softirq execute latency exceeds 100ms                        | cpu, pid, latency                                            |

