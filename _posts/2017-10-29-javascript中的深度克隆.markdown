---
layout: post
title: 'javascript深度克隆(深拷贝)'
subtitle: javascript
date: 2017-10-29
categories: javascript
tags: javascript
cover: 
---

## 浅克隆与深克隆

**克隆**就是复制一个对象的副本，而对象中又可能存在原始值和引用值。

**浅克隆**也叫做浅拷贝，是克隆后的对象里的原始类型修改了，但引用类型并没有修改。比如：

```js
function shadowClone (obj) {
    var _out = Array.isArray(obj) ? [] : {};
    for (var _key in obj) {
        _out[_key] = obj[_key];
    }
    return _out;
}
```

**深克隆**也叫深拷贝，是克隆出一样的对象，但是对象中的引用值地址并不相同。那么我们很容易就想到了递归。

## 深克隆的实现方法

javascript实现深克隆有很多种方法，其中比较简单的就是，通常对于请求回来的JSON数据这样进行拷贝是很方便的：

```js
let cloneObj = JSON.parse(JSON.stringify(obj));
```

但是上面这种方法的缺点是JSON转换函数不支持function、RegExp、Date这一类的对象，这一类对象无法被拷贝的。

那么下面这个代码会稍微完善一点：
```js
function deepClone (obj) {
    var _out = new obj.constructor;
    var getType = function (n) {
        return Object.prototype.toString.call(n).slice(8, -1);
    }
    for (var _key in obj) {
        if (obj.hasOwnProperty(_key)) {
            if (getType(obj[_key]) === 'Object' || getType(obj[_key]) === 'Array') {
                _out[_key] = deepClone(obj[_key]);
            } else {
                _out[_key] = obj[_key];
            }
        }
    }
    return _out;
}
```

写的紧凑一点就成了这样：
```js
function deepClone (obj) {
    var _out = new obj.constructor;
    var getType = function (n) {
        return Object.prototype.toString.call(n).slice(8, -1);
    }
    for (var _key in obj) {
        if (obj.hasOwnProperty(_key)) {
            _out[_key] = getType(obj[_key]) === 'Object' || getType(obj[_key]) === 'Array' ? deepClone(obj[_key]) : obj[_key];
        }
    }
    return _out;
}
```
以上就是我对于深度克隆的笔记，上边的方法我认为是比较完善易懂的代码，有更好的方法或不足的地方希望大家留言。