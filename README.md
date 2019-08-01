# SpringCloudDemo
基于springboot1.x的spring cloud项目

## 依赖服务
### etcd
#### 版本
3.2.25
#### 单节点部署：
##### 清空etcd上原有的数据
（只有在需要清空的时候才执行此操作）\
`rm -rf /tmp/etcd/`
##### 用docker启动etcd服务
```
docker run -d \
-p 2379:2379 \
-p 2380:2380 \
--volume=/tmp/etcd:/etcd-data \
--name etcd-single etcd:3.2.25 \
/usr/local/bin/etcd \
--data-dir=/etcd-data --name etcd-node-0 \
--initial-advertise-peer-urls http://10.5.7.245:2380 --listen-peer-urls http://0.0.0.0:2380 \
--advertise-client-urls http://10.5.7.245:2379 --listen-client-urls http://0.0.0.0:2379
```
##### 浏览器访问etcd
在浏览器页面输入：`http://localhost:2379/v2/keys/spring/cloud/discovery`出现如下页面：
![Image text](https://github.com/Cherry522/SpringCloudDemo/blob/master/README-img/etcd-1.jpg)

##### 注册服务到etcd后
启动config服务，config服务注册到etcd后，再次访问etcd，显示页面如下：
![Image text](https://github.com/Cherry522/SpringCloudDemo/blob/master/README-img/etcd-2.jpg)

##### 通过在etcd上查看服务是否具体启动成功
浏览器访问：`http://localhost:2379/v2/keys/在etcd上的key的名字`
比如:`http://localhost:2379/v2/keys/spring/cloud/discovery/config`
![Image text](https://github.com/Cherry522/SpringCloudDemo/blob/master/README-img/etcd-3.jpg)



