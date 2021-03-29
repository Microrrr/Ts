## Declaration类型

declare var 声明全局变量  
declare function 声明全局方法  
declare class 声明全局类  
declare enum 声明全局枚举类型  
declare namespace 声明（含有子属性的）全局对象  
interface 和 type 声明全局类型  
export 导出变量  
export namespace 导出（含有子属性的）对象  
export default ES6 默认导出  
export = commonjs 导出模块  
export as namespace UMD 库声明全局变量  
declare global 扩展全局变量  
declare module 扩展模块  
/// <reference /> 三斜线指令

## 什么是声明文件
通常我们会把声明语句放到一个单独的文件（jQuery.d.ts）中，这就是声明文件3：

// src/jQuery.d.ts

declare var jQuery: (selector: string) => any;
// src/index.ts

jQuery('#foo');
声明文件必需以 .d.ts 为后缀。

一般来说，ts 会解析项目中所有的 *.ts 文件，当然也包含以 .d.ts 结尾的文件。所以当我们将 jQuery.d.ts 放到项目中时，其他所有 *.ts 文件就都可以获得 jQuery 的类型定义了。
```
/path/to/project
├── src
|  ├── index.ts
|  └── jQuery.d.ts
└── tsconfig.json
```

假如仍然无法解析，那么可以检查下 tsconfig.json 中的 files、include 和 exclude 配置，确保其包含了 jQuery.d.ts 文件。

这里只演示了全局变量这种模式的声明文件，假如是通过模块导入的方式使用第三方库的话，那么引入声明文件又是另一种方式了，将会在后面详细介绍。

## 第三方声明文件
当然，jQuery 的声明文件不需要我们定义了，社区已经帮我们定义好了：jQuery in DefinitelyTyped。

我们可以直接下载下来使用，但是更推荐的是使用 @types 统一管理第三方库的声明文件。

@types 的使用方式很简单，直接用 npm 安装对应的声明模块即可，以 jQuery 举例：

`npm install @types/jquery --save-dev`  

## declare var  

在所有的声明语句中，declare var 是最简单的，如之前所学，它能够用来定义一个全局变量的类型。与其类似的，还有 declare let 和 declare const.
```ts
// src/jQuery.d.ts

declare let jQuery: (selector: string) => any;
```  

## declare function  
declare function 用来定义全局函数的类型。jQuery 其实就是一个函数，所以也可以用 function 来定义：
```ts
// src/jQuery.d.ts

declare function jQuery(selector: string): any;
```
```ts
// src/index.ts

jQuery('#foo');
```
在函数类型的声明语句中，函数重载也是支持的：
```ts
// src/jQuery.d.ts

declare function jQuery(selector: string): any;
declare function jQuery(domReadyCallback: () => any): any;
// src/index.ts

jQuery('#foo');
jQuery(function() {
    alert('Dom Ready!');
});
```

- declare class  
当全局变量是一个类的时候，我们用 declare class 来定义它的类型,
同样的，declare class 语句也只能用来定义类型，不能用来定义具体的实现，比如定义 sayHi 方法的具体实现则会报错：
```ts
// src/Animal.d.ts

declare class Animal {
    name: string;
    constructor(name: string);
    sayHi(): string;
}
```
```ts
// src/index.ts

let cat = new Animal('Tom');
```


