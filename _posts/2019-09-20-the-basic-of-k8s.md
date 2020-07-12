## k8s 基础概念

1、一个k8s集群包括

- 一个Master节点（主节点）

- 一群Node节点（计算节点）

2、`Master节点`

包括API Server、Scheduler、Controller manager、etcd。

- API Server是整个系统的对外接口，供客户端和其它组件调用，相当于“营业厅”。

- Scheduler负责对集群内部的资源进行调度，相当于“调度室”。

- Controller manager负责管理控制器，相当于“大总管”。

- etcd保存了整个集群的状态。

3、`Node节点`

Node节点包括Docker、kubelet、kube-proxy、Fluentd、kube-dns（可选），还有就是Pod。

- Pod是Kubernetes最基本的操作单元。一个Pod代表着集群中运行的一个进程，它内部封装了一个或多个紧密相关的容器。除了Pod之外，K8S还有一个Service的概念，一个Service可以看作一组提供相同服务的Pod的对外访问接口。

- Kubelet，主要负责监视指派到它所在Node上的Pod，包括创建、修改、监控、删除等。

- Kube-proxy，主要负责为Pod对象提供代理。

- Fluentd，主要负责日志收集、存储与查询。

4、

参考文章：

- [10分钟看懂Docker和K8S](https://my.oschina.net/jamesview/blog/2994112)

- [集群创建和Hello World](https://juejin.im/post/5efde9066fb9a07ead0f3d8d)
