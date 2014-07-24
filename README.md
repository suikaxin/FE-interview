## FE-interview

个人收集的前端知识点、面试题和答案，参考答案仅代表个人观点，方便复习
### 常见问题

- **什么是web语义化，有什么好处**  
web语义化是指通过HTML标记表示页面包含的信息，包含了HTML标签的语义化和css命名的语义化。  
HTML标签的语义化是指：通过使用包含语义的标签（如h1-h6）恰当地表示文档结构  
css命名的语义化是指：为html标签添加有意义的class，id补充未表达的语义，如[Microformat](http://en.wikipedia.org/wiki/Microformats)通过添加符合规则的class描述信息  
为什么需要语义化：
    - 去掉样式后页面呈现清晰的结构
    - 盲人使用读屏器更好地阅读
    - 搜索引擎更好地理解页面，有利于收录
    - 便团队项目的可持续运作及维护  

<br />

- **HTTP method**  
1.一台服务器要与HTTP1.1兼容，只要为资源实现**GET**和**HEAD**方法即可  
2.**GET**是最常用的方法，通常用于**请求服务器发送某个资源**。
3.**HEAD**与GET类似，但**服务器在响应中值返回首部，不返回实体的主体部分**。
4.**PUT**让服务器**用请求的主体部分来创建一个由所请求的URL命名的新文档，或者，如果那个URL已经存在的话，就用干这个主体替代它**  
4.**POST**起初是用来向服务器输入数据的。实际上，通常会用它来支持HTML的表单。表单中填好的数据通常会被送给服务器，然后由服务器将其发送到要去的地方。  
5.**TRACE**会在目的服务器端发起一个环回诊断，最后一站的服务器会弹回一个TRACE响应并在响应主体中携带它收到的原始请求报文。TRACE方法主要用于诊断，用于验证请求是否如愿穿过了请求/响应链。  
6**OPTIONS**方法请求web服务器告知其支持的各种功能。可以查询服务器支持哪些方法或者对某些特殊资源支持哪些方法。  
7.**DELETE**请求服务器删除请求URL指定的资源

<br />

- **从浏览器地址栏输入url到显示页面的步骤(以HTTP为例)**
    1. 在浏览器地址栏**输入URL**
    2. 浏览器查看**缓存**，如果请求资源在缓存中并且新鲜，转到解码步骤
    2. 浏览器**解析URL**获取协议，主机，端口，path
    3. 浏览器**组装一个HTTP请求报文**
    4. 浏览器**获取主机对应的ip地址**，过程如下：
        1. 浏览器缓存
        2. 本机缓存
        3. hosts文件
        4. 路由器缓存
        5. ISP DNS缓存
        3. DNS递归查询
    5. 浏览器**打开一个socket与目标IP地址，端口建立TCP链接**
    6. 建立TCP连接后，浏览器**发送HTTP请求**
    7. 目的主机**将请求转发到服务器软件（如Apache）**
    8. 服务器**解析请求并启动程序执行操作**
    9. 请求处理程序获取完整的请求并开始准备HTTP响应，可能需要查询数据库等操作
    10. 服务器将**组成响应报文并通过TCP连接向浏览器发送响应**
    11. 浏览器接收HTTP响应，然后根据情况选择关闭TCP链接或者保留重用
    11. 浏览器检查响应头：是否为信息（1xx）、重定向（3xx）、错误（4xx，5xx），这些情况与正常的2xx响应处理不同
    11. 如果资源可缓存，进行缓存
    11. 浏览器对响应进行解码（例如gzip压缩）
    12. 浏览器根据资源类型决定如何处理（假设资源为HTML文档）
    11. 浏览器**接受响应并解析HTML文档，构建DOM树**
    12. **解析过程中遇到图片，样式表，js文件，启动下载**
    13. **计算样式，执行脚本，显示页面**
    14. **关闭连接**



- **HTTP request报文结构是怎样的**  
[rfc2616](http://www.w3.org/Protocols/rfc2616/rfc2616-sec5.html)中进行了定义：  
1.首行是**Request-Line**包括：**请求方法**，**请求URI**，**协议版本**，**CRLF**  
2.首行之后是若干行**请求头**，包括**general-header**，**request-header**或者**entity-header**，每个一行以CRLF结束  
3.请求头和消息实体之间有一个**CRLF分隔**  
4.根据实际请求需要可能包含一个**消息实体**  
一个请求报文例子如下：

<pre>
GET /Protocols/rfc2616/rfc2616-sec5.html HTTP/1.1
Host: www.w3.org
Connection: keep-alive
Cache-Control: max-age=0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
User-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/35.0.1916.153 Safari/537.36
Referer: https://www.google.com.hk/
Accept-Encoding: gzip,deflate,sdch
Accept-Language: zh-CN,zh;q=0.8,en;q=0.6
Cookie: authorstyle=yes
If-None-Match: "2cc8-3e3073913b100"
If-Modified-Since: Wed, 01 Sep 2004 13:24:52 GMT

name=qiu&age=25
</pre>

<br />

- **HTTP response报文结构是怎样的**  
[rfc2616](http://www.w3.org/Protocols/rfc2616/rfc2616-sec6.html)中进行了定义：  
1.首行是**状态行**包括：**HTTP版本，状态码，状态描述**，后面跟一个CRLF  
2.首行之后是**若干行响应头**，包括：**通用头部，响应头部，实体头部**  
3.响应头部和响应实体之间用**一个CRLF空行**分隔  
4.最后是一个可能的**消息实体**  
响应报文例子如下：  

<pre>
HTTP/1.1 200 OK
Date: Tue, 08 Jul 2014 05:28:43 GMT
Server: Apache/2
Last-Modified: Wed, 01 Sep 2004 13:24:52 GMT
ETag: "40d7-3e3073913b100"
Accept-Ranges: bytes
Content-Length: 16599
Cache-Control: max-age=21600
Expires: Tue, 08 Jul 2014 11:28:43 GMT
P3P: policyref="http://www.w3.org/2001/05/P3P/p3p.xml"
Content-Type: text/html; charset=iso-8859-1

{"name": "qiu", "age": 25}
</pre>

<br />

- **如何进行网站性能优化**  
[雅虎Best Practices for Speeding Up Your Web Site](https://developer.yahoo.com/performance/rules.html)
    - content方面
        1. 减少HTTP请求：合并文件、CSS精灵、inline Image
        2. 减少DNS查询：DNS查询完成之前浏览器不能从这个主机下载任何任何文件。方法：DNS缓存、将资源分布到恰当数量的主机名，平衡并行下载和DNS查询
        3. 避免重定向：多余的中间访问
        4. 使Ajax可缓存
        5. 非必须组件延迟加载
        6. 未来所需组件预加载
        7. 减少DOM元素数量
        8. 将资源放到不同的域下：浏览器同时从一个域下载资源的数目有限，增加域可以提高并行下载量
        9. 减少iframe数量
        10. 不要404
    - Server方面
        1. 使用CDN
        2. 添加Expires或者Cache-Control响应头
        3. 对组件使用Gzip压缩
        4. 配置ETag
        5. Flush Buffer Early
        6. Ajax使用GET进行请求
        7. 避免空src的img标签
    - Cookie方面
        1. 减小cookie大小
        2. 引入资源的域名不要包含cookie
    - css方面
        1. 将样式表放到页面顶部
        2. 不使用CSS表达式
        3. 使用<link>不使用@import
        4. 不使用IE的Filter
    - Javascript方面
        1. 将脚本放到页面底部
        2. 将javascript和css从外部引入
        3. 压缩javascript和css
        4. 删除不需要的脚本
        5. 减少DOM访问
        6. 合理设计事件监听器
    - 图片方面
        1. 优化图片：根据实际颜色需要选择色深、压缩
        2. 优化css精灵
        3. 不要在HTML中拉伸图片
        4. 保证favicon.ico小并且可缓存
    - 移动方面
        1. 保证组件小于25k
        2. Pack Components into a Multipart Document



- **什么是渐进增强**  
渐进增强是指在web设计时强调可访问性、语义化HTML标签、外部样式表和脚本。保证所有人都能访问页面的基本内容和功能同时为高级浏览器和高带宽用户提供更好的用户体验。核心原则如下:  

    - 所有浏览器都必须能访问基本内容
    - 所有浏览器都必须能使用基本功能
    - 所有内容都包含在语义化标签中
    - 通过外部CSS提供增强的布局
    - 通过非侵入式、外部javascript提供增强功能
    - end-user web browser preferences are respected


- **HTTP状态码及其含义**  
参考[RFC 2616](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)
    - 1XX：信息状态码
        - **100 Continue**：客户端应当继续发送请求。这个临时相应是用来通知客户端它的部分请求已经被服务器接收，且仍未被拒绝。客户端应当继续发送请求的剩余部分，或者如果请求已经完成，忽略这个响应。服务器必须在请求万仇向客户端发送一个最终响应
        - **101 Switching Protocols**：服务器已经理解力客户端的请求，并将通过Upgrade消息头通知客户端采用不同的协议来完成这个请求。在发送完这个响应最后的空行后，服务器将会切换到Upgrade消息头中定义的那些协议。
    - 2XX：成功状态码
        - **200 OK**：请求成功，请求所希望的响应头或数据体将随此响应返回
        - **201 Created**：
        - **202 Accepted**：
        - **203 Non-Authoritative Information**：
        - **204 No Content**：
        - **205 Reset Content**：
        - **206 Partial Content**：
    - 3XX：重定向
        - **300 Multiple Choices**：
        - **301 Moved Permanently**：
        - **302 Found**：
        - **303 See Other**：
        - **304 Not Modified**：
        - **305 Use Proxy**：
        - **306 （unused）**：
        - **307 Temporary Redirect**：
    - 4XX：客户端错误
        - **400 Bad Request**:
        - **401 Unauthorized**:
        - **402 Payment Required**:
        - **403 Forbidden**:
        - **404 Not Found**:
        - **405 Method Not Allowed**:
        - **406 Not Acceptable**:
        - **407 Proxy Authentication Required**:
        - **408 Request Timeout**:
        - **409 Conflict**:
        - **410 Gone**:
        - **411 Length Required**:
        - **412 Precondition Failed**:
        - **413 Request Entity Too Large**:
        - **414 Request-URI Too Long**:
        - **415 Unsupported Media Type**:
        - **416 Requested Range Not Satisfiable**:
        - **417 Expectation Failed**:
    - 5XX: 服务器错误
        - **500 Internal Server Error**:
        - **501 Not Implemented**:
        - **502 Bad Gateway**:
        - **503 Service Unavailable**:
        - **504 Gateway Timeout**:
        - **505 HTTP Version Not Supported**:



<br />
## CSS部分


- **CSS有哪些继承属性**
    - 关于文字排版的属性如：`font`, `word-break`, `letter-spacing`,`text-align`,`tex--rendering`,`word-spacing`,`white-spacing`,`text-indent`,`text-transform`,`text-shadow`
    - `line-height`
    - `color`

<br />

- **IE浏览器有哪些常见的bug，缺陷或者与标准不一致的地方，如何解决**

1.IE5-8不支持``opacity``，解决办法：

<pre>
.opacity {
    filter: alpha(opacity=50); /* for IE5-7 */
    -ms-filter: "progid:DXImageTransform.Microsoft.Alpha(Opacity=50)"; /* for IE 8*/
}
</pre>
  
2.IE6在设置``height``小于``font-size``时高度值为``font-size``，解决办法：``font-size: 0;``

3.IE6不支持PNG透明背景，解决办法: **IE6下使用gif图片**

4.IE6-7不支持``display: inline-block``解决办法：设置inline并触发hasLayout

<pre>
    display: inline-block;
    *display: inline;
    *zoom: 1;
</pre>

5.IE6下浮动元素在浮动方向上的外边距会加倍。解决办法：  
1）使用padding控制间距。  
2）浮动元素``display: inline;``这样解决问题且无任何副作用：css标准规定浮动元素display:inline会自动调整为block


<br />

- **容器包含若干浮动元素时如何清理浮动**  
1.容器元素闭合标签前添加额外元素并设置``clear: both``  
2.设置容器元素伪元素进行清理  

<pre>
.container::after {
    content: "";
    display: block;
    line-height: 0;
    clear: both;
}
</pre>

3.父元素触发块级格式化上下文  
4.IE6下需触发hasLayout

- **什么是FOUC？如何避免？**  
Flash Of Unstyled Content：用户定义样式表加载之前浏览器使用默认样式显示文档，用户样式加载渲染之后再从新显示文档，造成页面闪烁。**解决方法**：把样式表放到文档的`head` 

<br />

- **如何创建块级格式化上下文（block formatting context）？有什么用**  
创建规则：  
1.根元素  
2.浮动元素（``float``不是``none``）  
3.绝对定位元素（``position``取值为``absolute``或``fixed``）  
4.``display``取值为``inline-block``,``table-cell``, ``table-caption``,``flex``, ``inline-flex``之一的元素  
5.``overflow``不是``visible``的元素  
作用：  
1.可以包含浮动元素  
2.不被浮动元素覆盖  
3.阻止父子元素的margin折叠

<br />
 

- **display, float, position的关系**  
1.如果``display``为none，那么position和float都不起作用，这种情况下元素不产生框  
2.否则，如果position值为absolute或者fixed，框就是绝对定位的，float的计算值为none，display根据下面的表格进行调整。  
3.否则，如果float不是none，框是浮动的，display根据下表进行调整  
4.否则，如果元素是根元素，display根据下表进行调整  
5.其他情况下display的值为指定值  
总结起来：**绝对定位、浮动、根元素都需要调整``display``**

![display转换规则](img/display-adjust.png)


<br />

- **外边距折叠（collapsing margins）**  
毗邻的两个或多个``margin``会合并成一个margin，叫做外边距折叠。规则如下：  
1.两个或多个毗邻的普通流中的块元素垂直方向上的margin会折叠  
2.浮动元素/inline-block元素/绝对定位元素的margin不会和垂直方向上的其他元素的margin折叠  
3.创建了块级格式化上下文的元素，不会和它的子元素发生margin折叠  
4.元素自身的margin-bottom和margin-top相邻时也会折叠


<br />

- **如何确定一个元素的包含块（containing block）**
    - 根元素的包含块叫做初始包含块，在连续媒体中他的尺寸与viewport相同并且anchored at the canvas origin；对于paged media，它的尺寸等于page area。初始包含块的direction属性与根元素相同。
    - <code>position</code>为``relative``或者``static``的元素，它的包含块由最近的块级（``display``为``block``,``list-item``, ``table``）祖先元素的**内容框**组成
    - 如果元素``position``为``fixed``。对于连续媒体，它的包含块为viewport；对于paged media，包含块为page area
    - 如果元素``position``为``absolute``，它的包含块由祖先元素中最近一个``position``为``relative``,``absolute``或者``fixed``的元素产生，规则如下：
        - 如果祖先元素为行内元素，the containing block is the bounding box around the **padding boxes** of the first and the last inline boxes generated for that element.
        - 其他情况下包含块由祖先节点的**padding edge**组成  

<br /><br /><br /><br />

- **stacking context，布局规则**  
z轴上的默认层叠顺序如下（从下到上）：  
1.根元素的边界和背景  
2.常规流中的元素按照html中顺序  
3.浮动块  
4.positioned元素按照html中出现顺序  
如何创建stacking context：  
1.根元素  
2.z-index不为auto的定位元素  
3.a flex item with a z-index value other than 'auto'  
4.opacity小于1的元素  
5.在移动端webkit和chrome22+，z-index为auto，position: fixed也将创建新的stacking context  




- **如何竖直居中一个元素**  
[盘点8种CSS实现垂直居中](http://blog.csdn.net/freshlover/article/details/11579669)  不同场景有不同的居中方案：
    - 元素高度声明的情况下在父容器中居中：**绝对居中法**

<pre>
&lt;div class="parent">
    &lt;div class="absolute-center">&lt;/div>
&lt;/div>

.parent {
    position: relative;
}
.absolute-center {
    position: absolute;
    margin: auto;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;

    height: 70%;
    width: 70%;
}
</pre>

优点：

1. 跨浏览器，包括IE8-10
2. 无需其他特色标记，CSS代码量少
3. 完美支持图片居中
4. 宽度高度可变，可用百分比

缺点

1. 必须声明高度
2. windows Phone设备上不起作用



    - **负外边距**：当元素宽度高度固定时。设置margin-top/margin-left为宽度高度一半的相反数，top:50%;left:50%

<pre>
&lt;div class="parent">
    &lt;div class="negative-margin-center">&lt;/div>
&lt;/div>

.parent {
    position: relative;
}
.absolute-center {
    position: absolute;
    left: 50%;
    top: 50%;

    margin-left: -150px;
    margin-top: -150px;


    height: 300px;
    width: 300px;
}
</pre>

优点：

1. 良好的跨浏览器特性，兼容IE6-7
2. 代码量少

缺点：

1. 不能自适应，不支持百分比尺寸和min-/max-属性设置
2. 内容可能溢出容器
3. 边距大小域与padding，box-sizing有关


    - **CSS3 Transform**居中：这是最简单的方法

<pre>
&lt;div class="parent">
    &lt;div class="transform-center">&lt;/div>
&lt;/div>

.parent {
    position: relative;
}
.absolute-center {
    position: absolute;
    left: 50%;
    top: 50%;

    margin: auto;
    width: 50%;

    -webkit-transform: translate(-50%， -50%);
       -moz-transform: translate(-50%， -50%);
            transform: translate(-50%, -50%);
}
</pre>

优点：

1. 内容高度可变
2. 代码量少

缺点：

1. IE8不支持
2. 属性需要浏览器厂商前缀
3. 可能干扰其他transform效果

    - **table-cell**居中：


<pre>
&lt;div class="center-container is-table">
    &lt;div class="table-cell">
        &lt;div class="center-block">&lt;/div>
    &lt;/div>
&lt;/div>

.center-container.is-table {
    display: table;
}

.is-table .table-cell {
    display: table-cell;
    vertical-align: middle;
}

.is-table .center-block {
    width: 50%;
    margin: 0 auto;
}
</pre>

优点：

1. 高度可变
2. 内容溢出会将父元素撑开
3. 跨浏览器兼容性好

缺点：

1. 需要额外html标记

    - **flexbox**居中


<br />

## javascript部分
- **javascript有哪几种方法定义函数？**
    1. [函数声明表达式](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)
    2. [function操作符](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/function)
    3. [Function 构造函数](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function)
    4. [ES6:arrow function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/arrow_functions)


重要参考资料：[MDN:Functions_and_function_scope](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions_and_function_scope)

<br />

- **应用程序存储和离线web应用**  
HTML5新增应用程序缓存，允许web应用将应用程序自身保存到用户浏览器中，用户离线状态也能访问。  
1.为html元素设置manifest属性:``<html manifest="myapp.appcache">``，其中后缀名只是一个约定，真正识别方式是通过``text/cache-manifest``作为MIME类型。所以需要配置服务器保证设置正确  
2.manifest文件首行为``CACHE MANIFEST``，其余就是要缓存的URL列表，每个一行，相对路径都相对于manifest文件的url。注释以#开头  
3.url分为三种类型：``CACHE``:为默认类型。``NETWORK``：表示资源从不缓存。 ``FALLBACK``:每行包含两个url，第二个URL是指需要加载和存储在缓存中的资源， 第一个URL是一个前缀。任何匹配该前缀的URL都不会缓存，如果从网络中载入这样的URL失败的话，就会用第二个URL指定的缓存资源来替代。以下是一个文件例子：

<pre>
CACHE MANIFEST

CACHE:
myapp.html
myapp.css
myapp.js

FALLBACK:
videos/ offline_help.html

NETWORK:
cgi/
</pre>

- **客户端存储localStorage和sessionStorage**

    - localStorage有效期为永久，sessionStorage有效期为顶层窗口关闭前
    - 同源文档可以读取并修改localStorage数据，sessionStorage只允许同一个窗口下的文档访问，如通过iframe引入的同源文档。
    - Storage对象通常被当做普通javascript对象使用：**通过设置属性来存取字符串值**，也可以通过**setItem(key, value)设置**，**getItem(key)读取**，**removeItem(key)删除**，**clear()删除所有数据**，**length表示已存储的数据项数目**，**key(index)返回对应索引的key**

<pre>
localStorage.setItem('x', 1); // storge x->1
localStorage.getItem('x); // return value of x

// 枚举所有存储的键值对
for (var i = 0, len = localStorage.length; i &lt; len; ++i ) {
    var name = localStorage.key(i);
    var value = localStorage.getItem(name);
}

localStorage.removeItem('x'); // remove x
localStorage.clear();  // remove all data

</pre>


<br />

- **cookie及其操作**  
    - cookie是web浏览器存储的少量数据，最早设计为服务器端使用，作为HTTP协议的扩展实现。cookie数据会自动在浏览器和服务器之间传输。
    - 通过读写cookie检测是否支持
    - cookie属性有**名**，**值**，**有效期**，**作用域**，**secure**；
    - cookie默认有效期为浏览器会话，一旦用户关闭浏览器，数据就丢失，通过设置**max-age=seconds**属性告诉浏览器cookie有效期
    - cookie作用域通过**文档源**和**文档路径**来确定，通过**path**和**domain**进行配置，web页面同目录或子目录文档都可访问
    - 通过cookie保存数据的方法为：为document.cookie设置一个符合目标的字符串如下
    - 读取document.cookie获得'; '分隔的字符串，key=value,解析得到结果

<pre>
document.cookie = 'name=qiu; max-age=9999; path=/; domain=domain; secure';

document.cookie = 'name=aaa; path=/; domain=domain; secure'; 
// 要改变cookie的值，需要使用相同的名字、路径和域，新的值
// 来设置cookie，同样的方法可以用来改变有效期

// 设置max-age为0可以删除指定cookie

//读取cookie，访问document.cookie返回键值对组成的字符串，
//不同键值对之间用'; '分隔。通过解析获得需要的值
</pre>

[cookieUtil.js](https://github.com/qiu-deqing/google/blob/master/module/js/cookieUtil.js)：自己写的cookie操作工具


<br />

- **javascript有哪些方法定义对象**
    1. 对象字面量： <code>var obj = {};</code>
    2. 构造函数： <code>var obj = new Object();</code>
    3. Object.create(): <code>var obj = Object.create(Object.prototype);</code>

<br />

- **===运算符判断相等的流程是怎样的**  

    1. 如果两个值不是相同类型，它们不相等
    2. 如果两个值都是null或者都是undefined，它们相等
    3. 如果两个值都是布尔类型true或者都是false，它们相等
    4. 如果其中有一个是**NaN**，它们不相等
    5. 如果都是数值型并且数值相等，他们相等， -0等于0
    6. 如果他们都是字符串并且在相同位置包含相同的16位值，他它们相等；如果在长度或者内容上不等，它们不相等；两个字符串显示结果相同但是编码不同==和===都认为他们不相等
    7. 如果他们指向相同对象、数组、函数，它们相等；如果指向不同对象，他们不相等

<br />

- **==运算符判断相等的流程是怎样的**

    1. 如果两个值类型相同，按照===比较方法进行比较
    2. 如果类型不同，使用如下规则进行比较

        1. 如果其中一个值是null，另一个是undefined，它们相等
        2. 如果一个值是**数字**另一个是**字符串**，将**字符串转换为数字**进行比较
        3. 如果有布尔类型，将**true转换为1，false转换为0**，然后用==规则继续比较
        4. 如果一个值是对象，另一个是数字或字符串，将对象转换为原始值然后用==规则继续比较
        5. **其他所有情况都认为不相等**


<br />

- **对象到字符串的转换步骤**
    1. 如果对象有toString()方法，javascript调用它。如果返回一个原始值（primitive value如：string number boolean）,将这个值转换为字符串作为结果
    2. 如果对象没有toString()方法或者返回值不是原始值，javascript寻找对象的valueOf()方法，如果存在就调用它，返回结果是原始值则转为字符串作为结果
    3. 否则，javascript不能从toString()或者valueOf()获得一个原始值，此时throws a TypeError

<br />

-  **对象到数字的转换步骤**
    1. 如果对象有valueOf()方法并且返回元素值，javascript将返回值转换为数字作为结果
    2. 否则，如果对象有toString()并且返回原始值，javascript将返回结果转换为数字作为结果
    3. 否则，throws a TypeError

<br />

- **&lt;,&gt;,&lt;=,&gt;=的比较规则**  
所有比较运算符都支持任意类型，但是**比较只支持数字和字符串**，所以需要执行必要的转换然后进行比较，转换规则如下:
    1. 如果操作数是对象，转换为原始值：如果valueOf方法返回原始值，则使用这个值，否则使用toString方法的结果，如果转换失败则报错
    2. 经过必要的对象到原始值的转换后，如果两个操作数都是字符串，按照字母顺序进行比较（他们的16位unicode值的大小）
    3. 否则，如果有一个操作数不是字符串，**将两个操作数转换为数字**进行比较


<br />

- **+运算符工作流程**
    1. 如果有操作数是对象，转换为原始值
    2. 此时如果有**一个操作数是字符串**，其他的操作数都转换为字符串并执行连接
    3. 否则：**所有操作数都转换为数字并执行加法**


<br />

- **函数内部arguments变量有哪些特性，有哪些属性，如何将它转换为数组**
    - arguments所有函数中都包含的一个局部变量，是一个类数组对象，对应函数调用时的实参。如果函数定义同名参数会在调用时覆盖默认对象
    - arguments[index]分别对应函数调用时的实参，并且通过arguments修改实参时会同时修改实参
    - arguments.length为实参的个数（Function.length表示形参长度）
    - arguments.callee为当前正在执行的函数本身，使用这个属性进行递归调用时需注意this的变化
    - arguments.caller为调用当前函数的函数（已被遗弃）
    - 转换为数组：<code>var args = Array.prototype.slice.call(arguments, 0);</code>
    

<br />

- **DOM事件模型是如何的，编写一个EventUtil工具类实现事件管理兼容**
    - DOM事件包含捕获（capture）和冒泡（bubble）两个阶段：捕获阶段事件从window开始触发事件然后通过祖先节点一次传递到触发事件的DOM元素上；冒泡阶段事件从初始元素依次向祖先节点传递直到window
    - 标准事件监听elem.addEventListener(type, handler, capture)/elem.removeEventListener(type, handler, capture)：handler接收保存事件信息的event对象作为参数，event.target为触发事件的对象，handler调用上下文this为绑定监听器的对象，event.preventDefault()取消事件默认行为，event.stopPropagation()/event.stopImmediatePropagation()取消事件传递
    - 老版本IE事件监听elem.attachEvent('on'+type, handler)/elem.detachEvent('on'+type, handler)：handler不接收event作为参数，事件信息保存在window.event中，触发事件的对象为event.srcElement，handler执行上下文this为window使用闭包中调用handler.call(elem, event)可模仿标准模型，然后返回闭包，保证了监听器的移除。event.returnValue为false时取消事件默认行为，event.cancleBubble为true时取消时间传播

    - 通常利用事件冒泡机制托管事件处理程序提高程序性能。

<pre>
/**
 * 跨浏览器事件处理工具。只支持冒泡。不支持捕获
 * @author  (qiu_deqing@126.com)
 */

var EventUtil = {
    getEvent: function (event) {
        return event || window.event;
    },
    getTarget: function (event) {
        return event.target || event.srcElement;
    },
    // 返回注册成功的监听器，IE中需要使用返回值来移除监听器
    on: function (elem, type, handler) {
        if (elem.addEventListener) {
            elem.addEventListener(type, handler, false);
            return handler;
        } else if (elem.attachEvent) {
            var wrapper = function () {
              var event = window.event;
              event.target = event.srcElement;
              handler.call(elem, event);
            };
            elem.attachEvent('on' + type, wrapper);
            return wrapper;
        }
    },
    off: function (elem, type, handler) {
        if (elem.removeEventListener) {
            elem.removeEventListener(type, handler, false);
        } else if (elem.detachEvent) {
            elem.detachEvent('on' + type, handler);
        }
    },
    preventDefault: function (event) {
        if (event.preventDefault) {
            event.preventDefault();
        } else if ('returnValue' in event) {
            event.returnValue = false;
        }
    },
    stopPropagation: function (event) {
        if (event.stopPropagation) {
            event.stopPropagation();
        } else if ('cancelBubble' in event) {
            event.cancelBubble = true;
        }
    }
};
</pre>


- **评价一下三种方法实现继承的优缺点，并改进**

<pre>
function Shape() {}

function Rect() {}

// 方法1
Rect.prototype = new Shape();

// 方法2
Rect.prototype = Shape.prototype;

// 方法3
Rect.prototype = Object.create(Shape.prototype);

Rect.prototype.area = function () {
  // do something
};
</pre>

1.方法1缺点：创建父类

<br />

- **完成一个函数，接受数组作为参数，数组元素为整数或者数组，数组元素包含整数或数组，函数返回扁平化后的数组**  
如：[1, [2, [ [3, 4], 5], 6]] => [1, 2, 3, 4, 5, 6]

<pre>
    var data =  [1, [2, [ [3, 4], 5], 6]];

    function flat(data, result) {
        var i, d, len;
        for (i = 0, len = data.length; i &lt; len; ++i) {
            d = data[i];
            if (typeof d === 'number') {
                result.push(d);
            } else {
                flat(d, result);
            }
        }
    }

    var result = [];
    flat(data, result);

    console.log(result);
</pre>

<br />

- **如何判断一个对象是否为数组**  
如果浏览器支持Array.isArray()可以直接判断否则需进行必要判断

<pre>
/**
 * 判断一个对象是否是数组，参数不是对象或者不是数组，返回false
 * 
 * @param {Object} arg 需要测试是否为数组的对象
 * @return {Boolean} 传入参数是数组返回true，否则返回false
 */
function isArray(arg) {
    if (typeof arg === 'object') {
        return Object.prototype.toString.call(arg) === '[object Array]';
    }
    return false;
}
</pre>

<br /><br /><br />

- **请评价以下代码并给出改进意见**

<pre>
if (window.addEventListener) {
  var addListener = function (el, type, listener, useCapture) {
    el.addEventListener(type, listener, useCapture);
  };
}
else if (document.all) {
  addListener = function (el, type, listener) {
    el.attachEvent('on' + type, function () {
      listener.apply(el);
    });
  };
}
</pre>

作用：浏览器功能检测实现跨浏览器DOM事件绑定

优点：  
1. 测试代码只运行一次，根据浏览器确定绑定方法  
2. 通过``listener.apply(el)``解决IE下监听器this与标准不一致的地方  
3. 在浏览器不支持的情况下提供简单的功能，在标准浏览器中提供捕获功能

缺点：  
1. document.all作为IE检测不可靠，应该使用if(el.attachEvent)  
2. addListener在不同浏览器下API不一样  
3. ``listener.apply``使this与标准一致但监听器无法移除  
4. 未解决IE下listener参数event。 target问题

改进

<pre>
var addListener;

if (window.addEventListener) {
  addListener = function (el, type, listener, useCapture) {
    el.addEventListener(type, listener, useCapture);
    return listener;
  };
}
else if (window.attachEvent) {
  addListener = function (el, type, listener) {
    // 标准化this，event，target
    var wrapper = function () {
      var event = window.event;
      event.target = event.srcElement;
      listener.call(el, event);
    };
    
    el.attachEvent('on' + type, wrapper);
    return wrapper; 
    // 返回wrapper。调用者可以保存，以后remove
  };
}
</pre>

<br /><br /><br /><br /><br />

- **如何判断一个对象是否为函数**  

<pre>
/**
 * 判断对象是否为函数，如果当前运行环境对可调用对象（如正则表达式）
 * 的typeof返回'function'，采用通用方法，否则采用优化方法
 * 
 * @param {Any} arg 需要检测是否为函数的对象
 * @return {boolean} 如果参数是函数，返回true，否则false
 */
function isFunction(arg) {
    if (arg) {
        if (typeof (/./) !== 'function') {
            return typeof arg === 'function';
        } else {
            return Object.prototype.toString.call(arg) === '[object Function]';
        }
    } // end if
    return false;
}
</pre>

<br />

- **编写一个函数接受url中query string为参数，返回解析后的Object，query string使用application/x-www-form-urlencoded编码**  

<pre>
/**
 * 解析query string转换为对象，一个key有多个值时生成数组
 * 
 * @param {String} query 需要解析的query字符串，开头可以是?，按照application/x-www-form-urlencoded编码
 * @return {Object} 参数解析后的对象
 */
function parseQuery(query) {
    var result = {};

    // 如果不是字符串返回空对象
    if (typeof query !== 'string') {
        return result;
    }

    // 去掉字符串开头可能带的?
    if (query.charAt(0) === '?') {
        query = query.substring(1);
    }

    var pairs = query.split('&');
    var pair;
    var key, value;
    var i, len;

    for (i = 0, len = pairs.length; i &lt; len; ++i) {
        pair = pairs[i].split('=');
        // application/x-www-form-urlencoded编码会将' '转换为+
        key = decodeURIComponent(pair[0]).replace(/\+/g, ' '); 
        value = decodeURIComponent(pair[1]).replace(/\+/g, ' ');

        // 如果是新key，直接添加
        if (!(key in result)) {
            result[key] = value;
        }
        // 如果key已经出现一次以上，直接向数组添加value
        else if (isArray(result[key])) {
            result[key].push(value);
        }
        // key第二次出现，将结果改为数组
        else {
            var arr = [result[key]];
            arr.push(value);
            result[key] = arr;
        } // end if-else
    } // end for 

    return result;
}

function isArray(arg) {
    if (arg && typeof arg === 'object') {
        return Object.prototype.toString.call(arg) === '[object Array]';
    }
    return false;
}
/**
console.log(parseQuery('sourceid=chrome-instant&ion=1&espv=2&ie=UTF-8#ie=UTF-8&q=url%20with%20query&sourceid=chrome-psyapi2'));
 */
</pre>

<br /><br /><br /><br />

- **解析一个完整的url，返回Object包含域与window.location相同**  

<pre>
/**
 * 解析一个url并生成window.location对象中包含的域
 * location:
 * {
 *      href: '包含完整的url',
 *      origin: '包含协议到pathname之前的内容',
 *      protocol: 'url使用的协议，包含末尾的:',
 *      username: '用户名', // 暂时不支持
 *      password: '密码',  // 暂时不支持
 *      host: '完整主机名，包含:和端口',
 *      hostname: '主机名，不包含端口'
 *      port: '端口号',
 *      pathname: '服务器上访问资源的路径/开头',
 *      search: 'query string，?开头',
 *      hash: '#开头的fragment identifier'
 * }
 * 
 * @param {string} url 需要解析的url
 * @return {Object} 包含url信息的对象
 */ 
function parseUrl(url) {
    var result = {};
    var keys = ['href', 'origin', 'protocol', 'host', 'hostname', 'port', 'pathname', 'search', 'hash'];
    var i, len;
    var regexp = /(([^:]+:)\/\/(([^:\/\?#]+)(:\d+)?))(\/[^?#]*)?(\?[^#]*)?(#.*)?/;

    var match = regexp.exec(url);

    if (match) {
        for (i = keys.length - 1; i >= 0; --i) {
            result[keys[i]] = match[i] ? match[i] : '';
        }
    }

    return result;
}
</pre>

<br /><br /><br /><br /><br /><br />

- **完成函数getScrollOffset返回窗口滚动条偏移量**

<pre>
/**
 * 获取指定window中滚动条的偏移量，如未指定则获取当前window
 * 滚动条偏移量
 * 
 * @param {window} w 需要获取滚动条偏移量的窗口
 * @return {Object} obj.x为水平滚动条偏移量,obj.y为竖直滚动条偏移量
 */
function getScrollOffset(w) {
    w =  w || window;
    // 如果是标准浏览器
    if (w.pageXOffset != null) {
        return {
            x: w.pageXOffset, 
            y: w.pageYOffset
        };
    }

    // 老版本IE，根据兼容性不同访问不同元素
    var d = w.document;
    if (d.compatMode === 'CSS1Compat') {
        return {
            x: d.documentElement.scrollLeft,
            y: d.documentElement.scrollTop
        }
    }

    return {
        x: d.body.scrollLeft,
        y: d.body.scrollTop
    };
}
</pre>

<br /><br />

- **现有一个字符串richText，是一段富文本，需要显示在页面上。有个要求，需要给其中只包含一个img元素的p标签增加一个叫pic的class。请编写代码实现。可以使用jQuery或KISSY。**

<pre>

function richText(text) {
    var div = document.createElement('div');
    div.innerHTML = text;
    var p = div.getElementsByTagName('p');
    var i, len;

    for (i = 0, len = p.length; i &lt; len; ++i) {
        if (p[i].getElementsByTagName('img').length === 1) {
            p[i].classList.add('pic');
        }
    }

    return div.innerHTML;
}

</pre>

<br /><br /><br /><br />

- **请实现一个Event类，继承自此类的对象都会拥有两个方法on和trigger**
<pre>
</pre>

<br /><br /><br /><br /><br /><br /><br />

- **编写一个函数将列表子元素顺序反转**

<pre>
&lt;ul id="target">
    &lt;li>1&lt;/li>
    &lt;li>2&lt;/li>
    &lt;li>3&lt;/li>
    &lt;li>4&lt;/li>
&lt;/ul>

&lt;script>
    var target = document.getElementById('target');
    var i;
    var frag = document.createDocumentFragment();

    for (i = target.children.length - 1; i &gt;= 0; --i) {
        frag.appendChild(target.children[i]);
    }
    target.appendChild(frag);
&lt;/script>
</pre>

<br /><br /><br /><br /><br />

- **以下函数的作用是？空白区域应该填写什么**

<pre>
// define
(function (window) {
    function fn(str) {
        this.str = str;
    }

    fn.prototype.format = function () {
        var arg = __1__;
        return this.str.replace(__2__, function (a, b) {
            return arg[b] || '';
        });
    };

    window.fn = fn;
})(window);

// use
(function () {
    var t = new fn('&lt;p>&lt;a href="{0}">{1}&lt;/a>&lt;span>{2}&lt;/span>&lt;/p>');
    console.log(t.format('http://www.alibaba.com', 'Alibaba', 'Welcome'));
})();
</pre>

define部分定义一个简单的模板类，使用{}作为转义标记，中间的数字表示替换目标，format实参用来替换模板内标记  
横线处填：  

1. ``Array.prototype.slice.call(arguments, 0)``
2. ``/\{\s*(\d+)\s*\}/g``

<br /><br /><br /><br />

- **编写一个函数实现form的序列化（即将一个表单中的键值序列化为可提交的字符串）**

<pre>
/**
 * 将一个表单元素序列化为可提交的字符串
 * 
 * @param {FormElement} form 需要序列化的表单元素
 * @return {string} 表单序列化后的字符串
 */
function serializeForm(form) {
  if (!form || form.nodeName.toUpperCase() !== 'FORM') {
    return;
  }

  var result = [];

  var i, len;
  var field, fieldName, fieldType;

  for (i = 0, len = form.length; i &lt; len; ++i) {
    field = form.elements[i];
    fieldName = field.name;
    fieldType = field.type;

    if (field.disabled || !fieldName) {
      continue;
    } // enf if

    switch (fieldType) {
      case 'text':
      case 'password':
      case 'hidden':
      case 'textarea':
        result.push(encodeURIComponent(fieldName) + '=' + 
            encodeURIComponent(field.value));
        break;

      case 'radio':
      case 'checkbox':
        if (field.checked) {
          result.push(encodeURIComponent(fieldName) + '=' + 
            encodeURIComponent(field.value));
        }
        break;

      case 'select-one':
      case 'select-multiple':
        for (var j = 0, jLen = field.options.length; j &lt; jLen; ++j) {
          if (field.options[j].selected) {
            result.push(encodeURIComponent(fieldName) + '=' + 
              encodeURIComponent(field.options[j].value || field.options[j].text));
          }
        } // end for
        break;

      case 'file':
      case 'submit':
        break; // 是否处理？

      default:
        break;
    } // end switch
  } // end for
    
    return result.join('&amp;');
}
</pre>

<br />

- **使用原生javascript给下面列表中的li节点绑定点击事件，点击时创建一个Object对象，兼容IE和标准浏览器**

<pre>
&lt;ul id="nav">
    &lt;li>&lt;a href="http://11111">111&lt;/a>&lt;/li>
    &lt;li>&lt;a href="http://2222">222&lt;/a>&lt;/li>
    &lt;li>&lt;a href="http://333">333&lt;/a>&lt;/li>
    &lt;li>&lt;a href="http://444">444&lt;/a>&lt;/li>
&lt;/ul>

Object:
{
    "index": 1,
    "name": "111",
    "link": "http://1111"
}
</pre>

script:

<pre>
var EventUtil = {
    getEvent: function (event) {
        return event || window.event;
    },
    getTarget: function (event) {
        return event.target || event.srcElement;
    },
    // 返回注册成功的监听器，IE中需要使用返回值来移除监听器
    on: function (elem, type, handler) {
        if (elem.addEventListener) {
            elem.addEventListener(type, handler, false);
            return handler;
        } else if (elem.attachEvent) {
            function wrapper(event) {
                return handler.call(elem, event);
            };
            elem.attachEvent('on' + type, wrapper);
            return wrapper;
        }
    },
    off: function (elem, type, handler) {
        if (elem.removeEventListener) {
            elem.removeEventListener(type, handler, false);
        } else if (elem.detachEvent) {
            elem.detachEvent('on' + type, handler);
        }
    },
    preventDefault: function (event) {
        if (event.preventDefault) {
            event.preventDefault();
        } else if ('returnValue' in event) {
            event.returnValue = false;
        }
    },
    stopPropagation: function (event) {
        if (event.stopPropagation) {
            event.stopPropagation();
        } else if ('cancelBubble' in event) {
            event.cancelBubble = true;
        }
    }
};
var DOMUtil = {
    text: function (elem) {
        if ('textContent' in elem) {
            return elem.textContent;
        } else if ('innerText' in elem) {
            return elem.innerText;
        }
    },
    prop: function (elem, propName) {
        return elem.getAttribute(propName);
    }
};

var nav = document.getElementById('nav');

EventUtil.on(nav, 'click', function (event) {
    var event = EventUtil.getEvent(event);
    var target = EventUtil.getTarget(event);

    var children = this.children;
    var i, len;
    var anchor;
    var obj = {};

    for (i = 0, len = children.length; i &lt; len; ++i) {
        if (children[i] === target) {
            obj.index = i + 1;
            anchor = target.getElementsByTagName('a')[0];
            obj.name = DOMUtil.text(anchor);
            obj.link = DOMUtil.prop(anchor, 'href');
        }
    }

    alert('index: ' + obj.index + ' name: ' + obj.name +
        ' link: ' + obj.link);
});
</pre>

<br />

- **有一个大数组，var a = ['1', '2', '3', ...]; a的长度是100，内容填充随机整数的字符串。请先构造此数组a，然后设计一个算法将其内容去重**  

<pre>
    /**
    * 数组去重
    **/
    function normalize(arr) {
        if (arr && Array.isArray(arr)) {
            var i, len, map = {};
            for (i = arr.length; i >= 0; --i) {
                if (arr[i] in map) {
                    arr.splice(i, 1);
                } else {
                    map[arr[i]] = true;
                }
            }
        }
        return arr;
    }

    /**
    * 用100个随机整数对应的字符串填充数组。
    **/
    function fillArray(arr, start, end) {
        start = start == undefined ? 1 : start;
        end = end == undefined ?  100 : end;

        if (end &lt;= start) {
            end = start + 100;
        }

        var width = end - start;
        var i;
        for (i = 100; i >= 1; --i) {
            arr.push('' + (Math.floor(Math.random() * width) + start));
        }
        return arr;
    }

    var input = [];
    fillArray(input, 1, 100);
    input.sort(function (a, b) {
        return a - b;
    });
    console.log(input);

    normalize(input);
    console.log(input);
</pre>


- 