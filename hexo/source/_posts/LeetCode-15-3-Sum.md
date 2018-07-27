---
title: 15. 3 Sum
categories: Leetcode
tags: Leetcode
date: 2018-05-13 01:08:02
---

# 3 Sum
Given an array nums of n integers, are there elements a, b, c in nums such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.

##### Note:

The solution set must not contain duplicate triplets.
<!--more-->

##### Example:
```
Given array nums = [-1, 0, 1, 2, -1, -4],
A solution set is:
[
   [-1, 0, 1],
   [-1, -1, 2]
]
```

# Solution
Input: int[] nums
Output: List<List<Integer>>

## Method O(N^2)
> 1. Two pointers, 确定第一个值之后，用two pointers来表示第二个和第三个值
> 2. **注意去重**： for循环进来的时候判断是不是跟前一个相同，然后找到答案之后看是不是有相同的left和right
> 3. 注意找到valid的结果之后，去重之后再改变指针
> 4. **这种方法一定要先排序**

```Java
public List<List<Integer>> threeSum(int[] nums) {
    List<List<Integer>> res = new ArrayList<>();
    if (nums == null || nums.length <= 2) return res;
    Arrays.sort(nums);
    for (int i = 0; i < nums.length; i++) {
        if (i > 0 && nums[i] == nums[i - 1]) continue;
        int left = i + 1;
        int right = nums.length - 1;
        while (left < right) {
          if (nums[i] + nums[left] + nums[right] == 0) {
            res.add(Arrays.asList(nums[i], nums[left], nums[right]));
            while (left < right && nums[left + 1] == nums[left]) left++;
            while (left < right && nums[right - 1] == nums[right]) right--;
            left++;
            right--;
          } else if (nums[i] + nums[left] + nums[right] < 0) {
            left++;
          } else {
            right--;
          }
        }
    }
    return res;
}
```
