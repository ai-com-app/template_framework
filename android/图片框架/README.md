## 图片框架


1. [Glide](https://github.com/ai-com-app/glide) An image loading and caching library for Android focused on smooth scrolling.

2. [Picasso](https://github.com/ai-com-app/picasso) A powerful image downloading and caching library for Android.

3. [Fresco](https://github.com/ai-com-app/fresco) An Android library for managing images and the memory they use. 

4. [PhotoView](https://github.com/chrisbanes/PhotoView)  Implementation of ImageView for Android that supports zooming, by various touch gestures.


### 介绍
## Picasso
### 优点
1. 自带统计监控功能 支持图片缓存使用的监控，包括缓存命中率、已使用内存大小、节省的流量等。
2. 支持优先级处理 每次任务调度前会选择优先级高的任务，比如 App 页面中 Banner 的优先级高于 Icon 时就很适用。
3.  支持延迟到图片尺寸计算完成加载
4. 支持飞行模式、并发线程数根据网络类型而变 手机切换到飞行模式或网络类型变换时会自动调整线程池最大并发数，比如 wifi 最大并发为 4， 4g 为 3，3g 为 2。这里 Picasso 根据网络类型来决定最大并发数，而不是 CPU 核数。
5. “无”本地缓存
无”本地缓存，不是说没有本地缓存，而是 Picasso 自己没有实现，交给了 Square 的另外一个网络库 okhttp 去实现，这样的好处是可以通过请求 Response Header 中的 Cache-Control 及 Expired 控制图片的过期时间。

### 缺点
1. 不支持GIF, 并且它可能是想让服务器去处理图片的缩放, 它缓存的图片是未缩放的, 并且默认使用ARGB_8888格式缓存图片, 缓存体积大。

## Glide
### 优点
1. 图片缓存->媒体缓存
Glide 不仅是一个图片缓存，它支持 Gif、WebP、缩略图。甚至是 Video，所以更该当做一个媒体缓存。
2. 支持优先级处理
3. 与 Activity/Fragment 生命周期一致，支持 trimMemory
Glide 对每个 context 都保持一个 RequestManager，通过 FragmentTransaction 保持与 Activity/Fragment 生命周期一致，并且有对应的 trimMemory 接口实现可供调用。
4. 支持 okhttp、Volley
Glide 默认通过 UrlConnection 获取数据，可以配合 okhttp 或是 Volley 使用。实际 ImageLoader、Picasso 也都支持 okhttp、Volley。
5. 内存友好
    * Glide 的内存缓存有个 active 的设计。
从内存缓存中取数据时，不像一般的实现用 get，而是用 remove，再将这个缓存数据放到一个 value 为软引用的 activeResources map 中，并计数引用数，在图片加载完成后进行判断，如果引用计数为空则回收掉。
    * 内存缓存更小图片
Glide 以 url、viewwidth、viewheight、屏幕的分辨率等做为联合 key，将处理后的图片缓存在内存缓存中，而不是原始图片以节省大小。
    * 与 Activity/Fragment 生命周期一致，支持 trimMemory
    * 图片默认使用默认 RGB565 而不是 ARGB888， 虽然清晰度差些，但图片更小，也可配置到 ARGB_888。

### 缺点
1. Glide 可以通过 signature 或不使用本地缓存支持 url 过期。

## Fresco
### 优点

1. 图片存储在安卓系统的匿名共享内存, 而不是虚拟机的堆内存中, 图片的中间缓冲数据也存放在本地堆内存, 所以, 应用程序有更多的内存使用,不会因为图片加载而导致oom, 同时也减少垃圾回收器频繁调用回收Bitmap导致的界面卡顿,性能更高。
2. 渐进式加载JPEG图片, 支持图片从模糊到清晰加载。
3. 图片可以以任意的中心点显示在ImageView, 而不仅仅是图片的中心。
4. JPEG图片改变大小也是在native进行的, 不是在虚拟机的堆内存, 同样减少OOM。
5. 很好的支持GIF图片的显示。

### 缺点
1. 框架较大, 影响Apk体积
2. 使用较繁琐

## PhotoView
### 优点
1. 使用多点触控和两次轻按即可进行缩放。
2. 滚动顺畅。
3. 在滚动父级（例如ViewPager）中使用时，效果很好。
4. 允许在显示的矩阵发生更改时通知应用程序。 在需要基于当前缩放/滚动位置更新用户界面。
5. 通过添加接口，允许在用户点击图片时发出通知，。


