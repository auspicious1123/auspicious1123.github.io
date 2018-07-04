---
title: 5. Longest Palindromic Substring
categories: Leetcode
tags: Leetcode
date: 2018-05-19 14:26:02
---

# Longest Palindromic Substring
Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.

Example 1:

>Input: "babad"
Output: "bab"
Note: "aba" is also a valid answer.

Example 2:

>Input: "cbbd"
Output: "bb"

<!--more-->

# Method 1:
> 分析： 找最长的回文子字符串，先找到所有的回文子串的长度保存在一个2d数组中，i 和 j 表示字串的起始位置，最后，返回最长的子串。
> Time complexity: O(N^2)
> Space complexity O(N^2)

> // input  "ababa"
// outpub "ababa"
dp =
1  -1   3  -1   5
0   1  -1   3  -1
0   0   1  -1   3
0   0   0   1  -1
0   0   0   0   1


```Java

public String longestPalindromicSubstring(String s) {
  if (s == null || s.length() == 0) {
    return null;
  }
  int[][] dp = new int[s.length()][s.length()];
  for (int i = 0; i < dp.length; i++) {
    dp[i][j] = 1;
  }
  int max = 0;
  int start = 0;
  int end = 0;
  for (int i = s.length() - 1; i >= 0; i--) {
    for (int j = i + 1; j < s.length(); j++) {
      if (s.charAt(i) == s.charAt(j) && dp[i + 1][j - 1] >= 0) {
        dp[i][i] = dp[i + 1][ j - 1] + 2;
        if (dp[i][j] > max) {
          max = dp[i][j];
          start = i;
          end = i;
        }
      } else {
        dp[i][j] = -1;
      }
    }
  }
  return s.substring(start, end + 1);
}

```

# Method 2
> Define a boolean array. 用boolean表示当前子串是不是回文子串，如果是的，找出最长的。
> Time complexity: O(N^2)
> Space complexity: O(N^2)

```Java
public String longestPalindromicSubstring(String s) {
  if (s == null || s.length() == 0) return null;
  boolean dp = new boolean[s.length()][s.length()];
  int max = 0;
  int start = 0;
  int end = 0;
  for (int j = 0; j < s.length(); j++) {
    for (int i = 0; i <= i; i++) {
      dp[i][j] = s.charAt(i) == s.charAt(j) && (j - i <= 2 || dp[i + 1][j - 1]);
      if (dp[i][j] && max > j - i + 1) {
        max = j - i + 1;
        start = i;
        end = j;
      }
    }
  }
  return s.substring(start, end + 1);
}
```

# Method 3
> 从中心寻找，向两边扩散

```Java
String res = "";
public String longestPalindromicSubstring(String s) {
  if (s == null || s.length() == 0) return null;
  for (int i = 0; i < s.length(); i++) {
    helper(s, i, i);
    helper(s, i, i + 1);
  }
  return res;
}

public void helper(String s, int left, int right) {
  while (left >= 0 && right < s.length() && s.charAt(left) == s.charAt(right)) {
    left--;
    right++;
  }
  String cur = s.substring(left + 1, right);
  if (cur.length() > res.length()) {
    res = cur;
  }
}
```
