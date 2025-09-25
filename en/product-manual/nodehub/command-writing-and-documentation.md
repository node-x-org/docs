---
description: >-
  The following examples are for reference only, as each command writing
  situation may vary.
---

# Command Writing and Documentation

<p align="right"><a href="https://docs.node-x.xyz/chan-pin-shou-ce/nodehub/zhi-ling-bian-xie-yu-wen-dang">中文</a></p>

## NodeHub Command Writing and Deployment Documentation

### 1.Installation Commands

1. **Install Template**\
   If the command execution exceeds 1 minute, it may fail. It is recommended to run the command in the background using the template below to avoid occupying the NodeHub thread:

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

{% hint style="info" %}
⚠️ Please fill in PARAMETER in the "Variables" column, and include the purpose of the parameter in the description.
{% endhint %}

### 2.Resource Limitation Issues

If resource usage increases continuously during project operation, consider limiting it using the methods below:

**(1) Docker**

Using docker run:

```bash
docker run -d \
  --name my_container \
  --cpus=".5" \
  --memory="256m" \
  --blkio-weight=500 \
  my_image
```

Using docker-compose:

```bash
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

**(2)systemctl**

Example Systemd service file:

```bash
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

### 2.Status Check Templates

**Docker method:**

```bash
PID=$(sudo docker inspect --format '{{.State.Pid}}' <Container Name>)
if [ -n "$PID" ]; then
   echo "<Project Name> is running (PID: $PID)."
   echo "running:$PID"
else
   echo "<Project Name> is not running"
fi
```

**PM2 / Systemctl / Screen：**

```bash
pid=$(pgrep <Process Name>)
if [ -n "$pid" ]; then
    echo "<Process Name> is running:$pid"
else
    echo "<Process Name> is not running"
fi
```

### 3.Health Check

Health checks should return true or false. Here is an example:

```bash
STATUS_OUTPUT=$(sphnctl fizz status 2>&1)
if echo "$STATUS_OUTPUT" | grep -q "Active - your node is currently active!"; then
    echo "true"
else
    echo "false"
fi
```

### 4.Upgrade Check

No unified template yet. The goal: check whether the current version differs from the latest version.

### 5.Query the last 100 logs

```bash
pid=$(pgrep pop)
if [ -n "$pid" ]; then
    tail -n 100 pipe.log
else
    tail -n 100 install_pipe.log
fi
```

### 6.Simulated input (expect script)

**Auto-fill password:**

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

**Standalone expect script example:**

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

### 7.Upgrade

Taking the t3rn project as an example:

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

### 8.Stop, Restart, Uninstall

* Stop:

```bash
docker stop <Container Name>
pm2 stop <Process Name>
screen -S <Screen Name> -X quit
systemctl stop <Service Name>
```

* Restart:

```
docker restart <Container Name>
pm2 restart <Process Name>
systemctl daemon-reload
systemctl enable <Service Name>
systemctl restart <Service Name>
```

* Uninstall:

```
docker stop XXXX && rm -rf install_XXXX.* && rm -rf $HOME/Project Folder/
```

### 9.Backup and Paths

**Backup:**

```
mkdir -p /root/backup && tar -czvf /root/backup/XXXX.tar.gz /path/to/target
```

**Backup file path:**

```
/root/backup/XXXX.tar.gz
```

### 10.Custom ScriptsCustom Scripts

You can add scripts according to actual needs, with no restrictions on custom content and no examples required. Most custom scripts are used for personal or interactive purposes.



### Conclusion

We hope this document helps you write commands and node scripts more efficiently, enabling flexible responses to various project requirements. If you have practical experience, feel free to share and contribute within the community.
