---
title: "alpaca设计文档"
date: 2024-01-20 18:13:52.872 +0800
summary: 'How to use hugo with the theme "paperMod"'
weight: 3
author: "MaisJet"
showToc: true
TocOpen: false
hidemeta: false
comments: false
disableHLJS: true 
disableShare: true
hideSummary: false
searchHidden: false
ShowReadingTime: false
ShowBreadCrumbs: false
ShowPostNavLinks: false
---
{{< katex >}}

## grpc通信
### proto设计
采用分层架构：ApplicationLayer , Datamodels , DomainLayer

#### ApplicationLayer
定义流式服务+task/node服务 

可以在这里首先拆解task/node结构，因为这两者是消息的核心，与后面的爬虫模块关系也十分紧密。

对于**task**，依照使用场景可以发现子节点需要拿到根节点的任务消息并提交任务结果，分别使用Unary RPC 和 Stream RPC ：

```
message TaskServiceSend{
  string node_key = 1;
  string task_id = 2;

}

service TaskService{
    rpc Get(Request) returns (Response) {}; //获取任务采用Unary RPC
    rpc Subscribe(stream StreamMessage) returns (Response) {};  //典型的流式文件上传需求
    rpc SendInformation(TaskServiceSend) returns (Response) {}; //提交单次信息
}
```

对于**node**，这是整个系统抽象的核心，考虑到rpc规范，我们需要拨号注册，subscribe与unsubscribe

#### Datamodels
这一块比较简单，定义task/node基本属性就好

#### DomainLayer
这一部分需要定义好消息主体，包括request,response，其中的核心是定义stream_message，需要基本属性信息和包括运行命令的StreamMessageEnum：

```
message StreamMessage {
  StreamMessageEnum enum = 1;
  string node_id=2;
  string node_key = 3;
  string key = 4;
  string source_id = 5;
  string target_id = 6;
  bytes data = 7;
  string error = 8;
}
```

### 编译命令

采用绝对路径或者相对路径的编译命令均可，相对路径可以方便维护。




