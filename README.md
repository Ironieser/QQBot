# Installation guide of zhenxun bot
## 0 Introduction
I installed the bot on the Tencent Cloud.
```
# Too expensive! Not recommended!
System: Ubuntu Server 18.04.1 LTS 64bit
location: shanghai
CPU: 2 core
mem: 2GB
bandwidth: 4Mbps
Price: 50 yuan per month
```

## 1 Create new QQ
Such as my new bot: 3059509092
## 2 Create new vps and connect by ssh
Add one new port for ssh because my college's firewall bans the 22 port.
```shell
vim /etc/ssh/sshd_config
# Add new port
Port 40230
```
If use Ubuntu, we need to adjust the config of ssh becuase the default user is not root.
First change the password.
```shell
sudo passwd root
```
Then revise the config of sshd.
```shell
sudo vi /etc/ssh/sshd_config 
```
To
```shell
PermitRootLogin yes
PasswordAuthentication yes
```
At last
```shell
sudo service ssh restart
```
## 3 create new virtual env
```shell
wget -c https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh
chmod 777 Miniconda3-latest-Linux-x86_64.sh #给执行权限
bash Miniconda3-latest-Linux-x86_64.sh #运行
cd /home/miniconda3/bin/
chmod 777 activate 
. ./activate
# mirrors of tsinghua
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/bioconda/
# create new virtual env
conda create -n name python==<version>
```
## 4 install go-cqhttp
```shell
wget https://github.com/Mrs4s/go-cqhttp/releases/download/v1.0.0-rc1/go-cqhttp_linux_amd64.tar.gz
tar -xczf go-cqhttp_linux_amd64.tar.gz
cd go-cqhttp_linux_amd64.tar.gz
# run go-cqhttp first time.
./go-cqhttp
# choose the third item which is reverse websocket
```
Then modify the comfig.yml as shown blow.
```config
uin:your bot qq
# need open 8080 port.
universal: ws://127.0.0.1:8080/onebot/v11/ws/
# restart go-cqhttp
./go-cqhttp
```
need another package for audio item
```shell
sudo apt install -y ffmpeg
```
## 5 install Postgresql database
```shell
# first update the apt tool
sudo apt update
# install postgresql and postgresql-contrib
sudo apt install postgresql postgresql-contrib
```
Create new database
```shell
# switch usr
sudo su - postgres
psql
```
```psql
       #  用户名↓                # 密码↓
 CREATE USER uname WITH PASSWORD 'zhenxun';      # 创建用户
         # 数据库名称↓       所有者↓
 CREATE DATABASE testdb OWNER uname;             # 创建数据库
```
## 6 install zhenxun bot
```shell
git clone -b main http://github.com/HibiKier/zhenxun_bot.git
cd zhenxun_bot
pip3 install poetry     
poetry install          

# if use conda virtual env , dont need to do.
poetry shell            

## playwright install chromiuw which is the headless browser.
playwright install chromium
playwright install-deps chromium
```
configure the super root
```python
vim .env.dev 
# add qq of super user
SUPERUSERS=["your qq"]
```
```shell
vim configs/config.py
```
```python
bind: str = ""  
sql_name: str = "postgresql"
user: str = "uname"
password: str = "zhenxun"
address: str = "127.0.0.1"
port: str = "5432"
database: str = "testdb"
```
## 7 run bot
```shell
python3 bot.py
```
## 8 screen
