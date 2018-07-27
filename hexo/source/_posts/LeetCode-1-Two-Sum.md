---
title: "[LeetCode] 1.Two Sum"
categories: Leetcode
tags: Leetcode
date: 2018-05-12 00:38:02
---

# Two Sum
Given an array of integers, return indices of the two numbers such that they add up to a specific target.
You may assume that each input would have exactly one solution, and you may not use the same element twice.
Example:
> Given nums = [2, 7, 11, 15], target = 9,
> Because nums[0] + nums[1] = 2 + 7 = 9,
> return [0, 1].
<!--more-->

# Solution
经典题目： 用hashmap保存`nums[i]`和`i`，遍历检查是否包含`target - nums[i]`。
> Time Complexity: O(N)
> Space Complexity: O(N)

```Java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> map = new HashMap();
        int[] result = new int[2];
        for (int i = 0; i < nums.length; i++){
            if (map.containsKey(target - nums[i])) {
                result[0] =  map.get(target - nums[i]);
                result[1] = i;
            } else {
                map.put(nums[i], i);
            }
        }
        return result;
    }
}
```
