# QQBot
## 1 Create new QQ
3059509092
## 2 Create new vps and connect by ssh
If use Ubuntu, we need to adjust the config of ssh.
```shell
vim /etc/ssh/sshd_config
```
Change the port of ssh to connect in college because the firewall bans the 22 port.

Ubuntu use root to connect the vps.

First change the password.
```shell
sudo passwd root
```
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
