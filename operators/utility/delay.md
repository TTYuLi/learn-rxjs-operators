# delay

#### 签名: `delay(delay: number | Date, scheduler: Scheduler): Observable`

## 根据给定时间延迟发出值。

### 示例

##### 示例 1: 延迟时间持续增加

( [jsBin](http://jsbin.com/zebatixije/1/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/1kxtzcu6/) )

```js
// 发出一项
const example = Rx.Observable.of(null);
// 每延迟一次输出便增加1秒延迟时间
const message = Rx.Observable.merge(
    example.mapTo('Hello'),
    example.mapTo('World!').delay(1000),
    example.mapTo('Goodbye').delay(2000),
    example.mapTo('World!').delay(3000)
  );
// 输出: 'Hello'...'World!'...'Goodbye'...'World!'
const subscribe = message.subscribe(val => console.log(val));
```

### 其他资源

* [delay](http://cn.rx.js.org/class/es6/Observable.js~Observable.html#instance-method-delay) :newspaper: - 官方文档
* [转换操作符: delay 和 delayWhen](https://egghead.io/lessons/rxjs-transformation-operators-delay-and-delaywhen?course=rxjs-beyond-the-basics-operators-in-depth) :video_camera: :dollar: - André Staltz

---
> :file_folder: 源码:  [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/delay.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/delay.ts)
