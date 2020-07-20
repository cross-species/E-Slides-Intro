---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "新闻爬虫及爬取结果的查询网站"
subtitle: "附代码"
summary: "◦1、选取3-5个代表性的新闻网站（比如新浪新闻、网易新闻等，或者某个垂直领域权威性的网站比如经济领域的雪球财经、东方财富等，或者体育领域的腾讯体育、虎扑体育等等）建立爬虫，针对不同网站的新闻页面进行分析，爬取出编码、标题、作者、时间、关键词、摘要、内容、来源等结构化信息，存储在数据库中。
    ◦2、建立网站提供对爬取内容的分项全文搜索，给出所查关键词的时间热度分析。"
authors: ["meijiayi"]
tags: ["front-end"]
categories: ["front-end"]
date: 2020-05-08T20:46:57+08:00
lastmod: 2020-05-08T20:46:57+08:00
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---
## 1	项目概述

新闻爬虫及爬取结果的查询网站
◦核心需求：
    ◦1、选取3-5个代表性的新闻网站（比如新浪新闻、网易新闻等，或者某个垂直领域权威性的网站比如经济领域的雪球财经、东方财富等，或者体育领域的腾讯体育、虎扑体育等等）建立爬虫，针对不同网站的新闻页面进行分析，爬取出编码、标题、作者、时间、关键词、摘要、内容、来源等结构化信息，存储在数据库中。
    ◦2、建立网站提供对爬取内容的分项全文搜索，给出所查关键词的时间热度分析。
◦技术要求：
    ◦1、必须采用Node.JS实现网络爬虫
    ◦2、必须采用Node.JS实现查询网站后端，HTML+JS实现前端（尽量不要使用任何前后端框架）

----
***话不多说，先放一个demo吧：*** 
[video(video-Bab35ECb-1589126460305)(type-bilibili)(url-https://player.bilibili.com/player.html?aid=625507495)(image-https://ss.csdn.net/p?http://i1.hdslb.com/bfs/archive/f10f2fbf0451bda1e197f4e9618f28ce00686dc6.jpg)(title-demo)]


***github链接：*** [https://github.com/Wence-May/News-Detector](https://github.com/Wence-May/News-Detector)

----
### 1.1	文件目录：
|---css/
|---fonts/
|---img/
|---js/
|---mysql.js（连接数据库，query）
|---crawler_scheduled.js
|---crw_163.js		（爬取网易新闻）
|---crw_chinanews.js	（爬取中国新闻网）
|---crw_sina.js	（爬取新浪新闻）
|---search_server.js（搜索服务器）
|---home.html （web搜索主页）
|---news.html	（跳转搜索结果）

### 1.2	使用
后端数据库：MySQL
爬虫以及server编程语言：Node.js
框架：无
package：

```javascript
var http = require('http');
var fs = require('fs');
var url = require('url');
var mysql = require("mysql");
var moment = require('moment');
var fs = require('fs');
var myRequest = require('request');
var myCheerio = require('cheerio');
var myIconv = require('iconv-lite');
require('date-utils');
```

## 2	爬虫部分
### 2.1 代码
（以爬取网易新闻为例）
首先，定义全局常量：
```javascript
var source_name = "网易新闻";
var domain = 'https://news.163.com/';
var myEncoding = "GBK";
var seedURL = 'https://news.163.com/';
```
URL信息，新闻网站的首页是要爬取的种子页面；

```javascript
var seedURL_format = "$('a')";
var keywords_format = " $('meta[name=\"keywords\"]').eq(0).attr(\"content\")";
var title_format = "$('title').text()";
var date_format = "$('html#ne_wrap').attr(\"data\-publishtime\")";//
var author_format = "$('.ep-editor').text()";
var content_format = "$('#endText').text()";
var desc_format = " $('meta[name=\"description\"]').eq(0).attr(\"content\")";
var source_format = "$('#ne_article_source').text()";
```
数据format：在二级页面上，通过id, name, class和标签等匹配到具体的某项html元素，以获得数据；

```javascript

var url_reg = /\/(\d{2})\/(\d{4})\/(\d{2})\/([A-Z0-9]{16}).html/;
var regExp = /((\d{4}|\d{2})(\-|\/|\.)\d{1,2}\3\d{1,2})|(\d{4}年\d{1,2}月\d{1,2}日)/
```
正则匹配
```javascript
//防止网站屏蔽我们的爬虫
var headers = {
    'User-Agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/39.0.2171.65 Safari/537.36'
}
```
为爬虫写一个header，在爬取网页时假装设备访问：
```javascript
//request模块异步fetch url
function request(url, callback) {
    var options = {
        url: url,
        encoding: null,
        //proxy: 'http://x.x.x.x:8080',
        headers: headers,
        timeout: 10000 //
    }
    myRequest(options, callback)
};
```
定义**request**函数，截获网页请求：
```javascript
//request模块异步fetch url
function request(url, callback) {
    var options = {
        url: url,
        encoding: null,
        //proxy: 'http://x.x.x.x:8080',
        headers: headers,
        timeout: 10000 //
    }
    myRequest(options, callback)
};
```
定义**seedget**函数，从种子页面抓取二级页面（具体新闻内容）的url：

```javascript
function seedget() {
    request(seedURL, function (err, res, body) { //读取种子页面
        try {
            // 用iconv转换编码
            var html = myIconv.decode(new Buffer(body), 'GBK');
            // console.log(html);
            //准备用cheerio解析html
            var $ = myCheerio.load(html, { decodeEntities: true });
        } catch (e) { console.log('读种子页面并转码出错：' + e) };
        var seedurl_news;
        try {
            seedurl_news = eval(seedURL_format);
        } catch (e) { console.log('url列表所处的html块识别出错：' + e) };
        seedurl_news.each(function (i, e) { //遍历种子页面里所有的a链接
            var myURL = "";
            try {
                //得到具体新闻url
                var href = "";
                href = $(e).attr("href");
                if (href == undefined) return;
                if (href.toLowerCase().indexOf('https://') >= 0 || href.toLowerCase().indexOf('http://') >= 0) myURL = href; //http://开头的
                else if (href.startsWith('//')) myURL = 'http:' + href; ////开头的
                else myURL = seedURL.substr(0, seedURL.lastIndexOf('/') + 1) + href; //其他

            } catch (e) { console.log('识别种子页面中的新闻链接出错：' + e) }

            if (!url_reg.test(myURL)) return; //检验是否符合新闻url的正则表达式
            console.log(myURL);

            var fetch_url_Sql = 'select url from fetches where url=?';
            var fetch_url_Sql_Params = [myURL];
            mysql.query(fetch_url_Sql, fetch_url_Sql_Params, function (qerr, vals, fields) {
                // console.log(vals)
                if (!vals) {
                    console.log('vals=NULL')
                }
                else if (vals.length > 0) {
                    console.log('URL duplicate!')
                } else newsGet(myURL); //读取新闻页面
            });
        });
    });
};
```
定义**newsGet**函数，传入二级页面URL，解析得到新闻title, publish_date, source_name, keywords, content的具体信息：

```javascript
function newsGet(myURL) { //读取新闻页面
    request(myURL, function (err, res, body) { //读取新闻页面
        try {
            var html_news = myIconv.decode(new Buffer(body), 'GBK'); //用iconv转换编码
            // console.log(html_news);
            //准备用cheerio解析html_news
            var $ = myCheerio.load(html_news, { decodeEntities: true });
            myhtml = html_news;
        } catch (e) { 
            console.log('读新闻页面并转码出错：' + e);
            return;
        };

        console.log("转码读取成功:" + myURL);
        //动态执行format字符串，构建json对象准备写入文件或数据库
        var fetch = {};
        fetch.title = "";
        fetch.content = "";
        fetch.publish_date = (new Date()).toFormat("YYYY-MM-DD");
        //fetch.html = myhtml;
        fetch.url = myURL;
        fetch.source_name = source_name;
        fetch.source_encoding = myEncoding; //编码
        fetch.crawltime = new Date();

        if (keywords_format == "") fetch.keywords = source_name; // eval(keywords_format);  //没有关键词就用sourcename
        else fetch.keywords = eval(keywords_format);

        if (title_format == "") fetch.title = ""
        else fetch.title = eval(title_format); //标题
        console.log(date_format);
        if (date_format != "") fetch.publish_date = eval(date_format); //刊登日期   
        console.log('date: ' + fetch.publish_date);
        if (fetch.publish_date) {
            fetch.publish_date = regExp.exec(fetch.publish_date)[0];
            fetch.publish_date = fetch.publish_date.replace('年', '-')
            fetch.publish_date = fetch.publish_date.replace('月', '-')
            fetch.publish_date = fetch.publish_date.replace('日', '')
            fetch.publish_date = new Date(fetch.publish_date).toFormat("YYYY-MM-DD");
        }
        console.log("@@@@@" + $('html#ne_wrap').attr("data-publishtime"));
        if (author_format == "") fetch.author = source_name; //eval(author_format);  //作者
        else fetch.author = eval(author_format);

        if (content_format == "") fetch.content = "";
        else fetch.content = eval(content_format).replace("\r\n" + fetch.author, ""); //内容,是否要去掉作者信息自行决定

        if (source_format == "") fetch.source = fetch.source_name;
        else fetch.source = eval(source_format).replace("\r\n", ""); //来源

        if (desc_format == "") fetch.desc = fetch.title;
        else fetch.desc = eval(desc_format);
        if(fetch.desc) fetch.desc.replace("\r\n", ""); //摘要   

        // console.log("keywords: " + fetch.keywords);
        // console.log("description: " + fetch.desc);;
        console.log("#####content: " + $('div#endText').text());
        
        if (fetch.content) {
            // var filename = source_name + "_" + (new Date()).toFormat("YYYY-MM-DD") +
            //     "_" + myURL.substr(myURL.lastIndexOf('/') + 1) + ".json";
            // ////存储json
            // fs.writeFileSync(filename, JSON.stringify(fetch));

            var fetchAddSql = 'INSERT INTO fetches(url,source_name,source_encoding,title,' +
                'keywords,author,publish_date,crawltime,content) VALUES(?,?,?,?,?,?,?,?,?)';
            var fetchAddSql_Params = [fetch.url, fetch.source_name, fetch.source_encoding,
            fetch.title, fetch.keywords, fetch.author, fetch.publish_date,
            fetch.crawltime.toFormat("YYYY-MM-DD HH24:MI:SS"), fetch.content
            ];

            //执行sql，数据库中fetch表里的url属性是unique的，不会把重复的url内容写入数据库
            mysql.query(fetchAddSql, fetchAddSql_Params, function (qerr, vals, fields) {
                if (qerr) {
                    console.log(qerr);
                    return;
                }
            }); //mysql写入
        } else console.log("404 Not found.");

    });
}
```
最后，调用seedget爬取新闻就可以了：

```javascript
seedget();
```

### 2.2 转码问题
遇到的第一个错误是Iconv转码报错：
在网上的很多示例里，转码是这么写的：

```javascript
 request(url, function (err, res, body) { //读取新闻页面
        try {
            var html_news = Iconv_lite.decode(body, Encoding); //用iconv转换编码
            //准备用cheerio解析html_news
        } catch (e) { 
            console.log('转码出错：' + e);
        };
});
```
这样运行总会报错：
[ERR_INVALID_ARG_TYPE]: The "buf" argument must be an instance of Buffer, TypedArray, or DataView. Received undefined.

刚接触这个函数不太懂参数类型和意思，但其实Iconv_lite.decode(body, encoding)函数是一个围绕utf-8展开的转码工具，它将其他各种编码的内容转成utf8格式，所以Encoding部分要填的应该是网页的原编码格式，而body部分是用来存储结果的Buffer。

上面代码中直接使用了body思路是可以的，但request()参数中的body是一个没有定义的类型，对于Buffer必须给它开辟一块空间，那么只需要在实例中改成：
```javascript
 request(url, function (err, res, body) { //读取新闻页面
        try {
            var html_news = Iconv_lite.decode(new Buffer(body), 'GBK'); //用iconv转换编码
            //准备用cheerio解析html_news
        } catch (e) { 
            console.log('转码出错：' + e);
        };
});
```
就可以了。

至于怎么确定网页原编码：打开新闻网站，按F12，进入console，输console.charset 就可以查看。一个网站的编码基本是统一的。

### 2.3	debug
在爬虫运行时经常会遇到的Error是：fetch.xxx = undefined.
这个错误表面上看是解析二级页面时没能解析成功，但可能有很多原因，比如

 1. 种子页面获取二级页面url的时候，有些url是http://开头，有些是https://开头，有些是相对路径，有些是//开头；
 2. 通过format从二级页面获取元素时，不同板块下的新闻可能内容、时间都有着不太一样的id/class，要多开几个报错的网页，读一下网页html源码，横向比较选择更有普遍性的id/name/class/tag用来定位；
 3. 有些网页的description、time等信息可能就是缺的，这时候处理一下代码逻辑，可以先判断某网页基本的content是否读取到，如果有content但其他属性undefined，那很有可能这是一次正确的读取操作；

最后，对于一些url形式符合正则表达式、但实际上是广告推广页面的个例，肯定会解析报错，程序中断。这个时候就要善于使用return语句，在throw error后直接return，接着解析下一个网页.......
这样运行结束后，只有寥寥几个error信息被返回，可以查阅是否误判；而大部分的新闻都被正确地写进数据库了。

## 3 数据库
在MysQL中创建database crawl，创建table fetches；
schema如下：

```sql
CREATE TABLE `fetches` (
  `id_fetches` int(11)  NOT NULL AUTO_INCREMENT,
  `url` varchar(200) DEFAULT NULL,
  `source_name` varchar(200) DEFAULT NULL,
  `source_encoding` varchar(45) DEFAULT NULL,
  `title` varchar(200) DEFAULT NULL,
  `keywords` varchar(200) DEFAULT NULL,
  `author` varchar(200) DEFAULT NULL,
  `publish_date` date DEFAULT NULL,
  `crawltime` datetime DEFAULT NULL,
  `content` longtext,
  `createtime` datetime DEFAULT CURRENT_TIMESTAMP,
  PRIMARY KEY (`id_fetches`),
  UNIQUE KEY `id_fetches_UNIQUE` (`id_fetches`),
  UNIQUE KEY `url_UNIQUE` (`url`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```
在爬虫部分中，crawl.js文件通过mysql.js来访问数据库，进行select，insert操作。mysql.js中需要自己定义**query**函数，将sql指令传给数据库执行：

```javascript
var query = function (sql, sqlparam, callback) {
    pool.getConnection(function (err, conn) {
        if (err) {
            callback(err, null, null);
            reject(err);
        } else {
            conn.query(sql, sqlparam, function (qerr, vals, fields) {
                conn.release(); //释放连接 
                callback(qerr, vals, fields); //事件驱动回调 
            });
        }
    });
};
```
最后别忘记

```javascript
exports.query = query;
```

## 3	Sever部分
Sever部分主要的难点是：在不用框架的情况下，用async/await方式将node.js的异步非阻塞式变成阻塞式，等待数据库query执行完毕后将结果写入response，才能执行response.end(). 否则在异步非阻塞式情况下，response.end()会直接执行，这时候query还在等待返回数据，数据被返回后无法再写入response.

而await起作用的条件是：await后面跟着的函数是一个Promise函数。所以我们要对mysql.query函数进行改写，将它变成一个Promise函数。由于此处mysql.js中的query是公用的（爬虫也调用），所以最好另行定义一个新的Promise的query函数：**promise_query**

```javascript
var promise_query = function (sqlparam, callback) {
    return new Promise((resolve, reject) => {
        pool.getConnection(function (err, conn) {

            if (err) {
                callback(err, null, null);
                reject(err);
            } else {
                conn.query(sqlparam, (err, rows, fields) => {
                    console.log(sqlparam);
                    if (err) {
                        console.log("$$$$$$");
                        reject(err);
                        callback(err, null, null);
                    } else {
                        console.log("#######");
                        resolve(rows);
                    }
                    conn.release();
                });
            }
        });
    });
};
exports.promise_query = promise_query;
```
两个query函数的参数也不一样，sever中sql的配置信息为

```javascript
var mysql = require("mysql");//定义了mysql的具体信息
var pool = mysql.createPool({
    host: '127.0.0.1',
    user: 'root',
    password: 'root',
    database: 'crawl'
});
```
这里sever通过pool连接数据库，不再需要向query指定sql，仅传入sqlparam即可。

## 4	web端
### 4.1 计算话题热度
使用了两个维度来衡量用户检索的新闻话题：Popularity & Freshness.

为了符合人脑遗忘曲线下降先快后慢的特点，粗略定义了两个变量的表达式：

$$Popularity =max\{  e^{-k_1 \cdot \Delta date}\}$$
$$Freshness = e^{-\frac{k_2}{num}}$$
其中$\Delta date$是新闻日期距当前的天数，$num$是检索得到的新闻条数，$k_1,k_2$作为参数供调节。

在实现中，服务器返回的value中是多个json对象，类似于{x : 1, y : 2},{x : 5, y : 3}......这样，所以要先将value解析成我们想要的num值，并遍历每一条news计算$e^{-k_1 \cdot \Delta date}$值。
下面是计算对应的代码：

```javascript
var num = 0;
var Popl = 0;
for (var i in value) {
	num += 1;
	}
var Popl = Math.exp(-1/num);
for (var j = 0; j < num; j++) {
	var delta = (new Date(publish_date) - new Date(now))/(1000*60*60*24);
	// console.log("delta time="+delta);
	if(Math.exp(delta/10) > Fresh) Fresh = Math.exp(delta/10);
}
```
最后化为百分比，保留一位小数输出。

```javascript
response.write("<h2>Popularity:  " + (Hot*100).toFixed(1)
 + "%&emsp;&emsp;&emsp;"+ "Freshness:  " + 
 + (Fresh*100).toFixed(1) +"%<h2>"); 
```
### 4.2 输出文本
新闻内容的直写输出法未免有些简陋，不妨加一些html tag：

```javascript
response.write("<h1>" + value[j].title + "</h1><br>");
                    response.write(value[j].author + "&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;" + publish_date + "&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;" + value[j].source_name + "<br>");
                    response.write("<p>" + value[j].content + "</p><br><br>");
```
这样输出的就是html，而非带着“\n"等转义字符的String了。

至此，项目的功能基本实现。


