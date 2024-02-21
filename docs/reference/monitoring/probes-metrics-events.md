# Probes, Metrics and Events

This documentation will introduce probes supported by KubeSkoop exporter, with their metrics and events.

## Probes

Probes supported by KubeSkoop exporter are listed below.

| Probe Name     | Description                                               | Probe Type      | Data Source | Overhead |
| -------------- | --------------------------------------------------------- | --------------- | ----------- | -------- |
| conntrack      | Statistics of conntrack                                   | Metrics         | netlink     | Low      |
| qdisc          | Statistics of tc qdisc                                    | Metrics         | netlink     | Low      |
| fd             | Statistics of file and socket descriptor                  | Metrics         | procfs      | Medium   |
| io             | Statistics of process IO                                  | Metrics         | procfs      | Low      |
| ipvs           | Statistics of IPVS                                        | Metrics         | procfs      | Low      |
| netdev         | Statistics of network device                              | Metrics         | procfs      | Low      |
| tcpext         | Statistics of the TCPExt                                  | Metrics         | procfs      | Low      |
| tcp            | Statistics of TCP from snmp                               | Metrics         | profcs      | Low      |
| udp            | Statistics of UDP                                         | Metrics         | profcs      | Low      |
| ip             | Statistics of IP                                          | Metrics         | profcs      | Low      |
| sock           | Statistics of socket                                      | Metrics         | procfs      | Low      |
| softnet        | Statistics of packet sent and dropped from network device | Metrics         | procfs      | Low      |
| tcpsummary     | Statistics of TCP queue and connection status             | Metrics         | procfs      | Medium   |
| netiftxlatency | Trace network delay during transmission                   | Metrics, Events | eBPF        | High     |
| biolatency     | Trace delay during block IO                               | Metrics, Events | eBPF        | Medium   |
| kernellatency  | Trace latency in kernel                                   | Metrics, Events | eBPF        | High     |
| packetloss     | Trace packet loss                                         | Metrics, Events | eBPF        | Medium   |
| socketlatency  | Trace latency in socket                                   | Metrics, Events | eBPF        | High     |
| tcpreset       | Trace TCP reset                                           | Events          | eBPF        | Low      |
| virtcmdlatency | Trace latency in virtio device                            | Metrics, Events | eBPF        | High     |
| net_softirq    | Trace latency in software interrupt                       | Metrics, Events | eBPF        | High     |

## Metrics

### Metric Labels

Theses labels are present on all metrics.

| Label Name       | Description                    |
| ---------------- | ------------------------------ |
| target_pod       | Pod name or "hostNetwork"      |
| target_namespace | Pod namespace or "hostNetwork" |
| target_node      | Node name                      |

### Metric List

| Metric Name                                  | Probe Name     | Description                                                  |
| -------------------------------------------- | -------------- | ------------------------------------------------------------ |
| inspector_pod_conntrackfound                 | conntrack      | conntrack statistics "found"                                 |
| inspector_pod_conntrackinvalid               | conntrack      | conntrack statistics "invalid"                               |
| inspector_pod_conntrackignore                | conntrack      | conntrack statistics "ignore"                                |
| inspector_pod_conntrackinsert                | conntrack      | conntrack statistics "insert"                                |
| inspector_pod_conntrackinsertfailed          | conntrack      | conntrack statistics "insert_failed"                         |
| inspector_pod_conntrackdrop                  | conntrack      | conntrack statistics "drop"                                  |
| inspector_pod_conntrackearlydrop             | conntrack      | conntrack statistics "early_drop"                            |
| inspector_pod_conntrackerror                 | conntrack      | conntrack statistics "error"                                 |
| inspector_pod_conntracksearchrestart         | conntrack      | conntrack statistics "search_restart"                        |
| inspector_pod_conntrackentries               | conntrack      | conntrack global statistics "entries"                        |
| inspector_pod_conntrackmaxentries            | conntrack      | conntrack global statistics "max_entries"                    |
| inspector_pod_qdiscbytes                     | qdisc          | tc qdisc statistics "bytes"                                  |
| inspector_pod_qdiscpackets                   | qdisc          | tc qdisc statistics "packets"                                |
| inspector_pod_qdiscdrops                     | qdisc          | tc qdisc statistics "drops"                                  |
| inspector_pod_qdiscqlen                      | qdisc          | tc qdisc statistics "qlen"                                   |
| inspector_pod_qdiscbacklog                   | qdisc          | tc qdisc statistics "backlog"                                |
| inspector_pod_qdiscoverlimits                | qdisc          | tc qdisc statistics "overlimits"                             |
| inspector_pod_fdopenfd                       | fd             | opened fd in pod                                             |
| inspector_pod_fdopensocket                   | fd             | opened socket in pod                                         |
| inspector_pod_ioioreadsyscall                | io             | io read syscalls count in pod                                |
| inspector_pod_ioiowritesyscall               | io             | io write syscalls count in pod                               |
| inspector_pod_ioioreadbytes                  | io             | io read bytes in pod                                         |
| inspector_pod_ioiowritebytes                 | io             | io write bytes in pod                                        |
| inspector_pod_ipvsconnections                | ipvs           | connections of IPVS in pod                                   |
| inspector_pod_ipvsincomingpackets            | ipvs           | incoming packets of IPVS in pod                                |
| inspector_pod_ipvsoutgoingbytes              | ipvs           | outgoing bytes of IPVS in pod                                |
| inspector_pod_ipvsincomingbytes              | ipvs           | incoming bytes of IPVS in pod                                |
| inspector_pod_ipvsoutgoingpackets            | ipvs           | outgoing packets of IPVS in pod                              |
| inspector_pod_netdevrxbytes                  | netdev         | rx bytes of all network devices in pod                       |
| inspector_pod_netdevrxerrors                 | netdev         | rx errors of all network devices in pod                      |
| inspector_pod_netdevtxbytes                  | netdev         | tx bytes of all network devices in pod                       |
| inspector_pod_netdevtxerrors                 | netdev         | tx error of all network devices in pod                       |
| inspector_pod_netdevrxpackets                | netdev         | rx packets of all network devices in pod                     |
| inspector_pod_netdevrxdropped                | netdev         | rx dropped packets of all network devices in pod             |
| inspector_pod_netdevtxpackets                | netdev         | tx packets of all network devices in pod                     |
| inspector_pod_netdevtxdropped                | netdev         | tx dropped packets of all network devices in pod             |
| inspector_pod_tcpextlistendrops              | tcpext         | ListenDrops of TCPExt                                        |
| inspector_pod_tcpextlistenoverflows          | tcpext         | ListenOverflow of TCPExt                                     |
| inspector_pod_tcpexttcpsynretrans            | tcpext         | TCPSynRetrans of TCPExt                                      |
| inspector_pod_tcpexttcpfastretrans           | tcpext         | TCPFastRetrans of TCPExt                                     |
| inspector_pod_tcpexttcpretransfail           | tcpext         | TCPRetransFail of TCPExt                                     |
| inspector_pod_tcpexttcptimeouts              | tcpext         | TCPTimeouts of TCPExt                                        |
| inspector_pod_tcpexttcpabortonclose          | tcpext         | TCPAbortOnClose of TCPExt                                    |
| inspector_pod_tcpexttcpabortonmemory         | tcpext         | TCPAbortOnMemory of TCPExt                                   |
| inspector_pod_tcpexttcpabortontimeout        | tcpext         | TCPAbortOnTimeout of TCPExt                                  |
| inspector_pod_tcpexttcpabortonlinger         | tcpext         | TCPAbortOnLinger of TCPExt                                   |
| inspector_pod_tcpexttcpabortondata           | tcpext         | TCPAbortOnData of TCPExt                                     |
| inspector_pod_tcpexttcpabortfailed           | tcpext         | TCPAbortFailed of TCPExt                                     |
| inspector_pod_tcpexttcpackskippedsynrecv     | tcpext         | TCPACKSkippedSynRecv of TCPExt                               |
| inspector_pod_tcpexttcpackskippedpaws        | tcpext         | TCPACKSkippedPAWS of TCPExt                                  |
| inspector_pod_tcpexttcpackskippedseq         | tcpext         | TCPACKSkippedSeq of TCPExt                                   |
| inspector_pod_tcpexttcpackskippedfinwait2    | tcpext         | TCPACKSkippedFinWait2 of TCPExt                              |
| inspector_pod_tcpexttcpackskippedtimewait    | tcpext         | TCPACKSkippedTimeWait of TCPExt                              |
| inspector_pod_tcpexttcpackskippedchallenge   | tcpext         | TCPACKSkippedChallenge of TCPExt                             |
| inspector_pod_tcpexttcprcvqdrop              | tcpext         | TCPRcvQDrop of TCPExt                                        |
| inspector_pod_tcpexttcpmemorypressures       | tcpext         | TCPMemoryPressures of TCPExt                                 |
| inspector_pod_tcpexttcpmemorypressureschrono | tcpext         | TCPMemoryPressuresChrono of TCPExt                           |
| inspector_pod_tcpextpawsactive               | tcpext         | PAWSActive of TCPExt                                         |
| inspector_pod_tcpextpawsestab                | tcpext         | PAWSEstab of TCPExt                                          |
| inspector_pod_tcpextembryonicrsts            | tcpext         | EmbryonicRsts of TCPExt                                      |
| inspector_pod_tcpexttcpwinprobe              | tcpext         | TCPWinProbe of TCPExt                                        |
| inspector_pod_tcpexttcpkeepalive             | tcpext         | TCPKeepAlive of TCPExt                                       |
| inspector_pod_tcpexttcpmtupfail              | tcpext         | TCPMTUPFail of TCPExt                                        |
| inspector_pod_tcpexttcpmtupsuccess           | tcpext         | TCPMTUPSuccess of TCPExt                                     |
| inspector_pod_tcpexttcpzerowindowdrop        | tcpext         | TCPZeroWindowDrop of TCPExt                                  |
| inspector_pod_tcpexttcpbacklogdrop           | tcpext         | TCPBacklogDrop of TCPExt                                     |
| inspector_pod_tcpextpfmemallocdrop           | tcpext         | PFMemallocDrop of TCPExt                                     |
| inspector_pod_tcpexttcpwqueuetoobig          | tcpext         | TCPWqueueTooBig of TCPExt                                    |
| inspector_pod_tcpactiveopens                 | tcp            | ActiveOpens of TCP                                           |
| inspector_pod_tcppassiveopens                | tcp            | PassiveOpens of TCP                                          |
| inspector_pod_tcpretranssegs                 | tcp            | RetransSegs of TCP                                           |
| inspector_pod_tcpattemptfails                | tcp            | AttemptFails of TCP                                          |
| inspector_pod_tcpestabresets                 | tcp            | EstabResets of TCP                                           |
| inspector_pod_tcpcurrestab                   | tcp            | CurrEstab of TCP                                             |
| inspector_pod_tcpinsegs                      | tcp            | InSegs of TCP                                                |
| inspector_pod_tcpoutsegs                     | tcp            | OutSegs of TCP                                               |
| inspector_pod_tcpinerrs                      | tcp            | InErrs of TCP                                                |
| inspector_pod_tcpoutrsts                     | tcp            | OutRsts of TCP                                               |
| inspector_pod_udpindatagrams                 | udp            | InDatagrams of UDP                                           |
| inspector_pod_udpnoports                     | udp            | NoPorts of UDP                                               |
| inspector_pod_udpinerrors                    | udp            | InErrors of UDP                                              |
| inspector_pod_udpoutdatagrams                | udp            | OutDatagrams of UDP                                          |
| inspector_pod_udprcvbuferrors                | udp            | RcvbufErrors of UDP                                          |
| inspector_pod_udpsndbuferrors                | udp            | SndbufErrors of UDP                                          |
| inspector_pod_udpincsumerrors                | udp            | InCsumErrors of UDP                                          |
| inspector_pod_udpignoredmulti                | udp            | IgnoredMulti of UDP                                          |
| inspector_pod_ipinnoroutes                   | ip             | InNoRoutes of IP                                             |
| inspector_pod_ipintruncatedpkts              | ip             | InTruncatedPkts of IP                                        |
| inspector_pod_sockinuse                      | sock           | Inuse of sock                                                |
| inspector_pod_sockorphan                     | sock           | Orphan of sock                                               |
| inspector_pod_socktw                         | sock           | TW of sock                                                   |
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
| TCPRESET_PROCESS        | tcpreset       | TCP connection sent RST because of no socket or exception in handshaking, etc. | 5-tuple(protocol, saddr, sport, daddr, dport), socket state  |
| TCPRESET_RECEIVE        | tcpreset       | TCP connection received RST                                  | 5-tuple(protocol, saddr, sport, daddr, dport), socket state  |
| VIRTCMDEXCUTE           | virtcmdlatency | Virtio send command slow                                     | cpu, pid, latency                                            |
| NETSOFTIRQ_SCHED_SLOW   | net_softirq    | Softirq sched slow (from `softirq_raise()` to `softirq_entry()`) | cpu, pid, latency                                            |
| NETSOFTIRQ_SCHED_100MS  | net_softirq    | Softirq sched latency exceeds 100ms                          | cpu, pid, latency                                            |
| NETSOFTIRQ_EXCUTE_SLOW  | net_softirq    | Softirq execute slow (from `softirq_entry()` to `softirq_exit()`) | cpu, pid, latency                                            |
| NETSOFTIRQ_EXCUTE_100MS | net_softirq    | Softirq execute latency exceeds 100ms                        | cpu, pid, latency                                            |

