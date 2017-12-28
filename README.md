# 30s-code-translate-into-Chinese-
本文经过个人的翻译，翻译自《30-seconds-of-code》，原作者[Chalarangelo](https://github.com/Chalarangelo/30-seconds-of-code)，收集了有用的 JavaScript 代码片段。

*翻译的同时加入了自己的理解，难免有疏漏，请多指教*


*转载请注明原作者和译者。未完待续*

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
* [difference](#difference)
* [differenceWith](#differenceWith)
* [distinceVlauesOfArray](#distinceVlauesOfArray)
* [dropElements](#dropElments)
* [dropRight](#dropRight)
* [everyNth](#everyNth)
* [filterNonUnique](#filterNonUnique)
* [flatten](#flatten)
* [flattenDepth](#flattenDepth)
* [groupBy](#groupBy)
* [head](#head)
* [initial](#initial)
* [initialize2DArray](#initialize2DArray)
* [initializeArrayWithValues](#initializeArrayWithValues)
* [initializeArrayWithRange](#initializeArrayWithRange)
* [intersection](#intersection)
* [last](#last)
* [mapObject](#mapObject)
* [nthElement](#nthElement)


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
   Array.from({length: Math.ceil(arr.length / size)},(val,index) => arr.slice(index * size, index * size + size));
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
const countOccurrences = (arr,val) => arr.reduce((accumulator,currentVal) => currentVal === val? accumulator + 1 : accumulator + 0, 0);    
// countOccurrences([1,1,2,1,2,3], 1) -> 3 
```
[回到目录](#目录)

### deepFlatten
对数组降维。  
使用递归。使用`Array.prototype.concat()`把空数组（`[]`）和使用扩展运算符（`...`）展开降维处理的数组。递归的降维入参数组中的每一个元素。  
```js
const deepFlatten = arr => [].concat(...arr.map(val => Array.isArray(val) ? deepFlatten(val) : val));
// deepFlatten([1,[2],[[3],4],5]) -> [1,2,3,4,5]
```
[回到目录](#目录)

### different
比较两个数组，返回一个目标数组之中没有的元素的数组。  
使用`Array.prototype.filter()`方法，把`arr`数组中有，而`target`数组中没有的元素返回出来。  
```js
const diffrence = (arr,target) => {const targetSet = new Set(target);return arr.filter(val => !targetSet.has(val))};
// difference([1,2,3], [1,2,4]) -> [3]
```
[回到目录](#目录)

### differenceWith
从一个数组过滤出比较函数没有返回`true`的所有值，作为数组返回。  
使用`Array.prototype.find()`和`Array.prototype.filter()`方法找到合适的值。  
```js
const differenceWith = (arr, val, comp) => arr.filer(arrElement => !val.find(valElment => copm(arrElement, valElment)))
// 从arr数组中找出与val数组中使用四舍五入比较不相等的元素。
// differenceWith([1, 1.2, 1.5, 3], [1.9, 3], (a,b) => Math.round(a) == Math.round(b)) -> [1, 1.2]
```
[回到目录](#目录)

### distinctValuesOfArray
返回一个去除重复元素的新数组。  
使用了ES6的`Set`和扩展语法（`...`）去除重复元素.  
```js
const distinctValuesOfArray = arr => [...new Set(arr)];
// distinctValuesOfArray([1,2,2,3,4,4,5]) -> [1,2,3,4,5]
```
[回到目录](#目录)

### dropElements
去除掉一个数组内不满足条件函数的所有元素，并返回剩下的元素。  
使用`Array.prototype.silce()`来切掉原数组上不满足条件的元素。  
```js
const dropElements = (arr,fuc) => {
    while(arr.length > 0 && !func(arr[0])) {
        arr = arr.silce(1);
    } 
    return arr;
};
// dropElements([1, 2, 3, 4], n => n >= 3) -> [3,4]
```
[回到目录](#目录)

### dropRight
返回一个移除`n`个右边元素的新数组。  
使用`Array.prototype.silce()`方法来切除数组右边指定长度，默认切掉一个。  
当`n = 0`时不做切除操作。  
```js
const dropRight = (arr, n = 1) => {
    if(n === 0) return arr;
    return arr.slice(0,-n);
}
//我加入了切掉0个数组的情况
//dropRight([1,2,3], 0) -> []
//dropRight([1,2,3]) -> [1,2]
//dropRight([1,2,3], 2) -> [1]
//dropRight([1,2,3], 42) -> []
```
[回到目录](#目录)

### everyNth
返回数组内的N的倍数的元素。  
使用`Array.prototype.filter()`方法包含给定数组的每一个N的倍数的元素的新数组。  
```js
const everyNth = (arr,nth) => arr.filter((element,index) => index % nth === nth - 1);
// everyNth([1,2,3,4,5,6], 2) -> [ 2, 4, 6 ]
```
[回到目录](#目录)

### filterNonUnique
过滤掉数组内所有非唯一元素，返回一个没有过重复元素的新数组。  
使用`Array.prototype.filter()`方法返回一个只有唯一值的新数组。  
```js
const filterNonUnique = arr => arr.filter(element => arr.indexOf(element) === arr.lastIndexOf(element));
// filterNonUnique([1,2,2,3,4,4,5]) -> [1,3,5]
```
[回到目录](#目录)

### flatten
二维数组降维。   
使用扩展运算符给二维数组展开为一维数组。这是一种浅降维方法，上文有深度降维法[deepFlatten](#deepFlatten)。
```js
const flatten = arr => [].concat(...arr);
// flatten([1,[2],3,4]) -> [1,2,3,4]
```
[回到目录](#目录)

### flattenDepth
用给定的深度使数组降维。   
使用递归，降低深度以1为每层单位。   
使用`Array.prototype.reduce()`和`Array.prototype.concat()`方法来合并元素或数组。   
基本情况下，深度层数等于1时不进行降维。省略第二个元素情况下，深度为1。   
```js
const flattenDepth = (arr,depth = 1) =>
    depth != 1? arr.reduce((a, v) => a.concat(Array.isArray(v) ? flattenDepth(v, depth - 1) : v), [])
    : : arr.reduce((a, v) => a.concat(v), []);
// flattenDepth([1,[2],[[[3],4],5]], 2) -> [1,2,[3],4,5]    
```
[回到目录](#目录)

### groupBy
基于给定函数，给数组内的元素分组。   
使用`Array.prototype.map()`方法，基于给定的函数或者属性来处理数组内的每个值。  
使用`Array.prototype.reduce()`方法，把处理好的值放到创建好的对象里面，该对象的键名为`map()`处理后的值，键值为原数组的元素经过分组后的数组。     
```js
const groupBy = (arr,func) => 
    arr.map(typeof func === 'function'? func : val => val[func]) //判断func是函数还是属性名
    .reduce((acc,val,index) => { acc[val] = (acc[val] || []).concat(arr[index]); return acc; }, {});
// groupBy([6.1, 4.2, 6.3], Math.floor) -> {4: [4.2], 6: [6.1, 6.3]}
// groupBy(['one', 'two', 'three'], 'length') -> {3: ['one', 'two'], 5: ['three']}
```
[回到目录](#目录)

### head
返回一个列表的头元素。    
使用`arr[0]`返回一个传入数组的第一个元素。    
```js
const head = arr => arr[0];
// head([1,2,3]) -> 1
```
[回到目录](#目录)

### initial
返回一个数组除了最后一个元素的其他所有元素。    
使用`Array.prototype.slice(0,-1)`方法来实现。    
```js
const initial = arr => arr.slice(0,-1);
// initial([1,2,3]) -> [1,2]
```
[回到目录](#目录)

### initialize2DArray
根据给定的元素长度，元素个数和元素值生成二维数组。       
使用`Array.prototype.map()`方法生成`h`个长度为`w`、值为`val`的新数组，`val`默认值为`null`。    
```js
const initialize2DArray = (w,h,val = null) => new Array(h).fill().map(() => new Array(w).fill(val));    // 为方便阅读加入了new操作符
// initializeArrayWithRange(2, 2, 0) -> [[0,0], [0,0]]
```
[回到目录](#目录)

### initializeArrayWithRange
生成一个包含`start`和`end`且指定范围的新数组。    
使用`Array((end + 1) - start)`计算出想要的新数组长度，`Array.prototype.map`方法给新数组填充想要的范围内的值。      
可以传入指定的`start`代替默认值。        
```js
const initializeArrayWithRange = (end,start = 0) => 
    Array.from({ length:(end + 1) - start }).map((val,index) => index + start);
// initializeArrayWithRange(5) -> [0,1,2,3,4,5]
// initializeArrayWithRange(7, 3) -> [3,4,5,6,7]
```
[回到目录](#目录)

### initializeArrayWithValues
生成指定长度和值的数组。    
用构造函数`new Array()`生成指定长度的空数组，再用`Array.prototype.fill()`方法填充指定的值。默认填充值为0。     
```js
const initializeArrayWithValues = (n,value = 0) => new Array(n).fill(value);
// initializeArrayWithValues(5, 2) -> [2,2,2,2,2]
```
[回到目录](#目录)
### intersection
返回两个数组都有的元素集合。      
创建`b`的`Set`对象，挑选出`a`数组内跟`b`数组所有相同的元素。       
```js
const intersection = (a,b) => {const bSet = new Set(b); return a.filter(x => bSet.has(x));};
// intersection([1,2,3], [4,3,2]) -> [2,3]
```
[回到目录](#目录)

###  last
返回数组最后一个元素。     
```js
const last = arr => arr[arr.length - 1];
// last([1,2,3]) -> 3
```
[回到目录](#目录)

### mapObject
使用给定函数把给定数组处理成一个特殊对象，这个对象的键名为数组的元素，键值为函数处理后的值。          
使用内部匿名函数来申明未定义的内存空间，用闭包来存储返回值。使用一个新数组以在其数据集上的函数映射一个数组和一个逗号操作符返回第二步，而无需从一个上下文转移到另一个上下文（由于闭包和操作顺序）。    
```js
const mapObject = (arr,func) =>
    (a => a = [arr, arr.map(fn)], a[0],reduce((acc,val,i) => (acc[val] = a[1][i],acc, {})))();
```
```js
const squareIt = arr => mapObject(arr, a => a*a);
squareIt([1,2,3]) // { 1: 1, 2: 4, 3: 9 }
```
[回到目录](#目录)

### nthElement
返回数组的第N个元素。        
使用`Array.prototype.slice`方法取得数组包含第N个元素的位置，如索引的元素超过了数组范围则返回空数组。         
省略第二个参数时，就返回数组的第一个元素。       
```js
const nthElement = (arr,n = 0) => (n > 0 ? arr.slice(n, n + 1) : arr.slice(n))[0];
nthElement(['a','b','c'],1) // 'b'
nthElement(['a','b','b'],-3) // 'a'
```
[回到目录](#目录)

