## FE-interview

个人收集的前端面试题和答案，参考答案仅代表个人观点

### 常见问题
<br />

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

<br />

- **什么是FOUC？如何避免？**  
Flash Of Unstyled Content：用户定义样式表加载之前浏览器使用默认样式显示文档，用户样式加载渲染之后再从新显示文档，造成页面闪烁。**解决方法**：把样式表放到文档的`head`  

<br />
## CSS部分
- **CSS有哪些继承属性**
    - 关于文字排版的属性如：`font`, `word-break`, `letter-spacing`,`text-align`,`tex--rendering`,`word-spacing`,`white-spacing`,`text-indent`,`text-transform`,`text-shadow`
    - `line-height`
    - `color`


<br />

## javascript部分
- **javascript有哪几种方法定义函数？**
    1. [函数声明表达式](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)
    2. [function操作符](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/function)
    3. [Function 构造函数](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function)

- 