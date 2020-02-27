# 001 - 两数之和（two-sum）

* [LeetCode攻略地址](https://github.com/LiangJunrong/document-library/tree/master/other-library/LeetCode)

## <a name="chapter-one" id="chapter-one">一 目录</a>

## <a name="chapter-two" id="chapter-two">二 前言</a>
* **难度**：简单
* **涉及知识点**：数组
* **题目地址**：https://leetcode-cn.com/problems/two-sum/
* **题目内容**：
```
给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。

你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。

示例:

给定 nums = [2, 7, 11, 15], target = 9

因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]
```

## <a name="chapter-three" id="chapter-three">三 解题</a>
### <a name="chapter-three-one" id="chapter-three-one">3.1 解法 - for()</a>
* **解题代码**
```js
var twoSum = function(nums, target) {
  for (var i = 0, len = nums.length; i < len; i++) {
    for (var j = i + 1; j < len; j++) {
      if (nums[j] + nums[i] === target) {
        return [i, j];
      }
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

>情执行用时 :128 ms, 在所有 JavaScript 提交中击败了48.87%的用户。

>内存消耗 :34.5 MB, 在所有 JavaScript 提交中击败了78.73%的用户


* **解题思路及分析**

1. 第一使用遍历标记为`i`。

2. 第二次遍历为`i+1`，因为要计算和，不能两次都用相同的下标。

3. 判断数组里两个数相加和是否等于`target`，如果等于直接`return`，不应考虑后面的数据。

4. 可以发现效率比较低下，时间复杂度为，有优化空间。

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

