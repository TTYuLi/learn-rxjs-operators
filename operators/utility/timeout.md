# timeout

#### 签名: `timeout(due: number, scheduler: Scheduler): Observable`

## 在指定时间间隔内不发出值就报错

### 示例

##### 示例 1: 2.5秒后超时

( [jsBin](http://jsbin.com/gonakiniho/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/nr4e1ofy/1/) )

```js
// 模拟请求
function makeRequest(timeToDelay) {
  return Rx.Observable.of('Request Complete!').delay(timeToDelay);
}

Rx.Observable.of(4000, 3000, 2000)
  .concatMap(duration =>
    makeRequest(duration)
      .timeout(2500)
      .catch(error => Rx.Observable.of(`Request timed out after: ${duration}`))
  )
  /*
  *  "Request timed out after: 4000"
  *  "Request timed out after: 3000"
  *  "Request Complete!"
  */
  .subscribe(val => console.log(val));
```

### 其他资源

* [timeout](https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/core/operators/timeout.md)
  :newspaper: - 官方文档

---

> :file_folder: 源码:
> [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/timeout.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/timeout.ts)
