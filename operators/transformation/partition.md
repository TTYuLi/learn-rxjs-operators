# partition

#### 签名: `partition(predicate: function: boolean, thisArg: any): [Observable, Observable]`

## Split one observable into two based on provided predicate.

### 示例

##### 示例 1: 分割偶数和奇数

( [jsBin](http://jsbin.com/hipehexaku/1/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/q0xo7gvv/) )

```js
const source = Rx.Observable.from([1, 2, 3, 4, 5, 6]);
// 第一个值(events)返回 true 的数字集合，第二个值(odds)是返回 false 的数字集合
const [evens, odds] = source.partition(val => val % 2 === 0);
/*
  输出:
  "Even: 2"
  "Even: 4"
  "Even: 6"
  "Odd: 1"
  "Odd: 3"
  "Odd: 5"
*/
const subscribe = Rx.Observable.merge(
  evens.map(val => `Even: ${val}`),
  odds.map(val => `Odd: ${val}`)
).subscribe(val => console.log(val));
```

##### 示例 2: 分割正常执行和错误

( [jsBin](http://jsbin.com/kukuguhuri/1/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/fe246u5p/) )

```js
const source = Rx.Observable.from([1, 2, 3, 4, 5, 6]);
// 如果大于3就抛出错误
const example = source
  .map(val => {
    if (val > 3) {
      throw `${val} greater than 3!`;
    }
    return { success: val };
  })
  .catch(val => Rx.Observable.of({ error: val }));
// 分割正常执行或错误
const [success, error] = example.partition(res => res.success);
/*
  输出:
  "Success! 1"
  "Success! 2"
  "Success! 3"
  "Error! 4 greater than 3!"
*/
const subscribe = Rx.Observable.merge(
  success.map(val => `Success! ${val.success}`),
  error.map(val => `Error! ${val.error}`)
).subscribe(val => console.log(val));
```

### 其他资源

* [partition](http://cn.rx.js.org/class/es6/Observable.js~Observable.html#instance-method-partition) :newspaper: - 官方文档

---
> :file_folder: 源码:  [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/partition.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/partition.ts)
