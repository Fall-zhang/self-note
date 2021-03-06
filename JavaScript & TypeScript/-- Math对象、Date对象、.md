> 创建时间：2021-05-26
> 更新时间：2021-12-10



## Math对象上的方法

| 方法             | 作用                                                        |
| ---------------- | ----------------------------------------------------------- |
| `Math.abs()`     | 返回取绝对值                                                |
| `Math.max()`     | 传入逗号分割的多个数，返回最大的参数                        |
| `Math.min()`     | 传入逗号分割的多个数，返回最小的参数                        |
| `Math.round()`   | 四舍五入到最接近的整数                                      |
| `Math.ceil()`    | 返回向上取整的值                                            |
| `Math.floor()`   | 返回向下取整的值                                            |
| `Math.random()`  | 返回值为随机数，无需传入值                                  |
| `Math.E`         | 常数 e≈2.71828                                              |
| `Math.trunc()`   | 返回该数值的整数部分                                        |
| `Math.sign()`    | 返回数值的类型，1 表示正数，-1 表示负数，0                  |
| `Math.cbrt()`    | 返回数值立方根                                              |
| `Math.clz32()`   | 返回数值的 32 位无符号整数形式，即32-该数值的二进制表示位数 |
| `Math.imul(a,b)` | 返回两个数相乘                                              |
| `Math.fround()`  | 返回数值的 32 位单精度浮点数形式                            |
| `Math.pow(x,y)`  | 求 x 的 y 次方                                              |

- `Math.hypot()`  返回所有数值平方和的平方根 `Math.hypot(4,4,4,4) == 8`    
- `Math.expm1()`：  返回`e^n - 1`
- `Math.log1p()`：返回 1 + n 的自然对数(`Math.log(1 + n)`)
- `Math.log10()`：返回以 10 为底的 n 的对数
- `Math.log2()`：返回以 2 为底的n的对数
- `Math.sinh()`：返回 n 的双曲正弦
- `Math.cosh()`：返回 n 的双曲余弦
- `Math.tanh()`：返回 n 的双曲正切
- `Math.asinh()`：返回 n 的反双曲正弦
- `Math.acosh()`：返回 n 的反双曲余弦
- `Math.atanh()`：返回 n 的反双曲正切

## RegExp

### 对象特性

```js
// 正则表达式的声明
const reg1 = new RegExp('hello','ig') 
const reg2 = new RegExp(/xYz\d+/gi, i) // 如果传入了第二个参数，以第二个为准
const reg3 = RegExp('hello','ig')
const reg4 = /hello/gi
// i 表示不区分大小写，g 表示可以同时选取多个，m 表示可以换行匹配，每一行的内容独立 
reg.flags // 可以返回当前正则的所有修饰符
```

**修饰符** 

- `u` 处理大于 `\uFFFF `的 `Unicode` 字符
- `i` 表示不区分大小写
- `g` 表示可以同时选取多个
- `m` 表示可以换行匹配，每一行的内容独立
- `y` 同样是全局匹配，只不过匹配必须连在一起
- `s` dotAll，只要有点，可以用`.`代替所有字符

`u` 修饰符：含义为 `Unicode` 模式，用来正确处理大于 `\uFFFF` 的 `Unicode` 字符。也就是说，如果待匹配的字符串中可能包含有大于 `\uFFFF` 的字符，就必须加上 `u` 修饰符，才能正确处理。

```js
// 加上 u 修饰符才能让 . 字符正确识别大于 \uFFFF 的字符
/^.$/.test('🤣')   // false
/^.$/u.test('🤣')  // true

// 大括号 Unicode 字符表示法必须加上 u 修饰符
/\u{61}/.test('a')   // false
/\u{61}/u.test('a')  // true

// 有 u 修饰符，量词才能正确匹配大于 \uFFFF 的字符 
/🤣{2}/.test('🤣🤣')  // false
/🤣{2}/u.test('🤣🤣') // true
```

`RegExp.prototype.unicode` 属性表示正则是否设置了 `u` 修饰符：

```js
/🤣/.unicode   // false
/🤣/u.unicode  // true
```

`y` 修饰符，与 `g` 修饰符类似也是全局匹配；不同的是 `g` 是剩余字符中匹配即可，而 `y` 则是必须在剩余的第一个字符开始匹配才行，所以 `y` 修饰符也叫黏连修饰符：

```js
let s = 'aaa_aa_a'
let r1 = /a+/g
let r2 = /a+/y

r1.exec(s)  // ["aaa"]
r2.exec(s)  // ["aaa"]

r1.exec(s)  // ["aa"]
r2.exec(s)  // null
```

`RegExp.prototype.sticky` 属性表示是否设置了 `y` 修饰符：

```js
/abc/y.sticky  // true
```

`s` 修饰符，开启 dotAll 模式，ES2018引入，通过 `.` 表示任意字符

```js
/fall.again/.test('fall\nagain') // false
/fall.again/s.test('fall\nagain') // true
```

具名匹配，可以将捕获的字符串进行命名，通过命名进行快速查找

没有使用具名匹配

```js
let day = /(\d{4})-(\d{2})-(\d{2})/
let result = day.exec('2021-08-12')
// result[0] === '2021-08-12'
// result[1] === '2021'
// result[2] === '08'
// result[3] === '12'
```

使用具名匹配

```js
let day = /(?<year>\d{4})-(?<month>\d{2})-(?<day>\d{2})/
let result = day.exec('2021-08-12')
// result.groups { year: "2021", month: "08", day: "12" }'
```

配合结构赋值

```js
let {groups: {year, month, day}} = /(?<year>\d{4})-(?<month>\d{2})-(?<day>\d{2})/.exec('2021-08-12')
console.log(year, month, day)  // 2021 08 12
```

后行断言 `(?<=y)x`，`x` 只有在 `y` 后面才能匹配：

```js
/(?<=\$)\d+/.exec('I have $100.')  // ['100']
// 否定断言： (?<!y)x，x 只有不在 y 后面才能匹配：

/(?<!\$)\d+/.exec('I have $100.')  // ['00']
```

### 实例方法

- `reg.test()` 测试是否符合，返回`true` 或者 `false`
- `reg.dotAll()` 检测该正则是否处在 dotAll 模式
- `reg.exec()` 返回符合的字符串组成的数组。

## JSON

`JSON.stringify` 

基本用法：`JSON.stringify(value[, replacer [, space]])`

第三个参数一般没什么用，作用是指定 space 个空格的缩进而已，想让代码更好看一点，就写上多少个空格的缩进。

`0xD800` 到 `0xDFFF` 之间的码点不能单独使用，所以 `JSON.stringify()` 对单个码点进行操作，如果符合`UTF-8`标准，会返回对应的字符，如果不满足会返回对应的码点。

```js
let replacerFun = function (key, value) {
  console.log(key, value)
  if (key === 'name') { // 如果key 等于 name<直接返回 undefined
    return undefined // 返回 undefined 时，该键值对直接忽略，
  }
  return value
}
let myIntro = {
  name: 'fall',
  age: 25,
  like: 'FE'
}
JSON.stringify(myIntro, replacerFun) // {"age":25,"like":"FE"}
```

**实现对象的深拷贝**

```js
let info = {
  name:'fall'
  age: 25,
  like: 'FE'
}
function deepClone() {
  return JSON.parse(JSON.stringify(myIntro))
}
let copyMe = deepClone(myIntro)
copyMe.like = 'Front End'
console.log(myIntro, copyMe)
// { age: 25, like: 'FE' } { age: 25, like: 'Front End' }
```

> 特别注意：`JSON.stringify(Infinity)` 之后，会存储的是 null，读取后，不是 Infinity
>
> 以下情况使用 `JSON.stringify()` 可能会出错，请确保使用前没有一下情况出现。
>
> - 转换属性值中有 toJSON 方法时。方法不会被JSON.stringify 识别，但如果是 toJSON，该方法会直接被执行，并且不会返回生成的字符串。详见例1。
> - 被转换值中有 undefined、任意的函数以及 symbol 值。详见例2、例3
> - 值为 NaN 和 Infinity。详见例2、例3
> - 以 symbol 为属性键的属性
> - 包含循环引用的对象，objA引用 objB，并且 objB 引用 objA
> - 具有不可枚举的属性值时

```js
var num = Infinity
JSON.stringify(num) // "null"
```

```js
// 例1：
let author = {
  name:'fall',
  age:23,
  toJSON:function(){
    return "成功"
  }
}
JSON.stringify(author) // "\"成功\""
// 例2：
let author = {
  wife:undefined,
  money:Infinity,
  string:NaN,
  girlfriend:Symbol("she")
}
JSON.stringify(author) // "{\"money\":null,\"like\":null}"
// 例3
let nothing = [undefined,Infinity,NaN,Symbol("she")]
JSON.stringify(nothing)
// 例4
let author = Object.create(null, {
  name: { value: "fall", enumerable: true },
  age: { value: "23", enumerable: false },
})
JSON.stringify(author)
// {"name":"fall"}
```



## 内容参考：

| 作者   | 链接                                   |
| ------ | -------------------------------------- |
| Gopal1 | https://www.jianshu.com/p/b714dc8e068e |

