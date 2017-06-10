# bufferWhen

#### 签名: `bufferWhen(closingSelector: function): Observable`

## 收集值，直到关闭选择器发出值才发出缓冲的值。

### 示例

##### 示例 1: 发出基于 interval 缓冲的值

( [jsBin](http://jsbin.com/vugerupube/1/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/nr9agfuL/) )

```js
// 每1秒发出值
const oneSecondInterval = Rx.Observable.interval(1000);
// 返回的 observable 每5秒发出值
const fiveSecondInterval = () => Rx.Observable.interval(5000);
// 每5秒发出缓冲的值
const bufferWhenExample = oneSecondInterval.bufferWhen(fiveSecondInterval);
// 输出值
// 输出: [0,1,2,3]...[4,5,6,7,8]
const subscribe = bufferWhenExample.subscribe(val =>
  console.log('Emitted Buffer: ', val)
);
```

### 其他资源

* [bufferWhen](http://cn.rx.js.org/class/es6/Observable.js~Observable.html#instance-method-bufferWhen) :newspaper: - 官方文档

---
> :file_folder: 源码:  [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/bufferWhen.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/bufferWhen.ts)
