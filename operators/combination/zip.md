# zip

#### 签名: `zip(observables: *): Observable`

### 描述

###### TL;DR: 在所有 observables 发出后，将它们的值作为数组发出

**zip** 操作符会订阅所有内部 observables，然后等待每个发出一个值。一旦发生这种情况，将发出具有相应索引的所有值。这会持续进行，直到至少一个内部 
observable 完成。

---

:bulb: 与 [interval](../creation/interval) 或 [timer](../creation/timer.md) 进行组合, zip 可以用来根据另一个 observable 进行定时输出！

---

### 示例

##### 示例 1: 以交替的时间间隔对多个 observables 进行 zip

( [jsBin](http://jsbin.com/lireyisira/1/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/ton462sg/) )

```js
const sourceOne = Rx.Observable.of('Hello');
const sourceTwo = Rx.Observable.of('World!');
const sourceThree = Rx.Observable.of('Goodbye');
const sourceFour = Rx.Observable.of('World!');
// 一直等到所有 observables 都发出一个值，才将所有值作为数组发出
const example = Rx.Observable.zip(
  sourceOne,
  sourceTwo.delay(1000),
  sourceThree.delay(2000),
  sourceFour.delay(3000)
);
// 输出: ["Hello", "World!", "Goodbye", "World!"]
const subscribe = example.subscribe(val => console.log(val));
```

##### 示例 2: 当一个 observable 完成时进行 zip

( [jsBin](http://jsbin.com/fisitatesa/1/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/oamyk3xr/) )

```js
// 每1秒发出值
const interval = Rx.Observable.interval(1000);
// 当一个 observable 完成时，便不会再发出更多的值了
const example = Rx.Observable.zip(interval, interval.take(2));
// 输出: [0,0]...[1,1]
const subscribe = example.subscribe(val => console.log(val));
```


### 其他资源

* [zip](http://cn.rx.js.org/class/es6/Observable.js~Observable.html#static-method-zip) :newspaper: - 官方文档
* [组合操作符: zip](https://egghead.io/lessons/rxjs-combination-operator-zip?course=rxjs-beyond-the-basics-operators-in-depth) :video_camera: :dollar: - André Staltz

---
> :file_folder: 源码:  [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/zip.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/zip.ts)
