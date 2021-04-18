# 剑指 Offer 65. 不用加减乘除做加法

写一个函数，求两个整数之和，要求在函数体内不得使用 “+”、“-”、“*”、“/” 四则运算符号。

### 解法1：
```
int add(int a, int b) {
    int sum, carry;
    do
    {
        sum = a^b;
        carry = ((unsigned int)(a&b))<<1;
        a = sum;
        b = carry;
    }while(b != 0);
    return a;
}
```