# QQBot
## 1 Create new QQ
3059509092
## 2 Create new vps and connect by ssh
If use Ubuntu, we need to adjust the config of ssh.
```
vim /etc/ssh/sshd_config
```
Change the port of ssh to connect in college because the firewall bans the 22 port.

Ubuntu use root to connect the vps.

First change the password.
```
sudo passwd root
```
```
sudo vi /etc/ssh/sshd_config 
```
To
```
PermitRootLogin yes
PasswordAuthentication yes
```
