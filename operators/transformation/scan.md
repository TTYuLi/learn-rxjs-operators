# scan

#### 签名: `scan(accumulator: function, seed: any): Observable`

## 随着时间的推移进行归并。

---

:bulb: 此操作符是许多基于 [Redux](http://redux.js.org) 实现的 RxJS 的核心！

---

### 示例

##### 示例 1: 随着时间的推移计算总数

( [jsBin](http://jsbin.com/kozidakose/1/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/d2g2a2c6/) )

```js
const subject = new Rx.Subject();
// 基础的 scan 示例，从0开始，随着时间的推移计算总数
const example = subject.startWith(0).scan((acc, curr) => acc + curr);
// 输出累加值
const subscribe = example.subscribe(val =>
  console.log('Accumulated total:', val)
);
// subject 发出的值会添加到当前的总数中
subject.next(1); //1
subject.next(2); //3
subject.next(3); //6
```

##### 示例 2: 对对象进行累加

( [jsBin](http://jsbin.com/fusunoguqu/1/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/36rbu38b/) )

```js
const subject = new Rx.Subject();
// scan 示例，随着时间的推移构建对象
const example = subject.scan((acc, curr) => Object.assign({}, acc, curr), {});
// 输出累加值
const subscribe = example.subscribe(val =>
  console.log('Accumulated object:', val)
);
// subject 发出的值会被添加成对象的属性
subject.next({name: 'Joe'}); // {name: 'Joe'}
subject.next({age: 30}); // {name: 'Joe', age: 30}
subject.next({favoriteLanguage: 'JavaScript'}); // {name: 'Joe', age: 30, favoriteLanguage: 'JavaScript'}
```

##### 示例 3: 随机发出累加数组中的值。

( [jsBin](http://jsbin.com/mudolideqo/1/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/afjgf4tz/) )

```js
// 累加数组中的值，并随机发出此数组中的值。
const scanObs = Rx.Observable.interval(1000)
  .scan((a, c) => a.concat(c), [])
  .map(r => r[Math.floor(Math.random() * r.length)])
  .distinctUntilChanged()
  .subscribe(console.log);
```

### 相关食谱

* [智能计数器](../../recipes/smartcounter.md)

### 其他资源

* [scan](http://cn.rx.js.org/class/es6/Observable.js~Observable.html#instance-method-scan) :newspaper: - 官方文档
* [使用 RxJS 中的 reduce 和 scan 聚集流](https://egghead.io/lessons/rxjs-aggregating-streams-with-reduce-and-scan-using-rxjs) :video_camera: - Ben Lesh
* [使用 scan 更新数据](https://egghead.io/lessons/rxjs-updating-data-with-scan?course=step-by-step-async-javascript-with-rxjs) :video_camera: :dollar: - John Linquist
* [转换操作符: scan](https://egghead.io/lessons/rxjs-transformation-operator-scan?course=rxjs-beyond-the-basics-operators-in-depth) :video_camera: :dollar: - André Staltz

---
> :file_folder: 源码:  [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/scan.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/scan.ts)
