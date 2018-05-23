# cecos-caas
----
## 管理节点（自动）

#### 安装
curl -s https://raw.githubusercontent.com/aiminickwong/cecos-caas/master/cecos-caas-deploy | bash
#### 删除
curl -s https://raw.githubusercontent.com/aiminickwong/cecos-caas/master/cecos-caas-deploy | bash -s clean

----
### 部署代理（手动）
#### Docker Swarm (HOST)  主机模式
curl -s https://raw.githubusercontent.com/aiminickwong/cecos-caas/master/cecos-caas-agent-deploy | bash

如果您还为部署主机为 Docker Swarm 集群模式，

请先执行命令 “ docker swarm init ” 初始您的节点为 Docker Swarm 集群模式

###### 注意：连接代理不支持主机模式工作（ 非 Docker Swarm 集群模式 -- 不支持！）

