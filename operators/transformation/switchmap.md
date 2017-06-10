# switchMap

#### 签名: ` switchMap(project: function: Observable, resultSelector: function(outerValue, innerValue, outerIndex, innerIndex): any): Observable`

## 映射成 observable，完成前一个内部 observable，发出值。

---

:bulb: 如果你想要维护多个内部 subscription 的话， 请尝试 [`mergeMap`](mergemap.md)！

:bulb: 此操作符通常被认为是 [`mergeMap`](mergemap.md) 的安全版本！

:bulb: 此操作符可以取消正在进行中的网络请求！

---

### Why use `switchMap`?

The main difference between `switchMap` and other flattening operators is the
cancelling effect. On each emission the previous inner observable (the result of
the function you supplied) is cancelled and the new observable is subscribed.
You can remember this by the phrase **switch to a new observable**.

This works perfect for scenarios like
[typeaheads](https://angular-2-training-book.rangle.io/handout/http/search_with_switchmap.html)
where you are no longer concerned with the response of the previous request when
a new input arrives. This also is a safe option in situations where a long lived
inner observable could cause memory leaks, for instance if you used
[mergeMap](mergemap.md) with an interval and forgot to properly dispose of inner
subscriptions. Remember, `switchMap` maintains only one inner subscription at a
time, this can be seen clearly in the
[first example](#example-1-restart-interval-every-5-seconds).

Be careful though, you probably want to avoid `switchMap` in scenarios where
every request needs to complete, think writes to a database. `switchMap` could
cancel a request if the source emits quickly enough. In these
scenarios [mergeMap](mergemap.md) is the correct option.

### 示例

##### 示例 1: 每5秒重新启动 interval

( [jsBin](http://jsbin.com/birepuveya/1/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/6pz981gd/) )

```js
// 立即发出值， 然后每5秒发出值
const source = Rx.Observable.timer(0, 5000);
// 当 source 发出值时切换到新的内部 observable，发出新的内部 observable 所发出的值
const example = source.switchMap(() => Rx.Observable.interval(500));
// 输出: 0,1,2,3,4,5,6,7,8,9...0,1,2,3,4,5,6,7,8
const subscribe = example.subscribe(val => console.log(val));
```

##### 示例 2: 每次点击时重置

( [jsBin](http://jsbin.com/zoruboxogo/1/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/y11v8aqz/) )

```js
// 发出每次点击
const source = Rx.Observable.fromEvent(document, 'click');
// 如果3秒内发生了另一次点击，则消息不会被发出
const example = source.switchMap(val =>
  Rx.Observable.interval(3000).mapTo('Hello, I made it!')
);
// (点击)...3s...'Hello I made it!'...(点击)...2s(点击)...
const subscribe = example.subscribe(val => console.log(val));
```

##### 示例 3: 使用 `resultSelector` 函数

( [jsBin](http://jsbin.com/qobapubeze/1/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/nqfu534y/) )

```js
// 立即发出值， 然后每5秒发出值
const source = Rx.Observable.timer(0, 5000);
// 当 source 发出值时切换到新的内部 observable，调用投射函数并发出值
const example = source.switchMap(
  () => Rx.Observable.interval(2000),
  (outerValue, innerValue, outerIndex, innerIndex) => ({
    outerValue,
    innerValue,
    outerIndex,
    innerIndex
  })
);
/*
	输出:
	{outerValue: 0, innerValue: 0, outerIndex: 0, innerIndex: 0}
	{outerValue: 0, innerValue: 1, outerIndex: 0, innerIndex: 1}
	{outerValue: 1, innerValue: 0, outerIndex: 1, innerIndex: 0}
	{outerValue: 1, innerValue: 1, outerIndex: 1, innerIndex: 1}
*/
const subscribe = example.subscribe(val => console.log(val));
```

##### 示例 4: 使用 switchMap 的倒计时定时器

( [jsBin](http://jsbin.com/devedeqiga/edit?js,output) |
[jsFiddle](https://jsfiddle.net/btroncone/ww7zg988/189/) )

```js
const countdownSeconds = 10;
const setHTML = id => val => document.getElementById(id).innerHTML = val;
const pauseButton = document.getElementById('pause');
const resumeButton = document.getElementById('resume');
const interval$ = Rx.Observable.interval(1000).mapTo(-1);

const pause$ = Rx.Observable.fromEvent(pauseButton, 'click').mapTo(false);
const resume$ = Rx.Observable.fromEvent(resumeButton, 'click').mapTo(true);

const timer$ = Rx.Observable
	.merge(pause$, resume$)
  .startWith(interval$)
  .switchMap(val => val ? interval$ : Rx.Observable.empty())
  .scan((acc, curr) => curr ? curr + acc : acc, countdownSeconds)
  .takeWhile(v => v >= 0)
  .subscribe(setHTML('remaining'));
```

###### HTML

```html
<h4>
Time remaining: <span id="remaining"></span>
</h4>
<button id="pause">
Pause Timer
</button>
<button id="resume">
Resume Timer
</button>
```

### 相关食谱

* [智能计数器](../../recipes/smartcounter.md)

### 其他资源

* [switchMap](http://cn.rx.js.org/class/es6/Observable.js~Observable.html#instance-method-switchMap) :newspaper: - 官方文档
* [使用 switchMap 开启流](https://egghead.io/lessons/rxjs-starting-a-stream-with-switchmap?course=step-by-step-async-javascript-with-rxjs) :video_camera: :dollar: - John Linquist
* [使用 RxJS 的 switchMap 操作符来映射并打平高阶 observables](https://egghead.io/lessons/rxjs-use-rxjs-switchmap-to-map-and-flatten-higher-order-observables?course=use-higher-order-observables-in-rxjs-effectively) :video_camera: :dollar: - André Staltz
* [在 RxJS 中，使用 switchMap 作为打平 observables 的安全默认操作符](https://egghead.io/lessons/rxjs-use-switchmap-as-a-safe-default-to-flatten-observables-in-rxjs?course=use-higher-order-observables-in-rxjs-effectively) :video_camera: :dollar: - André Staltz

---
> :file_folder: 源码:  [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/switchMap.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/switchMap.ts)
