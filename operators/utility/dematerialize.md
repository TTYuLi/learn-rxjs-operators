# dematerialize

#### 签名: `dematerialize(): Observable`

## 将 notification 对象转换成 notification 值。

### 示例

##### 示例 1: 将 notifications 转换成值。

( [jsBin](http://jsbin.com/vafedocibi/1/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/jw08mouy/) )

```js
// 发出 next 和 error 通知
const source = Rx.Observable.from([
  Rx.Notification.createNext('SUCCESS!'),
  Rx.Notification.createError('ERROR!')
])
  // 将 notification 对象转换成 notification 值
  .dematerialize();

// 输出: 'NEXT VALUE: SUCCESS' 'ERROR VALUE: 'ERROR!'
const subscription = source.subscribe({
  next: val => console.log(`NEXT VALUE: ${val}`),
  error: val => console.log(`ERROR VALUE: ${val}`)
});
```

### 其他资源

* [dematerialize](http://cn.rx.js.org/class/es6/Observable.js~Observable.html#instance-method-dematerialize) :newspaper: - 官方文档

---
> :file_folder: 源码:  [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/demterialize.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/dematerialize.ts)
