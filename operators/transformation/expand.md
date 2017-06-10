# expand

#### 签名: `expand(project: function, concurrent: number, scheduler: Scheduler): Observable`

## 递归调用提供的函数

### 示例

##### 示例 1: 每次调用加1

( [jsBin](http://jsbin.com/fuxocepazi/1/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/nu4apbLt/) )

```js
// 发出 2
const source = Rx.Observable.of(2);
const example = source
  // 递归调用提供的函数
  .expand(val => {
    // 2,3,4,5,6
    console.log(`Passed value: ${val}`);
    // 3,4,5,6
    return Rx.Observable.of(1 + val);
  })
  // 调用5次
  .take(5);
/*
	"RESULT: 2"
	"Passed value: 2"
	"RESULT: 3"
	"Passed value: 3"
	"RESULT: 4"
	"Passed value: 4"
	"RESULT: 5"
	"Passed value: 5"
	"RESULT: 6"
	"Passed value: 6"
*/
// 输出: 2,3,4,5,6
const subscribe = example.subscribe(val => console.log(`RESULT: ${val}`));
```

### 其他资源

* [expand](http://cn.rx.js.org/class/es6/Observable.js~Observable.html#instance-method-expand) :newspaper: - 官方文档

---
> :file_folder: 源码:  [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/expand.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/expand.ts)
