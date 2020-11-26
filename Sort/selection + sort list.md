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
O(1)的space就基本上要inplace了。如果是由上而下的话，虽然看起来是O(1)空间，其实会有logn个递归function在stack上没有释放。这里设计一种从下而上的tree，每次mergesort两个长度为l的“已经排序好”的list，l从1开始每次翻倍，即可达到nlogn的复杂度和“已经排序好”的特质。具体实现起来，看了一些答案的实现不是特别理想，自己有空设计一个比较好的吧（挖个坑先）。

po一个答案先
```c++
class Solution {
public:
    ListNode* sortList(ListNode* head) {
        if (head == nullptr) {
            return head;
        }
        int length = 0;
        ListNode* node = head;
        while (node != nullptr) {
            length++;
            node = node->next;
        }
        ListNode* dummyHead = new ListNode(0, head);
        for (int subLength = 1; subLength < length; subLength <<= 1) {
            ListNode* prev = dummyHead, *curr = dummyHead->next;
            while (curr != nullptr) {
                ListNode* head1 = curr;
                for (int i = 1; i < subLength && curr->next != nullptr; i++) {
                    curr = curr->next;
                }
                ListNode* head2 = curr->next;
                curr->next = nullptr;
                curr = head2;
                for (int i = 1; i < subLength && curr != nullptr && curr->next != nullptr; i++) {
                    curr = curr->next;
                }
                ListNode* next = nullptr;
                if (curr != nullptr) {
                    next = curr->next;
                    curr->next = nullptr;
                }
                ListNode* merged = merge(head1, head2);
                prev->next = merged;
                while (prev->next != nullptr) {
                    prev = prev->next;
                }
                curr = next;
            }
        }
        return dummyHead->next;
    }

    ListNode* merge(ListNode* head1, ListNode* head2) {
        ListNode* dummyHead = new ListNode(0);
        ListNode* temp = dummyHead, *temp1 = head1, *temp2 = head2;
        while (temp1 != nullptr && temp2 != nullptr) {
            if (temp1->val <= temp2->val) {
                temp->next = temp1;
                temp1 = temp1->next;
            } else {
                temp->next = temp2;
                temp2 = temp2->next;
            }
            temp = temp->next;
        }
        if (temp1 != nullptr) {
            temp->next = temp1;
        } else if (temp2 != nullptr) {
            temp->next = temp2;
        }
        return dummyHead->next;
    }
};

//作者：LeetCode-Solution
//链接：https://leetcode-cn.com/problems/sort-list/solution/pai-xu-lian-biao-by-leetcode-solution/
//来源：力扣（LeetCode）
//著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

