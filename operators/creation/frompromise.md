# fromPromise

#### 签名: `fromPromise(promise: Promise, scheduler: Scheduler): Observable`

## 创建由 promise 转换而来的 observable，并发出 promise 的结果。

---

:bulb: 打平类操作符通常可以接收 promises 而不需要 observable 包装！

:bulb: 你还可以使用 [Observable.from](from.md) 达到同样的效果！

---

### 示例

##### 示例 1: 将 promise 转换成 observable 并捕获错误

( [jsBin](http://jsbin.com/cokivecima/1/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/upy6nr6n/) )

```js
// 基于输入来决定是 resolve 还是 reject 的示例 promise
const myPromise = willReject => {
  return new Promise((resolve, reject) => {
    if (willReject) {
      reject('Rejected!');
    }
    resolve('Resolved!');
  });
};
// 先发出 true，然后是 false
const source = Rx.Observable.of(true, false);
const example = source.mergeMap(val =>
  Rx.Observable
    // 将 promise 转换成 observable
    .fromPromise(myPromise(val))
    // 捕获并优雅地处理 reject 的结果
    .catch(error => Rx.Observable.of(`Error: ${error}`))
);
// 输出: 'Error: Rejected!', 'Resolved!'
const subscribe = example.subscribe(val => console.log(val));
```


### 其他资源

* [fromPromise](http://cn.rx.js.org/class/es6/Observable.js~Observable.html#static-method-fromPromise) :newspaper: - 官方文档
* [创建操作符: from, fromArray, fromPromise](https://egghead.io/lessons/rxjs-creation-operators-from-fromarray-frompromise?course=rxjs-beyond-the-basics-creating-observables-from-scratch) :video_camera: :dollar: - André Staltz
* [fromPromise - 指南](https://github.com/Reactive-Extensions/RxJS/blob/master/doc/gettingstarted/promises.md)

---
> :file_folder: 源码:  [https://github.com/ReactiveX/rxjs/blob/master/src/observable/PromiseObservable.ts](https://github.com/ReactiveX/rxjs/blob/master/src/observable/PromiseObservable.ts)
