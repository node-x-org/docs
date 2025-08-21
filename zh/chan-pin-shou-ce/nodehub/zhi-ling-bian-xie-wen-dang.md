---
description: 以下示例仅供参考，因每个指令编写情况可能不同。
---

# 指令編寫與文檔

## NodeHub 指令編寫與部署文檔（繁體中文）

### 一、安裝指令

#### 1. 安裝模版

若指令執行超過 1 分鐘則可能導致失敗，建議使用下方模版將指令後台運行，以避免佔用 NodeHub 執行緒：

```bash
bash_file=$HOME/XXXX.sh
cat > $bash_file <<'bashEOF'
#!/bin/bash
XXXXXXXX
XXXXXXXXXXXXXXX
bashEOF
sudo chmod +x $bash_file
nohup bash $bash_file $KEY > install_XXXX.log 2>&1 &
```

若需參數傳入版本：

```bash
cat > $HOME/XXXX.sh <<'NODEEOF'
#!/bin/bash
parameter=$1
XXXXXXXX
XXXXXXXXXXXXXXX
NODEEOF

nohup bash $HOME/XXXX.sh $PARAMETER > install_XXXX.log 2>&1 < /dev/null &
```

> ⚠️ 請在「變數」欄填寫 `PARAMETER`，並在說明中補充該參數用途。

#### 2. 資源限制問題

若專案運行時資源使用不斷上升，可考慮使用以下方式限制：

**(1) Docker**

**使用 docker run：**

```bash
docker run -d \
  --name my_container \
  --cpus=".5" \
  --memory="256m" \
  --blkio-weight=500 \
  my_image
```

**使用 docker-compose：**

```yaml
version: '3.8'
services:
  my_service:
    image: my_image
    deploy:
      resources:
        limits:
          cpus: '0.5'
          memory: 256M
        reservations:
          cpus: '0.25'
          memory: 128M
    blkio_config:
      weight: 500
```

**(2) systemd**

**Systemd 服務檔案示例：**

```ini
[Unit]
Description=My Custom Service

[Service]
ExecStart=/usr/bin/my_executable
MemoryLimit=256M
CPUQuota=50%
IOReadBandwidth=8M
IOWriteBandwidth=8M

[Install]
WantedBy=multi-user.target
```

***

### 二、狀態檢查模版

#### Docker 方式：

```bash
PID=$(sudo docker inspect --format '{{.State.Pid}}' <容器名>)
if [ -n "$PID" ]; then
   echo "<項目名稱> is running (PID: $PID)."
   echo "running:$PID"
else
   echo "<項目名稱> is not running"
fi
```

#### PM2 / Systemctl / Screen：

```bash
pid=$(pgrep <進程名>)
if [ -n "$pid" ]; then
    echo "<進程名> is running:$pid"
else
    echo "<進程名> is not running"
fi
```

***

### 三、健康檢查

健康檢查需返回 `true` 或 `false`，以下為示例：

```bash
STATUS_OUTPUT=$(sphnctl fizz status 2>&1)
if echo "$STATUS_OUTPUT" | grep -q "Active - your node is currently active!"; then
    echo "true"
else
    echo "false"
fi
```

***

### 四、升級檢查

尚未統一模版。目的是：檢查當前版本與最新版本是否不同。

***

### 五、查詢最近 100 條日誌

```bash
pid=$(pgrep pop)
if [ -n "$pid" ]; then
    tail -n 100 pipe.log
else
    tail -n 100 install_pipe.log
fi
```

***

### 六、模擬輸入（expect腳本）

#### 自動填寫密碼：

```bash
expect -c "
spawn ./set-password.sh
set timeout 10
expect {
    \"Enter the password for accessing the Dashboard:\" {
        sleep 10
        send \"$1\r\"
    }
    timeout {
        puts \"Timeout waiting for password prompt\"
        exit 1
    }
}
expect eof
"
```

#### 單獨 expect 腳本範例：

```bash
#!/usr/bin/expect
if { $argc!= 1 } {
    puts "Usage: $argv0 password"
    exit 1
}
set password [lindex $argv 0]
spawn ./set-password.sh
set timeout 10
expect {
    "Enter the password for accessing the Dashboard:" {
        sleep 10
        send "$password\r"
    }
    timeout {
        puts "Timeout waiting for password prompt"
        exit 1
    }
}
expect eof
```

***

### 七、升級

以 t3rn 專案為例：

```bash
function download_t3rn() {
    mkdir -p t3rn
    cd t3rn
    curl -s https://api.github.com/repos/t3rn/executor-release/releases/latest \
    | grep -Po '"tag_name": "\\K.*?(?=")' \
    | xargs -I {} wget https://github.com/t3rn/executor-release/releases/download/{}/executor-linux-{}.tar.gz
    tar -xzf executor-linux-*.tar.gz
}
```

***

### 八、停止、重啟、卸載

#### 停止：

```bash
docker stop <容器名>
pm2 stop <進程名>
screen -S <屏幕名> -X quit
systemctl stop <服務名>
```

#### 重啟：

```bash
docker restart <容器名>
pm2 restart <進程名>
systemctl daemon-reload
systemctl enable <服務名>
systemctl restart <服務名>
```

#### 卸載：

```bash
docker stop XXXX && rm -rf install_XXXX.* && rm -rf $HOME/項目資料夾/
```

***

### 九、備份與路徑

#### 備份：

```bash
mkdir -p /root/backup && tar -czvf /root/backup/XXXX.tar.gz /path/to/target
```

#### 備份文件路徑：

```
/root/backup/XXXX.tar.gz
```

***

### 十、自定義腳本

可根據實際需求新增腳本，自定義內容不設限，無需範例。

***

### 結語

希望此文檔能幫助您更高效地編寫指令與節點腳本，靈活應對各類專案需求。若有更多實戰經驗，歡迎在社群中交流與補充。
