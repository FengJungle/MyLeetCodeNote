# 剑指 Offer 35. 复杂链表的复制
请实现 copyRandomList 函数，复制一个复杂链表。在复杂链表中，每个节点除了有一个 next 指针指向下一个节点，还有一个 random 指针指向链表中的任意节点或者 null。

https://leetcode-cn.com/problems/fu-za-lian-biao-de-fu-zhi-lcof/

### 解法1：哈希表
* 第一步：复制原始链表上的每一个节点N创建N'，然后把这些创建出来的节点用next连接起来；同时把(N, N')键值对放进一个哈希表中  
* 第二步：设置复制链表山给每个节点的random，如果原始链表上N的random指向S，那么新链表上N'也应该指向S'，根据哈希表即可找到S'节点。
```
Node* copyRandomList(Node* head) {
    if(head == NULL)
    {
        return NULL;
    }
    // 哈希表
    map<Node*, Node*> Map;
    // 新链表的head节点
    Node* newHead = NULL;
    Node* pre = NULL;
    // 原始链表节点
    Node* tmp = head;

    // 第一步：复制每个节点，并用next连接起来
    while(tmp != NULL)
    {
        Node* node = new Node(tmp->val);
        if(newHead == NULL)
        {
            newHead = node;
            pre = node;
        }
        else
        {
            pre->next = node;
            pre = node;
        }
        Map[tmp] = node;
        tmp = tmp->next;
    }

    // 第二步：根据哈希表，复制random指针
    tmp = head;
    pre = newHead;
    while(tmp != NULL)
    {
        pre->random = Map[tmp->random];
        pre = pre->next;
        tmp = tmp->next;
    }
    return newHead;
}
```

### 方法2：链表操作
```
Node* copyRandomList(Node* head) {
    if(head == NULL)
    {
        return NULL;
    }

    // 第一步：复制节点，将N'节点连接到N后面
    Node* cur = head;
    while(cur != NULL)
    {
        Node* node = new Node(cur->val);
        node->next = cur->next;
        cur->next = node;
        cur = cur->next->next;
    }

    // 第二步：复制random节点，N'的random节点指向的是N'的random的下一个节点
    cur = head;
    while(cur != NULL)
    {
        Node* pre = cur;
        cur = cur->next;
        if(pre->random != NULL)
        {
            cur->random = pre->random->next;
        }
        else
        {
            cur->random = NULL;
        }
        cur = cur->next;
    }

    // 第三步：将原链表拆分成两个链表
    Node* l1 = head;
    Node* l2 = head->next;
    Node* ret = l2;
    while(l1 != NULL && l2 != NULL)
    {
        l1->next = l2->next;
        l1 = l1->next;
        if(l1 != NULL)
        {
            l2->next = l1->next;
            l2 = l2->next;
        }
        else
        {
            l2->next = NULL;
            break;
        }
    }
    return ret;
}
```