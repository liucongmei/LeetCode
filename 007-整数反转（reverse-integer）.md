# 007 - 整数反转（reverse-integer）

* [LeetCode攻略地址](https://github.com/LiangJunrong/document-library/tree/master/other-library/LeetCode)

## <a name="chapter-one" id="chapter-one">一 目录</a>

## <a name="chapter-two" id="chapter-two">二 前言</a>
* **难度**：简单
* **涉及知识点**：数组,Math
* **题目地址**：https://leetcode-cn.com/problems/reverse-integer/
* **题目内容**：
```
给出一个 32 位的有符号整数，你需要将这个整数中每位上的数字进行反转。

示例一:

输入: 123
输出: 321

示例二：

输入: -123
输出: -321

示例三：

输入: 120
输出: 21

假设我们的环境只能存储得下 32 位的有符号整数，则其数值范围为 [−231,  231 − 1]。请根据这个假设，如果反转后整数溢出那么就返回 0。

```

## <a name="chapter-three" id="chapter-three">三 解题</a>
### <a name="chapter-three-one" id="chapter-three-one">3.1 解法 - 转字符串和数组</a>
* **解题代码**
```js
var reverse = function(x) {
    var fn = function(arr) {
        var arr2 = arr.reverse();
        if(arr2[0] === 0) {
            arr2.map((item, index) => {
                if(item > 0) {
                    return;
                }else {
                    arr2.plice(index, 0)
                }
            })

        }
        var int_x = parseInt(arr2.join(''))
        if(int_x >  Math.pow(2, 31) - 1) {
            return 0
        }else {
            return int_x;
        }
        
    }
    x = Math.abs(x) > Math.pow(2, 31) - 1 ? 0: x;
    if(x === 0) {
      return 0;
    }
    var arr = Math.abs(x).toString().split('');
    var new_x = fn(arr);
    if(x > 0) {
        return new_x;
    }
    if(x < 0) {
        return "-" + new_x
    }
};
``` 0
* **执行测试*01. `x`: `123`
3. `return`：
```js
  321
```
* **提交反馈执行结果**

>情执行用时 :80 ms, 在所有 JavaScript 提交中击败了89.47%的用户。

>内存消耗 :36.2 MB MB, 在所有 JavaScript 提交中击败了38.95%的用户


* **解题思路及分析**

1. 先取绝对值判断范围，排除大于的范围。

2. 转成字符串后转数据，利用数组的`reverse`反转，然后判断是否有`0`开头，删除头部的`0`。

3. 再转成`int`， 判断是否在范围内。

4. 根据原来值判断是否小于0,小于0添加`-`。

### <a name="chapter-three-two" id="chapter-three-two">3.2 解法 - Map</a>
* **解题代码**
```js
var twoSum = function(nums, target) {
  let map = new Map();
  for (let i = 0; i < nums.length; i++) {
    if (map.has(nums[i])) {
      return [map.get(nums[i]), i];
    } else {
      map.set(target - nums[i], i);
    }
  }
};
```
* **执行测试**
1. `nums`：`[1, 3, 2, 5, 6]`
2. `target`: `8`
3. `return`：
```js
[1, 3]
```
* **提交反馈执行结果**

>情执行用时 :64 ms, 在所有 JavaScript 提交中击败了89.16%的用户。

>内存消耗 :35.3 MB, 在所有 JavaScript 提交中击败了23.47%的用户


* **解题思路及分析**

**首先**，我们需要了解 `Map` 这个对象。

1. 它可以通过 `set()` 的形式，以 `[key, value]` 的形式保存一组数据。（题目中对应 `key` 就是存入的 `target - nums[i]` 值，`value` 就是索引）
2. 它可以通过 `get()` 的形式，获取到传入 `key` 值对应的 `value`。
3. 它可以通过 `has()` 的形式，判断 `Map` 对象里面是否存储了传入 `key` 对应的 `value`。

**然后**，我们遍历 `nums` 数组。

**最后**，我们判断 `nums[i]` 是否存在于 `Map` 对象中。没有的话，就存入 `target - nums[i]` 到 `Map` 中。有的话，因为上次存入的是 `target- nums[i]`，有点类似于解题的钥匙，既然我们看到 `nums[i]` 存在于 `Map` 中，它是解题的钥匙，所以我们只需要返回 `[map.get(nums[i]), i]` 这组值即可。

4. 你会发现效率提高了，但是内存的使用率同时也增加了。


### <a name="chapter-three-three" id="chapter-three-three">3.3 解法 - LeetCode大牛法</a>
```js
var twoSum = function(nums, target) {
     var temp = [];
    for(var i=0;i<nums.length;i++){
        var dif = target - nums[i];
        if(temp[dif] != undefined){
            return [temp[dif],i];
        }
        temp[nums[i]] = i;
    }
};
```
* **提交反馈执行结果**

>情执行用时 :60 ms, 在所有 JavaScript 提交中击败了95.14%的用户。

>内存消耗 :34.4 MB, 在所有 JavaScript 提交中击败了82.78%的用户

* **解题思路及分析**

* 使用数组存储下标的方式来替代值

