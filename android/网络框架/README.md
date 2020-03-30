## 三大网络框架
 1)    [Retrofit](https://github.com/ai-com-app/retrofit) Type-safe HTTP client for Android and Java by Square, Inc.

2)    [OkHttp](https://github.com/ai-com-app/okhttp) Square’s meticulous HTTP client for Java and Kotlin.

3)    [Volley](https://github.com/ai-com-app/volley) Volley is an HTTP library that makes networking for Android apps easier and, most importantly, faster.

### 介绍
## Retrofit
是Square公司出品的默认基于OkHttp封装的一套RESTful网络请求框架，RESTful是目前流行的一套api设计的风格。
Retrofit + OkHttp + RxJava + Dagger2 可以说是目前比较潮的一套框架。
### 优点
1. 可以配置不同HTTP client来实现网络请求，如OkHttp、HttpClient等
2. 请求的方法参数注解都可以定制
3. 支持同步、异步和RxJava
4. 超级解耦、rest风格，更安全和高效
5. 可以配置不同的反序列化工具来解析数据，如json、xml等使用非常方便灵活

### 缺点
1. 不能接触序列化实体和响应数据
2. 执行的机制太严格
3. 使用转换器比较低效
4. 只能支持简单自定义参数类型


## OkHttp
Square 公司开源的 OkHttp 是一个专注于连接效率的 HTTP 客户端。OkHttp 提供了对 HTTP/2 和 SPDY 的支持，并提供了连接池，GZIP 压缩和 HTTP 响应缓存功能。
### 优点
1. 支持http请求，https请求、支持同步异步。
2. 支持文件下载、加载图片、基于Http的文件上传。
3. 使用的是HttpURLConnection,不要担心android版本的变换。（至少目前是都支持的）。
4. 利用响应缓存来避免重复的网络请求。
5. 支持 SPDY，允许连接同一主机的所有请求分享一个socket。
6. 如果SPDY不可用，会使用连接池减少请求延迟。
使用GZIP压缩下载内容，且压缩操作对用户是透明的。

### 缺点
1. 比如callback回来是在线程里面, 不能刷新UI，需要我们手动处理。
2. 封装比较麻烦。

## Volley
是Goole在2013年Google I/O大会上推出了一个新的网络通信框架，它是开源的。
### 优点
1. 非常适合进行数据量不大，但通信频繁的网络操作
2. 可以取消请求，容易扩展，面向接口编程
3. 网络请求线程NetworkDispatcher默认开启了4个，可以优化，通过手机CPU数量
4. 可直接在主线程调用服务端并处理返回结果

### 缺点

1. 对大文件下载 Volley的表现非常糟糕。
2. 只支持http请求。
3. 在BasicNetwork中判断了statusCode(statusCode < 200 || statusCode >
299)，如何符合条件直接抛出IOException()，不够合理
4. 图片加载性能一般。
5. 使用的是HttpClient，HttpURLConnection。不过在android
6. 6.0不支持HttpClient了，如果想支持得添加org.apache.http.legacy.jar。


