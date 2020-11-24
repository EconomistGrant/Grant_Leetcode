今天面HRT tech和做leetcode遇到两个排序的题目 还蛮有意思的
其实面试面的不太好 思路基本都是对的但计算出了一些问题 虽然我一直边做边bb 自己的思路有被给不少正面评价 但是算出来第一个答案基本都是错的 需要引导几次才能帮我debug出计算错误  基于这是一家非常math非常tech bar非常高的公司而且面试官是一个从业十几年的物理phd 基本算是凉了 但是经验还是可以总结一些 这个招聘季也差不多了 明年再来吧= =

# Selection Sort with maximum deviation from the right position
假如有一组数据需要sort 已经得知每个数离sort后的位置“距离”不大于k 口头设计一个排序的算法
这道题其实挺妙的 我亏在一开始不知道selection sort是啥（我好像只知道几个O（nlogn）的算法）被面试官告知是go thru data find the smallest one, then go thru again find the second smallest one...之后 设计了一个长度为k的moving window（被面试官暗示再思考一下长度，反应过来是k+1），最小的数字在moving window里面，然后remove，然后把下一个值放进moving window，再在window里找最小值作为排序后数组第二个值，一直往前。

至于window自然是用heap了，buildheap， removemin这些都是老操作了，复杂度是nlog(k+1)

# Sort List
其实这玩意是真的挺简单的 没啥意思 放上来主要是自己平时操作的都是stl容器 链表操作的比较少 算是练练手
148. Sort List
Given the head of a linked list, return the list after sorting it in ascending order.

Follow up: Can you sort the linked list in O(nlogn) time and O(1) memory (i.e. constant space)?

## 思路
nlogn的复杂度得用树，无论是实际的二叉树、特殊的heap、还是mergesort抽象的树
O(1)的space就基本上要inplace了。这里设计一种从下而上的tree：
