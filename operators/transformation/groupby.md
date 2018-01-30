# groupBy

#### 签名: `groupBy(keySelector: Function, elementSelector: Function): Observable`

## 基于提供的值分组成多个 observables

### 示例

##### 示例 1: 根据属性分组

( [jsBin](http://jsbin.com/buworowuye/edit?js,console) |
[jsFiddle](https://jsfiddle.net/btroncone/utncxxvf/) )

```js
const people = [
  { name: 'Sue', age: 25 },
  { name: 'Joe', age: 30 },
  { name: 'Frank', age: 25 },
  { name: 'Sarah', age: 35 }
];
// 发出每个 people
const source = Rx.Observable.from(people);
// 根据 age 分组
const example = source
  .groupBy(person => person.age)
  // 将每个分组项作为数组返回
  .mergeMap(group => group.toArray());
/*
  输出:
  [{age: 25, name: "Sue"},{age: 25, name: "Frank"}]
  [{age: 30, name: "Joe"}]
  [{age: 35, name: "Sarah"}]
*/
const subscribe = example.subscribe(val => console.log(val));
```

### 其他资源

* [groupBy](http://cn.rx.js.org/class/es6/Observable.js~Observable.html#instance-method-groupBy) :newspaper: - 官方文档
* [使用 RxJS 的 groupBy 操作符分组成高阶 observables](https://egghead.io/lessons/rxjs-group-higher-order-observables-with-rxjs-groupby?course=use-higher-order-observables-in-rxjs-effectively) :video_camera: :dollar: - André Staltz
* [在真实的 RxJS 应用中使用 groupBy](https://egghead.io/lessons/rxjs-use-groupby-in-real-rxjs-applications?course=use-higher-order-observables-in-rxjs-effectively) :video_camera: :dollar: - André Staltz

---
> :file_folder: 源码:  [https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/groupBy.ts](https://github.com/ReactiveX/rxjs/blob/master/src/internal/operators/groupBy.ts)
