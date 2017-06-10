# do

#### 签名: `do(nextOrObserver: function, error: function, complete: function): Observable`

## Transparently perform actions or side-effects, such as logging.
## 透明地执行操作或副作用，比如打印日志。

### 示例

##### 示例 1: 使用 do 输出日志

( [jsBin](http://jsbin.com/jimazuriva/1/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/qtyakorq/) )

```js
const source = Rx.Observable.of(1, 2, 3, 4, 5);
// 使用 do 透明地打印 source 中的值
const example = source
  .do(val => console.log(`BEFORE MAP: ${val}`))
  .map(val => val + 10)
  .do(val => console.log(`AFTER MAP: ${val}`));
// 'do' 并不转换值
// 输出: 11...12...13...14...15
const subscribe = example.subscribe(val => console.log(val));
```

### 其他资源

* [do](http://cn.rx.js.org/class/es6/Observable.js~Observable.html#instance-method-do) :newspaper: - 官方文档
* [使用 do 打印流](https://egghead.io/lessons/rxjs-logging-a-stream-with-do?course=step-by-step-async-javascript-with-rxjs) :video_camera: :dollar: - John Linquist
* [工具操作符: do](https://egghead.io/lessons/rxjs-utility-operator-do?course=rxjs-beyond-the-basics-operators-in-depth) :video_camera: :dollar: - André Staltz

---
> :file_folder: 源码:  [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/do.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/do.ts)
