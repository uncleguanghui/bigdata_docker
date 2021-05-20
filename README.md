# Multiarch Bigdata Docker

在多种架构下，统一大数据环境部署。

目前支持 `amd64`、`arm/v7`、`arm64`，树莓派上也可以运行~

## 单节点部署

修改 `.env` 文件的内容为

```text
ZOO_SERVERS=server.1=0.0.0.0:2888:3888
```

然后，运行

```shell script
docker-compose up -d
```

## 多节点集群部署

假设部署 3 台机器。

步骤如下：

1. 修改 `docker-compose.yml` 文件：机器 1 的 ZOO_ID 为 1，机器 2 的 ZOO_ID 为 2，机器 3 的 ZOO_ID 为 3。
1. 修改 `docker-compose.yml` 文件：机器 1 的 KAFKA_BROKER_ID 为 1，机器 2 的 KAFKA_BROKER_ID 为 2，机器 3 的 KAFKA_BROKER_ID 为 3。
1. 修改 `.env` 文件的 ZOO_SERVERS 变量：机器 1 的 server.1 值为 0.0.0.0:2888:3888，server.x 的值改为对应的 IP:2888:3888；机器 2 的 server.2 值为 0.0.0.0:2888:3888，server.x 的值改为对应的 IP:2888:3888；机器 3 的 server.3 值为 0.0.0.0:2888:3888，server.x 的值改为对应的 IP:2888:3888；
1. 修改 `.env` 文件的 ZOO_CONNECT 变量：IP 替换为 3 台机器的 IP

注意到了吧，ZOO_ID、KAFKA_BROKER_ID，以及 `.env` 文件中的值为 0.0.0.0:2888:3888 的 server.x 里的 x，这三个数字要保持一样。

然后，运行

```shell script
docker-compose up -d
```
