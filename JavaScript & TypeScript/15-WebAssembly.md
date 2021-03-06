> Create by **fall** on 2021-12-27
> Recently revised in 2022-02-25

## 调试错误的方法

可以通过 `F12` 打开调试窗口进行调试

> anonymous 表示匿名的

## Error

```js
new Error('你的年龄太小了，看不得')
// Error: 你的年龄太小了，看不得
//     <anonymous> debugger eval code:1
new TypeError('类型错误！')
```

## throw

```js
let a = '你太小了'
throw a
// Uncaught 你太小了
throw new Error('请勿靠近！')
```

尽量抛出，或者是返回 Error 对象，或者是继承 Error 对象的其他错误对象，以便于调试

## try & catch

在传输过程中可能出现错误，应用在ajax的兼容和新添加代码块时，可以使用，避免错误影响过大

执行过程

- 先执行try中的代码
- try中代码正常，不执行catch中的代码
- try中代码出现错误，直接执行catch中的代码进行补救

```js
try{
    // 尝试执行
}catch(error){
    // error 错误对象，try括号中代码执行的异常信息
}
```

相比于 if else 判断， try catch效率更高，更加适合执行流程

try_throw_catch

throw 抛出异常

```js
try{
  alert("这里有个错误");
  throw new Error("别紧张，只是演习");
  alert("怎么会来到了错误后面");
}catch(error){
  alert("补救代码,"+error)
}
```

## debugger

相当于一个断点，程序执行到 debugger 的时候会暂停

```js
// 当在某一点的时候，如果你不想要执行，可以直接使用 debugger 进行调试

debugger
```

## finally

在 Promise 中进行使用，无论请求成功或者失败，都会执行的内容

```js
axios.get('https://www.baidu.com').then(res=>{
  // do something
}).catch(res=>{
  // do something handle the error
}).finally(()=>{
  // the thing always do after quest
})
```

## 更好地捕获错误

为了确保下一个开发者能够看懂，需要避免

```js
// 同时捕获两个函数，可能不清楚哪个函数会抛出异常
try{
  const foo = task()
  const bar = task()
}catch(e){
  console.log('Error: ',e)
}
```

改进：为每一个可能抛出异常的代码进行显示捕获

```js
try {
  const foo = runTask1();
} catch (e) {
  console.log('Error:', e);
}

try {
  const bar = runTask2();
} catch (e) {
  console.log('Error:', e);
}
```

