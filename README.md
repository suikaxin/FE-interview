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


- **什么是FOUC？如何避免？**  
Flash Of Unstyled Content：用户定义样式表加载之前浏览器使用默认样式显示文档，用户样式加载渲染之后再从新显示文档，造成页面闪烁。**解决方法**：把样式表放到文档的`head` 

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

## CSS部分
- **CSS有哪些继承属性**
    - 关于文字排版的属性如：`font`, `word-break`, `letter-spacing`,`text-align`,`tex--rendering`,`word-spacing`,`white-spacing`,`text-indent`,`text-transform`,`text-shadow`
    - `line-height`
    - `color`

- **如何确定一个元素的包含块（containing block）**
    - 根元素的包含块叫做初始包含块，在连续媒体中他的尺寸与viewport相同并且anchored at the canvas origin；对于paged media，它的尺寸等于page area。初始包含块的direction属性与根元素相同。
    - <code>position</code>为``relative``或者``static``的元素，它的包含块由最近的块级（``display``为``block``,``list-item``, ``table``）祖先元素的**内容框**组成
    - 如果元素``position``为``fixed``。对于连续媒体，它的包含块为viewport；对于paged media，包含块为page area
    - 如果元素``position``为``absolute``，它的包含块由祖先元素中最近一个``position``为``relative``,``absolute``或者``fixed``的元素产生，规则如下：
        - 如果祖先元素为行内元素，the containing block is the bounding box around the **padding boxes** of the first and the last inline boxes generated for that element.
        - 其他情况下包含块由祖先节点的**padding edge**组成

- **如何竖直居中一个元素**
不同场景有不同的居中方案：
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




## javascript部分
- **javascript有哪几种方法定义函数？**
    1. [函数声明表达式](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)
    2. [function操作符](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/function)
    3. [Function 构造函数](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function)
    4. [ES6:arrow function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/arrow_functions)


重要参考资料：[MDN:Functions_and_function_scope](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions_and_function_scope)

- **javascript有哪些方法定义对象**
    1. 对象字面量： <code>var obj = {};</code>
    2. 构造函数： <code>var obj = new Object();</code>
    3. Object.create(): <code>var obj = Object.create(Object.prototype);</code>

- **===运算符判断相等的流程是怎样的**  

    1. 如果两个值不是相同类型，它们不相等
    2. 如果两个值都是null或者都是undefined，它们相等
    3. 如果两个值都是布尔类型true或者都是false，它们相等
    4. 如果其中有一个是**NaN**，它们不相等
    5. 如果都是数值型并且数值相等，他们相等， -0等于0
    6. 如果他们都是字符串并且在相同位置包含相同的16位值，他它们相等；如果在长度或者内容上不等，它们不相等；两个字符串显示结果相同但是编码不同==和===都认为他们不相等
    7. 如果他们指向相同对象、数组、函数，它们相等；如果指向不同对象，他们不相等

- **==运算符判断相等的流程是怎样的**

    1. 如果两个值类型相同，按照===比较方法进行比较
    2. 如果类型不同，使用如下规则进行比较

        1. 如果其中一个值是null，另一个是undefined，它们相等
        2. 如果一个值是**数字**另一个是**字符串**，将**字符串转换为数字**进行比较
        3. 如果有布尔类型，将**true转换为1，false转换为0**，然后用==规则继续比较
        4. 如果一个值是对象，另一个是数字或字符串，将对象转换为原始值然后用==规则继续比较
        5. **其他所有情况都认为不相等**


- **对象到字符串的转换步骤**
    1. 如果对象有toString()方法，javascript调用它。如果返回一个原始值（primitive value如：string number boolean）,将这个值转换为字符串作为结果
    2. 如果对象没有toString()方法或者返回值不是原始值，javascript寻找对象的valueOf()方法，如果存在就调用它，返回结果是原始值则转为字符串作为结果
    3. 否则，javascript不能从toString()或者valueOf()获得一个原始值，此时throws a TypeError

-  **对象到数字的转换步骤**
    1. 如果对象有valueOf()方法并且返回元素值，javascript将返回值转换为数字作为结果
    2. 否则，如果对象有toString()并且返回原始值，javascript将返回结果转换为数字作为结果
    3. 否则，throws a TypeError

- **&lt;,&gt;,&lt;=,&gt;=的比较规则**  
所有比较运算符都支持任意类型，但是**比较只支持数字和字符串**，所以需要执行必要的转换然后进行比较，转换规则如下:
    1. 如果操作数是对象，转换为原始值：如果valueOf方法返回原始值，则使用这个值，否则使用toString方法的结果，如果转换失败则报错
    2. 经过必要的对象到原始值的转换后，如果两个操作数都是字符串，按照字母顺序进行比较（他们的16位unicode值的大小）
    3. 否则，如果有一个操作数不是字符串，**将两个操作数转换为数字**进行比较

- **+运算符工作流程**
    1. 如果有操作数是对象，转换为原始值
    2. 此时如果有**一个操作数是字符串**，其他的操作数都转换为字符串并执行连接
    3. 否则：**所有操作数都转换为数字并执行加法**

- **函数内部arguments变量有哪些特性，有哪些属性，如何将它转换为数组**
    - arguments所有函数中都包含的一个局部变量，是一个类数组对象，对应函数调用时的实参。如果函数定义同名参数会在调用时覆盖默认对象
    - arguments[index]分别对应函数调用时的实参，并且通过arguments修改实参时会同时修改实参
    - arguments.length为实参的个数（Function.length表示形参长度）
    - arguments.callee为当前正在执行的函数本身，使用这个属性进行递归调用时需注意this的变化
    - arguments.caller为调用当前函数的函数（已被遗弃）
    - 转换为数组：<code>var args = Array.prototype.slice.call(arguments, 0);</code>
    
- **DOM事件模型是如何的**
    - DOM事件包含捕获（capture）和冒泡（bubble）两个阶段：捕获阶段事件从window开始触发事件然后通过祖先节点一次传递到触发事件的DOM元素上；冒泡阶段事件从初始元素依次向祖先节点传递直到window
    - 添加事件监听器的方法有三种：
        - e.addEventListener(type, handler, capture)/e.removeEventListener(type, handler, capture)
        - e.onclick = handler
        - &lt;button onclick="alert(33)">&lt;/button>
        - 老版本IE没有捕获只有冒泡，使用e.attachEvent(on + type, handler)/e.detachEvent(on + type, handler)
    - 事件处理函数中this为当前事件触发的元素，e.target为实际触发事件的元素（老IE中为e.srcElement），事件处理函数的第一个参数为event对象（老IE中为window.event）
    - 通常利用事件冒泡机制托管事件处理程序提高程序性能。

- **评价一下三种方法实现继承的优缺点**
<pre>
function Person()
</pre>


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


- **请实现一个Event类，继承自此类的对象都会拥有两个方法on和trigger**
<pre>
</pre>


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


- 

- 