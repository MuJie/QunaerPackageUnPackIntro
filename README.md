# QunaerPackageUnPackIntro
> `关于去哪儿APK拆分简要解析`

 **版本：** 去哪儿V8.4.3 （33.1M）
 
 **环境：** windows
 
 **工具：** [dex2jar2.0](http://code.google.com/p/dex2jar/downloads/list), [jd-gui1.4.0](http://jd.benow.ca/), [apktool2.1.0](https://code.google.com/p/android-apktool/downloads/list)

------
## 目录结构
![目录结构](/image/package_structure.png)

## APK分析图解
![APK分析图](/image/apk_unpack.png)

## 去哪儿APK使用的相关技术和框架

------
### 第三方SDK
* #### 支付SDK
  * alipay(阿里支付)
  * payeco(易联支付)

* #### 推送SDK
  * gigexin 个推

* #### 地图SDK
  * 百度地图
  * Mapquest

* #### 授权登录SDK
  * 携程
  * 腾讯
  * 华为
  * 魅族
  
------
### 数据
* 解析
  * fastjson
  * Jackson
* DB
  * **XUtils(DBUtils)**
  
    XUtils是基于afinal开发的，比afinal稳定性高。主要分为四大模块：DbUtils、ViewUtils、HttpUtils、BitmapUtils.
  
    * DbUtils模块：    
      * `android中的orm框架，一行代码就可以进行增删改查；`
      * `支持事务，默认关闭；`
      * `可通过注解自定义表名，列名，外键，唯一性约束，NOT NULL约束，CHECK约束等（需要混淆的时候请注解表名和列名）；`
      * `支持绑定外键，保存实体时外键关联实体自动保存或更新；`
      * `自动加载外键关联实体，支持延时加载；`
      * `支持链式表达查询，更直观的查询语义，参考下面的介绍或sample中的例子。`
    * ViewUtils模块：
      * `android中的ioc框架，完全注解方式就可以进行UI，资源和事件绑定；`
      * `新的事件绑定方式，使用混淆工具混淆后仍可正常工作；`
      * `目前支持常用的20种事件绑定，参见ViewCommonEventListener类和包com.lidroid.xutils.view.annotation.event。`
    * HttpUtils模块：
      * `支持同步，异步方式的请求；`
      * `支持大文件上传，上传大文件不会oom；`
      * `支持GET，POST，PUT，MOVE，COPY，DELETE，HEAD，OPTIONS，TRACE，CONNECT请求`
      * `下载支持301/302重定向，支持设置是否根据Content-Disposition重命名下载的文件；`
      * `返回文本内容的请求(默认只启用了GET请求)支持缓存，可设置默认过期时间和针对当前请求的过期时间。`
    * BitmapUtils模块
      * `加载bitmap的时候无需考虑bitmap加载过程中出现的oom和android容器快速滑动时候出现的图片错位等现象；`
      * `支持加载网络图片和本地图片；`
      * `内存管理使用lru算法，更好的管理bitmap内存；`
      * `可配置线程加载线程数量，缓存大小，缓存路径，加载显示动画等...`


------
### [React-Native + Hybrid](http://www.cnblogs.com/dailc/archive/2016/10/04/5930238.html)
 * React-Native
 
 > `(简称RN)是Facebook于2015年四月开源的跨平台移动应用开发框架，是Facebook早先开源的Web UI框架 React 在原生移动应用平台的衍生产物，目前支持iOS和安卓两大平台。该框架使用Javascript，类似于HTML的JSX，以及CSS来开发移动应用UI，因此熟悉Web开发的人只需很少的学习成本就可以转入移动应用开发。`
 * Hybrid
 
 > `Hybrid App（混合模式移动应用）开发是指介于Web-app、Native-App这两者之间的一种开发模式，兼具「Native App 良好用户交互体验的优势」和「Web App 跨平台开发的优势。由Native通过JSBridge等方法提供统一的API,然后用Html5+JS来写实际的逻辑,调用API,这种模式下,由于Android,iOS的API一般有一致性,而且最终的页面也是在webview中显示,所有有跨平台效果`

------
### 序列化
* **Protobuf**

 > `protobuf是google提供的一个开源序列化框架，类似于XML，JSON这样的数据表示语言，其最大的特点是基于二进制，因此比传统的XML表示高效短小得多。虽然是二进制数据格式，但并没有因此变得复杂，开发人员通过按照一定的语法定义结构化的消息格式，然后送给命令行工具，工具将自动生成相关的类，可以支持php、java、c++、Python等语言环境。通过将这些类包含在项目中，可以很轻松的调用相关方法来完成业务消息的序列化与反序列化工作。`
 
------
### 网络
* **okhttp** 
  OkHttp是一个高效的HTTP库：
  
> * `支持 SPDY ，共享同一个Socket来处理同一个服务器的所有请求`

> * `如果SPDY不可用，则通过连接池来减少请求延时`

> * `无缝的支持GZIP来减少数据流量`

> * `缓存响应数据来减少重复的网络请求`

    它会从很多常用的连接问题中自动恢复，如果您的服务器配置了多个IP地址，当第一个IP连接失败的时候，OkHttp会自动尝试下一个IP。OkHttp还处理了代理服务器问题和SSL握手失败问题。它使用 OkHttp 无需重写您程序中的网络代码。OkHttp实现了几乎和java.net.HttpURLConnection一样的API。如果您用了 Apache HttpClient，则OkHttp也提供了一个对应的okhttp-apache 模块。
    
------
### 框架工具

* 异步
 * **bolts函数库**
  
     `Bolts是Parse和Facebook共同努力将两家公司各自独立开发的小型底层工具类合并的结果。Tasks是GitHub上第一个可用的Bolts组件，旨在按照JavaScript Promises模型处理异步操作`
  
      **Tasks与Android AsyncTask和iOS NSOperation相比有以下优势：**
  
      * 连续执行数个任务不会像只使用回调函数时那样创建嵌套的“金字塔（pyramid）”代码。
      * Tasks是完全可组合的，允许开发人员执行分支、并行和复杂的错误处理。
      * 开发人员可以按照执行顺序安排基于任务的代码，而不必将逻辑分解到分散的回调函数中。
      
* 图片
 * **Fresco**
 
 > `Fresco是Facebook最新推出的一款用于Android应用中展示图片的强大图片库，可以从网络、本地存储和本地资源中加载图片。相对于ImageLoader，拥有更快的图片下载速度以及可以加载和显示gif图等诸多优势，是个强大的图片加载框架`
 
 ```html
 <!-- XML里面声明控件>
 <com.facebook.drawee.view.SimpleDraweeView
    android:id="@+id/image_view"
    android:layout_width="20dp"
    android:layout_height="20dp"
    fresco:placeholderImage="@drawable/my_drawable"
  />
 ```
 
 ```java
 //Java代码加载图片
 Uri uri = Uri.parse("https://raw.githubusercontent.com/facebook/fresco/gh-pages/static/fresco-logo.png");
 SimpleDraweeView draweeView = (SimpleDraweeView) findViewById(R.id.my_image_view);
 draweeView.setImageURI(uri);
 ```

* 动画
 * **nineoldandroids**
 
 > `NineOldAndroids是一个向下兼容的动画库，主要是使低于API 11的系统也能够使用View的属性动画。它的类名、用法与官方的都一样，只是包名不一样。使用该库，你就可以在API 版本很低的情况下也能够使用各种属性动画，让你的应用更加有动感、平滑。` **如果用户的系统低于API 11，那么就不会调用View的set属性方法来修改它的属性，而是通过矩阵(Matrix)来修改View的缩放、平移、旋转等动画。**
 
* 依赖注入
 * javax.inject
 
 > `Spring的一种依赖注入jar`
 
* UUID
 * utdid
 
 > `阿里提供的一种设备标识（UUID）生成库`



