# windowCount

#### 签名: `windowCount(windowSize: number, startWindowEvery: number): Observable`

## 源 observable 中的值的 observable，每次发出N个值(N由参数决定)。

### 示例

##### 示例 1: 每发出x个项就开启一个新窗口

( [jsBin](http://jsbin.com/nezuvacexe/1/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/xjgbnqp5/) )

```js
// 每1秒发出值
const source = Rx.Observable.interval(1000);
const example = source
  // 每发出4个值就开启新窗口
  .windowCount(4)
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
  "NEW WINDOW!"
  4
  5
  6
  7 
*/
  .subscribe(val => console.log(val));
```

### 其他资源

* [windowCount](http://cn.rx.js.org/class/es6/Observable.js~Observable.html#instance-method-windowCount) :newspaper: - 官方文档

---
> :file_folder: 源码:  [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/windowCount.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/windowCount.ts)
