# Neuralnetworks
### 系统运行环境

#### 硬件环境

| 名称       | 参数              | 备注           |
| ---------- | ----------------- | -------------- |
| 服务器CPU  | Intel core i5     | 非最低         |
| 服务器内存 | 4G                | 最低           |
| 服务器存储 | 50G               |                |
| 服务器网络 | 1000M             |                |
| 服务器显卡 | Nvidia Tesla P100 | 16G （非必要） |
| 手机CPU    | 双核2GHz及以上    |                |
| 机身内存   | 4G及其以上        |                |

#### 软件环境

|     名称      |                                          版本号                                          |                                   备注                                   |
| ------------- | --------------------------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| 服务器操作系统 | Ubuntu18.04                                                                             | 64位                                                                    |
| 服务器数据库   | MySql 5.7                                                                               |                                                                         |
| 服务器开发环境 | anaconda 4.10.1<br />Python3.8<br /> paddlepaddle2.0.2<br />paddlehub 2.0.4<br />jdk1.8 | 为了简便部署，本系统采用<br />jar方式部署后台，预测服务<br />采用paddlehub。 |


### 系统运行环境的搭建

#### 服务端搭建

+ Anaconda的安装 ，在[官网](https://www.anaconda.com/products/individual#Downloads)选择合适的安装包下载 

  使用命令行安装,开始后按照默认操作进行选择即可

  ```bash
  $ sudo sh ./Anaconda3-2020.11-Linux-x86_64.sh
  ```

  以下所有操作，均是在Anaconda终端完成。

  安装完成之后，激活python 环境以及配置 pip

  ```bash
  $ conda create --name py38 python==3.8
  $ conda activate py38
  $ python -m pip install --upgrade pip
  ```

  

+ paddlepaddle安装(cpu版本) ,其余版本的安装请查看[飞浆官网](https://www.paddlepaddle.org.cn/)

```bash
$ python -m pip install paddlepaddle -i https://mirror.baidu.com/pypi/simple
```


+ paddlehub安装

```bash
$ pip install paddlehub
```

+ jdk安装 

```bash
$ sudo add-apt-repository ppa:webupd8team/java 
$ sudo apt-get update
$ sudo apt-get install oracle-java8-installer
$ sudo update-java-alternatives -s java-8-oracle
```



### 部署系统

1. 预测服务部署,打开ubuntu命令行，并将工作目录转到我们的ocr_predict里面，执行如下命令

```bash
$ conda activate py38
$ hub install ocr_system/
$ hub serving start -m ocr_system
```

到此预测服务以及启动

2. 后台服务的开启，使用我们提供的jar包运行即可。由于本地部署没有域名服务，将局域网ip改为192.168.1.110 。

```bash
$java -jar eureka-comsumer.jar       
$java -jar ocr-predict.jar
$java -jar ocr-parames-server-2.4.5.jar
$java -jar eureka-server.jar
```
