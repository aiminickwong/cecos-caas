# cecos-caas

## 管理节点（自动）

#### 安装

curl -s https://raw.githubusercontent.com/aiminickwong/cecos-caas/master/cecos-caas-deploy | bash

#### 删除

curl -s https://raw.githubusercontent.com/aiminickwong/cecos-caas/master/cecos-caas-deploy | bash -s clean

------

</br>

## 部署代理（手动）

#### Docker Swarm (HOST)  主机模式

curl -s https://raw.githubusercontent.com/aiminickwong/cecos-caas/master/cecos-caas-agent-deploy | bash

如果您还为部署主机为 Docker Swarm 集群模式，

请先执行命令 “ docker swarm init ” 初始您的节点为 Docker Swarm 集群模式

###### 注意：连接代理不支持主机模式工作（ 非 Docker Swarm 集群模式 -- 不支持！）

------

</br>

## 附注：

### /etc/docker/daemon.json 文件的一些配置举例

</br>

注：修改daemon.json文件后需要执行命令
```
systemctl daemon-reload ; systemctl restart docker.service
```
才能生效

</br>

#### 中国镜像加速源（官方）

```
{
  "registry-mirrors": ["https://registry.docker-cn.com"]
}
```

</br>

#### 连接私有镜像（未启用安全认证的仓库）

```
{
  "insecure-registries" : ["yourPrivateRegistryIPaddress:5000"]
}
```

</br>

#### 开启接受远程连接模式

```
{
  "hosts": ["fd://", "tcp://0.0.0.0:2375"],
}
```

</br>

###### 可能遇到的问题

开启接受远程连接模式后无法启动docker服务，提示一下问题（ syslog 系统日志）：

```
unable to configure the Docker daemon with file /etc/docker/daemon.json: the following directives are specified both as a flag and in the configuration file: hosts: (from flag: [fd://], from file: [tcp://0.0.0.0:2375, unix:///var/run/docker.socket])
```

</br>

修改 '/lib/systemd/system/docker.service' 文件后

执行命令 'systemctl daemon-reload ; systemctl restart docker.service'

修复问题

</br>

修改前：
```
# ...省略
# 关键行
ExecStart=/usr/bin/dockerd -H fd://
# ...省略
```

</br>

修改后：
```
# ...省略
# 关键行
# ExecStart=/usr/bin/dockerd -H fd://
ExecStart=/usr/bin/dockerd
# ...省略
```

</br>

注意：部分系统 '/lib/systemd/system/docker.service' 文件的路径可能与上述路径不一样，请根据实际的文件路径修改文件。

</br>

#### 一个完整的配置样例

```
{
  "registry-mirrors": ["https://registry.docker-cn.com"],
  "hosts": ["fd://", "tcp://0.0.0.0:2375"],
  "insecure-registries" : ["192.168.100.100:5000"]
}
```
