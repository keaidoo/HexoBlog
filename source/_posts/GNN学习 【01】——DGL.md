---
title: GNN学习 【01】——DGL
author: 可爱多
avatar: https://cdn.jsdelivr.net/gh/keaidoo/CDN/img/custom/avatar3.jpg
authorLink: 
authorAbout: 喜爱一切可爱的事物～
authorDesc: 喜爱一切可爱的事物～
categories: 技术
date: 2019-6-04 16:11:01
comments: true
tags: 
 - 深度学习
keywords: GNN
description: 图神经网络
photos: http://pic.netbian.com/uploads/allimg/170605/130458-149663909840b3.jpg
---
## 学习内容：[DGL - Get Started](https://docs.dgl.ai)

## 讨论问题
### 1. 如何借助networkx创建dgl图？如何直接创建dgl图
networkx可以将图形可视化。
借助networkx创建dgl图

```
import networkx as nx
import dgl

g_nx = nx.petersen_graph()
g_dgl = dgl.DGLGraph(g_nx)
```
直接创建dgl图
```
import dgl
g = dgl.DGLGraph()
```
### 2. 如何添加结点和边？
添加结点：
```
# add 34 nodes into the graph; nodes are labeled from 0~33
    g.add_nodes(34)
```
添加边：
边缘在DGL是有方向的，让边具有双向性

```
# add edges two lists of nodes: src and dst
src, dst = tuple(zip(*edge_list))
g.add_edges(src, dst)
# edges are directional in DGL; make them bi-directional
g.add_edges(dst, src)
```

### 3. 如何访问结点的属性？

```
# access node set with integer, list, or integer tensor
g.nodes[0].data['x'] = th.zeros(1, 3)
g.nodes[[0, 1, 2]].data['x'] = th.zeros(3, 3)
g.nodes[th.tensor([0, 1, 2])].data['x'] = th.zeros(3, 3)
```

### 4. 访问边的属性有哪两种方法？

```
g.edata['w'] = th.randn(9, 2)

# access edge set with IDs in integer, list, or integer tensor
g.edges[1].data['w'] = th.randn(1, 2)
g.edges[[0, 1, 2]].data['w'] = th.zeros(3, 2)
g.edges[th.tensor([0, 1, 2])].data['w'] = th.zeros(3, 2)

# one can also access the edges by giving endpoints
g.edges[1, 0].data['w'] = th.ones(1, 2)                 # edge 1 -> 0
g.edges[[1, 2, 3], [0, 0, 0]].data['w'] = th.ones(3, 2) # edges [1, 2, 3] -> 0
```

### 5. 边和点的属性用什么数据结构进行存贮？边和点属性对应的scheme包含哪些信息？
用字典来进行存贮

```
#After assignments, each node/edge field will be associated with a scheme containing the shape and data type (dtype) of its field value.
print(g.node_attr_schemes())
g.ndata['x'] = th.zeros((10, 4))
print(g.node_attr_schemes())
```

对应的scheme包含了形状和数据类型

```
#Out:
{'x': Scheme(shape=(3,), dtype=torch.float32)}
{'x': Scheme(shape=(4,), dtype=torch.float32)}
```

### 6. 如何删除边或节点的属性？

```
#One can also remove node/edge states from the graph. This is particularly useful to save memory during inference.
g.ndata.pop('x')
g.edata.pop('w')
```

### 7. 什么叫multi graph。请举出一个现实的例子

Multigraphs ~~~ Many graph applications need multi-edges.
许多图的应用都需要多边。
构造类:```DGLGraph with multigraph=True```
实际例子：
1、地图，两个地点之间在地图上可能会有不同的路径。
2、同学之间的关系：两个同学可能有合作关系，合作论文，互相做实验，但是做的事情是不同的。

### 8. 在dgl库中，```message```和```reduce```分别完成什么功能？

首先，我们使用DGL的内置函数定义消息传递：
使用源节点“h”作为信息传递

```
def gcn_message(edges):
    # The argument is a batch of edges.
    # This computes a (batch of) message called 'msg' using the source node's feature 'h'.
    return {'msg' : edges.src['h']}
```

定义消息累和函数。
```
def gcn_reduce(nodes):
    # The argument is a batch of nodes.
    # This computes the new 'h' features by summing received 'msg' in each node's mailbox.
    return {'h' : torch.sum(nodes.mailbox['msg'], dim=1)}

```

### 9. 说明```send， recv,  update_all， copy_src```的功能。
发送消息到所有边
```
def pagerank_naive(g):
    # Phase #1: send out messages along all edges.
    for u, v in zip(*g.edges()):
        g.send((u, v))
```

接受消息来计算新的页面排名的值
```
    # Phase #2: receive messages to compute new PageRank values.
    for v in g.nodes():
        g.recv(v)
```
 通过所有的边来获取消息并更新所有的节点
```
def pagerank_level2(g):
    g.update_all()
```
利用源结点的特征属性来计算输出
```
dgl.function.copy_src(src, out) is an edge UDF that computes the output using the source node feature data.
```
### 10. 使用```builtin```函数有什么好处？
 使用内置函数的好处是：使用内置函数，比普通的Python实现，速度要快一倍左右。 代码简洁，提升性能。

### 11. 例子
```Batched Graph Classification with DGL```
在```Classifier.forward()```中，设隐层1节点数为256，隐层2节点数为266。输入层节点为1，对应一个graph，输出层 节点为8，对应8个类别。一个batch的大小为32，图的节点数为400。经过以下变换后，h的维度是多少？

 1. 调用 g.update_all 之前 :1

 2. g.update_all 之后 :1

 3. 经过线性变换之后:256

 4. 再次调用g.update_all 之后 :256

 5. 再次经过线性变换之后:266

 6. 调用dgl.mean_nodes之后 :266

 7. 调用classify之后:8