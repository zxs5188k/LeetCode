<!--

 * @Descripttion: 说明
 * @Author: ZXS
 * @Date: 2022-07-29 00:01:33
 * @LastEditors: ZXS
 * @LastEditTime: 2022-08-23 22:34:24
-->

### 前言

这里是小双的刷题记录，匆匆忙忙的学习完数据结构之后，在能做到用 js 来封装其简单的功能，也了解了前端常见的几个排序算法，冒泡排序、插入排序、选择排序、希尔排序、快速排序等，并每天都手写了两三遍以致于熟练，就斗志昂扬的踏上了我的力扣算法刷题之路了，也不知道在这条路上能遇到什么样的困难...

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
- [LeetCode-206-反转链表](#leetcode-206-反转链表)
- [LeetCode-21-合并两个有序链表](#leetcode-21-合并两个有序链表)
- [LeetCode-94-二叉树的中序遍历](#leetcode-94-二叉树的中序遍历)
- [LeetCode-136-只出现一次的数字](#leetcode-136-只出现一次的数字)

# LeetCode-1-两数之和

![image text](https://gitee.com/zxs5188k/LeetCode/raw/master/images/LeetCode-1-两数之和.png)

<img src="C:\Users\小双哥哥\Desktop\LeetCode刷题记录\LeetCode\images\LeetCode-1-两数之和.png" style="zoom:80%;" />

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

# LeetCode-206-反转链表

![image text](https://gitee.com/zxs5188k/LeetCode/raw/master/images/LeetCode-206-反转链表.png)

```js
// 熟悉链表的基本结构就可以解出
// 对链表进行遍历，声明一个新的头，让当前节点的指针指向新的头,再把当前节点赋值给新的头
// 注意在在让当前节点的指针指向新的头之前需要保存一下指针，不让其丢失无法继续遍历下去
var reverseList = function (head) {
  let curr = head
  let prev = null
  while (curr) {
    let next = curr.next
    curr.next = prev
    prev = curr
    curr = next
  }
  return prev
}
```

# LeetCode-21-合并两个有序链表

![image text](https://gitee.com/zxs5188k/LeetCode/raw/master/images/LeetCode-21-合并两个有序链表.png)

```js
// 思路：可以想象递归就是程序内部维护了一个栈，这题用递归把最小的先压入栈，最后出栈的时候，依次连接在一起就可以了
// 递归终止条件：list1或list2为空时结束
// 返回值：返回排好的链表头，递归到最后最先返回的一定是链表的最后一项
var mergeTwoLists = function (list1, list2) {
  if (list1 == null) {
    return list2
  }
  if (list2 == null) {
    return list1
  }
  if (list1.val < list2.val) {
    list1.next = mergeTwoLists(list1.next, list2)
    return list1
  } else {
    list2.next = mergeTwoLists(list2.next, list1)
    return list2
  }
}
```

**迭代解法：**

把每个节点想成珠子，合并的过程就是用线把珠子串起来，比较两个链表当前节点大小，串进小的，再将指向较小值的指针后移，直到某个链表的珠子全都串完，再把另一个链表剩下的珠子一次性都给串进去

```js
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} list1
 * @param {ListNode} list2
 * @return {ListNode}
 */
var mergeTwoLists = function(list1, list2) {
        var head = new ListNode(0)  //先往里面放了个无关数
        var cur = head
        //直接每次判断两边的节点值，cur.next指向较小值，更新cur的位置，list前进
        while(list1 && list2){
            if(list1.val < list2.val){
                cur.next = list1
                list1 = list1.next
            } else {
                 cur.next = list2
                list2 = list2.next
            }
            cur = cur.next
        }
        cur.next = list1 ? list1 : list2  //cur.next指向剩余链表
        return head.next  //最开始的节点不属于两个链表，返回下一个节点组成的有序链表
        };
};
```

# LeetCode-94-二叉树的中序遍历

![image text](https://gitee.com/zxs5188k/LeetCode/raw/master/images/LeetCode-94-二叉树的中序遍历.png)

首先我们需要了解什么是二叉树的中序遍历：按照访问左子树——根节点——右子树的方式遍历这棵树，而在访问左子树或者右子树的时候我们按照同样的方式遍历，直到遍历完整棵树。因此整个遍历过程天然具有递归的性质，我们可以直接用递归函数来模拟这一过程。

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number[]}
 */
var inorderTraversal = function (root) {
  var result = []
  var inorder = function (root) {
    if (!root) return
    inorder(root.left)
    result.push(root.val)
    inorder(root.right)
  }
  inorder(root)
  return result
}
```

# LeetCode-136-只出现一次的数字

![image text](https://gitee.com/zxs5188k/LeetCode/raw/master/images/LeetCode-21-只出现一次的数字.png)

很无语的算法，`^`异或运算符，始终不理解是怎么运算的，题目规定其他数只出现两次，如果不是只出现两次，异或运算符又解不了

```js
// 异或运算符解
var singleNumber = function (nums) {
  return nums.reduce((a, b) => a ^ b)
}
```

```js
// 自己的思路，灵活运用数组的api
var singleNumber = function (nums) {
  var result = null
  nums.forEach((item) => {
    if (nums.indexOf(item) == nums.lastIndexOf(item)) {
      result = item
    }
  })
  return result
}
// 救命可是时间复杂度真的好高
```
