# sample

#### 签名: `sample(sampler: Observable): Observable`

## 当提供的 observable 发出时从源 observable 中取样。

### 示例

##### 示例 1: 每2秒对源 observable 取样

( [jsBin](http://jsbin.com/gemebopifu/1/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/8wsbuvjb/) )

```js
// 每1秒发出值
const source = Rx.Observable.interval(1000);
// 每2秒对源 observable 最新发出的值进行取样
const example = source.sample(Rx.Observable.interval(2000));
// 输出: 2..4..6..8..
const subscribe = example.subscribe(val => console.log(val));
```

##### 示例 2: 当 interval 发出时对源 observable 取样

( [jsBin](http://jsbin.com/cunicepube/1/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/b33kg9dn/) )

```js
const source = Rx.Observable.zip(
  // 发出 'Joe', 'Frank' and 'Bob' in sequence
  Rx.Observable.from(['Joe', 'Frank', 'Bob']),
  // 每2秒发出值
  Rx.Observable.interval(2000)
);
// 每2.5秒对源 observable 最新发出的值进行取样
const example = source.sample(Rx.Observable.interval(2500));
// 输出: ["Joe", 0]...["Frank", 1]...........
const subscribe = example.subscribe(val => console.log(val));
```


### 其他资源

* [sample](http://cn.rx.js.org/class/es6/Observable.js~Observable.html#instance-method-sample) :newspaper: - 官方文档

---
> :file_folder: 源码:  [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/sample.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/sample.ts)
