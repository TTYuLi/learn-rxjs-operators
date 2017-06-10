# throw

#### 签名: `throw(error: any, scheduler: Scheduler): Observable`

## 在订阅上发出错误

### 示例

##### 示例 1: 在订阅上抛出错误

( [jsBin](http://jsbin.com/punubequju/1/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/mks82xqz/) )

```js
// 在订阅上使用指定值来发出错误
const source = Rx.Observable.throw('This is an error!');
// 输出: 'Error: This is an error!'
const subscribe = source.subscribe({
  next: val => console.log(val),
  complete: () => console.log('Complete!'),
  error: val => console.log(`Error: ${val}`)
});
```


### 其他资源

* [throw](http://cn.rx.js.org/class/es6/Observable.js~Observable.html#static-method-throw) :newspaper: - 官方文档
* [创建操作符: empty, never 和 throw](https://egghead.io/lessons/rxjs-creation-operators-empty-never-throw?course=rxjs-beyond-the-basics-creating-observables-from-scratch) :video_camera: :dollar: - André Staltz

---
> :file_folder: 源码:  [https://github.com/ReactiveX/rxjs/blob/master/src/observable/ErrorObservable.ts](https://github.com/ReactiveX/rxjs/blob/master/src/observable/ErrorObservable.ts)
