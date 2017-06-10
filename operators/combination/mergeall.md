# mergeAll

#### 签名: `mergeAll(concurrent: number): Observable`

## 收集并订阅所有的 observables 。

---

:bulb:  在很多情况下，你可以使用只使用单个操作符 [mergeMap](../transformation/mergemap.md) 来替代！
> 译者注：mergeMap === map + mergeAll

---

### 示例

( [示例测试](https://github.com/btroncone/learn-rxjs/blob/master/operators/specs/combination/mergeall-spec.ts) )

##### 示例 1: 使用 promise 来进行 concatAll

( [jsBin](http://jsbin.com/worecuhiba/1/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/0sc4nsxa/) )

```js
const myPromise = val =>
  new Promise(resolve => setTimeout(() => resolve(`Result: ${val}`), 2000));
// 发出 1,2,3
const source = Rx.Observable.of(1, 2, 3);

const example = source
  // 将每个值映射成 promise
  .map(val => myPromise(val))
  // 发出 source 的结果
  .mergeAll();

/*
  输出:
  "Result: 1"
  "Result: 2"
  "Result: 3"
*/
const subscribe = example.subscribe(val => console.log(val));
```

##### 示例 2: 使用**并发的**参数来进行 mergeAll

( [jsFiddle](https://jsfiddle.net/zra3zxhs/) )

```js
console.clear();

const interval = Rx.Observable.interval(500).take(5);

/*
  interval 每0.5秒发出一个值。这个值会被映射成延迟1秒的 interval 。mergeAll 操作符接收一个可选参数
  以决定在同一时间有多少个内部 observables 可以被订阅。其余的 observables 会先暂存以等待订阅。
*/
const example = interval
  .map(val => interval.delay(1000).take(3))
  .mergeAll(2)
  .subscribe(val => console.log(val));
/*
  一旦操作符发出了所有值，则 subscription 完成。
*/
```


### 其他资源

* [mergeAll](http://cn.rx.js.org/class/es6/Observable.js~Observable.html#instance-method-mergeAll) :newspaper: - 官方文档
* [[使用 RxJS 的 mergeAll 来打平高阶 observable](https://egghead.io/lessons/rxjs-flatten-a-higher-order-observable-with-mergeall-in-rxjs?course=use-higher-order-observables-in-rxjs-effectively) :video_camera: :dollar: - André Staltz

---
> :file_folder: 源码:  [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/mergeAll.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/mergeAll.ts)
