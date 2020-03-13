# 009 - 回文数（palindrome-numbe）

* [LeetCode攻略地址](https://github.com/LiangJunrong/document-library/tree/master/other-library/LeetCode)

## <a name="chapter-one" id="chapter-one">一 目录</a>

## <a name="chapter-two" id="chapter-two">二 前言</a>
* **难度**：简单
* **涉及知识点**：字符串，算法
* **题目地址**：https://leetcode-cn.com/problems/palindrome-number/
* **题目内容**：
```
判断一个整数是否是回文数。回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。

示例:

1. 给定 121
    return true
2. -121
    return false

```

## <a name="chapter-three" id="chapter-three">三 解题</a>
### <a name="chapter-three-one" id="chapter-three-one">3.1 解法 - toString()</a>
* **解题代码**
```js
var isPalindrome = function(x) {
  if(x < 0) return false;
    return parseInt(x.toString().split("").reverse().join("")) == x ? true:false 
};
```
* **执行测试**
1. `x`：`1221`
2. `return`: `true`
```js
true
```
* **提交反馈执行结果**

>情执行用时 :356 ms, 在所有 JavaScript 提交中击败了0%的用户。

>内存消耗 :45.9 MB, 在所有 JavaScript 提交中击败了41%的用户


* **解题思路及分析**

1. 转成字符串再转成数据然后反转对比。效率低下

### <a name="chapter-three-two" id="chapter-three-two">3.2 解法 - 对比数组的一半</a>
* **解题代码**
```js
var isPalindrome = function(x) {
  if(x < 0) return false;
    let flag = true;
    x = x.toString()
    for(let i =0 ; i < x.length / 2; i++) {
        if(x[i] !== x[x.length-1-i]) {
            flag = false;
            break;
        }
    }
    return flag
};
```
* **执行测试**
1. `x`：`121`
2. `return`: `true`
```js
ture
```
* **提交反馈执行结果**

>情执行用时 :320 ms, 在所有 JavaScript 提交中击败了6.7%的用户。

>内存消耗 :45.9 MB, 在所有 JavaScript 提交中击败了38.42%的用户


* **解题思路及分析**

**首先**，我们需要了解 `Map` 这个对象。

1. 转成数据，对比数组的前后是否相等


### <a name="chapter-three-three" id="chapter-three-three">3.3 解法 - LeetCode大牛法（取得后半部分）</a>
```js
var isPalindrome = function(x) {
    if(x < 0 || (x % 10 === 0 && x != 0)) return false;
    if(x < 10) return true;
    let revertedNumber  = 0;
    while( x > revertedNumber) {
        revertedNumber = revertedNumber * 10 + x % 10;
        x = parseInt(x / 10);
    }
    return x == revertedNumber || x == parseInt(revertedNumber/10)
};
```
* **提交反馈执行结果**

>情执行用时 :204 ms, 在所有 JavaScript 提交中击败了91.28%的用户。

>内存消耗 :44.7 MB, 在所有 JavaScript 提交中击败了97%的用户

* **解题思路及分析**

* 先排除小于10和末尾为0的数据

* 取得后半部分的和`revertedNumber`;当后半部分大于剩余的值，表示已经过半，停止循环

* ` parseInt(revertedNumber/10)` 用于排除`12321`这样的数据

