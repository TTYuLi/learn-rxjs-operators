# take

#### 签名: ` take(count: number): Observable`

## 在完成前发出N个值(N由参数决定)。

### 为什么使用 `take`？

当只对开头的一组值感兴趣时，你想要的便是 `take` 操作符。也许你想看看当用户第一次进入页面时，用户首先点击的是什么，你想要订阅点击事件并只取首个值。举例来说，你想要观看赛跑，但其实你只对首先冲过终点的人感兴趣。此操作符很清晰明了，你想要取开头*n*个值。

---

:bulb: 如果想基于某个逻辑或另一个 observable 来取任意数量的值，你可以 [takeUntil](takeuntil.md) 或 [takeWhile](takewhile.md)！

---

### 示例

##### 示例 1: 从源 observable 中取第一个值

( [jsBin](http://jsbin.com/vaxitupiwi/1/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/f9bz0tr3/) )

```js
// 发出 1,2,3,4,5
const source = Rx.Observable.of(1, 2, 3, 4, 5);
// 取第一个发出的值然后完成
const example = source.take(1);
// 输出: 1
const subscribe = example.subscribe(val => console.log(val));
```

##### 示例 2: 从源 observable 中取前5个值

( [jsBin](http://jsbin.com/kexenuzulu/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/g1fhxgua/) )

```js
// 每1秒发出值
const interval = Rx.Observable.interval(1000);
// 取前5个发出的值
const example = interval.take(5);
// 输出: 0,1,2,3,4
const subscribe = example.subscribe(val => console.log(val));
```

##### 示例 3: 取得首次点击的坐标

([jsFiddle](https://jsfiddle.net/ElHuy/9c5j064x/))

```html
<div id="locationDisplay">
  Where would you click first?
</div>
```

```js
const oneClickEvent = Rx.Observable
	.fromEvent(document, 'click')
  .take(1)
  .do(v => {
  	document.getElementById('locationDisplay').innerHTML
    	= `Your first click was on location ${v.screenX}:${v.screenY}`;
  });

const subscribe = oneClickEvent.subscribe();
```

### 其他资源

* [take](http://cn.rx.js.org/class/es6/Observable.js~Observable.html#instance-method-take) :newspaper: - 官方文档
* [过滤操作符: take, first, skip](https://egghead.io/lessons/rxjs-filtering-operators-take-first-skip?course=rxjs-beyond-the-basics-operators-in-depth) :video_camera: :dollar: - André Staltz

---
> :file_folder: 源码:  [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/take.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/take.ts)
