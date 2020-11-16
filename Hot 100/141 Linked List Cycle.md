141. Linked List Cycle
Given head, the head of a linked list, determine if the linked list has a cycle in it.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer. Internally, pos is used to denote the index of the node that tail's next pointer is connected to. Note that pos is not passed as a parameter.

Return true if there is a cycle in the linked list. Otherwise, return false.

# Hash Table Implementation - Trivial

# Fast / Slow Pointer - Interesting
Maintaining two pointers: one going forward twice per step, one going forward once per step
If there is no cycle: they will both hit nullptr
If there is a cycle:  they will meet

```c++
class Solution {
public:
    bool hasCycle(ListNode *head) {
        if (head == NULL) return false;
        ListNode *fast = head;
        ListNode *slow = head;
        while (true) {
            if (slow -> next != NULL && fast -> next != NULL && fast -> next -> next != NULL){
                slow = slow -> next;
                fast = fast -> next -> next;
                if (slow == fast) return true;
            }
            else return false;
        }
    }
};
```

# Get the starting point of the circle - More than interesting!
Where you stopped for the first thought:
say, steps before loop: a, loop length: b
x_slow = x, x_fast = 2x, so x = b (every time the distance is getting one position closer/further, so first time they meet, it must be an exact circle)
c = a - x

slow: a + c
fast: a + x + c

How to think from this:
slow is a steps away from a exact loop, but you dont know a
design another pointer, coming from origin, going once per step, they will meet at the starting point!

```c++
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        if (head == NULL) return NULL;
        ListNode *fast = head;
        ListNode *slow = head;
        while (true) {
            if (slow -> next != NULL && fast -> next != NULL && fast -> next -> next != NULL){
                slow = slow -> next;
                fast = fast -> next -> next;
                if (slow == fast) break;
            }
            else return NULL;
        }
        //same as before
        ListNode *slow_2 = head;
        while (slow!=slow_2) {
            slow = slow -> next;
            slow_2 = slow_2 -> next;
        }

        return slow;
    }
};
```