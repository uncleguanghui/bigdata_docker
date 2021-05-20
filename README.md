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

第一步，先添加以下端口到入站规则里：2181、2888、3888、9092、9093、6379，或者关闭防火墙（不建议）。

第二步，修改 `.env` 的内容为：

1. `MACHINE_ID`：每台机器分别修改为不同的数字，例如机器 B 的 MACHINE_ID 修改为 2。
1. `SERVER_IP`：每台机器分别修改为本机的 IP 地址，注意不能一样，也不能是 0.0.0.0/127.0.0.1/localhost 等。
1. `ZOO_SERVERS`：将 server.x 的值修改为 0.0.0.0:2888:3888（这里的 x 就是上面的 MACHINE_ID 对应的数字），其他 server.y 的值改为对应的 IP:2888:3888。
1. `ZOO_CONNECT`：3 台机器的 IP:2181，用半角逗号分隔开。

第三步，运行容器：

```shell script
docker-compose up -d
```

🔥 **注意**：如果修改过 `.env` 或 `docker-compose.yml` 两个文件后，导致无法启动 kafka，只需要把当前目录下的 kafka 目录删掉，再重新运行 `docker start kafka` 就可以了。redis、zookeeper 亦如此。
