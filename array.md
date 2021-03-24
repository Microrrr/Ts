## 数组的类型
在 TypeScript 中，数组类型有多种定义方式，比较灵活。

-「类型 + 方括号」表示法§
最简单的方法是使用「类型 + 方括号」来表示数组：

```ts
let fibonacci: number[] = [1, 1, 2, 3, 5];
```
- 数组泛型
我们也可以使用数组泛型（Array Generic） Array<elemType> 来表示数组：

```ts
let fibonacci: Array<number> = [1, 1, 2, 3, 5];
```

- any 在数组中的应用
一个比较常见的做法是，用 any 表示数组中允许出现任意类型：

```ts
let list: any[] = ['xcatliu', 25, { website: 'http://xcatliu.com' }];
```

- 类数组
类数组（Array-like Object）不是数组类型，比如 arguments：
```ts
function sum() {
    let args: number[] = arguments;
}

// Type 'IArguments' is missing the following properties from type 'number[]': pop, push, concat, join, and 24 more.
上例中，arguments 实际上是一个类数组，不能用普通的数组的方式来描述，而应该用接口：

function sum() {
    let args: {
        [index: number]: number;
        length: number;
        callee: Function;
    } = arguments;
}
```
