# 剑指 Offer 50. 第一个只出现一次的字符

在字符串 s 中找出第一个只出现一次的字符。如果没有，返回一个单空格。 s 只包含小写字母。

##### 示例:
  
s = "abaccdeff"  
返回 "b"  
  
s = ""   
返回 " "  
### 解法1：哈希表
```
char firstUniqChar(string s) {
    int hash[26] = {0};
    for(int i = 0;i<s.length();i++)
    {
        hash[s[i]-'a']++;
    }
    for(int i = 0;i<s.size();i++)
    {
        if(hash[s[i]- 'a'] == 1)
        {
            return s[i];
        }
    }
    return ' ';
}
```