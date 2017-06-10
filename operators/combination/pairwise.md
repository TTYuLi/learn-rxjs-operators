# pairwise

#### 签名: `pairwise(): Observable<Array>`

## 将前一个值和当前值作为数组发出

### 示例

##### 示例 1:

( [jsBin](http://jsbin.com/keteyahido/1/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/8va47bq3/) )

```js
var interval = Rx.Observable.interval(1000);

// 返回: [0,1], [1,2], [2,3], [3,4], [4,5]
interval
  .pairwise()
	.take(5)
	.subscribe(console.log);
```

### 其他资源

* [pairwise](http://cn.rx.js.org/class/es6/Observable.js~Observable.html#instance-method-pairwise) :newspaper: - 官方文档

---
> :file_folder: 源码:  [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/pairwise.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/pairwise.ts)
