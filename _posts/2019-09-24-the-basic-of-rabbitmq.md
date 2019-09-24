### Rabbit MQ 基础概念

`Exchange`：交换机，接收消息，根据路由键转发消息到绑定的队列

`Binding`：Exchange和Queue之间的虚拟连接，binding中可以包含routing key

`Binding key`： 在绑定（Binding）Exchange与Queue的同时，一般会指定一个binding key；消费者将消息发送给Exchange时，一般会指定一个routing key；当binding key与routing key相匹配时，消息将会被路由到对应的Queue中。

`Routing key`：一个路由规则，虚拟机可用它来确定如何路由一个特定消息

`Queue`：也称为Message Queue,消息队列，保存消息并将它们转发给消费者，消费者直接监听队列就能收到消息了


### 学习教程

- [RabbitMq 教程](https://blog.csdn.net/hellozpc/article/details/81436980)