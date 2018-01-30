# retryWhen

#### 签名: `retryWhen(receives: (errors: Observable) => Observable, the: scheduler): Observable`

## 当发生错误时，基于自定义的标准来重试 observable 序列。

### 示例

##### 示例 1: 在指定的时间间隔后触发重试

( [jsBin](http://jsbin.com/miduqexalo/1/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/49mkhsyr/) )

```js
// 每1秒发出值
const source = Rx.Observable.interval(1000);
const example = source
  .map(val => {
    if (val > 5) {
      // 错误将由 retryWhen 接收
      throw val;
    }
    return val;
  })
  .retryWhen(errors =>
    errors
      // 输出错误信息
      .do(val => console.log(`Value ${val} was too high!`))
      // 5秒后重启
      .delayWhen(val => Rx.Observable.timer(val * 1000))
  );
/*
  输出: 
  0
  1
  2
  3
  4
  5
  "Value 6 was too high!"
  --等待5秒后然后重复此过程
*/
const subscribe = example.subscribe(val => console.log(val));
```

##### 示例 2: 增加重试之间的时间间隔

( [jsBin](http://jsbin.com/nexuxoyifa/1/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/tLx1c3j6/2/) )

```js
// 每1秒发出值
const source = Rx.Observable.interval(1000);
const example = source
  .map(val => {
    if (val > 2) {
      // 错误将由 retryWhen 接收
      throw val;
    }
    return val;
  })
  .retryWhen(attempts => {
    return attempts.zip(Rx.Observable.range(1, 4)).mergeMap(([error, i]) => {
      if (i > 3) {
        return Rx.Observable.throw(error);
      }
      console.log(`Wait ${i} seconds, then retry!`);
      return Rx.Observable.timer(i * 1000);
    });
  })
  .catch(_ => Rx.Observable.of('Ouch, giving up!'));

const subscribe = example.subscribe(val => console.log(val));
```

### 其他资源

* [retryWhen](http://cn.rx.js.org/class/es6/Observable.js~Observable.html#instance-method-retryWhen) :newspaper: - 官方文档
* [错误处理操作符: retry 和 retryWhen](https://egghead.io/lessons/rxjs-error-handling-operator-retry-and-retrywhen?course=rxjs-beyond-the-basics-operators-in-depth) :video_camera: :dollar: - André Staltz

---
> :file_folder: 源码:  [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/retryWhen.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/retryWhen.ts)
