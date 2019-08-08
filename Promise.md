# Promise微探

## Promise是什么

Promise是为了解决js中回调地狱的问题。

## 如何用callback实现then

```
function dosomething () {
  return {
    then: function (callback) {
      ...
      callback()
    }
  }
```

## 定义一个Promise

```
function Promise (fn) {
  var callback = null

  this.then = function (cb) = {
    callback = cb
  }

  function resolve (value) {
    // 将 callback 打出当前执行线程，使之可以被 then 函数设定
    setTimeout(function() {
      callback(value);
    }, 1);
  }

  fn(resolve)
}

function doSomething() {
  return new Promise(function(resolve) {
    var value = 42;
    resolve(value);
  });
}
```

## Promise状态

1. pedding: 等待态
2. resolved: 解决态
3. rejected: 拒绝态