---
description: 以下示例仅供参考，因每个指令编写情况可能不同。
---

# 指令编写文档

&#x4E00;**、安装指令**\
**1、安装模版**

若指令执行超过1分钟则可能执行失败，编写安装指令时，可以使用下方的模版，使指令在后台运行，这样就不会占用 NODEHUB 的线程，避免执行失败。若某些指令执行时间较长，也可以使用 `nohup` 指令。

<pre><code>PARAMETER=$PARAMETER
cat > $HOME/XXXX.sh &#x3C;&#x3C;EOF
#!/bin/bash
parameter=$PARAMETER
XXXXXXXX
XXXXXXXXXXXXXXX
EOF
sudo chmod +x $HOME/XXXX.sh
<strong>nohup bash $HOME/XXXX.sh > install_XXXX.log 2>&#x26;1 &#x3C; /dev/null &#x26;
</strong></code></pre>

```
cat > $HOME/XXXX.sh <<'NODEEOF'
#!/bin/bash
parameter=$1
XXXXXXXX
XXXXXXXXXXXXXXX
NODEEOF
nohup bash $HOME/XXXX.sh $PARAMETER > install_XXXX.log 2>&1 < /dev/null &
```

然后下方添加变量，环境变脸一栏填写PARAMETER，说明一栏则填写关于该参数的描述。\
\
**2、关于资源限制问题**

当运行项目所占资源会随着时间不断增加，导致系统资源不断减少，因此需要进行资源限制，目前通常使用的工具就下面的两种，若有其他的方法大家可以在群里分享分享。\
（1）Docker管理的项目可以进行资源限制，当然也可以自己创建docker镜像使用docker进行管理并进行资源限制，更便于管理。

```
// 示例
# 使用docker run启动
docker run -d \
  --name my_container \
  --cpus=".5" \
  --memory="256m" \
  --blkio-weight=500 \
  my_image
```

```
// 示例
# 使用docker compose进行启动，如何编写文档
version: '3.8'

services:
  my_service:
    image: my_image
    deploy:
      resources:
        limits:
          cpus: '0.5'        # 限制 CPU 使用最高占0.5个CPU
          memory: 256M       # 限制内存最高占用256MB
        reservations:
          cpus: '0.25'       # 【可选】设置 CPU 使用最低占用0.25个CPU
          memory: 128M       # 【可选】设置内存最低占用 128MB
    blkio_config:
      weight: 500            # 【可选】设置磁盘 I/O 权重，设置对磁盘进行I/O操作的优先级
```

（2）systemd管理的项目也可以进行资源限制

```
// 编写服务文件示例
[Unit]
Description=My Custom Service

[Service]
ExecStart=/usr/bin/my_executable   # 替换为实际的可执行文件路径
MemoryLimit=256M                     # 限制内存使用为 256MB，即该服务最多占用256MB内存
CPUQuota=50%                         # 限制 CPU 使用率为 50%，即服务器总CPU的50%
IOReadBandwidth=8M                   # 限制 I/O 读带宽，即读取带宽最多8MB/s
IOWriteBandwidth=8M                  # 限制 I/O 写带宽，即写入带宽最多8MB/s

[Install]
WantedBy=multi-user.target
```

\
**二、状态检查模版**\
编写状态检查的指令

```
# 若该项目为docker运行，检查其容器是否存在且处于运行状态
PID=$(sudo docker inspect --format '{{.State.Pid}}' <容器名>)
if [ -n "$PID" ]; then
   echo "<项目名称> is running (PID: $PID)."
   echo "running:$PID"
else
   echo "<项目名称> is not running"
fi
```

```
# 若该项目为pm2、systemctl、screen运行，则检查其进程是否存在
pid=$(pgrep <进程名>)
if [ -n "$pid" ]; then
    echo "<进程名> is running:$pid"
else
    echo "<进程名> is not running"
fi
```

**三、健康检查**

健康检查因每个项目情况不同，没有模版，但最终需要返回 `true` 或 `false`，NODEHUB 会获取其返回的值，`true` 为健康，`false` 为不健康。以下是一些健康检查的判断依据：

* 项目运行日志
* 项目的cli工具中存在查看status的指令
* 项目面板上存在检查节点状态的端口

例子：

```
# 这里以SPHERON项目为例子
STATUS_OUTPUT=$(sphnctl fizz status 2>&1)

# 检查输出中是否包含"Active - your node is currently active!"
if echo "$STATUS_OUTPUT" | grep -q "Active - your node is currently active!"; then
    echo "true"
else
    echo "false"
fi
```

**四、升级检查**

升级检查用于检查当前安装的版本以及获取项目最新版本，如果两个版本不同，则提醒该项目可以升级到新的版本。目前没有写升级检查，后续更新。

**五、查询最近100条日志**

若项目状态不正常，可以查看最近 100 条日志。可根据状态检查编写查看日志指令：\
例子：

```
# 检查最近100条日志
pid=$(pgrep pop)
if [ -n "$pid" ]; then
    tail -n 100 pipe.log
else
    tail -n 100 install_pipe.log
fi
```

**六、模拟输入**\
若项目的工具或其他工具在执行后弹出提示输入参数而不能通过指令解决时，可以使用 `expect` 脚本或语句，也可以应对TTY报错。\
例子：

```
# 具体场景
root@vmi2339892:~/shardeum# ./set-password.sh

Password requirements: 
min 8 characters, at least 1 lower case letter, at least 1 upper case letter, at least 1 number, at least 1 special character !@#$%^&*()_+$ 

Enter the password for accessing the Dashboard: *******
```

```
# 在bash脚本中使用expect语句
# 检查是否安装了expect
if ! command -v expect &> /dev/null; then
    echo "'expect' is not installed. Attempting to install..."
    
    # 尝试通过 apt 安装 expect（适用于 Debian/Ubuntu）
    if sudo apt-get install -y expect; then
        echo "'expect' installed successfully."
    else
        echo "Failed to install 'expect'. Please install it manually."
        exit 1
    fi
fi

# 检查是否提供了密码参数
if [ $# -ne 1 ]; then
    echo "Usage: $0 password"
    exit 1
fi

expect -c "
spawn ./set-password.sh
set timeout 10

expect {
    \"Enter the password for accessing the Dashboard:\" 
    {
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

```
# 另一种办法，调用编写的expect脚本
#!/usr/bin/expect

if { $argc!= 1 } {
    puts "Usage: $argv0 password"
    exit 1
}
set password [lindex $argv 0]
spawn ./set-password.sh
set timeout 10

expect {
    "Enter the password for accessing the Dashboard:" 
    {
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

**七、升级**

升级指令目的为部署节点更新到最新版本，有些项目方有自动升级的方法则可以不用编写，例如SPHERON,

当然大部分是需要手动升级的，偷个懒，拿t3rn这个现成的做个例子：

```
# 脚本太长，就将方法写这里
function download_t3rn() {
    # Create and navigate to t3rn directory
    mkdir -p t3rn
    cd t3rn
    
    # Download latest release
    curl -s https://api.github.com/repos/t3rn/executor-release/releases/latest | \
    grep -Po '"tag_name": "\K.*?(?=")' | \
    xargs -I {} wget https://github.com/t3rn/executor-release/releases/download/{}/executor-linux-{}.tar.gz
    
    # Extract the archive
    tar -xzf executor-linux-*.tar.gz
}
```

**八、停止、重启以及卸载**

停止、重启以及卸载：需要看项目是由什么管理的，这个我就不赘述了，懂得都懂

&#x20;例子：

<pre><code># 停止
<strong># docker管理:
</strong>docker stop &#x3C;容器名>
# pm2管理：
pm2 stop &#x3C;设置的进程名>
# screen管理：
screen -S &#x3C;设置的屏幕名> -X quit
# systemctl管理：
systemctl stop &#x3C;服务文件名>
</code></pre>

```
# 重启：若重启需要很长时间，则可以使用nohup
# docker管理:
docker restart <容器名>
# pm2管理：
pm2 restart <设置的进程名>
# screen管理则先关闭之前的屏幕，再重新部署一次
# systemctl管理：
systemctl daemon-reload
systemctl enable <服务文件名>
systemctl restart <服务文件名>
```

```
# 卸载:先停止项目进程或容器，再删除加载的资源文件，当然若有重要的文件或秘钥，需要先备份
docker stop XXXX && rm -rf install_XXXX.* && rm -rf $HOME/项目文件夹/
```

九、备份及备份文件地址

备份就是将必要文件夹或存储重要秘钥的文件压缩保存在特定的文件夹下\
备份文件地址则为备份文件保存的文件路径

```
# 备份
mkdir -p  && tar -czvf <压缩文件路径> <被压缩文件夹路径或文件路径>
```

```
# 备份文件地址
/root/backup/XXXX.tar.gz
```

十、自定义脚本\
每个项目不同，可能这几个默认脚本并不满足，则可以点击增加脚本进行自定义脚本，这个我就不举例了。

结语

希望文档能够帮助大家更高效的编写指令。面对不同的项目需求，灵活运用上述模版和方法。如在实践中遇到问题，欢迎与大家在群里讨论。
