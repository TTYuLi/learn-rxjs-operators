# skip

#### 签名: `skip(the: Number): Observable`

## 跳过N个(由参数提供)发出值。

### Why use `skip`?
Skip allows you to ignore the first x emissions from the source. Generally `skip` is used when you have an observable that always emits certain values on subscription that you wish to ignore. Perhaps those first few aren't needed or you are subscribing to a `Replay` or `BehaviorSubject` and do not need to act on the initial values. Reach for `skip` if you are only concerned about later emissions.

You could mimic `skip` by using [`filter`](./filter.md) with indexes. Ex. `.filter((val, index) => index > 1)`

### 示例

##### 示例 1: 在发送前跳过N个值

( [jsBin](http://jsbin.com/hacepudabi/1/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/ar1eqbya/) )

```js
// 每1秒发出值
const source = Rx.Observable.interval(1000);
// 跳过前5个发出值
const example = source.skip(5);
// 输出: 5...6...7...8........
const subscribe = example.subscribe(val => console.log(val));
```

#### Example 2: Short hand for a specific filter use case

( [jsBin](http://jsbin.com/judamurego/edit?js,console) | [jsFiddle](https://jsfiddle.net/ElHuy/4jswLn3z/) )
```js
const numArrayObs = Rx.from([1,2,3,4,5,6,7,8,9,10]);

// 3,4,5...
const skipObs = numArrayObs
    .skip(2)
    .subscribe(console.log);

// 3,4,5...
const filterObs = numArrayObs
    .filter((val, index) => index > 1)
    .subscribe(console.log);

//Same output!
```

### 其他资源

* [skip](http://cn.rx.js.org/class/es6/Observable.js~Observable.html#instance-method-skip) :newspaper: - 官方文档
* [过滤操作符: take, first, skip](https://egghead.io/lessons/rxjs-filtering-operators-take-first-skip?course=rxjs-beyond-the-basics-operators-in-depth) :video_camera: :dollar: - André Staltz

---
> :file_folder: 源码:  [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/skip.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/skip.ts)
