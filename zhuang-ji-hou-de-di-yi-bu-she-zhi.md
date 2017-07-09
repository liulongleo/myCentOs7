

1. 更新系统

yum -y update

2. 安装vim

yum install vim

3. 配置普通用户的sudo权限

先备份/etc/sudoers 

编辑/etc/sudoers

添加普通用户的sudo，可在Root 行下添加新用户的行

4. 设置ssh登录

a. 禁止root通过ssh登录

先备份/etc/ssh/sshd\_config

编辑/etc/ssh/sshd\_config, 将PermitRootLogin 设置为no

刷新生效 systemctl restart sshd.service

b. 修改ssh端口

已备份过/etc/ssh/sshd\_cofig

编辑Port为新端口，建议为10000以上

c. 修改防火墙端口

备份/usr/lib/firewalld/services/ssh.xml

编辑port端口与ssh端口一致

d. 修改SELinux设置

备份/etc/sysconfig/selinux

编辑selinux中SELINUX=permissive

5. 设置笔记本合盖不休眠

备份/etc/system/logind.conf

编辑HandleLidSwitch为lock

