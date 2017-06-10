# share

#### 签名: `share(): Observable`

## 在多个订阅者间共享源 observable 。

---

:bulb:  share 就像是使用了 Subject 和 refCount 的 [multicast](multicast.md)！

---

### 示例

##### 示例 1: 多个订阅者共享源 observable 

( [jsBin](http://jsbin.com/jobiyomari/1/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/Lmesxxaq/) )

```js
// 1秒后发出值
const source = Rx.Observable.timer(1000);
// 输出副作用，然后发出结果
const example = source
  .do(() => console.log('***SIDE EFFECT***'))
  .mapTo('***RESULT***');
/*
  ***不共享的话，副作用会执行两次***
  输出: 
  "***SIDE EFFECT***"
  "***RESULT***"
  "***SIDE EFFECT***"
  "***RESULT***"
*/
const subscribe = example.subscribe(val => console.log(val));
const subscribeTwo = example.subscribe(val => console.log(val));

// 在多个订阅者间共享 observable
const sharedExample = example.share();
/*
  ***共享的话，副作用只执行一次***
  输出: 
  "***SIDE EFFECT***"
  "***RESULT***"
  "***RESULT***"
*/
const subscribeThree = sharedExample.subscribe(val => console.log(val));
const subscribeFour = sharedExample.subscribe(val => console.log(val));
```


### 其他资源

* [share](http://cn.rx.js.org/class/es6/Observable.js~Observable.html#instance-method-share) :newspaper: - 官方文档
* [使用 share 共享流](https://egghead.io/lessons/rxjs-sharing-streams-with-share?course=step-by-step-async-javascript-with-rxjs) :video_camera: :dollar: - John Linquist

---
> :file_folder: 源码:  [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/share.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/share.ts)
