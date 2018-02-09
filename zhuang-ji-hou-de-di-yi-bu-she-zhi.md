* 更新系统

yum -y update

* 安装vim

yum install vim

* 配置普通用户的sudo权限

先备份/etc/sudoers

编辑/etc/sudoers

添加普通用户的sudo，可在Root 行下添加新用户的行

* 设置ssh登录

a. 禁止root通过ssh登录 && 修改ssh端口

先备份/etc/ssh/sshd\_config

编辑/etc/ssh/sshd\_config, 将PermitRootLogin 设置为no

编辑Port为新端口，建议为10000以上

刷新生效 systemctl restart sshd.service


b. 通过ssh-copy-id命令在client端将公钥添加到服务器中，实现免密登录

默认使用ssh的22端口

ssh-copy-id -i ~/.ssh/id_rsa.pub "user@server"

自定义端口为

ssh-copy-id -i ~/.ssh/id_rsa.pub "-p 10022 user@server"

要求.ssh目录权限是755，文件authorized_keys的权限是600
`chmod 755 ~/.ssh`
`chmod 600 authorized_keys`

c. 修改防火墙端口

备份/usr/lib/firewalld/services/ssh.xml

编辑port端口与ssh端口一致

d. 修改SELinux设置

备份/etc/sysconfig/selinux

编辑selinux中SELINUX=permissive

* 设置笔记本合盖不休眠

备份/etc/system/logind.conf

编辑HandleLidSwitch为lock

