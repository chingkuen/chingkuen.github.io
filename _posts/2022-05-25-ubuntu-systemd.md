---
layout: post
title: Ubuntu Systemd
subtitle: Ubuntu Systemd
categories: linux
tags: [linux]
---

# Ubuntu systemd

Create a echo server Python script in /opt/echo_server.py

```python
#!/usr/bin/env python3
import socket

# 建立 socket
serv = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# 綁定所有網路介面的 9000 連接埠
serv.bind(('0.0.0.0', 9000))

# 開始接受 client 連線
serv.listen()

while True:

    # 接受 client 連線
    conn, addr = serv.accept()
    print('Client from', addr)

    while True:

        # 接收資料
        data = conn.recv(1024)

        # 若無資料則離開
        if not data: break

        # 傳送資料
        conn.send(data)

    conn.close()
    print('Client disconnected')
```

## Create new system service unit

Create a new service file

/etc/systemd/system/echo_server.service

```linux
[Unit]
Description=Echo Server

[Service]
Type=simple
ExecStart=/opt/echo_server.py
Restart=always

[Install]
WantedBy=multi-user.target
```

Change the permission of the file

```linux
sudo chmod 644 /etc/systemd/system/echo_server.service
```

## Reload the systemd service

```linux
sudo systemctl daemon-reload
```

## Start the customized systemd service

```linux
sudo systemctl start echo_server
```

## Check the status of the customized systemd service

```linux
systemctl status echo_server
```

## Stop the customized systemd service

```linux
sudo systemctl stop echo_server
```

## Autostart the customized systemd service when start Ubuntu 

```linux
sudo systemctl enable echo_server
```

## Stop autostart the customized systemd service when start Ubuntu

```linux
sudo systemctl disable echo_server
```

## The example of Systemd service unit file

```linux
[Unit]
# 服務名稱
Description=Your Server

# 服務相關文件
# Documentation=https://example.com
# Documentation=man:nginx(8)

# 設定服務啟動的先後相依姓，例如在網路啟動之後：
# After=network.target

[Service]
# 行程類型
Type=simple

# 啟動服務指令
ExecStart=/opt/your_command

# 服務行程 PID（通常配合 forking 的服務使用）
# PIDFile=/run/your_server.pid

# 啟動服務前，執行的指令
# ExecStartPre=/opt/your_command

# 啟動服務後，執行的指令
# ExecStartPost=/opt/your_command

# 停止服務指令
# ExecStop=/opt/your_command

# 停止服務後，執行的指令
# ExecStopPost=/opt/your_command

# 重新載入服務指令
# ExecReload=/opt/your_command

# 服務終止時自動重新啟動
Restart=always

# 重新啟動時間格時間（預設為 100ms）
# RestartSec=3s

# 啟動服務逾時秒數
# TimeoutStartSec=3s

# 停止服務逾時秒數
# TimeoutStopSec=3s

# 執行時的工作目錄
# WorkingDirectory=/opt/your_folder

# 執行服務的使用者（名稱或 ID 皆可）
# User=myuser

# 執行服務的群組（名稱或 ID 皆可）
# User=mygroup

# 環境變數設定
# Environment="VAR1=word1 word2" VAR2=word3 "VAR3=$word 5 6"

# 服務輸出訊息導向設定
# StandardOutput=syslog

# 服務錯誤訊息導向設定
# StandardError=syslog

# 設定服務在 Syslog 中的名稱
# SyslogIdentifier=your-server

[Install]
WantedBy=multi-user.target
```

Reference: https://ithelp.ithome.com.tw/articles/10199339