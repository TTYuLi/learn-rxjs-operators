# empty

#### 签名: `empty(scheduler: Scheduler): Observable`

## 立即完成的 observable 。

### 示例

##### 示例 1: empty 会立即完成

( [jsBin](http://jsbin.com/rodubucaqa/1/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/bz71mzuy/) )

```js
// 创建的 observable 会立即完成
const example = Rx.Observable.empty();
// 输出: 'Complete!'
const subscribe = example.subscribe({
  next: () => console.log('Next'),
  complete: () => console.log('Complete!')
});
```

### 源码解析

*即将发布...*

### Additional Resources
* [empty](http://cn.rx.js.org/class/es6/Observable.js~Observable.html#static-method-empty) :newspaper: - 官方文档
* [Creation operators: empty, never, and throw](https://egghead.io/lessons/rxjs-creation-operators-empty-never-throw?course=rxjs-beyond-the-basics-creating-observables-from-scratch) :video_camera: :dollar: - André Staltz

---
> :file_folder: 源码:  [https://github.com/ReactiveX/rxjs/blob/master/src/observable/EmptyObservable.ts](https://github.com/ReactiveX/rxjs/blob/master/src/observable/EmptyObservable.ts)
