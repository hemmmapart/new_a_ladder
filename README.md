## 新梯子的最基本制备过程  
### 1、安装软件
```bash
yum install epel-release
yum update
yum install python-setuptools m2crypto supervisor
yum -y install wget
wget "tar -xzvf pip-1.5.4.tar.gz
cd pip-1.5.4
python setup.py installhttps://pypi.python.org/packages/source/p/pip/pip-1.5.4.tar.gz#md5=834b2904f92d46aaa333267fb1c922bb" --no-check-certificate
pip install shadowsocks
```
### 2、
```bash
vi /etc/shadowsocks.json 
```
输入一下配置：
```bash
{
	"server":"0.0.0.0",  #your_IP
	"server_port":server_port,    
	"local_port":1080,
	"password":"password",
	"timeout":600,
	"method":"aes-256-cfb"
}
```
### 3、
```bash
vi /etc/supervisord.conf
```
添加以下到末尾处：
```bash
[program:shadowsocks]
command=ssserver -c /etc/shadowsocks.json
autostart=true
autorestart=true
user=root
log_stderr=true
logfile=/var/log/shadowsocks.log
```
### 4、
```bash
vi /etc/rc.local
```
添加：
```bash
service supervisord start
```
### 5、启动/关闭
```bash
启动服务：
ssserver -c /etc/shadowsocks.json -d start
停止服务：
ssserver -c /etc/shadowsocks.json -d stop
```
