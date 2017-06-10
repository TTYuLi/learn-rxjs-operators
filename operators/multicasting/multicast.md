# multicast

#### 签名: `multicast(selector: Function): Observable`

## 使用提供 的 Subject 来共享源 observable

### 示例

##### 示例 1: 使用标准的 Subject 进行 multicast

( [jsBin](http://jsbin.com/zexuyosuvi/1/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/x2z7p1gm/) )

```js
// 每2秒发出值并只取前5个
const source = Rx.Observable.interval(2000).take(5);

const example = source
  // 因为我们在下面进行了多播，所以副作用只会调用一次
  .do(() => console.log('Side Effect #1'))
  .mapTo('Result!');

// 使用 subject 订阅 source 需要调用 connect() 方法
const multi = example.multicast(() => new Rx.Subject());
/*
  多个订阅者会共享 source 
  输出:
  "Side Effect #1"
  "Result!"
  "Result!"
  ...
*/
const subscriberOne = multi.subscribe(val => console.log(val));
const subscriberTwo = multi.subscribe(val => console.log(val));
// 使用 subject 订阅 source
multi.connect();
```

##### 示例 2: 使用 ReplaySubject 进行 multicast

( [jsBin](http://jsbin.com/ruhexuhike/1/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/oj68u58j/) )

```js
// 每2秒发出值并只取前5个
const source = Rx.Observable.interval(2000).take(5);

// 使用 ReplaySubject 的示例
const example = source
  // 因为我们在下面进行了多播，所以副作用只会调用一次
  .do(() => console.log('Side Effect #2'))
  .mapTo('Result Two!');
// 可以使用任何类型的 subject
const multi = example.multicast(() => new Rx.ReplaySubject(5));
// 使用 subject 订阅 source
multi.connect();

setTimeout(() => {
  /*
   因为使用的是 ReplaySubject，订阅者会接收到 subscription 中的之前所有值。
   */
  const subscriber = multi.subscribe(val => console.group(val));
}, 5000);
```


### 其他资源

* [multicast](http://cn.rx.js.org/class/es6/Observable.js~Observable.html#instance-method-multicast) :newspaper: - 官方文档

---
> :file_folder: 源码:  [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/multicast.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/multicast.ts)
