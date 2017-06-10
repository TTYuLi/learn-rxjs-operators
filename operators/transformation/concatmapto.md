# concatMapTo

#### 签名: `concatMapTo(observable: Observable, resultSelector: function): Observable`

## 当前一个 observable 完成时订阅提供的 observable 并发出值。

### 示例

##### 示例 1: 映射成基础的 observable

( [jsBin](http://jsbin.com/telovuhupa/1/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/La0bam0u/) )

```js
// 每2秒发出值
const interval = Rx.Observable.interval(2000);
const message = Rx.Observable.of('Second(s) elapsed!');
// 当 interval 发出值，订阅 message 直到它完成，然后合并结果
const example = interval.concatMapTo(message, (time, msg) => `${time} ${msg}`);
// 输出值
// 输出: '0 Second(s) elapsed', '1 Second(s) elapsed'
const subscribe = example.subscribe(val => console.log(val));
```

##### 示例 2: 映射的 observable 以较慢的速度发出值

( [jsBin](http://jsbin.com/fogefebisu/1/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/s19wtscb/) )

```js
// 每2秒发出值
const interval = Rx.Observable.interval(2000);
// 每1秒发出值，共5秒
const source = Rx.Observable.interval(1000).take(5);
/* 
  ***小心***: 像这种情况下，源 observable 以比内部 observable 完成速度更快的速度发出，内存问题可能会出现。
  (interval 每1秒发出值，source 每5秒钟完成)
*/
// source 会在5秒后完成， 发出 0,1,2,3,4
const example = interval.concatMapTo(
  source,
  (firstInterval, secondInterval) => `${firstInterval} ${secondInterval}`
);
/*
  输出: 0 0
        0 1
        0 2
        0 3
        0 4
        1 0
        1 1
        继续...
          
*/
const subscribe = example.subscribe(val => console.log(val));
```

### 其他资源

* [concatMapTo](http://cn.rx.js.org/class/es6/Observable.js~Observable.html#instance-method-concatMapTo) :newspaper: - 官方文档

---
> :file_folder: 源码:  [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/concatMapTo.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/concatMapTo.ts)
