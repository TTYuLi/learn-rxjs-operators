# publish

#### 签名: `publish() : ConnectableObservable`

## 共享源 observable 并通过调用 connect 方法使其变成热的。

### 示例

##### 示例 1: 在订阅之后调用 observable 的 connect 方法

( [jsBin](http://jsbin.com/laguvecixi/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/fpe6csaz/) )

```js
// 每1秒发出值
const source = Rx.Observable.interval(1000);
const example = source
  // 副作用只会执行1次
  .do(() => console.log('Do Something!'))
  // 不会做任何事直到 connect() 被调用
  .publish();

/*
  source 不会发出任何值直到 connect() 被调用
  输出: (5秒后)
  "Do Something!"
  "Subscriber One: 0"
  "Subscriber Two: 0"
  "Do Something!"
  "Subscriber One: 1"
  "Subscriber Two: 1"
*/
const subscribe = example.subscribe(val =>
  console.log(`Subscriber One: ${val}`)
);
const subscribeTwo = example.subscribe(val =>
  console.log(`Subscriber Two: ${val}`)
);

// 5秒后调用 connect，这会使得 source 开始发出值
setTimeout(() => {
  example.connect();
}, 5000);
```


### 其他资源

* [publish](http://cn.rx.js.org/class/es6/Observable.js~Observable.html#instance-method-publish) :newspaper: - 官方文档

> :file_folder: 源码:  [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/publish.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/publish.ts)
