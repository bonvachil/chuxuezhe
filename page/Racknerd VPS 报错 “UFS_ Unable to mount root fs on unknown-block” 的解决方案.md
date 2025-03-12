# Racknerd VPS 报错 “UFS: Unable to mount root fs on unknown-block” 的解决方案

最近，我在 Racknerd 的 2023 黑五活动中购买了一台价格较高的 Linux VPS，操作系统选择的是 Ubuntu 22.04，机房位于洛杉矶 DC02（亚洲优化线路）。然而，在使用过程中，偶然遇到了 “UFS: unable to mount root fs on unknown-block” 的启动报错问题。以下是我的排查与解决步骤分享。

👉 [【建议收藏】2025年Racknerd最新优惠套餐整理汇总 - 每日更新可用活动优惠](https://bit.ly/Rack_Nerd)

---

## 遇到的问题

最初，我完成了系统的基本配置工作，包括：

- **更新系统软件包列表**：确保系统和软件包保持最新。
- **开启 BBR 加速** 以优化网络性能：
  bash
  # 设置默认队列调度算法为 "fq"
  echo "net.core.default_qdisc=fq" >> /etc/sysctl.conf
  # 设置 TCP 拥塞控制算法为 "bbr"
  echo "net.ipv4.tcp_congestion_control=bbr" >> /etc/sysctl.conf
  # 立即应用新的系统控制参数
  sysctl -p
  

然而，在第二次尝试通过 SSH 连接 VPS 时，遇到了无法连接的问题。即使配置了代理，依然无效。为了排查问题，我通过 Racknerd 的控制面板对 VPS 执行了重启操作，但 VPS 卡在重启界面并显示错误信息。通过 VNC 连接查看，系统提示报错信息为：`UFS: unable to mount root fs on unknown-block`。

---

## 排查与解决步骤

经过网络搜索和查阅资料，我找到了有效的解决方案。以下是具体操作流程：

### 1. 启动旧内核进入系统

1. 登录 Racknerd 控制面板后，选择 **Shutdown** 停机操作。
2. 使用 VNC 远程连接，在启动初期选择 **Advanced options for Ubuntu**。
3. 从列表中选择一个旧版本内核（例如：`Linux 5.5.0-70-generic`），进入系统。

### 2. 修复问题

进入旧内核后，根据 [Ask Ubuntu 社区的相关问题解答](https://askubuntu.com/questions/41930/kernel-panic-not-syncing-vfs-unable-to-mount-root-fs-on-unknown-block0-0)，我采取了以下操作：

- 更新并重新安装与内核加载相关的关键模块和依赖。
- 确保 GRUB 的更新以及系统引导配置文件正确。

完成这些操作后，重新启动新内核（例如：`5.15.0-88-generic`），发现系统成功进入。

---

## 网络故障的修复

虽然系统已成功启动，但出现网络连接不上的问题。排查过程中，我检查了 `/etc/resolv.conf` 文件（用于 DNS 配置），发现其默认配置为 Google 的公共 DNS，无明显错误。我尝试更新为以下 DNS 配置后重启网络服务，但依然无效：

bash
nameserver 1.1.1.1  # CF DNS
nameserver 8.8.8.8  # Google DNS


后来，在参考更多资料后，发现解决方案是如下步骤：
1. 在旧内核中安装与新内核相关的网络依赖。
2. 使用 `reboot` 命令重启 VPS。

最终，网络恢复正常，并且成功切换至新内核。

---

## 经验总结

通过整个排查过程，我对 VPS 系统问题有了更多了解。这次遇到问题后没有选择直接重装系统，而是一步步分析并解决问题，感受到了迎难而上所带来的成就感。如果你也遇到类似问题，建议按照本文方法尝试修复，希望对你有所帮助！

---

你是否也在关注 VPS 活动？别错过 [Racknerd 最新优惠合集](https://bit.ly/Rack_Nerd)，获取最新套餐信息和每日更新的优惠活动！