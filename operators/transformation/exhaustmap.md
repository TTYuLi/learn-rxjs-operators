# exhaustMap

#### 签名: `exhaustMap(project: function, resultSelector: function): Observable`

## 映射成内部 observable，忽略其他值直到该 observable 完成。

---

### 示例

##### 示例 1: 使用 interval 的 exhaustMap 

( [jsBin](http://jsbin.com/woposeqobo/1/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/9ovzapp9/) )

```js
const interval = Rx.Observable.interval(1000);
const delayedInterval = interval.delay(10).take(4);

const exhaustSub = Rx.Observable.merge(
  // 延迟10毫秒，然后开始 interval 并发出4个值
  delayedInterval,
  // 立即发出
  Rx.Observable.of(true)
)
  /*
   *  第一个发出的值 (of(true)) 会被映射成每秒发出值、 
   *  5秒后完成的 interval observable 。
   *  因为 delayedInterval 的发送是晚于前者的，虽然 observable 
   *  仍然是活动的，但它们会被忽略。
   *
   *  与类似的操作符进行下对比:
   *  concatMap 会进行排队
   *  switchMap 会在每次发送时切换成新的内部 observable
   *  mergeMap 会为每个发出值维护新的 subscription
   */
  .exhaustMap(_ => interval.take(5))
  // 输出: 0, 1, 2, 3, 4
  .subscribe(val => console.log(val))
```

##### 示例 2: 另一个使用 interval 的 exhaustMap 

( [jsBin](http://jsbin.com/fizuduzuti/1/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/5ck8yg5k/3/) )

```js
const firstInterval = Rx.Observable.interval(1000).take(10);
const secondInterval = Rx.Observable.interval(1000).take(2);

const exhaustSub = firstInterval
.do(i => console.log(`Emission of first interval: ${i}`))
.exhaustMap(f => secondInterval)
/*
  当我们订阅第一个 interval 时，它开始发出值(从0开始)。
  这个值会映射成第二个 interval，然后它开始发出值(从0开始)。
  当第二个 interval 出于激活状态时，第一个 interval 的值会被忽略。
  我们可以看到 firstInterval 发出的数字为3，6，等等...
  
    输出:
    Emission of first interval: 0
    0
    1
    Emission of first interval: 3
    0
    1
    Emission of first interval: 6
    0
    1
    Emission of first interval: 9
    0
    1
*/
  .subscribe(s => console.log(s));
```


### 其他资源

* [exhaustMap](http://cn.rx.js.org/class/es6/Observable.js~Observable.html#instance-method-exhaustMap) :newspaper: - 官方文档

---
> :file_folder: 源码:  [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/exhaustMap.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/exhaustMap.ts)
