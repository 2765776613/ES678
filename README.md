## ES6的一些新特性

### 1. let和const

  1. 之前js定义变量只有一个关键字：`var`    **(`var`存在一个问题，就是定义的变量有时会莫名奇妙的成为全局变量)**

     ```js
     for (var i = 0; i < 5; i++) {
         console.log(i);
     }
     console.log("循环外" + i);  // 5
     ```

     	2. `let`所声明的变量，只在`let`命令所在的代码块内有效。

     ```js
     for (let i = 0; i < 5; i++) {
         console.log(i);
     }
     console.log("循环外" + i);   // 报错
     ```

     	3. `const`声明的变量是常量，不能被修改

     ```js
     const a = 10;
     a = 321;  // 报错
     ```

### 2. 字符串扩展

 1. `includes()`：返回布尔值，表示是否找到了参数字符串

 2. `startsWith()`：返回布尔值，表示参数字符串是否在原字符串的头部。

 3. `endsWith()`：返回布尔值，表示参数字符串是否在原字符串的尾部

    ```js
    let str = "hello";
    console.log(str.includes("ell"));  // true
    console.log(str.startsWith("he")); // true
    console.log(str.endsWith("llo"));  // true
    ```

4. ES6中提供了\`来作为字符串模板标记，在两个`之间的部分都会被作为字符串的值，不管你任意换行，甚至加入js脚本。

### 3. 解构表达式

1. 数组解构

   ```js
   let arr = [1, 2, 3, 4];
   const [x, y, z, ] = arr;
   console.log(x, y, z);  // 1 2 3
   let [, ...rest] = arr;
   console.log(rest);  // [2,3,4]
   ```

2. json对象解构

   ```js
   const person = {
       name:"jack",
       age:21,
       language: ['java','js','css']
   }
   // 解构表达式获取值
   const {name,age,language} = person;
   // 浏览器控制台打印
   console.log(name);
   console.log(age);
   console.log(language);
   const { name: n } = person;
   console.log(n);   // jack
   ```

### 4. 函数优化

1. 函数参数可预设默认值

2. 箭头函数

   + 一个参数时

     ```js
     var print = function (obj) {
         console.log(obj);
     }
     // 简写为：
     var print = obj => console.log(obj);
     ```

   + 多个参数时

     ```js
     var sum = function (a , b) {
         return a + b;
     }
     // 简写为：
     var sum = (a,b) => a+b;
     ```

### 5. map和reduce方法

1. ` map()`：接收一个函数，将原数组中的所有元素用这个函数处理后放入新数组返回。

   ```js
   let arr = ['1', '20', '-5', '3'];
   console.log(arr);  // ["1", "20", "-5", "3"]
   let arr2 = arr.map(s => parseInt(s));
   console.log(arr2)  // [1, 20, -5, 3]
   ```

2. `reduce()`：接收一个函数（必须）和一个初始值（可选），它会从左到右依次把数组中的元素用reduce处理，并把处理的结果作为下次reduce的第一个参数。如果是第一次，会把前两个元素作为计算参数，或者把用户指定的初始值作为起始参数。

   ```js
   const arr = [1, 20, -5, 3];
   // 未指定初始值
   let num = arr.reduce((a, b) => a + b);
   console.log(num);  // 1+20+-5+3=19
   // 指定初始值
   let num2 = arr.reduce((a, b) => a + b, 1);
   console.log(num2);  // 1+1+20+-5+3=20
   ```

### 6. promise

1. 所谓Promise，简单说就是一个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果。从语法上说，Promise 是一个对象，从它可以获取异步操作的消息。Promise 提供统一的 API，各种异步操作都可以用同样的方法进行处理。

   ```js
   const p = new Promise(function (resolve, reject) {
       // 这里我们用定时任务模拟异步
       setTimeout(() => {
           const num = Math.random();
           // 随机返回成功或失败
           if (num < 0.5) {
               resolve("成功！num:" + num)  // 调用resolve，代表Promise将返回成功的结果
           } else {
               reject("出错了！num:" + num) // 调用reject，代表Promise会返回失败的结果
           }
       }, 300)
   })
   
   // 调用promise
   p.then(function (msg) {
       // 异步执行成功后的回调
       console.log(msg);
   }).catch(function (msg) {
       // 异步执行失败后的回调
       console.log(msg);
   })
   ```

### 7. 模块化

1. 模块化就是把代码进行拆分，方便重复利用。类似java中的导包：要使用一个包，必须先导包。模块功能主要由两个命令构成：`export`和`import`。

   - `export`命令用于规定模块的对外接口。
   - `import`命令用于导入其他模块提供的功能。

2. `export`：

   ```js
   // 导出对象
   export const util = {
       sum(a,b){
           return a + b;
       }
   }
   // 导出变量
   var name = "jack"
   var age = 21
   export {name,age}	
   ```

3. 使用`export`命令定义了模块的对外接口以后，其他 JS 文件就可以通过`import`命令加载这个模块。

   ```js
   // 导入util
   import util from 'hello.js'
   // 调用util中的属性
   util.sum(1,2)
   
   import {name, age} from 'user.js'
   console.log(name + " , 今年"+ age +"岁了")
   ```

### 8. 数组扩展方法

1. find(callback)：把数组中的元素逐个传递给函数callback执行，如果返回true，则返回该元素
2. findIndex(callback)：与find类似，不过返回的是匹配到的元素的索引
3. includes(callback)：与find类似，如果匹配到元素，则返回true，代表找到了。



## ES7的新特性

1. 什么是`async`、`await`？

   + async顾名思义是“异步”的意思，async用于声明一个函数是异步的。而await从字面意思上是“等待”的意思，就是用于等待异步完成。**（await只能在async函数中使用）**

   + 通常async、await都是跟随Promise一起使用的。

   + await得到Promise对象之后就等待Promise接下来的resolve或者reject。

   ```js
   async function testSync() {
        const response = await new Promise(resolve => {
            setTimeout(() => {
                resolve("async await test...");
             }, 1000);
        });
        console.log(response);
   }
   testSync();//async await test...
   ```

   
