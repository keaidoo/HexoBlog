---
title: 使用Pycharm将数据库文件导入到MongoDB
author: 可爱多
avatar: https://cdn.jsdelivr.net/gh/keaidoo/CDN/img/custom/avatar.jpg
authorLink: 
authorAbout: 喜爱一切可爱的事物～
authorDesc: 喜爱一切可爱的事物～
categories: 技术
date: 2019-1-19 22:01:01
comments: true
tags: 
 - pycharm
keywords: pycharm
description: 
photos: https://cdn.jsdelivr.net/gh/keaidoo/cdn@1.2/img/custom/paperPhoto/8.jpg
---
## 1.工具：MongoDB,Pycharm

## 2.在Pycharm安装 pymongo

## 3.我是在虚拟环境下安装
因为不同的项目需要不同的环境，为了保持每个环境之间的纯净，这里我先进入一个我创建好的虚拟环境vene,如果没有虚拟环境，可以直接在cmd运行`pip install pymongo`。

### （1）`workon venv`   进入虚拟环境

### （2）`pip install pymongo`   安装pymongo

![Successfully installed pymongo-3.7.2, 成功安装
](https://upload-images.jianshu.io/upload_images/15933937-b60035101e55aa99.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


### (3)进入 pycharm-settings-Project Interpreter

![Project Interpreter看见pymongo
](https://upload-images.jianshu.io/upload_images/15933937-8deb98d24adf0369.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


## 4.创建 importMongo.py，代码如下：
```
# -*- coding:utf-8 -*-
from pymongo import *
import json
import os
class JsonToMongo():
    def __init__(self):
        self.host='localhost'
        self.port=27017
        self.client = MongoClient(self.host, self.port)
        # 创建数据库
        self.db = self.client['log']
    def close_file(self):
        self.file.close()
    #读取json文件
    def open_file(self):
        self.path='D:\\log'
   #这里写自己保存的数据文件路径，注意使用英文路径，这里是双斜杠\\！！！
        self.fileList=[]
        files = os.listdir(self.path)
        for file in files:
            self.collection=self.db[file]
            filePath = os.path.join(self.path, file)
            self.fileList.append(filePath)
            print(filePath)
            for line in open(filePath,'rb'):
                data=json.loads(line)
                try:
                    self.collection.insert(data)
                    print('写入成功')
                except Exception as e:
                    print(e)
```

## 5.运行就可以啦

![成功](https://upload-images.jianshu.io/upload_images/15933937-8ab94c731f77fc11.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

