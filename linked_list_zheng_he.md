# Linked List 整合

Remove Nth Node From End of List
* 在删除节点的前一个节点停住 while (fast.next != null)

Partition List [leet](https://leetcode.com/problems/partition-list/)
* two dummy node & 注意这里原链表可能big后面还有点 要把他指向空

Remove Duplicates from Sorted List II
* 如果相等存一个value 和head.next比较

Convert Sorted Array to Binary Search Tree

***Convert Sorted List to Binary Search Tree***
[leet](https://leetcode.com/problems/convert-sorted-list-to-binary-search-tree/) [link](https://gretchency.gitbooks.io/leetcode/content/convert_sorted_list_to_balanced_bst.html)
* 每个链表节点被访问一次，故时间复杂度为 O(n)
* 分治法 利用len求得链表的中点 注意右边的Len = len - len/2 - 1 分别减去左子树长度和根节点

**Copy list with Random Pointer**
* HashMap记录深拷贝映射关系
* 运用dummy和curr node往下copy
* Map处理映射关系，先copy链表元素再copy Random指针指向元素，每次copy前在map里判断是否已经生成，避免出现重复节点

Sort List
* MergeSort
* 注意先判断head是否只有一个节点
* merge里面判断lList或者rList是否没走完完用if， while会死循环！

***Reorder List*** [leet](https://leetcode.com/problems/reorder-list/)
* 快慢指针找中点，分成左右两半
* 把右半边reverse
* 左右一一Merge,注意merge的时候，小心处理链表节点的断开及链接！next value要处理前先存成tmp.

Reverse Linked List II
* 注意最后首尾相连
* 遍历过程中要存放preM和mNode
* preM和prev连首部，mNode和curr连尾部

---
[Add Two Numbers](https://gretchency.gitbooks.io/leetcode/content/add_two_numbers.html)  ***高频***
* 用dummy node 构建新list
* 维护carry的值
* 分三种情况：l1,l2都没走完，l1没走完,l2没走完、
* l1,l2都走完以后，如果```carry != 0```, 还要加一下最后一次carry的值

[Odd Even Linked List](https://gretchency.gitbooks.io/leetcode/content/odd_even_linked_list.html)
* 两个指针来做，odd指向奇节点，even指向偶节点，然后把偶节点even后面的那个奇节点提前到odd的后面，偶节点的next也指向下下个节点, 然后odd和even各自前进一步，此时even又指向偶节点，odd指向当前奇节点的末尾，以此类推直至把所有的奇偶节点都连好，
* 最后要把奇节点和第一个偶节点连起来