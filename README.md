### 前言

这里是小双的刷题记录，在匆匆忙忙的学习完数据结构之后，在能做到用 js 来封装其简单的功能，也学习了前端常见的几个排序算法，冒泡排序、插入排序、选择排序、希尔排序、快速排序等，并每天都手写了两三遍以致于熟练，就斗志昂扬的踏上了我的力扣算法刷题之路了，也不知道在这条路上能遇到什么样的困难...

### 怎样刻意练习？

**一道题尽可能的做到多解**

**五部刷题法**

1. 刷题第一遍：花 5-10 分钟读题+思考，有好的解法后背诵、默写很重要
2. 刷题第二遍：马上自己手写
3. 刷题第三遍：过了 24 小时，再重复做题
4. 刷题第四遍：过了一周，反复回来练习新同类型题目
5. 刷题第五遍：面试前一周或者半个月专门性进行恢复性训练，强烈建议在纸上手写

**切忌不要为了刷题而刷题**

---

# 目录结构

- [目录结构](#目录结构)
- [LeetCode-1-两数之和](#leetcode-1-两数之和)

# LeetCode-1-两数之和

<img src="C:\Users\小双哥哥\Desktop\刷题记录\images\LeetCode-1-两数之和.png" style="zoom:80%;" />

```js
//  解法一：暴力解法，两次循环判断
// 由于两次循环，时间复杂度较高
var twoSum1 = function (nums, target) {
  for (var i = 0; i < nums.length; i++) {
    for (var k = 0; k < nums.length; k++) {
      // 这里还要加一个条件 i !== k 就是不能拿同一个元素比较
      if (nums[i] + nums[k] === target && i !== k) {
        return [i, k]
      }
    }
  }
```

```js
//  解法二：利用 Map 进行记录
// 一次循环，时间复杂度低，但是创建了一个Map集合，牺牲了内驱来换取时间
var twoSum2 = function (nums, target) {
  var map = new Map()
  var result = []
  nums.forEach((item, index) => {
    if (map.has(target - item)) {
      result = [map.get(target - item), index]
      return
    }
    map.set(item, index)
  })
  return result
}
```