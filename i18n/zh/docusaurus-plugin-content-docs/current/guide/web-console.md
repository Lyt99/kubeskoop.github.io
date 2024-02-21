---
sidebar_position: 0
---

# Web控制台

KubeSkoop提供了方便用户使用的Web控制台，能够直接部署至集群内。KubeSkoop Web控制台提供了如下能力：

- 网络问题诊断
  - 网络连通性诊断
  - 抓包
  - 延迟探测
- 集群网络监控
  - 网络抖动和性能大盘
  - 网络抖动事件
  - 网络链路图

## 诊断网络问题

### 网络连通性诊断

可以通过Web控制台对集群内网络发起连通性诊断。

![Diagnose](/img/diagnose.png)

在 Diagnosis - Connectivity Diagnosis 下输入诊断的源地址、目的地址、端口和协议，点击`Diagnose` 发起诊断。诊断完成后，可以在列表中看到诊断结果。

![Diagnosis Result](/img/diagnosis_result.png)

### 抓包

你可以在Diagnosis - Packet Capturing中进行集群内Node/Pod的抓包操作。

![Packet Capturing](/img/packet_capturing.png)

:::tip
抓包过滤表达式使用pcap filter语法（和tcpdump所使用的一致），关于该语法的更多信息，请参考[手册](https://www.tcpdump.org/manpages/pcap-filter.7.html)。
:::

### 延迟探测

在Diagnosis - Latency Detection中，对集群内多个Node/Pod之间的网络延迟进行探测。

![Latency Detection](/img/ping_mesh.png)

## 监控集群网络

### 查看网络抖动和性能大盘

在Monitoring - Dashboard中，可以查看当前集群内网络大盘，从大盘中可查询对应性能问题时间点的各深度指标的水位情况。
![grafana_performance](/img/monitoring.png)

### 查看网络抖动事件

在Monitoring - Event下，可以看到当前时间点集群内产生的异常事件。你也可以手动选择需要的时间范围，或者根据事件类型、节点、事件产生的Pod命名空间/名称等信息进行筛选。

点击右上角的`Live`，可以实时根据当前筛选条件，实时监控集群内事件。

![Events](/img/events.png)

### 网络链路图

在主页或Monitoring - Network Graph中，可以看到当前集群内的网络实际链路图，并通过时间、命名空间进行筛选。你也可以将模式改为`Table`按条查看连接信息。

![Network Graph Table](/img/network_graph_table.png)
