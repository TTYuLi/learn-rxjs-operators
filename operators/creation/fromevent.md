# fromEvent

#### 签名: `fromEvent(target: EventTargetLike, eventName: string, selector: function): Observable`

## 将事件转换成 observable 序列。

### 示例

##### 示例 1: 鼠标事件转换而来的 observable

( [jsBin](http://jsbin.com/xikapewoqa/1/edit?js,console,output) |
[jsFiddle](https://jsfiddle.net/btroncone/vbLz1pdx/) )

```js
// 创建发出点击事件的 observable
const source = Rx.Observable.fromEvent(document, 'click');
// 映射成给定的事件时间戳
const example = source.map(event => `Event time: ${event.timeStamp}`);
// 输出 (示例中的数字以运行时为准): 'Event time: 7276.390000000001'
const subscribe = example.subscribe(val => console.log(val));
```

### 相关食谱

* [智能计数器](../../recipes/smartcounter.md)

### 其他资源

* [fromEvent](http://cn.rx.js.org/class/es6/Observable.js~Observable.html#static-method-fromEvent) :newspaper: - 官方文档

---
> :file_folder: 源码:  [https://github.com/ReactiveX/rxjs/blob/master/src/observable/FromEventObservable.ts](https://github.com/ReactiveX/rxjs/blob/master/src/observable/FromEventObservable.ts)
