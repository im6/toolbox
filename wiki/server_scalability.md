### 服务器集群的伸缩性设计常见方法

1. HTTP重定向 
Web服务器可通过Http响应头信息中的Location标记来返回一个新的URL，浏览器自动去访问这个新的URL。
2. DNS负载均衡
DNS负责将用户请求的域名映射为实际的IP地址，这种映射可以是一对多的（ DNS的A记录，用来指定域名对应的IP地址），这样DNS服务器便充当负载均衡调度器。
3. 反向代理负载均衡
反向代理服务器的核心工作是转发HTTP，它工作在HTTP层面，因此，基于反向代理的负载均衡也称为七层负载均衡。
4. IP负载均衡
网络地址转换(NAT)负载均衡工作在传输层，对数据包中的IP地址和端口进行修改，从而达到转发的目的，称为四层负载均衡。 
5. 直接路由
这种方式工作在数据链路层。它修改数据包的目标MAC地址，并没有修改目标IP（因为这种转发工作在数据链路层，它对上层端口无能为力），然后发给实际的服务器，实际服务器的响应数据直接发回给用户，而不用经过调度器。但实际服务器必须接入外网，而且不能将调度器作为默认网关，要给实际服务器添加和调度器IP地址相同的IP别名。
6. IP隧道
基于IP隧道的负载均衡系统也可以使用LVS来实现，称为LVS-TUN。与LVS-DR不同的是，实际服务器和调度器可以不在同一个WAN网段，调度器通过IP隧道技术来转发请求到实际服务器，所以实际服务器必须有合法的IP地址。基于IP隧道的请求转发机制，是将调度器收到的IP数据包封装在一个新的IP数据包中，转交给实际服务器，然后实际服务器的响应数据包可以直接到达用户端。基于IP隧道的独特方式，可以将实际服务器部署在不同的地域并根据就近原则转移请求，比如一些CDN服务器就是基于IP隧道技术实现的。