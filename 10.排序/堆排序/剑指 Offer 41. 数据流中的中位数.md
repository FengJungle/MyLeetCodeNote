# 剑指 Offer 41. 数据流中的中位数
如何得到一个数据流中的中位数？如果从数据流中读出奇数个数值，那么中位数就是所有数值排序之后位于中间的数值。如果从数据流中读出偶数个数值，那么中位数就是所有数值排序之后中间两个数的平均值。  
例如，  

[2,3,4] 的中位数是 3  
  
[2,3] 的中位数是 (2 + 3) / 2 = 2.5  

设计一个支持以下两种操作的数据结构：  

void addNum(int num) - 从数据流中添加一个整数到数据结构中。  
double findMedian() - 返回目前所有元素的中位数。  
##### 示例 1：

输入：
["MedianFinder","addNum","addNum","findMedian","addNum","findMedian"]  
[[],[1],[2],[],[3],[]]  
输出：[null,null,null,1.50000,null,2.00000]  
##### 示例 2：  
    
输入：  
["MedianFinder","addNum","findMedian","addNum","findMedian"]  
[[],[2],[],[3],[]]  
输出：[null,null,2.00000,null,2.50000]  

### 解法1：堆排序
中位数是排序后的数组中的中间位置的数字，我们可以以中间数字num为界，用一个大顶堆来管理小于num的数字，也就是前半部分；用一个小顶堆来管理大于num的数字，也就是后半部分。最后返回两个堆堆顶值和的平均值即可。  
如果大顶堆的数据量比小顶堆数据量少，那就把小顶堆堆顶（即后半部分最小值）压入大顶堆。
```
class MedianFinder {
public:
    /** initialize your data structure here. */
    MedianFinder() {

    }
    
    void addNum(int num) {
        max_heap.push(num);
        min_heap.push(max_heap.top());
        max_heap.pop();

        if(max_heap.size() < min_heap.size())
        {
            max_heap.push(min_heap.top());
            min_heap.pop();
        }
    }
    
    double findMedian() {
        if(max_heap.size() == min_heap.size())
        {
            return ((double)(min_heap.top()+max_heap.top()))/2;
        }
        return max_heap.top();
    }
private:
    priority_queue<int>max_heap;  // 默认是最大堆
    priority_queue<int, vector<int>, greater<int>>min_heap;
};
```