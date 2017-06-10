# windowTime

#### 签名: `windowTime(windowTimeSpan: number, windowCreationInterval: number, scheduler: Scheduler): Observable`

## 在每个提供的时间跨度内，收集源 obsercvable 中的值的 observable 。

### 示例

##### 示例 1: 每个指定持续时间都会开启新窗口

( [jsBin](http://jsbin.com/mifayacoqo/1/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/g04b3qeb/) )

```js
// 立即发出值，然后每秒发出值
const source = Rx.Observable.timer(0, 1000);
const example = source
  // 每3秒开启一个新窗口
  .windowTime(3000)
  .do(() => console.log('NEW WINDOW!'));

const subscribeTwo = example
  // 窗口发出嵌套的 observable
  .mergeAll()
  /*
  输出:
  "NEW WINDOW!"
  0
  1
  2
  "NEW WINDOW!"
  3
  4
  5
*/
  .subscribe(val => console.log(val));
```

### 其他资源

* [windowTime](http://cn.rx.js.org/class/es6/Observable.js~Observable.html#instance-method-windowTime) :newspaper: - 官方文档

---
> :file_folder: 源码:  [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/windowTime.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/windowTime.ts)
