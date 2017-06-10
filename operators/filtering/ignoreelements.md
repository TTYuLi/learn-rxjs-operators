# ignoreElements

#### 签名: `ignoreElements(): Observable`

## 忽略所有通知，除了 complete 和 error 。

### 示例

##### 示例 1: 忽略源 observable 的所有数据项

( [jsBin](http://jsbin.com/yiyefelubi/1/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/59scjqss/) )

```js
// 每100毫秒发出值
const source = Rx.Observable.interval(100);
// 忽略所有值，只发出 complete
const example = source.take(5).ignoreElements();
// 输出: "COMPLETE!"
const subscribe = example.subscribe(
  val => console.log(`NEXT: ${val}`),
  val => console.log(`ERROR: ${val}`),
  () => console.log('COMPLETE!')
);
```

##### 示例 2: 只显示错误

( [jsBin](http://jsbin.com/gogonawuze/1/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/srcwdgw6/) )

```js
// 每100毫秒发出值
const source = Rx.Observable.interval(100);
// 忽略所有值，只发出 error
const error = source
  .flatMap(val => {
    if (val === 4) {
      return Rx.Observable.throw(`ERROR AT ${val}`);
    }
    return Rx.Observable.of(val);
  })
  .ignoreElements();
// 输出: "ERROR: ERROR AT 4"
const subscribe = error.subscribe(
  val => console.log(`NEXT: ${val}`),
  val => console.log(`ERROR: ${val}`),
  () => console.log('SECOND COMPLETE!')
);
```


### 其他资源

* [ignoreElements](http://cn.rx.js.org/class/es6/Observable.js~Observable.html#instance-method-ignoreElements) :newspaper: - 官方文档

---
> :file_folder: 源码:  [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/ignoreElements.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/ignoreElements.ts)
