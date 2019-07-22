# Linux

## 命令行

## 切换到ROOT

>su root

## 查看文件内容

>vim 文件名

## 端口操作

- 开启某个端口
  >firewall-cmd --zone=public --add-port=端口号/tcp --permanent
- 查看端口是否开启
  >firewall-cmd --query-port=端口号/tcp
- 永久删除8080端口，禁止外网访问
  >firewall-cmd --permanent --remove-port=8080/tcp

## 文件写权限

>chmod ［who］ ［+ | - | =］ ［mode］ 文件名
>
>e: chmod 777 -R /home/PycharmProjects/

## 查看程序是否执行

>ps -ef | grep 程序名

## 设置程序开机启动

>chkconfig 程序名 on

## 防火墙操作

- 查看防火墙状态
  >sudo systemctl start firewalld

- 关闭防火墙
  >sudo systemctl stop firewalld

- 开启防火墙
  >sudo systemctl status firewalld

## **文件操作**

- 复制操作
  >cp 初始文件全路径  目标路径
  - a ：将文件的特性一起复制
  - p ：连同文件的属性一起复制，而非使用默认方式，与-a相似，常用于备份
  - i ：若目标文件已经存在时，在覆盖时会先询问操作的进行
  - r ：递归持续复制，用于目录的复制行为
  - u ：目标文件与源文件有差异时才会复制

- 删除操作
  >rm 文件名
  - f ：就是force的意思，忽略不存在的文件，不会出现警告消息- i ：互动模式，在删除前会询问用户是否操作
  - r ：递归删除，最常用于目录删除，它是一个非常危险的参数

- 移动操作
  >mv 初始文件路径  目标文件路径
  - f ：force强制的意思，如果目标文件已经存在，不会询问而直接覆盖
  - i ：若目标文件已经存在，就会询问是否覆盖
  - u ：若目标文件已经存在，且比目标文件新，才会更新

- 查看当前工作目录的全路径
  >pwd -P

## 文件解压

- 压缩解压
  >tar 文件名
  - c ：新建打包文件
  - t ：查看打包文件的内容含有哪些文件名
  - x ：解打包或解压缩的功能，可以搭配-C（大写）指定解压的目录，注意-c,-t,-x不能同时出现在同一条命令中
  - j ：通过bzip2的支持进行压缩/解压缩
  - z ：通过gzip的支持进行压缩/解压缩
  - v ：在压缩/解压缩过程中，将正在处理的文件名显示出来
  - f filename ：filename为要处理的文件
  - C dir ：指定压缩/解压缩的目录dir

## 创建文件目录

- mkdir
  >mkdir 文件夹名
  - m, --mode=模式，设定权限<模式> (类似 chmod)，而不是 rwxrwxrwx 减 umask
  - p, --parents  可以是一个路径名称。此时若路径中的某些目录尚不存在,加上此选项后,系统将自动建立好那些尚不存在的目录,即一次可以建立多个目录;
  - v, --verbose  每次创建新目录都显示信息

## 删除目录

- rmdir
  >rmdir 文件夹名
  - p 递归删除目录dirname，当子目录删除后其父目录为空时，也一同被删除。如果整个路径被删除或者由于某种原因保留部分路径，则系统在标准输出上显示相应的信息。
  - v --verbose  显示指令执行过程
  