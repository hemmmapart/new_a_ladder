#### 记录一下装新梯子的过程，方便以后复现，以后看需求决定要不要写成脚本形式
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
## 加速配置
bbr 实际加速感觉一般，这里我用的别人写的脚本的 brook 端口转发加速
### 1、
```bash
wget -N --no-check-certificate https://raw.githubusercontent.com/ToyoDAdoubiBackup/doubi/master/brook-pf.sh && chmod +x brook-pf.sh && bash brook-pf.sh
```
运行如下指令运行脚本执行操作即可
```bash
bash brook-pf.sh
```

### 防火墙配置

关闭 22 端口，以其他端口作为进入通道（端口）
