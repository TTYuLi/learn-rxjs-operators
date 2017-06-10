# concatMap

#### 签名: `concatMap(project: function, resultSelector: function): Observable`

## 将值映射成内部 observable，并按顺序订阅和发出。

### 示例

##### 示例 1: 映射成内部 observable

( [jsBin](http://jsbin.com/powivemaxu/1/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/y3yx666r/) )

```js
// 发出 'Hello' 和 'Goodbye'
const source = Rx.Observable.of('Hello', 'Goodbye');
// 将 source 的值映射成内部 observable，当一个完成发出结果后再继续下一个
const example = source.concatMap(val => Rx.Observable.of(`${val} World!`));
// 输出: 'Example One: 'Hello World', Example One: 'Goodbye World'
const subscribe = example.subscribe(val => console.log('Example One:', val));
```

##### 示例 2: 映射成 promise

( [jsBin](http://jsbin.com/celixodeba/1/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/Lym33L97//) )

```js
// 发出 'Hello' 和 'Goodbye'
const source = Rx.Observable.of('Hello', 'Goodbye');
// 使用 promise 的示例
const examplePromise = val => new Promise(resolve => resolve(`${val} World!`));
// 将 source 的值映射成内部 observable，当一个完成发出结果后再继续下一个
const example = source.concatMap(val => examplePromise(val));
// 输出: 'Example w/ Promise: 'Hello World', Example w/ Promise: 'Goodbye World'
const subscribe = example.subscribe(val =>
  console.log('Example w/ Promise:', val)
);
```

##### 示例 3: 应用投射函数

( [jsBin](http://jsbin.com/vihacewozo/1/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/5sr5zzgy/) )

```js
// 发出 'Hello' 和 'Goodbye'
const source = Rx.Observable.of('Hello', 'Goodbye');
// 使用 promise 的示例
const examplePromise = val => new Promise(resolve => resolve(`${val} World!`));
// 返回结果前，第一个参数的结果将传递给第二个参数选择器函数
const example = source.concatMap(
  val => examplePromise(val),
  result => `${result} w/ selector!`
);
// 输出: 'Example w/ Selector: 'Hello w/ Selector', Example w/ Selector: 'Goodbye w/ Selector'
const subscribe = example.subscribe(val =>
  console.log('Example w/ Selector:', val)
);
```

##### 示例 4: 说明 concatMap 和 mergeMap 之间的区别

( [jsBin](http://jsbin.com/kiwuvamafo/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/3xd74d89/) )

```js
const concatMapSub = Rx.Observable.of(2000, 1000)
  .concatMap(v => Rx.Observable.of(v).delay(v))
  // concatMap: 2000, concatMap: 1000
  .subscribe(v => console.log('concatMap:', v));

const mergeMapSub = Rx.Observable.of(2000, 1000)
  .mergeMap(v => Rx.Observable.of(v).delay(v))
  // mergeMap: 1000, mergeMap: 2000
  .subscribe(v => console.log('mergeMap:', v));
```


### 其他资源

* [concatMap](http://cn.rx.js.org/class/es6/Observable.js~Observable.html#instance-method-concatMap) :newspaper: - 官方文档
* [使用 RxJS 的 concatMap 操作符来映射并连接高阶 observables](https://egghead.io/lessons/rxjs-use-rxjs-concatmap-to-map-and-concat-high-order-observables?course=use-higher-order-observables-in-rxjs-effectively) :video_camera: :dollar: - André Staltz

---
> :file_folder: 源码:  [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/concatMap.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/concatMap.ts)
