# Racknerd VPS 配置指南：如何开放80-443端口解决Nginx访问问题

在搭建网站时，很多用户会选择Racknerd的海外VPS服务器。最近有用户反馈在CentOS 7系统上安装Nginx后，遇到了外网无法访问的问题。本文将详细介绍如何通过防火墙配置解决这个问题。

## 问题诊断与解决方案

当Nginx安装后外网无法访问，最常见的原因是防火墙未开放80(HTTP)和443(HTTPS)端口。以下是完整的排查和解决步骤：

### 第一步：验证Nginx是否正常运行

bash
$ wget http://127.0.0.1
--2025-01-03 20:11:34--  http://127.0.0.1/
正在连接 127.0.0.1:80... 已连接。
已发出 HTTP 请求，正在等待回应... 200 OK
长度：615 [text/html]
正在保存至: "index.html"
2025-01-03 20:11:34 (83.5 MB/s) - 已保存 "index.html" [615/615])

👉 [【点击查看】2025年最新 Racknerd 优惠码及特价云服务器方案汇总](https://bit.ly/Rack_Nerd)

### 第二步：检查端口开放状态

bash
$ firewall-cmd --query-port=80/tcp
output: no
$ firewall-cmd --query-port=443/tcp
output: no

### 第三步：开放必要端口

bash
$ firewall-cmd --permanent --add-port=80/tcp
output: success
$ firewall-cmd --permanent --add-port=443/tcp
output: success

### 第四步：重启防火墙使配置生效

bash
$ firewall-cmd --reload
output: success

## Firewall防火墙常用命令大全

掌握这些命令可以帮助你更好地管理VPS服务器的防火墙设置：

- **查看防火墙服务状态**
bash
$ systemctl status firewalld

- **检查防火墙运行状态**
bash
$ firewall-cmd --state

- **查看所有防火墙规则**
bash
$ firewall-cmd --list-all

- **查询特定端口状态**
bash
$ firewall-cmd --query-port=19999/tcp

- **开放/关闭端口**
bash
# 开放端口
$ firewall-cmd --permanent --add-port=80/tcp

# 关闭端口
$ firewall-cmd --permanent --remove-port=80/tcp

- **重启防火墙**
bash
$ firewall-cmd --reload

通过以上步骤，你应该已经成功解决了Racknerd VPS上Nginx无法通过外网访问的问题。如果仍有疑问，可以参考官方文档或联系技术支持。