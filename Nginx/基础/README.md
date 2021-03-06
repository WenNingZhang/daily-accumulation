![](/assets/Nginx概念优势.png)

* 概念

  Nginx 是一个开源且高性能\(支持海量并发\)、可靠的HTTP中间件、代理服务。

* 中间件出现的目的  
      后台有许多应用服务，为了让应用只处理逻辑，出现中间件。

* 常见的中间件架构

  * HTTPD   Apache 基金会
  * ISS         微软
  * GWS      Google

优势

* I/O多路复用epoll

  * 先看什么是I/O多路复用技术
    * 多个描述符的I/O操作都能在一个线程中交替并发的完成，为I/O多路复用，这里复用的是一个线程。
  * I/O多路复用的实现方式
    * select 
      * 应用向内核发送请求时，要等待内核处理完成，再向应用发送相应消息，这个时候，应用一直处在等待状态。
      * 缺点         1. 监视文件描述符的数量存在最大限制    2. 线性扫描效率低下
    * epoll
      * 应用无需等待，每当文件描述符就绪，采用系统的回调函数将文件描述符放入，效率更高
      * 最大连接无限制

* 轻量级

  * 代码模块少
  * 代码模块化

* CPU的亲和  affinity

  * 把CPU核心和Nginx 工作进程绑定的方式，把每个worker进程固定到一个CPU上执行，减少切换CPU时间，获得更好的性能。

* Nginx 的sendfile

![](/assets/sendfile1.png)

从内核层用read系统调用读到用户层，再从用户层用write系统调用写到内核层，效率低下。

![](/assets/sendfile2.png)

nginx在支持了sendfile系统调用后，避免了内核层与用户层的上线文切换（content swith）工作，大大减少了系统性能的开销。提高效率。

