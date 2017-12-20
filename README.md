# 30s-code-translate-into-Chinese-
本文经过个人的翻译，翻译自《30-seconds-of-code》，原作者[Chalarangelo](https://github.com/Chalarangelo/30-seconds-of-code)，收集了有用的 JavaScript 代码片段。


# 目录
## Array
* [arrayMax](#arrayMax)
* [arrayMin](#arrayMin)
* [chunk](#chunk)

## Array

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
使用`Array.from`方法将伪数组和可迭代对象转化数组，该方法返回一个处理好的数组实例。
对于处理伪数组来说`Array.from`可接受两个参数，第一个为属性为`length`的对象，第二个可选参数是一个回调函数，用来处理被传进新数组的每个元素。
`Array.protype.slice()`可以把原数组切割成指定的长度。
```js
const chunk = (arr,size) => 
   Array.from({length: Math.ceil(arr.length / size)},(value,index) => arr.slice(index * size, index * size + size));
//chunk([1,2,3,4,5],2) ->[[1,2],[3,4],[5]]
```
[回到目录](#目录)
