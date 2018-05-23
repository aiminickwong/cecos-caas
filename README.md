# cecos-caas
----
## 管理节点
### 集群自动模式
#### 安装
curl -s https://raw.githubusercontent.com/aiminickwong/cecos-caas/master/cecos-caas-deploy | bash
#### 删除
curl -s https://raw.githubusercontent.com/aiminickwong/cecos-caas/master/cecos-caas-deploy | bash -s clean

----
### 部署代理
#### Docker Swarm (HOST)  主机模式
curl -s https://raw.githubusercontent.com/aiminickwong/cecos-caas/master/cecos-caas-agent-deploy | bash

###### 注意：连接代理不支持主机模式工作（ 非DockerSwarm集群模式 -- 不支持！）

