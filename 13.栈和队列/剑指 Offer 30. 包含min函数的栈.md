# 剑指 Offer 30. 包含min函数的栈
定义栈的数据结构，请在该类型中实现一个能够得到栈的最小元素的 min 函数在该栈中，调用 min、push 及 pop 的时间复杂度都是 O(1)。

##### 示例:  

MinStack minStack = new MinStack();  
minStack.push(-2);  
minStack.push(0);  
minStack.push(-3);  
minStack.min();   --> 返回 -3.  
minStack.pop();  
minStack.top();      --> 返回 0.  
minStack.min();   --> 返回 -2.  

### 解法1：
数据栈s正常使用，辅助栈s_min用于存储最小值。  
对于每个新插入的元素x：
- 1. 如果x比当前辅助栈s_min栈顶元素还小，则直接压入x；
- 2. 如果x比当前辅助栈s_min栈顶元素大，则压入辅助栈栈顶元素。  
```
class MinStack {
public:
    /** initialize your data structure here. */
    MinStack() {

    }
    
    void push(int x) {
        s.push(x);
        if(s_min.empty())
        {
            s_min.push(x);
        }
        else
        {
            if(x < s_min.top())
            {
                s_min.push(x);
            }
            else
            {
                s_min.push(s_min.top());
            }
        }
    }
    
    void pop() {
        s.pop();
        s_min.pop();
    }
    
    int top() {
        return s.top();
    }
    
    int min() {
        return s_min.top();
    }
private:
    stack<int> s;
    stack<int> s_min;
};
```