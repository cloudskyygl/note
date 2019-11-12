# Shadowsocks 安装与配置

操作系统为 Ubuntu 16.04 

内核升级和开启 BBR 加速参考此文章 https://www.dz9.net/blog/4246.html

**命令行要特别注意 python 和 pip 的版本问题**

1. 从 https://pypi.org/project/pip/ 安装 pip

```
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py

python3 get-pip.py
```

2. 安装 Shadowsocks

```
pip3 install shadowsocks
```

3. 编写配置文件

```
vi /etc/shadowsocks.json
```

内容为

```
{ 
   "server":"server_ip", 
   "server_port":25, 
   "local_address": "127.0.0.1", 
   "local_port":1080, 
   "password":"mypassword",
   "timeout":300, 
   "method":"aes-256-cfb", 
   "fast_open": false
}
```

4. 启动 Shadowsocks 服务器

```
ssserver -c /etc/shadowsocks.json

#后台启动和停止

ssserver -c /etc/shadowsocks.json -d start
ssserver -c /etc/shadowsocks.json -d stop
```

日志保存位置为 `/var/log/shadowsocks.log`