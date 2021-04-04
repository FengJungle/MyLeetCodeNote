# 剑指 Offer 22. 链表中倒数第k个节点
输入一个链表，输出该链表中倒数第k个节点。为了符合大多数人的习惯，本题从1开始计数，即链表的尾节点是倒数第1个节点。

例如，一个链表有 6 个节点，从头节点开始，它们的值依次是 1、2、3、4、5、6。这个链表的倒数第 3 个节点是值为 4 的节点。  

##### 示例：  
  
给定一个链表: 1->2->3->4->5, 和 k = 2.  
   
返回链表 4->5.  

### 方法1：快慢指针
设定快慢两个指针，fast指针先往前移动k个节点，然后fast和slow同步前进，当fast到达末尾的时候，slow指针刚好走到倒数第k个节点
```
ListNode* getKthFromEnd(ListNode* head, int k) {
    ListNode* fast = head;
    ListNode* slow = head;
    for(int i = 0; i<k; i++)
    {
        if(fast == NULL)
        {
            return NULL;
        }
        fast = fast->next;
    }
    while(fast != NULL)
    {
        fast = fast->next;
        slow = slow->next;
    }
    return slow;
}
```