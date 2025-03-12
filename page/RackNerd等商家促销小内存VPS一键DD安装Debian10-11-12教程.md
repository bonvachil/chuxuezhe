# RackNerd等商家促销小内存VPS一键DD安装Debian10-11-12教程

许多商家提供的小内存 VPS，往往默认只支持安装低版本的系统，如 Debian9 或 Debian10。当尝试使用常规方法 DD Debian11 或 Debian12 时，由于内存不足可能会导致安装失败。本文将以 RackNerd 的促销 VPS 为例，介绍如何在小内存VPS上成功安装 Debian11 或 Debian12 系统。

👉 [【建议收藏】2025年Racknerd最新优惠套餐整理汇总 - 每日更新可用活动优惠](https://bit.ly/Rack_Nerd)

## 第 1 步：DD服务商提供的同版本系统

首先，根据服务商默认提供的 Debian 版本选择相同版本的 DD 镜像进行安装。如果服务商提供的是 Debian9，就安装 Debian9；如果提供的是 Debian10，就安装 Debian10。这种方式能够保持稳定，避免因越级而导致卡死或失败。

**Debian9 DD命令：**

bash
bash <(wget --no-check-certificate -qO- 'https://raw.githubusercontent.com/MoeClub/Note/master/InstallNET.sh') -d 9 -v 64 -p "设置密码" -firmware


**Debian10 DD命令：**

bash
bash <(wget --no-check-certificate -qO- 'https://raw.githubusercontent.com/MoeClub/Note/master/InstallNET.sh') -d 10.3 -v 64 -p "设置密码" -firmware


## 第 2 步：更新当前系统

在 DD 安装完成后，建议将当前版本的包更新到最新，以确保系统稳定性。运行以下命令：

bash
apt update
apt upgrade -y
apt dist-upgrade -y
apt autoclean
apt autoremove -y


更新过程中可能会收到重新启动服务或更新配置文件的提示。在涉及到关键库（如 libpam、libc 和 libssl）更新时，选择 "**是 (Yes)**"，系统服务会自动重新启动；若出现 OpenSSH 配置文件更新提示，选择 "**保留当前版本 (Keep current version)**"。完成更新后，使用以下命令重启系统：

bash
reboot


## 第 3 步：替换sources.list文件

接下来，需要将 `/etc/apt/sources.list` 文件中的软件源替换为对应版本的 Debian 源（例如 Debian10 或 Debian11 的源）。您可以选择逐级升级（如 Debian9 升级到 Debian10，再升级到 Debian11），也可以直接越级到某个目标版本（如 Debian9 直接升级到 Debian12）。

请查找适合的源并替换，国内的用户建议使用国内镜像源以提升下载速度。

## 第 4 步：系统升级

执行以下命令将系统升级至目标版本：

bash
apt update
apt upgrade -y
apt dist-upgrade -y


期间的选项操作与第2步类似。完成升级后，使用以下命令重启系统：

bash
reboot


## 第 5 步：验证系统版本

升级完成后，在重新启动系统后，可以通过以下命令验证当前操作系统版本：

bash
cat /etc/os-release


输出内容将显示已成功升级至目标版本的 Debian 系统。

接下来，可选择清理旧版软件包及其依赖项以释放空间，但需确保清理的软件包不影响当前环境的正常运行：

bash
apt autoclean
apt autoremove -y


如果您选择逐级升级版本，则重复第2步至第5步即可完成所有版本的升级。

至此，小内存 VPS 成功安装 Debain11 或 Debian12 系统的教程结束，祝您使用愉快！