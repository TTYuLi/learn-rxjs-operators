# race

#### 签名: `race(): Observable`

## 使用首先发出值的 observable 。

### 示例

##### 示例 1: 使用 4个 observables 进行 race

( [jsBin](http://jsbin.com/goqiwobeno/1/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/8jcmb1ec/) )

```js
// 接收第一个发出值的 observable
const example = Rx.Observable.race(
  // 每1.5秒发出值
  Rx.Observable.interval(1500),
  // 每1秒发出值
  Rx.Observable.interval(1000).mapTo('1s won!'),
  // 每2秒发出值
  Rx.Observable.interval(2000),
  // 每2.5秒发出值
  Rx.Observable.interval(2500)
);
//输出: "1s won!"..."1s won!"...etc
const subscribe = example.subscribe(val => console.log(val));
```

##### 示例 2: 使用 error 进行 race

( [jsFiddle](https://jsfiddle.net/gbeL4t55/2/) )

```js
console.clear();

// 抛出错误并忽略其他的 observables 。
const first = Rx.Observable.of('first')
  .delay(100)
  .map(() => {
    throw 'error';
  });
const second = Rx.Observable.of('second').delay(200);
const third = Rx.Observable.of('third').delay(300);

const race = Rx.Observable.race(first, second, third).subscribe(val =>
  console.log(val)
);
```

### 其他资源

* [race](http://cn.rx.js.org/class/es6/Observable.js~Observable.html#instance-method-race) :newspaper: - 官方文档

---
> :file_folder: 源码:  [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/race.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/race.ts)
