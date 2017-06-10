# interval

#### 签名: `interval(period: number, scheduler: Scheduler): Observable`

## 基于给定时间间隔发出数字序列。

### 示例

##### 示例 1: Emit sequence of values at 1 second interval

( [jsBin](http://jsbin.com/vigohomabo/1/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/x3mrwzr0/) )

```js
// 每1秒发出数字序列中的值
const source = Rx.Observable.interval(1000);
// 数字: 0,1,2,3,4,5....
const subscribe = source.subscribe(val => console.log(val));
```

### Additional Resources

* [interval](http://cn.rx.js.org/class/es6/Observable.js~Observable.html#static-method-interval) :newspaper: - 官方文档
* [创建操作符: interval 和 timer](https://egghead.io/lessons/rxjs-creation-operators-interval-and-timer?course=rxjs-beyond-the-basics-creating-observables-from-scratch) :video_camera: :dollar: - André Staltz

---
> :file_folder: 源码:  [https://github.com/ReactiveX/rxjs/blob/master/src/observable/IntervalObservable.ts](https://github.com/ReactiveX/rxjs/blob/master/src/observable/IntervalObservable.ts)
