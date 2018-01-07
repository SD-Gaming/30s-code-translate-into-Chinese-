# 30s-code-translate-into-Chinese-
本文经过个人的翻译，翻译自《30-seconds-of-code》，原作者[Chalarangelo](https://github.com/Chalarangelo/30-seconds-of-code)，收集了有用的 JavaScript 代码片段。

*翻译的同时加入了自己的理解，难免有疏漏，请多指教*


*转载请注明原作者和译者。未完待续*

# 目录
## 📚 Array
* [arrayGCD](#arraygcd)
* [arrayLCM](#arraylcm)
* [arrayMax](#arraymax)
* [arrayMin](#arraymin)
* [chunk](#chunk)
* [compact](#compact)
* [countOccurrences](#countoccurrences)
* [deepFlatten](#deepflatten)
* [difference](#difference)
* [differenceWith](#differencewith)
* [distinctValuesOfArray](#distinctvaluesofarray)
* [dropElements](#dropelements)
* [dropRight](#dropright)
* [everyNth](#everynth)
* [filterNonUnique](#filternonunique)
* [flatten](#flatten)
* [flattenDepth](#flattendepth)
* [groupBy](#groupby)
* [head](#head)
* [initial](#initial)
* [indexOfAll](#indexofall)
* [initialize2DArray](#initialize2darray)
* [initializeArrayWithValues](#initializearraywithvalues)
* [initializeArrayWithRange](#initializearraywithrange)
* [intersection](#intersection)
* [isSorted](#issorted)
* [join](#join)
* [last](#last)
* [mapObject](#mapobject)
* [nthElement](#nthelement)
* [pick](#pick)
* [pull](#pull)
* [pullAtIndex](#pullatindex)
* [pullAtValue](#pullatvalue)
* [quickSort](#quicksort)
* [reducedFilter](#reducedfilter)
* [sample](#sample)
* [shuttle](#shuttle)
* [sampleSize](#samplesize)
* [similarity](#similarity)
* [sortedIndex](#sortedindex)
* [symmetricDifference](#symmetricdifference)
* [tail](#tail)
* [take](#take)
* [takeRight](#takeright)
* [union](#union)
* [without](#without)
* [zip](#zip)
* [zipObject](#zipobject)

## 🌐 Browser


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
```

<details>
    <summary>Examples</summary>
    
```js
chunk([1,2,3,4,5],2) // [[1,2],[3,4],[5]]
```

</details>

<br>[回到目录](#目录)

### compact
去除不需要的元素。  
使用`Array.prototype.filter()`过滤掉不需要的元素（`null`,`undefined`,`""`,`false`,`NaN`）。
```js
const compact = arr => arr.filter(Boolean);     //Boolean为布尔值对象包装器的函数指针
```

<details>
    <summary>Examples</summary>
    
```js
compact([0, 1, false, 2, '', 3, 'a', 'e'*23, NaN, 's', 34]);   // [ 1, 2, 3, 'a', 's', 34 ]
```

</details>

<br>[回到目录](#目录)

### countOccurrences
对数组中出现相同元素个数进行计数。  
使用`Array.prototype.filter()`，每当遇到数组中指定元素，则进行计数。   
```js
const countOccurrences = (arr,val) => arr.reduce((accumulator,currentVal) => currentVal === val? accumulator + 1 : accumulator + 0, 0); 
```

<details>
    <summary>Examples</summary>
    
```js
countOccurrences([1,1,2,1,2,3], 1);   // 3
```

</details>

<br>[回到目录](#目录)

### deepFlatten
对数组降维。  
使用递归。使用`Array.prototype.concat()`把空数组（`[]`）和使用扩展运算符（`...`）展开降维处理的数组。递归的降维入参数组中的每一个元素。  
```js
const deepFlatten = arr => [].concat(...arr.map(val => Array.isArray(val) ? deepFlatten(val) : val));
```

<details>
    <summary>Examples</summary>
    
```js
deepFlatten([1, [2], [[3], 4], 5]); // [1,2,3,4,5]
```

</details>

<br>[回到目录](#目录)

### difference
比较两个数组，返回一个目标数组之中没有的元素的数组。  
使用`Array.prototype.filter()`方法，把`arr`数组中有，而`target`数组中没有的元素返回出来。  
```js
const difference = (arr,target) => {const targetSet = new Set(target);return arr.filter(val => !targetSet.has(val))};
```

<details>
    <summary>Examples</summary>
    
```js
difference([1, 2, 3], [1, 2, 4]); // [3]
```

</details>

<br>[回到目录](#目录)

### differenceWith
从一个数组过滤出比较函数没有返回`true`的所有值，作为数组返回。  
使用`Array.prototype.find()`和`Array.prototype.filter()`方法找到合适的值。  
```js
const differenceWith = (arr, val, comp) => arr.filer(arrElement => !val.find(valElment => copm(arrElement, valElment)))
// 从arr数组中找出与val数组中使用四舍五入比较不相等的元素。
```

<details>
    <summary>Examples</summary>
    
```js
differenceWith([1, 1.2, 1.5, 3, 0], [1.9, 3, 0], (a, b) => Math.round(a) === Math.round(b)); // [1, 1.2]
```

</details>

<br>[回到目录](#目录)

### distinctValuesOfArray
返回一个去除重复元素的新数组。  
使用了ES6的`Set`和扩展语法（`...`）去除重复元素.  
```js
const distinctValuesOfArray = arr => [...new Set(arr)];
```

<details>
<summary>Examples</summary>

```js
distinctValuesOfArray([1, 2, 2, 3, 4, 4, 5]); // [1,2,3,4,5]
```

</details>
<br>[回到目录](#目录)

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
```
<details>
<summary>Examples</summary>

```js
dropElements([1, 2, 3, 4], n => n >= 3); // [3,4]
```

</details>

<br>[回到目录](#目录)

### dropRight
返回一个移除`n`个右边元素的新数组。  
使用`Array.prototype.silce()`方法来切除数组右边指定长度，默认切掉一个。  
当`n = 0`时不做切除操作。  
```js
const dropRight = (arr, n = 1) => {
    if(n === 0) return arr;
    return arr.slice(0,-n);
}
```

<details>
<summary>Examples</summary>

```js
//我加入了切掉0个数组的情况
dropRight([1,2,3], 0) -> []
dropRight([1, 2, 3]); // [1,2]
dropRight([1, 2, 3], 2); // [1]
dropRight([1, 2, 3], 42); // []
```

</details>


<br>[回到目录](#目录)

### everyNth
返回数组内的N的倍数的元素。  
使用`Array.prototype.filter()`方法包含给定数组的每一个N的倍数的元素的新数组。  
```js
const everyNth = (arr,nth) => arr.filter((element,index) => index % nth === nth - 1);
```

<details>
<summary>Examples</summary>

```js
everyNth([1, 2, 3, 4, 5, 6], 2); // [ 2, 4, 6 ]
```

</details>

<br>[回到目录](#目录)

### filterNonUnique
过滤掉数组内所有非唯一元素，返回一个没有过重复元素的新数组。  
使用`Array.prototype.filter()`方法返回一个只有唯一值的新数组。  
```js
const filterNonUnique = arr => arr.filter(element => arr.indexOf(element) === arr.lastIndexOf(element));
```
<details>
<summary>Examples</summary>

```js
filterNonUnique([1, 2, 2, 3, 4, 4, 5]); // [1,3,5]
```

</details>

<br>[回到目录](#目录)

### flatten
二维数组降维。   
使用扩展运算符给二维数组展开为一维数组。这是一种浅降维方法，上文有深度降维法[deepFlatten](#deepFlatten)。
```js
const flatten = arr => [].concat(...arr);
```

<details>
<summary>Examples</summary>

```js
flatten([1, [2], 3, 4]); // [1,2,3,4]
```

</details>

<br>[回到目录](#目录)

### flattenDepth
用给定的深度使数组降维。   
使用递归，降低深度以1为每层单位。   
使用`Array.prototype.reduce()`和`Array.prototype.concat()`方法来合并元素或数组。   
基本情况下，深度层数等于1时不进行降维。省略第二个元素情况下，深度为1。   
```js
const flattenDepth = (arr,depth = 1) =>
    depth != 1? arr.reduce((a, v) => a.concat(Array.isArray(v) ? flattenDepth(v, depth - 1) : v), [])
    : : arr.reduce((a, v) => a.concat(v), []);
```
<details>
<summary>Examples</summary>

```js
flattenDepth([1, [2], 3, 4]); // [1,2,3,4]
```

</details>

<br>[回到目录](#目录)

### groupBy
基于给定函数，给数组内的元素分组。   
使用`Array.prototype.map()`方法，基于给定的函数或者属性来处理数组内的每个值。  
使用`Array.prototype.reduce()`方法，把处理好的值放到创建好的对象里面，该对象的键名为`map()`处理后的值，键值为原数组的元素经过分组后的数组。     
```js
const groupBy = (arr,func) => 
    arr.map(typeof func === 'function'? func : val => val[func]) //判断func是函数还是属性名
    .reduce((acc,val,index) => { acc[val] = (acc[val] || []).concat(arr[index]); return acc; }, {});
```

<details>
<summary>Examples</summary>

```js
groupBy([6.1, 4.2, 6.3], Math.floor); // {4: [4.2], 6: [6.1, 6.3]}
groupBy(['one', 'two', 'three'], 'length'); // {3: ['one', 'two'], 5: ['three']}
```

</details>

<br>[回到目录](#目录)

### head
返回一个列表的头元素。    
使用`arr[0]`返回一个传入数组的第一个元素。    
```js
const head = arr => arr[0];
```

<details>
<summary>Examples</summary>

```js
head([1, 2, 3]); // 1
```

</details>

<br>[回到目录](#目录)

### initial
返回一个数组除了最后一个元素的其他所有元素。    
使用`Array.prototype.slice(0,-1)`方法来实现。    
```js
const initial = arr => arr.slice(0,-1);
```
<details>
<summary>Examples</summary>

```js
initial([1, 2, 3]); // [1,2]
```

</details>
<br>[回到目录](#目录)

### indexOfAll
返回数组中包含指定值的索引。如果指定值不存在则返回`[-1]`。
使用 `Array.prototype.forEach()` 方法来遍历所有元素， 使用 `Array.push()` 方法来把找到的索引值储存起来。
```js
const indexOfAll = (arr, val) => {
  const indices = [];
  arr.forEach((el, i) => el === val && indices.push(i));
  return indices.length ? indices : [-1];
};
```

<details>
<summary>Examples</summary>

```js
indexOfAll([1, 2, 3, 1, 2, 3], 1); // [0,3]
indexOfAll([1, 2, 3], 4); // [-1]
```

</details>

<br>[回到目录](#目录)

### initialize2DArray
根据给定的元素长度，元素个数和元素值生成二维数组。       
使用`Array.prototype.map()`方法生成`h`个长度为`w`、值为`val`的新数组，`val`默认值为`null`。    
```js
const initialize2DArray = (w,h,val = null) => new Array(h).fill().map(() => new Array(w).fill(val));    // 为方便阅读加入了new操作符
```

<details>
<summary>Examples</summary>

```js
initialize2DArray(2, 2, 0); // [[0,0], [0,0]]
```

</details>

<br>[回到目录](#目录)

### initializeArrayWithRange
生成一个包含`start`和`end`且指定范围的新数组。    
使用`Array((end + 1) - start)`计算出想要的新数组长度，`Array.prototype.map`方法给新数组填充想要的范围内的值。      
可以传入指定的`start`代替默认值。        
```js
const initializeArrayWithRange = (end,start = 0) => 
    Array.from({ length:(end + 1) - start }).map((val,index) => index + start);
```

<details>
<summary>Examples</summary>

```js
initializeArrayWithRange(5); // [0,1,2,3,4,5]
initializeArrayWithRange(7, 3); // [3,4,5,6,7]
initializeArrayWithRange(9, 0, 2); // [0,2,4,6,8]
```

</details>

<br>[回到目录](#目录)

### initializeArrayWithValues
生成指定长度和值的数组。    
用构造函数`new Array()`生成指定长度的空数组，再用`Array.prototype.fill()`方法填充指定的值。默认填充值为0。     
```js
const initializeArrayWithValues = (n,value = 0) => new Array(n).fill(value);
```

<details>
<summary>Examples</summary>

```js
initializeArrayWithValues(5, 2); // [2,2,2,2,2]
```

</details>

<br>[回到目录](#目录)

### intersection
返回两个数组都有的元素集合。      
创建`b`的`Set`对象，挑选出`a`数组内跟`b`数组所有相同的元素。       
```js
const intersection = (a,b) => {const bSet = new Set(b); return a.filter(x => bSet.has(x));};
```

<details>
<summary>Examples</summary>

```js
intersection([1, 2, 3], [4, 3, 2]); // [2,3]
```

</details>

<br>[回到目录](#目录)


### isSorted

如果数组为升序排列返回`1`， 降序排列返回`-1`，除此之外返回`0`。
计算出第一、第二个元素的排序方式。
使用 `Object.prototype》entries()`方法遍历数组对象，比较它的键值对数组。    
当真个数组顺序有变则返回`0`，或者遍历完成后顺序没有变化就返回数组顺序的代号。   
```js
const isSorted = arr => {
  const direction = arr[0] > arr[1] ? -1 : 1;
  for (let [i, val] of arr.entries())
    if (i === arr.length - 1) return direction;
    else if ((val - arr[i + 1]) * direction > 0) return 0;
};
```

<details>
<summary>Examples</summary>

```js
isSorted([0, 1, 2, 2]); // 1
isSorted([4, 3, 2]); // -1
isSorted([4, 3, 5]); // 0
```

</details>

<br>[回到目录](#目录)

### join
连接数组的所有元素成为一个字符串，并返回它。   
使用`Array.prototype.reduce()`方法连接数组元素成字符串。省略第二个参数则使用默认的分隔符`,`，省略第三个参数则使用同第二个参数相同的值。   
```js
const join = (arr, seprator = ',',  end = seprator) => 
    arr.reduce(
    (acc,val,i) =>
        i === arr.length -2
        ? acc + val + end
        : i === arr.length - 1 ? acc + val : acc + val + seprator
    ,''
);
```

<details>
    <summary>Examples</summary>
    
```js
join(['pen', 'pineapple', 'apple', 'pen'], ',', '&'); // "pen,pineapple,apple&pen"
join(['pen', 'pineapple', 'apple', 'pen'], ','); // "pen,pineapple,apple,pen"
join(['pen', 'pineapple', 'apple', 'pen']); // "pen,pineapple,apple,pen"
```

</details>

<br>[回到目录](#目录)

###  last
返回数组最后一个元素。     
```js
const last = arr => arr[arr.length - 1];
```

<details>
<summary>Examples</summary>

```js
last([1, 2, 3]); // 3
```

</details>

<br>[回到目录](#目录)

### mapObject
使用给定函数把给定数组处理成一个特殊对象，这个对象的键名为数组的元素，键值为函数处理后的值。          
使用内部匿名函数来申明未定义的内存空间，用闭包来存储返回值。使用一个新数组以在其数据集上的函数映射一个数组和一个逗号操作符返回第二步，而无需从一个上下文转移到另一个上下文（由于闭包和操作顺序）。    
```js
const mapObject = (arr,func) =>
    (a => a = [arr, arr.map(fn)], a[0],reduce((acc,val,i) => (acc[val] = a[1][i], acc), {})))();
```
```js
const squareIt = arr => mapObject(arr, a => a*a);
```

<details>
<summary>Examples</summary>

```js
const squareIt = arr => mapObject(arr, a => a * a);
squareIt([1, 2, 3]); // { 1: 1, 2: 4, 3: 9 }
```

</details>

<br>[回到目录](#目录)

### nthElement
返回数组的第N个元素。        
使用`Array.prototype.slice`方法取得数组包含第N个元素的位置，如索引的元素超过了数组范围则返回空数组。         
省略第二个参数时，就返回数组的第一个元素。       
```js
const nthElement = (arr,n = 0) => (n > 0 ? arr.slice(n, n + 1) : arr.slice(n))[0];
```

<details>
<summary>Examples</summary>

```js
nthElement(['a', 'b', 'c'], 1); // 'b'
nthElement(['a', 'b', 'b'], -3); // 'a'
```

</details>

<br>[回到目录](#目录)

### pick
从给定的对象中，找出与给定键名相同的键值对。    
使用`Array.prototype.slice`方法将需要筛选/过滤的键转换为具有指定键和值的对象，如果给定键名存在于给定的对象中的话。
```js
const pick = (obj,arr) =>
    arr.reduce((acc, cur) => (cur in obj && (acc[cur] = obj[cur])), acc), {});
```

<details>
<summary>Examples</summary>

```js
pick({ a: 1, b: '2', c: 3 }, ['a', 'c']); // { 'a': 1, 'c': 3 }
```

</details>

<br>[回到目录](#目录)

### pull
过滤掉指定的元素，把原数组进行异变。      
使用`Array.prototype.filter()`和`Array.prototype.includes()`方法去掉不需要的元素。    
使用`Array.length = 0`把原数组长度重置为0， 再使用`Array.prototype.push()`把需要的元素放入新数组。    
```js
const pull = (arr,...args) => {
    let argState = Array.isArray(args[0])? args[0] : args;
    let pulled = arr.filter((val,i) => !argState.includes(v));
    arr.length = 0;
    pulled.forEach(val => arr.push(val));
```

<details>
<summary>Examples</summary>

```js
let myArray = ['a', 'b', 'c', 'a', 'b', 'c'];
pull(myArray, 'a', 'c'); // myArray = [ 'b', 'b' ]
```

</details>

<br>[回到目录](#目录)

### pullAtIndex
移除数组指定索引的元素，异化原数组。   
使用`Array.prototype.filter()`和`Array.prototype.includes()`方法移除掉不需要的元素。    
使用`Array.length = 0`把原数组长度重置为0， 再使用`Array.prototype.push()`把需要的元素放入新数组，返回移除的元素。     
```js
const pullAtIndex = (arr, pullArr) => {
  let removed = [];
  let pulled = arr
    .map((v, i) => (pullArr.includes(i) ? removed.push(v) : v))
    .filter((v, i) => !pullArr.includes(i));
  arr.length = 0;
  pulled.forEach(v => arr.push(v));
  return removed;
};
```

<details>
<summary>Examples</summary>

```js
let myArray = ['a', 'b', 'c', 'd'];
let pulled = pullAtIndex(myArray, [1, 3]); // myArray = [ 'a', 'c' ] , pulled = [ 'b', 'd' ]
```

</details>

<br>[回到目录](#目录)

### pullAtValue
移除数组中与指定值相同的元素，异化原数组并返回移除的元素。   
使用`Array.prototype.filter()`和`Array.prototype.includes()`方法移除掉不需要的元素。   
使用`Array.length = 0`把原数组长度重置为0， 再使用`Array.prototype.push()`把需要的元素放入新数组，返回移除的元素。   
```js
const pullAtIndex = (arr, pullArr) => {
  let removed = [];
  let pulled = arr
    .map((v, i) => (pullArr.includes(i) ? removed.push(v) : v))
    .filter((v, i) => !pullArr.includes(i));
  arr.length = 0;
  pulled.forEach(v => arr.push(v));
  return removed;
};
```

<details>
<summary>Examples</summary>

```js
let myArray = ['a', 'b', 'c', 'd'];
let pulled = pullAtValue(myArray, ['b', 'd']); // myArray = [ 'a', 'c' ] , pulled = [ 'b', 'd' ]
```

</details>

<br>[回到目录](#目录)

### quickSort
对数组快速排序，默认为升序。   
使用递归。使用`Array.prototype.filter()`和扩展运算符创建一个新数组：比关键数小的数排在关键数前面，比关键数小的数排在关键数后面。如果参数`desc`为`true`，则按照降序排列所有元素。   
```js
const quickSort = ([n,...nums],desc) =>
  Number.isNaN(n)
  ? []
  : [
      ...quickSort(nums.filter(v => (desc ? v > n : v <= n)), desc),
      n,
      ...quickSort(nums.filter(v => (!desc ? v > n : v <= n)), desc)
    ];

// quickSort([4, 1, 3, 2]); -> [1,2,3,4]
// quickSort([4, 1, 3, 2], true); -> [4,3,2,1]
```
<br>[回到目录](#目录)

### reducedFilter
过滤出元素为对象的数组中满足条件的键。   
使用`Array.prototype.filter()`方法过滤出数组中满足`fn`函数的元素。对这些元素使用`Array.prototype.map()`方法，把`keys`参数中指定的键以键值对的形式从元素中过滤出来并返回。   
```js
const reducedFilter = (data, keys, fn) =>
    data.filter(fn).map(el =>
        keys.reduce((acc, key) => {
            acc[key] = el[key];
            return acc;
        }, {})
    );
```

<details>
    <summary>Examples</summary>

```js
const data = [
  {
    id: 1,
    name: 'john',
    age: 24
  },
  {
    id: 2,
    name: 'mike',
    age: 50
  }
];
reducedFilter(data, ['id', 'name'], item => item.age > 24); // [{ id: 2, name: 'mike'}]
```

</details>

<br>[回到目录](#目录)

### sample
从一个数组中提取随机一个元素。   
使用`Math.random`生成随机数，与数组长度相乘再使用`Math.floor`方法向下取整，得到随机数的索引。   
该方法对字符串同样有效。   
```js
const sample = arr => arr[Math.floor(Math.random() * arr.length)];
```

<details>
    <summary>Examples</summary>
    
```js
sample([3, 7, 9, 11]); // 9
```

</details>

<br>[回到目录](#目录)
    
### shuttle
将数组打乱顺序，并返回出新数组。   
使用`Fisher-Yates algorithm`（洗牌算法）给数组重新洗牌。   
```js
const shuffle = ([...arr]) => {
  let m = arr.length;
  while (m) {
    const i = Math.floor(Math.random() * m--);
    [arr[m], arr[i]] = [arr[i], arr[m]];
  }
  return arr;
};
```

<details>
    <summary>Examples</summary>
    
```js
const foo = [1, 2, 3];
shuffle(foo); // [2,3,1]
console.log(foo); // [1,2,3]
```

</details>

<br>[回到目录](#目录)
    
### sampleSize
获取数组中的`n`个随机元素，最大不超过数组的大小。   
首先给数组重新*洗牌*。使用`Array.prototype.slice()`方法获取到`n`个随机元素。省略第二个参数则默认获取一个随机元素。   
```js
const sampleSize = ([...arr], n = 1) => {
  let m = arr.length;
  while (m) {
    const i = Math.floor(Math.random() * m--);
    [arr[m], arr[i]] = [arr[i], arr[m]];
  }
  return arr.slice(0, n);
};
```

<details>
    <summary>Examples</summary>
    
```js
sampleSize([1, 2, 3], 2); // [3,1]
sampleSize([1, 2, 3], 4); // [2,3,1]
```

</details>

<br>[回到目录](#目录)

### similarity
返回两个数组共有元素。   
使用`Array.prototype.filter()`方法从第一个数组中过滤出第二个数组也拥有的元素(第二个数组采用`Array.prototype.includes()`方法判断是否拥有)。   
```js
const similarity = (arr,value) => arr.filter(v => value.includes(v));
```

<details>
    <summary>Examples</summary>
    
```js
similarity([1, 2, 3], [1, 2, 4]); // [1,2]
```

</details>

<br>[回到目录](#目录)

### sortedIndex
返回插入一个元素到数组中能够保持原有排序的索引值。   
检查数组是否是降序排列。使用`Array.prototype.findIndex()`方法找到插入元素所在的位置。   
```js
const sortedIndex = (arr, n) => {
    const isDescending = arr[0] > arr[arr.length - 1];
    const index = arr.findIndex(el => (isDescending ? n > el : n <= el));
    return index === -1 ? arr.length : index;
};
```

<details>
    <summary>Examples</summary>
    
```js
sortedIndex([5, 3, 2, 1], 4); // 1
sortedIndex([30, 50], 40); // 1
```

</details>

<br>[回到目录](#目录)

### symmetricDifference
返回两个数组中互不不相同的元素。  
创建`Set`给两个数组去重，然后使用`Array.prototype.filter()`方法过滤出彼此都没有的元素集合。   
```js
const symmetricDifference = (a, b) => {
    const sA = new Set(a),
        sB = new Set(b);
    return [...a.filter(x => !sB.has(x)),...b.filter(x => !sA.has(x))];
|;
```

<details>
    <summary>Examples</summary>
    
```js
symmetricDifference([1, 2, 3], [1, 2, 4]); // [3,4]
```

</details>

<br>[回到目录](#目录)

### tail
返回数组的第一个元素之外的其他元素。   
当数组长度大于`1`时使用`arr.slice(1)`返回剩余元素的数组，当只有一个元素时，返回整个数组。  
```js
const tail = arr => (arr.length > 1 ? arr.slice(1) : arr);
```

<details>
    <summary>Examples</summary>
    
```js
tail([1, 2, 3]); // [2,3]
tail([1]); // [1]
```

</details>

<br>[回到目录](#目录)

### take
返回数组中的前`n`个元素。   
使用`Array.prototype.slice()`方法切下前`n`个元素。   
```js
const take = (arr,n = 1) => arr.slice(0,n);
```

<details>
    <summary>Examples</summary>
    
```js
take([1, 2, 3], 5); // [1, 2, 3]
take([1, 2, 3], 0); // []
```

</details>

<br>[回到目录](#目录)

### takeRight
返回数组中的后`n`个元素。   
使用`Array.prototype.slice()`方法切下后`n`个元素。  
```js
const takeRight = (arr,n = 1) => arr.slice(arr.length - n, arr.length);
```

<details>
    <summary>Examples</summary>
    
```js
takeRight([1, 2, 3], 2); // [ 2, 3 ]
takeRight([1, 2, 3]); // [3]
```

</details>

<br>[回到目录](#目录)

### union
返回两个数组的所有不重复元素。
```js
const union = (a, b) => Array.from(new Set([...a, ...b]));
```

<details>
    <summary>Examples</summary>
    
```js
union([1, 2, 3], [4, 3, 2]); // [1,2,3,4]
```

</details>

<br>[回到目录](#目录)

### without
过滤出数组中非指定元素。   
使用`Array.prototype.filter()`方法创建一个新数组，新数组内不含指定元素。   
```js
const without = (arr,...args) => arr.filter(v => !args.includes(v));
```

<details>
    <summary>Examples</summary>
    
```js
union([1, 2, 3], [4, 3, 2]); // [1,2,3,4]
```

</details>

<br>[回到目录](#目录)

### zip
创建一个新数组，其元素基于原始数组的位置排列。   
使用扩展操作符和`Math.max()`方法找到作为参数的数组的最大长度。创建一个数组，它的长度为参数数组的最大长度，它的元素为参数数组中对应位置的元素，并通过`Array.prototype.from()`方法转化为数组。   
如果对应位置没有元素存在，则填充`undefined`。   
```js
const zip = (...arrays) => {
    const maxLength = Math.max(...arrays.map(x => x.length));
    return Array.from({ length: maxLength }).map((_, i) => {
        return Array.from({l ength: arrays.length }, (_,k) => arrays[k][i]);
    });
};
```

<details>
    <summary>Examples</summary>
    
```js
zip(['a', 'b'], [1, 2], [true, false]); // [['a', 1, true], ['b', 2, false]]
zip(['a'], [1, 2], [true, false]); // [['a', 1, true], [undefined, 2, false]]
```

</details>

<br>[回到目录](#目录)

### zipObject
给定一个有效键名的数组和一个键值的数组，返回一个把属性名和属性值关联起来的对象。   
因为对象的键值可以是`undefined`，键名不能是，所以用提供键名的数组使用`Array.prototype.reduce()`来决定结果对象的结构。   
```js
const zipObject = (props, values) =>
  props.reduce((obj, prop, index) => ((obj[prop] = values[index]), obj), {});
```

<details>
    <summary>Examples</summary>
    
```js
zipObject(['a', 'b', 'c'], [1, 2]); // {a: 1, b: 2, c: undefined}
zipObject(['a', 'b'], [1, 2, 3]); // {a: 1, b: 2}
```

</details>

<br>[回到目录](#目录)



