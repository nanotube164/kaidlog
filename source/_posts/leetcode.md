---
title: Leetcode 1
date: 2019-12-05 22:51:24
tags: leetcode
top_img: https://i.imgur.com/U4tOhlG.jpg
cover: https://i.imgur.com/U4tOhlG.jpg

categories:
 - Software Development
 - leetcode
---


# 解 Leetcode 大作戰 Day 1

給定一個整數數組 nums 和一個目標值 target，請你在該數組中找出和為目標值的那 兩個 整數，並返回他們的數組下標。

你可以假設每種輸入只會對應一個答案。但是，你不能重復利用這個數組中同樣的元素。

示例:


> 给定 nums = [2, 7, 11, 15], target = 9
>
>因为 nums[0] + nums[1] = 2 + 7 = 9
>所以返回 [0, 1]


~~~
	class Solution(object):
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """

        hashmap={}
        for i,num in enumerate(nums):
            if hashmap.get(target - num) is not None:
                return [i,hashmap.get(target - num)]
            hashmap[num] = i
~~~

測試結果複製以下代碼:
~~~
	nums = [2, 7, 11, 15]
	target = 9
	test = Solution(nums,target)
	test.twoSum(nums, target)
~~~

## 解題邏輯:

### ❤❤❤ 關鍵: 想到 "target - num" 是否存在 nums 陣列之中

這裡用的 enumerate 的函數，可以快速將陣列裡面的元素加上編號，詳細可以看 [enumerate](https://www.runoob.com/python/python-func-enumerate.html)，所以這邊的 enumerate(nums) 會變成 
> [(0:2), (1:7),(2,11),(3,15)]


判定如果 target - num 如果存在於 nums 中的話，就拿出來放在 hashmap 這個字典內，直接省略了一個 for 迴圈去找另一個值，反正如果有解肯定可以被抓出來丟到 hashmap 裡面 

所以這題的結果是這樣的


> 9 減 2 得到 7 在 nums 陣列中，return[0,7], 把 [2]:0 放進 hashmap 裡面，同理往下做
> 最後找到兩個值[2]:0、[7]:1
> 所以得到 0:1
	

{% note info %}用 repl.it 測試一下，確實可行{% endnote %}

<iframe height="800px" width="100%" src="https://repl.it/@Daekony/WirySilverChapters?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>