# Install Packages You need

## 介绍

这里因为我需要学习分布式计算和模型训练，这里整体安装一下分布式用到的包：anaconda python环境， tensorflow， dl-on-flink, flink,



## Anaconda python环境安装

anaconda可以在这里下载安装

{% embed url="https://www.anaconda.com/" %}

安装python环境可以用一下命令, 其中可以通过python=xxx指定要安装的python版本

```
conda create -n <YOUR_ENV_NAME> python=3.8.3 
```

安装python之后， python的环境会安装到 anaconda3/envs/\<YOUR\_ENV\_NAME>/这个目录下面, 如果需要特别用到这个环境的python， 可以通过 \<path\_to\_anaconda3>/anaconda3/envs/\<YOUR\_ENV\_NAME>/bin/python 调用对应环境的python

有用的conda命令：

```
conda env list
conda env remove env_name

```

## Python里面安装对应的包

以安装tensorflow为例子

```
# 使用pip 安装， 
pip install tensorflow-cpu=2.4.x
# 或者指定对应版本的python 去安装python包
<path-to-python>/python -m pip install tensorflow-cpu=2.4.x
```

如果按照python 包时下载太慢， 一般是资源服务器问题， 如果要换一个下载地址可以用一下命令：

```
<path-to-python>/python -m pip install -i https://pypi.tuna.tsinghua.edu.cn/simple 
 tensorflow-cpu=2.4.x
```

其中 -i 后面接要访问下载资源的网站路径

## DL-ON\_FLINK

在使用tensorflow 分布式框架时， 如果是基于flink去做计算节点分配， 或者结合flink做实时训练， 实时分布式计算， 可以使用dl-on-flink这个框架去结合flink， tensorflow去使用

{% embed url="https://github.com/flink-extended/dl-on-flink" %}









