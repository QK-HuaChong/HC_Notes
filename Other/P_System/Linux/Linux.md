# Linux

## 命令行

## 切换到ROOT

>su root

## 查看文件内容

>vim 文件名

## 开启某个端口

>firewall-cmd --zone=public --add-port=端口号/tcp --permanent

## 查看端口是否开启

>firewall-cmd --query-port=端口号/tcp

## 文件写权限

>chmod ［who］ ［+ | - | =］ ［mode］ 文件名
>
>e: chmod 777 -R /home/PycharmProjects/

## 查看程序是否执行

>ps -ef | grep 程序名

## 防火墙操作

### 查看防火墙状态

>sudo systemctl start firewalld

### 关闭防火墙

>sudo systemctl stop firewalld

### 开启防火墙

>sudo systemctl start firewalld
