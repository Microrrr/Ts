## 元组

数组合并了相同类型的对象，而元组（Tuple）合并了不同类型的对象。
元组起源于函数编程语言（如 F#），这些语言中会频繁使用元组。

### 简单的例子

定义一对值分别为 string 和 number 的元组：
```ts
let tom: [string, number] = ['Tom', 25];
```

可以直接赋值或访问一个已知索引的元素:
```ts
let tom: [string, number];
tom[0] = 'Tom';
tom[1] = 25;

tom[0].slice(1);
tom[1].toFixed(2);

let tom1: [string, number];
tom1[0] = 'Tom';
```

当直接对元组类型的变量进行初始化或者赋值的时候，需要提供所有元组类型中指定的项
```ts
let tom: [string, number];
tom = ['Tom', 25];
```
```ts
let tom: [string, number];
tom = ['Tom'];

// Property '1' is missing in type '[string]' but required in type '[string, number]'.
```