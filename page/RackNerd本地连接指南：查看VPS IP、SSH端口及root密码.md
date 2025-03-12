# RackNerd本地连接指南：查看VPS IP、SSH端口及root密码

购买 [RackNerd](https://bit.ly/Rack_Nerd) VPS 后，您需要获取并配置SSH连接信息，包括服务器的IP地址、SSH端口和root账户密码，以便在本地设备上进行远程连接操作。无论您使用的是Windows、Mac电脑或移动设备，本文将为您逐步解答如何查找和使用这些信息，实现便捷连接。

---

## 一、获取RackNerd远程连接信息

在完成 [RackNerd](https://bit.ly/Rack_Nerd) VPS的购买后，RackNerd会发送包含连接信息的邮件到您注册的邮箱，邮件标题通常为“KVM VPS Login Information”。如果您没有在邮箱中找到这封邮件，可以通过以下步骤在RackNerd后台直接获取这份信息：

1. 登录到您的RackNerd账户。
2. 进入【View Email Log】页面。
3. 找到标题为“KVM VPS Login Information”的邮件记录。
4. 点击【View Message】查看详细的SSH连接信息，包括IP地址、SSH端口以及root密码。

确保记录下这些信息，后续操作都需要使用它们。

👉 [【建议收藏】2025年RackNerd最新优惠套餐整理汇总 - 每日更新可用活动优惠](https://bit.ly/Rack_Nerd)

---

## 二、本地连接RackNerd VPS教程

通过上述步骤获取到连接信息后，您即可在本地设备上使用SSH工具连接到RackNerd VPS。以下是几种常见设备和工具的使用方法：

### Windows用户

推荐使用免费的SSH连接工具，例如Xshell或PuTTY进行连接：

- [Xshell使用教程：如何用Xshell连接Linux](https://bit.ly/Rack_Nerd)
- [PuTTY使用教程：基于PuTTY远程连接Linux VPS的方法](https://bit.ly/Rack_Nerd)

### Mac用户

Mac操作系统自带终端工具，无需额外下载任何软件。打开终端输入以下命令即可连接：

bash
ssh root@<服务器IP地址> -p <端口号>


### 安卓设备用户

安卓设备可通过JuiceSSH工具实现远程连接，应用商店可免费获取。使用手持设备轻松管理VPS。

### 苹果设备用户

iPhone或iPad推荐使用Termius工具，该应用支持用户界面的交互操作，是远程管理的实用工具。

---

只需通过支持SSH连接的工具，将获取的RackNerd登录信息正确配置，便可在任意设备上便捷连接您的VPS。希望这篇指南能够帮助您快速上手，开始使用RackNerd VPS实现高效管理和操作！