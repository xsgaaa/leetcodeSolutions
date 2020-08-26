### leetcode [459. 重复的子字符串](https://leetcode-cn.com/problems/repeated-substring-pattern/)

解法：在`s+s`中下标为`1`的位置开始查找`s`。如果找到了`s`，且`pos`等于`s.size()`，表明不存在重复子字符串。否则，重复子字符串为`(s+s).substr(0,pos)`。

```cpp
bool repeatedSubstringPattern(string s) {
        string str=s+s;
        int pos=str.find(s,1);
        if(pos==s.size())   return false;
        return true;
    }
```

