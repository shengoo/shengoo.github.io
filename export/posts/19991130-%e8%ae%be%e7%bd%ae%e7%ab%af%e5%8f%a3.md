title: Sql Server设置端口
link: http://www.sheng00.com/76.html
author: admin
description: 
post_id: 76
created: 1999/11/30 08:00:00
created_gmt: 1999/11/30 00:00:00
comment_status: open
post_name: %e8%ae%be%e7%bd%ae%e7%ab%af%e5%8f%a3
status: publish
post_type: post

# Sql Server设置端口

### 设置SQL Server服务器：

  1. “开始” → “程序” → “Microsoft SQL Server 2005” → “配置工具” → “SQL Server Configuration Manager”（确认“SQL Server Management Studio”已关闭）

  2. “SQL Server 2005 服务”中停止服务“SQL Server （SQLEXPRESS）”（默认是启动状态）

  3. “SQL Server 2005 网络配置” → “MSSQLSERVER 的协议”，启动“TCP/IP”（默认是禁用状态），然后双击“TCP/IP”进入属性设置，在“IP 地址”里，确认“IPAll”中的“TCP 端口”为1433

  4. “SQL Server 2005 服务”中启动服务“SQL Server （MSSQLSERVER ）”（默认是停止状态）

  5. 关闭“SQL Server Configuration Manager”（此时可以启动“SQL Server Management Studio”，并用帐户sa、密码123登录，SQL Server服务器设置正确的话应该能登录成功）