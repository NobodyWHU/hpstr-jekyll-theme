---
layout: post
title: "Leetcode318 Maximum Product of Word Length"
description: "python solution for leetcode problem 318"
tags: [python, code, leetcode]
date: 2016-04-20 19:30:00
image:
  feature: abstract-2.jpg
  credit: dargadgetz
  creditlink: http://www.dargadgetz.com/ios-7-abstract-wallpaper-pack-for-iphone-5-and-ipod-touch-retina/
---

题目[链接](https://leetcode.com/problems/maximum-product-of-word-lengths/)在此。

题目原文摘抄如下：

Given a string array words, find the maximum value of length(word[i]) * length(word[j]) where the two words do not share common letters. You may assume that each word will contain only lower case letters. If no such two words exist, return 0.

Example 1:
Given ["abcw", "baz", "foo", "bar", "xtfn", "abcdef"]

Return 16

The two words can be "abcw", "xtfn".

Example 2:
Given ["a", "ab", "abc", "d", "cd", "bcd", "abcd"]

Return 4

The two words can be "ab", "cd".

Example 3:
Given ["a", "aa", "aaa", "aaaa"]

Return 0

No such pair of words.

---
题目解释：给定一个字符串数组，要求各个单词中出现的字母不能重复，然后求不同字符串长度的最大值

思路：最简单的解法就是暴力枚举求解，然后看了下问题的标签，有`Bit Manipulation`这一项，可以尝试用Bit做。

既然题目设定了只会出现小写字母，因此我们可以用int代表字母。即1代表a，2代表b，4代表c等等。那么单词`abc`就可以用`1|2|4`表示，最后对两个单词做`&`操作，如果两个单词不含有重复的字符串，`&`操作后的结果会是0，即达到了我们的要求。

{% highlight python %}
class Solution(object):
    def maxProduct(self, words):
        """
        :type words: List[str]
        :rtype: int
        """
        n = len(words)
        elements = [0]*n
        for i, s in enumerate(words):
            for c in s:
                elements[i] |= 1 << (ord(c)-97)
        
        
        ans = 0
        for i in range(n):
            for j in range(i+1, n):
                if not (elements[i] & elements[j]):
                    ans = max(ans, len(words[i])*len(words[j]))
        
        return ans

{% endhighlight %}