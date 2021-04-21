# 剑指 Offer 62. 圆圈中最后剩下的数字
0,1,···,n-1这n个数字排成一个圆圈，从数字0开始，每次从这个圆圈里删除第m个数字（删除后从下一个数字开始计数）。求出这个圆圈里剩下的最后一个数字。  
例如，0、1、2、3、4这5个数字组成一个圆圈，从数字0开始每次删除第3个数字，则删除的前4个数字依次是2、0、4、1，因此最后剩下的数字是3。  
##### 示例 1：

输入: n = 5, m = 3  
输出: 3  
##### 示例 2：

输入: n = 10, m = 17  
输出: 2  

### 解法1：环形链表（超时）
使用环形链表，但是会超时
```
typedef struct _Node
{
    int val;
    struct _Node* next;
    _Node(int ival)
    {
        val = ival;
        next = nullptr;
    }
}Node;
int lastRemaining(int n, int m) {
    if(n == 1)
    {
        return 0;
    }
    if(m == 1)
    {
        return n-1;
    }
    Node* head = new Node(0);
    Node* tmp = head;
    for(int i = 1;i<n;i++)
    {
        tmp->next = new Node(i);
        tmp = tmp->next;
    }
    tmp->next = head;

    tmp = head;
    Node* pre = nullptr;
    while(tmp->next != tmp)
    {
        int n = m;
        while(n != 1)
        {
            pre = tmp;
            tmp = tmp->next;
            n--;
        }
        pre->next = tmp->next;
        delete tmp;
        tmp = pre->next;
    }
    int ret = tmp->val;
    delete tmp;
    tmp = nullptr;
    return ret;
}
```
用例[70866, 116922]超时。
### 解法2：