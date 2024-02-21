---
sidebar_position: 4
---

# 网络链路图

:::tip
你需要在[Web控制台](./web-console.md)中使用该功能。
:::

KubeSkoop提供了网络链路图功能，可以查看集群中某个时间点节点之间的网络连接情况。
你可以在Web控制台的首页或者`Monitoring - Network Graph`页面查看网络链路图。

该功能依赖`flow`探针和`info`探针开启。

![Network Graph](/img/network-graph.png)

节点在图中将会以命名空间的形式分组（节点将会放置在`<Node>`分组中），并默认隐藏来自集群外部的节点。你可以通过启用`Show External Endpoints`来显示外部节点。

链路信息只会在进入页面时加载一次，你可以点击`Refresh`按钮来刷新链路信息。

## 展示历史时间的链路图

通过`Time`时间选择器，可以查询某个特定时间点15分钟范围内的链路信息。

## 根据命名空间筛选节点

你可以通过`Namespaces`下拉菜单来根据命名空间名称筛选节点。若不进行选择，则默认显示所有命名空间下的节点。

## 查看详细链路信息

通过切换`ViewMode`为`Table`模式，可以以表格形式查看详细的链路信息。除了源和目的节点之外，还会显示IP、端口、连接流量等详细信息。

![Network Graph Table](/img/network_graph_table.png)
