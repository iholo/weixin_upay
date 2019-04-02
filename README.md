​    最近在网上看好多人做个人支付系统，其实就是hook微信或支付宝，生成收款码，于是我也想研究研究，也做作 了一套，不过只做了微信，没有做支付宝，不想浪费时间 了，要做的话应该也不用多长时间 ，毕竟都差不多。

​    本来想把源码撰在自己手里，毕竟也是花了时间和精力的，想想还是算了，开发出来的东西如果没有人用就没有任何价值，所以决定开源，代码很简陋，毕竟不是商业产品 ，我不想花那么时间再维护下去，想要继续开发的可以找我有偿服务。



### 一、系统介绍

不需要申请微信公众号，不需要与微信签约，交易没有手续费
不需要上传指定金额的二维码，系统自动根据金额生成二维码。
新的二维码调配机制 ，在保证每一张二维码都是唯一的情况下，相同金额的二维码不会重新生成。
使用个人微号收款，资金直接到自己账上，安全放心 。
同一个收款系统或账号可多台手机 、多个微信同时上线，系统将自动调配在线设备 ，可解决微信限制二维码生成数量限制。

### 二、 运行流程

用户向支付服务器发起支付请求，服务器调用支付接口

支付接口查找系统是否有相同金额的二维码，如果有并且未使用，直接返回二维码

如果系统没有相同金额的付款码，则服务器向手机端发出通知 ，告诉手机端生成付款码，手机端生成付款码后将付款码数据发回服务器，服务器将收到的付款码信息后展示到页面。

用户扫描付款码完成支付，微信端此时收到付款通知后，通知服务器用户已经付款，并将金额和付款码的编号发给服务器

服务器收到付款完成的通知后，修改订单状态，将回调支付通知接口



### 三、使用教程

#####服务端准备工作

1. 准备工作

   安装 php+mysql+redis，并将 数据库将导入数据，sql文件在 php 目录下，这个很简单，网上教程多的是；

   配置好server服务端的配置文件，server服务端/config.ini

2. 如何启动后台服务

   将服务端程序拷贝到服务器(必须ubuntu 16.04及以上的系统)任意目录下，配置好config.ini后，输入命令：./upay_server start 即可启动

##### android 端准备工作 

1. 安装 VirtualXposed ，并将微信和upay安装到 xposed 内，微信使用的是 6.6.7的版本，其他版本不一定保证能用。
2. 在xposed 登录自己的微信后，再打开 upay ,此时界面上会看到 自己的微信号和微信ID，用自己微信号和微信ID在 device 表内新建一个设备账号并与user表的账号关联。
3. 进入微信，点击 收付款  -  二维码收款，进入到这一部，如果前面一切顺利 ，应该可以调用PHP的接口收款了，可以任意输入金额。

   




### 四、系统组成

整个系统由三个部分组成： 

1、后台服务端（用C++开发），主要负责监听用户实时下单并与APP端的通信； 

2、后台接口服务（用PHP开发），负责支付接口调用请求、连接后台服务端通、付款码的调用逻辑逻辑、和接收付款完成的通知； 

3、安卓APP，主要是生成二维码和接收付款通知

测试链接：http://upay.yixinu.com/  ,  设备不一定在线，测试前可以加我微信，提醒我上线设备测试，我的微信号(xianglou)。




### 五、作者微信

我的微信号(xianglou)


