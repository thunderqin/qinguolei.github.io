---
layout:     post
title:      "export,export default,exports,module.exports区别"
subtitle:   "es6 & node的模块化"
date:       2016-09-12 12:00:00
author:     "Guolei"
header-img: ""
header-mask: 0.3
catalog:    true
tags:
    - module
    - node
    - es6
    - export
---

> 项目越来越复杂，模块化显得格外重要，好的规范，可以让你的大代码简介易懂

## exports module.export

这两个是node的写法，遵循commionJS规范
区别

a.js

```js
 exports.a = function(){
 	console.log('a')
 }

```

index.js

```js

 var x = require('./a');

 console.log(x.a()) //输出 a
```

b.js

```js
 module.exports.b = function(){
 	console.log('a')
 }

```

index2.js

```js

 var x = require('./b');

 console.log(x()) //输出 b
```

**export导出的是一个对象{a:function(){}}**
**module.exports导出的就是fn**


## export default & export

## export default 和 export是es6模块化的写法，区别于commonjs ##

profile.js

```
export var name = 'guolei';

export default {
	a:1,
	b:2,
	fn(){console.log(111)}
}
```

index.js

```
import {name} from './profile'

import obj from './profile'
```

export default 默认导出 接收的时候随便命名一个变量
export 需要在{}内，接收对应的变量name(要和export一样)


代码地址：[github](https://github.com/thunderqin/babel-demo)





