

## RPC的定义是什么？

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;服务之间的进程调用，可以使用HTTP协议的网络请求，也可以是TCP协议的网络请求，同样也可以是UDP的网络协议请求。在公司发展的初期，我们通常是自己编写公共方法来进行相应的网络请求，这些方法相对而言，是通用的(编写一次会复用多次),当然不排除对应的业务场景，开发人员会进行二次封装
   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;RPC的实现思想，便是负责屏蔽底层的传输方式，封装序列化协议，网络传输，从而使调用方像调用本地方法一样去调用远程服务。



 ![GitHub][github1]

[github1]: http://fmn.rrimg.com/fmn086/20181022/2330/large_dY19_4344000071a61e7f.jpg "GitHub,Social Coding" 


我们可以参考上面的原理图，如果要我们设计一个RPC框架，应该做些什么？

#### RPC的服务端设计

(1) 网络监听端设计 

现有的很多开源框架，在处理网络协议的时候，都将这部分逻辑外包给了Netty进行处理，得益于Netty的强大，使我们可以快速搭建网络的建设。   

代码路径:  com.starter.rpc_server.core.RpcProcessor   

这边就不详细解释了

---
(2) 序列化设计   

当进行跨进程服务调用的时候，需要将被输出的数据序列化为字节数组或者ByteBuffer,而当远程服务读取到ByteBuffer或者字节数组的时候，也需要将其反序列化为元素的数据。上述的过程，需要利用序列化框架来完成
 
 
 ##### Java默认的序列化机制
 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在Java体系中，只需要实现java.io.Serializable并且生成序列ID便可以，但是其自身的缺点导致无法在RPC中使用
 
 （1）无法跨语言，这是最致命的    
 
 （2）Java默认的序列化性能比较低，数据在序列化之后的字节数组体积比较大，性能比较低（编码后的字节数组越大，在网络传输的时候更加占据带宽，导致系统的吞吐量降低）

---
(3) 服务注册  



(4) 接口类的扫描与映射关系的维护

 [如何生成代码](https://github.com/grpc/grpc-java/blob/master/README.md)
