# RabbitMQ

## 消息队列

>消息队列，即MQ，Message Queue。消息队列是典型的：生产者、消费者模型。生产者不断向消息队列中生产消息，消费者不断的从队列中获取消息。因为消息的生产和消费都是异步的，而且只关心消息的发送和接收，没有业务逻辑的侵入，这样就实现了生产者和消费者的解耦。

## 消息队列的物种消息模式

![1527068544487](1527068544487.png)

## 安装RabbitMQ

### 1. 安装Erlang

```shell
    yum install esl-erlang_17.3-1~centos~6_amd64.rpm
    yum install erlang
```

### 2. 安装RabbitMQ

- 解压文件

```sh
    rpm -ivh rabbitmq-server-3.4.1-1.noarch.rpm
```

- 修改配置信息

```sh
    cp /usr/share/doc/rabbitmq-server-3.4.1/rabbitmq.config.example /etc/rabbitmq/rabbitmq.config
```

```config
    {loopback_users,[]}
```

- **注意要去掉后面的逗号**

### 3.启动应用

- service rabbitmq-server start  启动
- service rabbitmq-server stop  关闭
- service rabbitmq-server restart  重启

### 4. 设置开机启动

```sh
    chkconfig rabbitmq-server on
```
