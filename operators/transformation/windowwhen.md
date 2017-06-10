# windowWhen

#### 签名: `windowWhen(closingSelector: function(): Observable): Observable`

## 在提供的时间帧处关闭窗口，并发出从源 observable 中收集的值的 observable 。

### 示例

##### 示例 1: 根据定时器开启和关闭窗口

( [jsBin](http://jsbin.com/tuhaposemo/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/gnx9fb3h/) )

```js
// 立即发出值，然后每秒发出值
const source = Rx.Observable.timer(0, 1000);
const example = source
  // 每5秒关闭窗口并发出从源 observable 中收集的值的 observable
  .windowWhen(val => Rx.Observable.interval(5000))
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
  3
  4
  "NEW WINDOW!"
  5
  6
  7
  8
  9
*/
  .subscribe(val => console.log(val));
```

### 其他资源

* [windowWhen](http://cn.rx.js.org/class/es6/Observable.js~Observable.html#instance-method-windowWhen) :newspaper: - 官方文档

---
> :file_folder: 源码:  [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/windowWhen.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/windowWhen.ts)
