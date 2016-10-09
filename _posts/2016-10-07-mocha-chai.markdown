---
layout:     post
title:      "mocha使用指南"
subtitle:   "写好测试单元才能保证质量"
date:       2016-10-08 12:00:00
author:     "Guolei"
header-img: ""
header-mask: 0.3
catalog:    true
tags:
    - mocha
    - chai
---

> Mocha is a feature-rich JavaScript test framework running on Node.js and in the browser, making asynchronous testing simple and fun.

mocha 是一个代码测试框架，针对异步的单元测试，简单有趣。

## 安装

 ```js
 npm install mocha -g
 ```

 ## 项目

保存在package.json中
```js
npm install mocha --save
```

进入项目并创建test目录（mocha会自动执行test目录下面的测试文件）

```js
mkdir test
touch ./test/add.js
touch ./test/add.text.js
```

写一个简单的add方法

```js
function add(x,y){
  return x+y;
}
module.exports = add;
```
add.js

测试代码

```js
var add = require('./add.js');
var expect = require('chai').expect;

describe('加法函数的测试',function(){
  it('1+1等于2',function(){
    expect(add(1,1)).to.be.equal(2);
  });
  it('1+1为true',function(){
    expect(add(1,1)).to.be.ok;
  });
  it('1+1相加不等于250',function(){
    expect(add(1,1)).to.be.not.equal(250);
  });
  it('[1,3,4]数组中含有3',function(){
    expect([1,3,4]).to.include(3);
  });
});

```

* 需要引进断言库chai（作用就是判断结果和预期的关系，相等，大于，小于，布尔，包含等关系）

*一个describe可以包含多个it

* it 的第一个参数是描述，第二个是一个fn

* expect传入结果，to.be后面是预期


### 执行

可以在test 目录中执行 mocha add.test.js
也可以在 demo01中 直接只执行 Mocha

运行结果

![](http://www.qinguolei.com/img/in-post/npm/npm-test.jpeg)

## 异步

```js
var expect = require('chai').expect;

it('测试应该5000毫秒后结束', function(done) {
  var x = true;
  var f = function() {
    x = false;
    expect(x).to.be.not.ok;
    done(); // 通知Mocha测试结束
  };
  setTimeout(f, 4000);
});
```

5s延迟 执行结果


报错了，因为mocha默认超过2000ms就结束

所以 需要设置超时时间

```
mocha -t 5000 add.test.js
```

执行结果


## promise

```js
var fetch = require('node-fetch');
var expect = require('chai').expect;

describe('promise.test.js - 异步测试', function() {
  it('异步请求应该返回一个对象', function() {
    return fetch('https://api.github.com')
      .then(function(res) {
        return res.json();
      }).then(function(json) {
        expect(json).to.be.an('object');
      });
  });
});

```
需要安装一个node-fetch的库

```js
npm install node-fetch --save
```

执行

```js
mocha promise.test.js
```

res代表返回的所有信息 （响应码，响应体，响应头）

res.json

```
function () {

  // for 204 No Content response, buffer will be empty, parsing it will throw error
  if (this.status === 204) {
    return Body.Promise.resolve({});
  }

  return this._decode().then(function(buffer) {
    return JSON.parse(buffer.toString());
  });

}
```
返回响应体，并格式化为对象

最后断言判断是否是一个对象

## before after

```js

```

mocha 还有很多有趣的功能，包括导出markdowm格式的报表，网页浏览结果,还通过--watch 可以试试检测代码，重新测试。

代码地址：[github](https://github.com/thunderqin/mocha.git)
### 著作权声明

本文demo主要参照了[一峰](http://www.cnblogs.com/whoamme/p/3467374.html)老师的博客
