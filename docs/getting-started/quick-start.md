---
sidebar_position: 2
---

# Quick Start

How to diagnose your kubernetes cluster by KubeSkoop?

## Kind of kubernetes network issues:

* Persistent network failure
  Most of persistent network failure issue are misconfig of network stack, e.g. error iptables rule, misconfig of VM security group.
  KubeSkoop generates a traffic graph by analyzing the link of `src->dst`, and then performs rule verification and simulation on the nodes and edges on the graph to locate the network misconfiguration.

* Occasional network jitter
  Occasional packet delays, losses, and retransmissions in network links often lead to application jitter problems. Because they are sporadic, it is difficult to trace back and locate the root cause of the problem.
  KubeSkoop monitors the key path of the protocol stack in the kernel through eBPF in-depth, integrates multiple indicators to correlate typical jitter scenarios, and records and traces back to the root cause of network anomalies.

* Network performance bottlenecks
  Application network dependencies are usually associated with many network links, such as upstream and downstream services, DNS resolution, etc., and it is difficult to analyze the root cause when the performance cannot improve.
  KubeSkoop finds out key links that affect performance by analyzing application-related links and application-layer bottlenecks.

## Installation

You can quickly deploy KubeSkoop, Prometheus, Grafana and Loki to your cluster via [skoopbundle.yaml](deploy/skoopbundle.yaml).

```bash
kubectl apply -f https://github.com/alibaba/kubeskoop/deploy/skoopbundle.yaml
```

***Note: skoopbundle.yaml starts with the minimum number of replicas and default configurations, which is not suitable for production environments.***

When installation is done, you can acess the KubeSkoop Web Console by service `webconsole`.

```bash
kubectl get svc -n kubeskoop webconsole
```

You may need a `Nodeport` or `LoadBalancer` to acess from outside of the cluster.

Default username is `admin`, and password is `kubeskoop`.

![Web Console](/img/web_console.png)

### Network diagnosis

#### Connectivity Diagnosis

Connectivity diagnosis can be submitted through the web console.

![Diagnose](/img/diagnose.png)

Under **Diagnosis - Connectivity Diagnosis**, you can enter the source address, destination address, port, and protocol for diagnosis, and click `Diagnose` to submit the diagnosis. After the diagnosis is complete, you can see the result in the history list.

![Diagnosis Result](/img/diagnosis_result.png)

#### Packet Capturing

Under **Diagnosis - Packet Capturing**，you can perform packet capturing for node/pod in the cluster.

![Packet Capturing](/img/packet_capturing.png)

#### Latency Detection

Under **Diagnosis - Latency Detection**，you can detect latencies between multiple nodes and pods.

![Latency Detection](/img/ping_mesh.png)

### Monitor network jitter and bottlenecks

#### Network Performance Dashboard

View the network permance dashboard from **Monitoring - Dashboard**. In the dashboard, you can check the water level of each monitor item corresponding to the time point of the performance problem.
![grafana_performance](/img/monitoring.png)

#### Network Jitter & Anomy Event Analysis

Under **Monitoring - Event**, you can view the anomaly events occurring within the cluster at the current time point. You can also manually select the desired time range, or filter based on event type, node, and information such as the namespace/name of the Pod where the event occurred.

Click `Live` on the right top to view the live event stream according to the current filters.
![Events](/img/events.png)

#### Network Link Graph

Under the homepage or **Monitoring - Network Graph**, you can see the actual network link graph in the cluster, with time and namespaces. You can also switch view mode to `Table` to view each connection.
