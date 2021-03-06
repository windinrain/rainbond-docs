---
title: 快速安装
summary: 快速在线安装云帮.
toc: false
toc_not_nested: true
asciicast: true
---

<div id="toc"></div>

<!--
&emsp;&emsp;通过grctl在线安装云帮。
-->
## 安装前准备

{{site.data.alerts.callout_danger}}

确保第一个节点可以ssh免密登陆其他节点。

{{site.data.alerts.end}}


## 安装

{{site.data.alerts.callout_danger}}
首先确保当前用户是root或者具有root权限。
{{site.data.alerts.end}}

### 快速安装

{% include copy-clipboard.html %}
```bash
# 通过此脚本可快速安装上线云帮 (管理节点 & 计算节点)
bash <(curl -s https://repo.goodrain.com/install/3.4/start.sh)
```

<!--
### 拆分安装

- 安装grctl

{% include copy-clipboard.html %}
```bash
bash -c "$(curl -s repo.goodrain.com/install/grctl)"
```
grctl是云帮datacenter controller util,通过此命令初始化集群，扩容节点。更多细节请参考[组件：grctl](http://www.rainbond.com/docs/stable/platform-maintenance/add-management-node/component-introduction/grctl.html)

- 初始化集群

{% include copy-clipboard.html %}
```bash
# 默认会将第一个节点初始化为管理节点&计算节点
grctl init
```

- 安装计算节点服务

```bash
# 获取第一个节点的uid
uuid=$(cat /etc/goodrain/host_uuid.conf | awk -F '=' '{print $2}')
# 安装计算节点服务
grctl install compute --nodes $uuid
```

- 上线计算节点

```
grctl node up $uuid
# ready字段显示为true
grctl node list
```

- 访问web控制台

```bash
# 第一个节点的ip
grctl show
<ip>:7070
```

-->

- grctl

grctl是云帮datacenter controller util,通过此命令初始化集群，扩容节点。更多细节请参考[组件：grctl](http://www.rainbond.com/docs/stable/platform-maintenance/add-management-node/component-introduction/grctl.html)

- 扩容相关节点参考

[扩容计算节点](http://www.rainbond.com/docs/stable/platform-maintenance/add-compute-node/install-command.html)

- 安装使用问题FQA

安装使用问题，更多请参照 [平台安装，维护-常见问题](http://rb.goodrain.com/docs/stable/FAQs/install-maintenance-faqs.html)

{{site.data.alerts.callout_danger}}
- 首先应安装云帮的主节点(上面的命令即是安装主节点的命令)。
- 主节点具备云帮平台的所有功能，但不支持高可用。
- 高可用特性需要将集群至少扩容到3个节点。
{{site.data.alerts.end}}
