# 30s-code-translate-into-Chinese-
本文经过个人的翻译，翻译自《30-seconds-of-code》，原作者[Chalarangelo](https://github.com/Chalarangelo/30-seconds-of-code)，收集了有用的 JavaScript 代码片段。

*翻译的同时加入了自己的理解，难免有疏漏，请多指教*


*未完待续*

# 目录
## Array
* [arrayGCD](#arrayGCD)
* [arrayLCM](#arrayLCM)
* [arrayMax](#arrayMax)
* [arrayMin](#arrayMin)
* [chunk](#chunk)
* [compact](#compact)
* [countOccurrences](#countOccurrences)
* [deepFlatten](#deepFlatten)
* [diffrence](#diffrence)

## Array

### arrayGCD

计算一个纯数字数组的最大公约数。  
**最大公约数**是几个自然数之间最大的能被除尽，也就是没有余数的数，比如`9,36`，最大公约数是`9`。  
首先定义`Array.prototype.reduce()`方法的回调函数`gcd`,该函数采用递归的方式，可以处理两个自然数，得出最大公约数。  
然后可以使用这个回调函数，处理任意只含数字的数组了，其中的形参`a`是上次运算得出的最大公约数，形参`b`是当前正在处理的元素。  
```js
const arrayGCD = arr => {
    const gcd = (x,y) => !y ? x : gcd(y, x % y);
    return arr.reduce((a,b) => gcd(a,b));
}
// arrayGCD([1,2,3,4,5]) -> 1
// arrayGCD([9,36,3]) -> 3
```

[回到目录](#目录)

### arrayLCM

计算一个纯数字数组的最小公倍数。  
**最小公倍数**是几个数共有的倍数中除开0意外最小的数叫做这几个数的最小公倍数。  
首先定义`Array.prototype.reduce()`方法的回调函数`lcm`,该函数采用递归的方式，可以处理两个自然数，得出最小公倍数。  
然后可以使用这个回调函数，处理任意只含数字的数组了，其中的形参`a`是上次运算得出的最小公倍数，形参`b`是当前正在处理的元素。  
```js
const arrayLCM = arr => {
    const gcd = (x,y) => !y ? x : gcd(y, x % y);
    const lcm = (x,y) =>(x*y)/gcd(x,y);
    return arr.reduce((a,b) => lcm(a,b));
}
// arrayLCM([1,2,3,4,5]) -> 60
// arrayLCM([9,36,3]) -> 36
```

[回到目录](#目录)

### arrayMax

返回一个数组中最大的数值。  
使用扩展运算符展开数组，使用`Math.max()`找出最大数。  
```js
const arrayMax = arr => Math.max(...arr);
// arrayMax([10, 1, 5]) -> 10
```

[回到目录](#目录)

### arrayMin

返回一个数组中最小的数值。  
使用扩展运算符展开数组，使用`Math.min()`找出最小数。  
```js
const arrayMin = arr => Math.min(...arr);
// arrayMin([10, 1, 5]) -> 1
```

[回到目录](#目录)

### chunk

把数组切割成指定长度的小块数组。  
使用`Array.from()`方法将伪数组和可迭代对象转化数组，该方法返回一个处理好的数组实例。  
对于处理伪数组来说`Array.from()`可接受两个参数，第一个为属性为`length`的对象，第二个可选参数是一个回调函数，用来处理被传进新数组的每个元素。  
第二个参数——回调函数里的`Array.protype.slice()`可以把原数组切割成指定的长度。  
```js
const chunk = (arr,size) => 
   Array.from({length: Math.ceil(arr.length / size)},(value,index) => arr.slice(index * size, index * size + size));
//chunk([1,2,3,4,5],2) ->[[1,2],[3,4],[5]]
```

[回到目录](#目录)

### compact
去除不需要的元素。  
使用`Array.prototype.filter()`过滤掉不需要的元素（`null`,`undefined`,`""`,`false`,`NaN`）。
```js
const compact = arr => arr.filter(Boolean);     //Boolean为布尔值对象包装器的函数指针
// compact([0, 1, false, 2, '', 3, 'a', 'e'*23, NaN, 's', 34]) -> [ 1, 2, 3, 'a', 's', 34 ]
```

[回到目录](#目录)

### countOccurrences
对数组中出现相同元素个数进行计数。  
使用`Array.prototype.filter()`，每当遇到数组中指定元素，则进行计数。   
```js
const countOccurrences = (arr,value) => arr.reduce((accumulator,currentValue) => currentValue === value? accumulator + 1 : accumulator + 0, 0);    
// countOccurrences([1,1,2,1,2,3], 1) -> 3 
```

[回到目录](#目录)

### deepFlatten
对数组降维。  
使用递归。使用`Array.prototype.concat()`把空数组（`[]`）和使用扩展运算符（`...`）展开降维处理的数组。递归的降维入参数组中的每一个元素。  
```js
const deepFlatten = arr => [].concat(...arr.map(value => Array.isArray(value) ? deepFlatten(value) : value));
// deepFlatten([1,[2],[[3],4],5]) -> [1,2,3,4,5]
```

[回到目录](#目录)

### different
比较两个数组，返回一个目标数组之中没有的元素的数组。  
使用`Array.prototype.filter()`方法，把`arr`数组中有，而`target`数组中没有的元素返回出来。  
```js
const diffrence = (arr,target) => {const targetSet = new Set(target);return arr.filter(value => !targetSet.has(value))};
// difference([1,2,3], [1,2,4]) -> [3]
```
