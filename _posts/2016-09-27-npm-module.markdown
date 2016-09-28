---
layout:     post
title:      "npm 模块开发教程"
subtitle:   "从入门到入门"
date:       2016-09-26 12:00:00
author:     "Guolei"
header-img: ""
header-mask: 0.3
catalog:    false
tags:
    - npm
---

> 现在项目开发，离不开各种组件框架，比如express,pm2,vue,react,npm，那么如何上传自己的组件呢，下面带大家入门

## 创建组件

新建一个目录

```js
mkdir npm-module
```

然后初始化

```js
npm init
```

输入项目名称等信息，不清楚的直接按确认

你会发现一个package.json文件，这个文件是用来表述项目信息的，包括名称，版本，依赖，版权，git地址。。。。（非常重要）

现在我们开发一个** 获取URL参数 **的组件

原则就是 最后导出一个对象  供别人使用

具体实现看代码

```js
function query2json(url) {
    var hashIndex = url.indexOf('#'),
        strQuery,
        arrQuery,
        map = {};

    strQuery = url.substring(url.indexOf('?') + 1, hashIndex < 0 ? undefined : hashIndex);

    arrQuery = strQuery.split('&');

    for (var i = 0, len = arrQuery.length; i < len; i++) {
        var queryItem = arrQuery[i],
            arrTemp = queryItem.split('='),
            key = arrTemp[0];

        if (arrTemp.length > 0 && key) {
            map[key] = arrTemp[1] || '';
        }
    }

    return map;
};

exports.query2json = query2json;

```

index.js

现在我们新建一个test.js  测试我们代码

```js
var fn = require('./index.js');

var obj = fn.query2json('https://segmentfault.com/t/javascript?type=newest&page=2');

console.log(obj);
```

执行test.js

![](/img/in-post/npm/npm-test.jpeg)


## 发布到NPM

1. **去官网注册一个自己的开发账号**

记住自己的账号，密码，邮箱

2. 命令行连接npm

```js
npm adduser
```
![](/img/in-post/npm/npm-adduser.jpeg)

查看当前用户

```js
npm whoami
```
![](/img/in-post/npm/npm-whoami.jpeg)

3. 发布

```js
npm publish
```

4. 使用

进入项目目录

```js
npm install qinguolei
```
![](/img/in-post/npm/npm-install.jpeg)

```
var fn = require('qinguolei');

var obj = fn.query2json('https://segmentfault.com/t/javascript?type=newest&page=2');

console.log(obj)
```
index.js

```js
node index.js
```

![](/img/in-post/npm/npm-run.jpeg)


是不是很炫酷，是不是，是不是。。。。(二笔)

其实npm的威力，不仅仅如此，npm可以引用Node的各个模块，http，fs，path等等，对文件，路由，进程进行管理调用，我们可以用它来开发**脚手架**，**node框架**等等。

## 问题

1. 提示你 correct user ，发布失败。

解决办法： 你把package.json里面的author改成自己npm的名字

2. 提示你 version错误

![](/img/in-post/npm/npm-publish-version.jpeg)

发布后，再次修改代码记得更改版本号

3. npm registry 代理连接失败

因为国内被强，很多实用cnpm或者tnpm代理，需要改回来

```
npm config set registry https://registry.npmjs.org/
```

***常用的代理***

 * npm ---- https://registry.npmjs.org/
 * cnpm --- http://r.cnpmjs.org/
 * eu ----- http://registry.npmjs.eu/
 * au ----- http://registry.npmjs.org.au/
 * sl ----- http://npm.strongloop.com/
 * nj ----- https://registry.nodejitsu.com/


### 著作权声明


