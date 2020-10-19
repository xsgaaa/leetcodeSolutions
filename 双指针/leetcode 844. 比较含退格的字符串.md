### leetcode [844. 比较含退格的字符串](https://leetcode-cn.com/problems/backspace-string-compare/)

> 给定 S 和 T 两个字符串，当它们分别被输入到空白的文本编辑器后，判断二者是否相等，并返回结果。 # 代表退格字符。
>
> 注意：如果对空文本输入退格字符，文本继续为空
>

```cpp
/*
	解法1：利用栈。
*/
class Solution {
public:
    bool backspaceCompare(string S, string T) {
        stack<char> stS,stT;
        for(auto &c:S)
        {
            if(c=='#' && !stS.empty())
            {
                stS.pop();
            }
            else if(c!='#')
            {
                stS.push(c);
            }
        }
        for(auto &c:T)
        {
            if(c=='#' && !stT.empty())
            {
                stT.pop();
            }
            else if(c!='#')
            {
                stT.push(c);
            }
        }
        while(!stS.empty() && !stT.empty())
        {
            if(stS.top()==stT.top())
            {
                stS.pop();
                stT.pop();
            }
            else
                return false;
        }
        return stS.empty() && stT.empty();
    }
};
```

```cpp
/*
	解法2：利用双指针。
*/
class Solution {
public:
    bool backspaceCompare(string S, string T) {
        int i=S.size()-1,j=T.size()-1;
        int nums=0,numt=0;
        while(i>=0 || j>=0)
        {
            if(i>=0 && S[i]=='#')   
            {
                nums++;
                i--;
                continue;
            }
            if(j>=0 && T[j]=='#')  
            {
                numt++;
                j--;
                continue;
            } 
            if(i>=0 && nums>0)
            {
                i--;
                nums--;
                continue;
            }
            if(j>=0 && numt>0)
            {
                j--;
                numt--;
                continue;
            }
            if(i>=0 &&j>=0 && S[i]==T[j])
                i--,j--;
            else
                return false;
        }
        return true;
    }
};
```

