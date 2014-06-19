## FE-interview

个人收集的前端面试题和答案，参考答案仅代表个人观点，方便复习

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

- 