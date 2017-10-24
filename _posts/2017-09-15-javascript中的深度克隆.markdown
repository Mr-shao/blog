---
layout: post
title: 'javascript深度克隆'
subtitle: javascript
date: 2017-05-19
tags: javascript
cover: 
---

## 浅克隆与深克隆

克隆就是复制一个对象的副本，而对象中又可能存在原始值和引用值，浅克隆就是克隆后的对象里的原始类型修改了，但引用类型没有修改。比如：

```js
    function shadowClone (obj) {
        var _out = Array.isArray(obj) ? [] : {};
        for (var _key in obj) {
            _out[_key] = obj[_key];
        }
        return _out;
    }
```

深克隆就是克隆出一样的对象，但是对象中的引用值地址并不相同。那么我们很容易就想到了递归。

javascript实现深克隆有很多种方法，其中比较简单的就是：

```js
let cloneObj = JSON.parse(JSON.stringify(obj));
```

但是上面这种方法的缺点就是function、RegExp、Date这一类的对象是无法被拷贝的。所以下面这个代码会稍微完善一点：
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
## 浅克隆与深克隆反正这里有好多好多好多好多字

这里是一个标签  
这里是一个标签  
这里是一个标签  
这里是一个标签  
这里是一个标签  
这里是一个标签  
这里是一个标签  
这里是一个标签  
这里是一个标签  
这里是一个标签  
这里是一个标签  
这里是一个标签  
这里是一个标签  
这里是一个标签  
这里是一个标签  
### 浅克隆与深克隆 13

这里是一个标签  
这里是一个标签  
这里是一个标签  
这里是一个标签  
这里是一个标签  
这里是一个标签  
这里是一个标签  
这里是一个标签  
这里是一个标签  
这里是一个标签  
这里是一个标签  
这里是一个标签  
这里是一个标签  
这里是一个标签  
这里是一个标签  
## 浅克隆与深克隆 12

这里是一个标签  
这里是一个标签  
这里是一个标签  
这里是一个标签  
这里是一个标签  
这里是一个标签  
这里是一个标签  
这里是一个标签  
这里是一个标签  
这里是一个标签  
这里是一个标签  
这里是一个标签  
这里是一个标签  
这里是一个标签  
这里是一个标签  

#### 浅克隆与深克隆 12