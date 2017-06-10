# delayWhen

#### 签名: `delayWhen(selector: Function, sequence: Observable): Observable`

## 延迟发出值，延迟时间由提供函数决定。

### 示例

##### 示例 1: 基于 observable 的延迟

( [jsBin](http://jsbin.com/topohekuje/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/b057mxkL/) )

```js
// 每1秒发出值
const message = Rx.Observable.interval(1000);
// 5秒后发出值
const delayForFiveSeconds = () => Rx.Observable.timer(5000);
// 5秒后，开始发出 interval 延迟的值
const delayWhenExample = message.delayWhen(delayForFiveSeconds);
// 延迟5秒后输出值
// 例如， 输出: 5s....1...2...3
const subscribe = delayWhenExample.subscribe(val => console.log(val));
```

### 其他资源

* [delayWhen](http://cn.rx.js.org/class/es6/Observable.js~Observable.html#instance-method-delayWhen) :newspaper: - 官方文档
* [转换操作符: delay 和 delayWhen](https://egghead.io/lessons/rxjs-transformation-operators-delay-and-delaywhen?course=rxjs-beyond-the-basics-operators-in-depth) :video_camera: :dollar: - André Staltz

---
> :file_folder: 源码:  [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/delayWhen.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/delayWhen.ts)
