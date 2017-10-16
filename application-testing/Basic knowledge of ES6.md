# ES6基础语法

## 1. 变量声明，let 和 const

* 如果声明的变量，在将来会改变，使用let，如果不会改变，用const。
* 在let和const之间，建议优先使用const。
* 所有的函数都应该设置为常量。

```
let x = 'hello world';
if (true) {
    x = 'hello';
}

const a = 1;
const b = 2;
const c = 3;
```

## 2. 字符串

* 静态字符串一律使用单引号，不使用双引号。动态字符串使用反引号。

```
// bad
const a = "foobar";
const b = 'foo' + a + 'bar';

// good
const a = 'foobar';
const b = `foo${a}bar`;
const c = 'foobar';
```

* includes()：返回布尔值，表示是否找到了参数字符串。
* startsWith()：返回布尔值，表示参数字符串是否在原字符串的头部。
* endsWith()：返回布尔值，表示参数字符串是否在原字符串的尾部。

```
const s = 'Hello world!';

s.includes('o') // true
s.startsWith('Hello') // true
s.endsWith('!') // true
```

## 3. 数组

* 数组

```
// bad
const a = [1, 2, 3, 4,];
const b = [
    1,
    2,
    3,
    4
]

// good
const a = [1, 2, 3, 4];
const b = [
    1,
    2,
    3,
    4,
]
```

* 操作数组

```
const arr = [1, 3, 4];

// 获取数组长度
arr.length // 3
// 数组尾部添加元素
arr.push(5)
// 移除数组尾部元素
arr.pop();
// 数组开头添加元素
arr.unshift(9);
// 移除数组开头元素
arr.unshift();
```

* 扩展运算符

```
const arr = [1, 2, 3, 4];

const arr1 = [...arr]; // [1, 2, 3, 4]

const arr2 = [7, 8, ...arr]; // [7, 8, 1, 2, 3, 4]

const arr3 = [...arr1, ...arr2]; // [1, 2, 3, 4, 7, 8, 1, 2, 3, 4];
```

* 遍历数组的值

```
for (const item of [1, 2, 3, 4]) {
    console.log(item);
}
// 1
// 2
// 3
// 4
```

* filter方法

```
[1, 2, 3, 4, 5].filter(x => x > 3); // [4, 5]

[1, 2, 3, 4, 5].filter(x => x * 2 < 5); // [1, 2]
```

* map方法

```
[1, 2, 3, 4, 5].map(x => x * 3); // [ 3, 6, 9, 12, 15 ]
```



## 4. 对象

* 单行定义的对象，最后一个成员不以逗号结尾。多行定义的对象，最后一个成员以逗号结尾。
```
// bad
const a = { k1: v1, k2: v2, };
const b = {
    k1: v1,
    k2: v2
};

// good
const a = { k1: v1, k2: v2 };
const b = {
    k1: v1,
    k2: v2,
};
```

* 遍历对象

```
const obj = {a: 1, b: 2};

// 遍历对象的key和vaule
for (const item of Reflect.ownKeys(obj)) {
    console.log(item); // key
    console.log(obj[itme]); // value
}
// a
// 1
// b
// 2
```

## 5. 解构赋值

* 使用数组和对象成员对变量赋值时，优先使用解构赋值。
```
const arr = [1, 2, 3, 4];

// bad
const first = arr[0];
const second = arr[1];

// good
const [first, second] = arr;
```

```
const obj = {
    a: 'apple',
    b: 'banana',
}

// bad
const a = obj['a'];
const b = obj['b'];

// good
const {a, b: abc} = obj;
```

## 6. 函数

* 立即执行函数可以写成箭头函数的形式。
```
(() => {
    console.log('Welcome to the Internet.');
})();
```

* 那些需要使用函数表达式的场合，尽量用箭头函数代替。因为这样更简洁，而且绑定了this。

```
// bad
[1, 2, 3].map(function (x) {
    return x * x;
});

// good
[1, 2, 3].map((x) => {
    return x * x;
});

// best
[1, 2, 3].map(x => x * x);
```

* rest 参数（形式为...变量名），用于获取函数的多余参数

```
const toArr = (...values) => values; // [2, 5, 3]

toArr(2, 5, 3); // [2, 5, 3]
```

```
const func = (str, ...items) => {
    // str >> 'a'
    // items >> [1, 2, 3]
}

func('a', 1, 2, 3)
```

* 注意，rest 参数之后不能再有其他参数（即只能是最后一个参数），否则会报错。

```
// 报错
const = f => (a, ...b, c) {
    // ...
}
```

* 函数的参数设置默认值

```
const log = (x, y = 'World') => console.log(x, y);

log('Hello') // Hello World
log('Hello', 'China') // Hello China
log('Hello', '') // Hello
```

## 7. 控制语句

* 逻辑判断

```
    'abc' === 'abc'; // true
    123 === 123; // true
    '123' === 123; // false
    '123' !== 123; // true
    
    [] === []; // false
    {} === {}; // false
    
    const obj = {};
    obj === obj; // true
    
    const arr = [];
    arr === arr; // true
    
    1 > 5; // false
    1 >= 5; // false
    1 < 5; // true
    1 <= 5; // true
    
    true === true // true
    false === false // true
    true === false // false
    true === !false // true
    !true === false // true
    
    true && true; // true
    true && false; // false
    false && false; // false
    true || true; // true   
    true || false; // true
    false || false; // false
```

* 控制语句

```
if (true) {

}

if (true) {

} else {

}

if (flase) {

} else if (true) {

} else if (true) {

} else {

}
```

* 循环语句

```
let i = 5;
while (i > 0) {
    console.log(i);
    i--; // i = i - 1;
}
// 5
// 4
// 3
// 2
// 1
```

```
for (let i = 0; i < 5; i++) {
    console.log(i);
}
// 0
// 1
// 2
// 3
// 4
```



## 8. 正则表达式

* 请自行查询资料

    [w3school RegExp](http://www.w3school.com.cn/jsref/jsref_obj_regexp.asp)

## * 9. Map数据结构

* 注意区分Object和Map，只有模拟现实世界的实体对象时，才使用Object。如果只是需要key: value的数据结构，使用Map结构。因为Map有内建的遍历机制。

```
let map = new Map(arr);

for (let key of map.keys()) {
    console.log(key);
}

for (let value of map.values()) {
    console.log(value);
}

for (let item of map.entries()) {
    console.log(item[0], item[1]);
}
```

```
const map = new Map();

map.set(1, 'aaa').set(1, 'bbb');

map.get(1) 
```

* size属性
    
    size属性返回 Map 结构的成员总数。

```
const map = new Map();
map.set('foo', true);
map.set('bar', false);

map.size // 2
```

* set(key, value)
    
    set方法设置键名key对应的键值为value，然后返回整个 Map 结构。如果key已经有值，则键值会被更新，否则就新生成该键。
```
const m = new Map();

m.set('edition', 6)        // 键是字符串
m.set(262, 'standard')     // 键是数值
m.set(undefined, 'nah')    // 键是 undefined

let map = new Map()
    .set(1, 'a')
    .set(2, 'b')
    .set(3, 'c');
```

* get(key)

    get方法读取key对应的键值，如果找不到key，返回undefined。
    
```
const m = new Map();

const hello = function() {console.log('hello');};
m.set(hello, 'Hello ES6!') // 键是函数

m.get(hello)  // Hello ES6!
```

* has(key)

    has方法返回一个布尔值，表示某个键是否在当前 Map 对象之中。
    
```
const m = new Map();

m.set('edition', 6);
m.set(262, 'standard');
m.set(undefined, 'nah');

m.has('edition')     // true
m.has('years')       // false
m.has(262)           // true
m.has(undefined)     // true
```

* delete(key)

    delete方法删除某个键，返回true。如果删除失败，返回false。

```
const m = new Map();
m.set(undefined, 'nah');
m.has(undefined)     // true

m.delete(undefined)
m.has(undefined)       // false
```

* clear()

    clear方法清除所有成员，没有返回值。
    
```
let map = new Map();
map.set('foo', true);
map.set('bar', false);

map.size // 2
map.clear()
map.size // 0
```

* 遍历方法

    Map 结构原生提供三个遍历器生成函数和一个遍历方法。

    * keys()：返回键名的遍历器。
    * values()：返回键值的遍历器。
    * entries()：返回所有成员的遍历器。
    * forEach()：遍历 Map 的所有成员。

    需要特别注意的是，Map 的遍历顺序就是插入顺序。
```
const map = new Map([
    ['F', 'no'],
    ['T',  'yes'],
]);

for (let key of map.keys()) {
    console.log(key);
}
// "F"
// "T"

for (let value of map.values()) {
    console.log(value);
}
// "no"
// "yes"

for (let item of map.entries()) {
    console.log(item[0], item[1]);
}
// "F" "no"
// "T" "yes"

// 或者
for (let [key, value] of map.entries()) {
    console.log(key, value);
}
// "F" "no"
// "T" "yes"

// 等同于使用map.entries()
for (let [key, value] of map) {
    console.log(key, value);
}
// "F" "no"
// "T" "yes"
```

## * 10. Set数据结构

* Set类似于数组，但是成员的值都是唯一的，没有重复的值。

* Set 本身是一个构造函数，用来生成 Set 数据结构。
```
const s = new Set();

[2, 3, 5, 4, 5, 2, 2].forEach(x => s.add(x));

for (let i of s) {
    console.log(i);
}
// 2 
// 3 
// 5 
// 4
```

```
const set = new Set([1, 2, 3, 4, 4]);

for (let i of s) {
  console.log(i);
}
// 1
// 2 
// 3 
// 4
```

* 操作方法

    * add(value)：添加某个值，返回Set结构本身。
    * delete(value)：删除某个值，返回一个布尔值，表示删除是否成功。
    * has(value)：返回一个布尔值，表示该值是否为Set的成员。
    * clear()：清除所有成员，没有返回值。
```
s.add(1).add(2).add(2);
// 注意2被加入了两次

s.size // 2

s.has(1) // true
s.has(2) // true
s.has(3) // false

s.delete(2);
s.has(2) // false

s.clear();
s.size // 0
```

* 遍历操作

    * keys()：返回键名的遍历器
    * values()：返回键值的遍历器
    * entries()：返回键值对的遍历器
    * forEach()：使用回调函数遍历每个成员
```
let set = new Set(['red', 'green', 'blue']);

for (let item of set.keys()) {
    console.log(item);
}
// red
// green
// blue

for (let item of set.values()) {
    console.log(item);
}
// red
// green
// blue

for (let item of set.entries()) {
    console.log(item);
}
// ["red", "red"]
// ["green", "green"]
// ["blue", "blue"]
```

















