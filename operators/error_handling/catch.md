# catch

#### 签名: `catch(project : function): Observable`

## 优雅地处理 observable 序列中的错误

---

:warning:  记住要在 catch 函数中返回一个 observable !

---

### 示例

( [示例测试](https://github.com/btroncone/learn-rxjs/blob/master/operators/specs/error_handling/catch-spec.ts) )

##### 示例 1: 捕获 observable 中的错误

( [jsBin](http://jsbin.com/porevoxelu/1/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/wk4oLLqc/) )

```js
// 发出错误
const source = Rx.Observable.throw('This is an error!');
// 优雅地处理错误，并返回带有错误信息的 observable
const example = source.catch(val => Rx.Observable.of(`I caught: ${val}`));
// 输出: 'I caught: This is an error'
const subscribe = example.subscribe(val => console.log(val));
```

##### 示例 2: 捕获拒绝的 promise

( [jsBin](http://jsbin.com/rusaxubanu/1/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/sLq92gLv/) )

```js
// 创建立即拒绝的 Promise
const myBadPromise = () =>
  new Promise((resolve, reject) => reject('Rejected!'));
// 1秒后发出单个值
const source = Rx.Observable.timer(1000);
// 捕获拒绝的 promise，并返回包含错误信息的 observable
const example = source.flatMap(() =>
  Rx.Observable.fromPromise(myBadPromise()).catch(error =>
    Rx.Observable.of(`Bad Promise: ${error}`)
  )
);
// 输出: 'Bad Promise: Rejected'
const subscribe = example.subscribe(val => console.log(val));
```


### 其他资源

* [错误处理操作符: catch](https://egghead.io/lessons/rxjs-error-handling-operator-catch?course=rxjs-beyond-the-basics-operators-in-depth) :video_camera: :dollar: - André Staltz

---
> :file_folder: 源码:  [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/catch.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/catch.ts)
