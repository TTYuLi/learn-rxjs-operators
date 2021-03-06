# buffer

#### 签名: `buffer(closingNotifier: Observable): Observable`

## 收集输出值，直到提供的 observable 发出才将收集到的值作为数组发出。

### 示例

##### 示例 1: 缓冲值直到点击页面

( [jsBin](http://jsbin.com/fazimarajo/edit?js,console,output) |
[jsFiddle](https://jsfiddle.net/btroncone/7451s67k/) )

```js
// 创建每1秒发出值的 observable
const myInterval = Rx.Observable.interval(1000);
// 创建页面点击事件的 observable
const bufferBy = Rx.Observable.fromEvent(document, 'click');
/*
  收集由 myInterval 发出的所有值，直到我们点击页面。此时 bufferBy 会发出值以完成缓存。
  将自上次缓冲以来收集的所有值传递给数组。
*/
const myBufferedInterval = myInterval.buffer(bufferBy);
// 打印值到控制台
// 例如 输出: [1,2,3] ... [4,5,6,7,8]
const subscribe = myBufferedInterval.subscribe(val =>
  console.log(' Buffered Values:', val)
);
```

### 其他资源

* [buffer](http://cn.rx.js.org/class/es6/Observable.js~Observable.html#instance-method-buffer) :newspaper: - 官方文档
* [转换操作符: buffer](https://egghead.io/lessons/rxjs-transformation-operator-buffer?course=rxjs-beyond-the-basics-operators-in-depth) :video_camera: :dollar: - André Staltz

---
> :file_folder: 源码:  [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/buffer.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/buffer.ts)
