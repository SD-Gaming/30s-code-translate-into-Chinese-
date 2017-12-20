# 30s-code-translate-into-Chinese-
本文经过个人的翻译，翻译自《30-seconds-of-code》，原作者Chalarangelo，收集了有用的 JavaScript 代码片段。


# 目录
## Array
* [`arrayMax`](#arrayMax)
* [`arrayMin`](#arrayMin)

## Array

### arrayMax

返回一个数组中最大的数值。
使用扩展运算符展开数组，使用`Math.max()`找出最大数。
```js
   const arrayMax = arr => Math.max(...arr);
   // arrayMax([10, 1, 5]) -> 10
```
[回到目录](#目录）

### arrayMin

返回一个数组中最小的数值。
使用扩展运算符展开数组，使用`Math.min()`找出最小数。
```
  const arrayMin = arr => Math.min(...arr);
  // arrayMin([10, 1, 5]) -> 1
```
[回到目录](#目录）
