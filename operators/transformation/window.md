# window

#### 签名: `window(windowBoundaries: Observable): Observable`

## 时间窗口值的 observable 。

### 示例

##### 示例 1: 打开由内部 observable 指定的窗口

( [jsBin](http://jsbin.com/jituvajeri/1/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/rmgghg6d/) )

```js
// 立即发出值，然后每秒发出值
const source = Rx.Observable.timer(0, 1000);
const example = source.window(Rx.Observable.interval(3000));
const count = example.scan((acc, curr) => acc + 1, 0);
/*
  "Window 1:"
  0
  1
  2
  "Window 2:"
  3
  4
  5
  ...
*/
const subscribe = count.subscribe(val => console.log(`Window ${val}:`));
const subscribeTwo = example.mergeAll().subscribe(val => console.log(val));
```

### 其他资源

* [window](http://cn.rx.js.org/class/es6/Observable.js~Observable.html#instance-method-window) :newspaper: - 官方文档
* [使用 window 分割 RxJS observable](https://egghead.io/lessons/rxjs-split-an-rxjs-observable-with-window?course=use-higher-order-observables-in-rxjs-effectively) :video_camera: :dollar: - André Staltz

---
> :file_folder: 源码:  [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/window.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/window.ts)
