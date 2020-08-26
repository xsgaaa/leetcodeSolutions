### leetcode [32. 最长有效括号](https://leetcode-cn.com/problems/longest-valid-parentheses/)

```cpp
/*
解法1：动态规划。
核心思想：dp[i]表示以i为结尾能获取的最长有效括号的长度。如果s[i]='('，则dp[i]恒为0，因为左括号只有碰到对应的右括号才会有效。
如果s[i]=')'有两种情况：
	(1) s[i-1]='('	-->	那么如果 dp[i]=(i>=2?dp[i-2]:0)+2;
	(2) s[i-1]=')' 	-->	那么如果 i>dp[i-1] && dp[i-dp[i]-1]='(',dp[i]=dp[i-1]+2+(i-1>dp[i-1]?dp[i-dp[i-1]-2]:0);
*/
```

```cpp
int longestValidParentheses(string s) {
        int n=s.size(),ans=0;
        //int dp[n];
        //memset(dp,0,sizeof dp);
        vector<int> dp(n,0);
        for(int i=1;i<n;i++)
        {
            if(s[i]==')' && s[i-1]=='(')
            {
                dp[i]=(i>=2?dp[i-2]:0)+2;
            }
            else if(s[i]==')' && s[i-1]==')')
            {
                if(i>dp[i-1] && s[i-dp[i-1]-1]=='(')
                    dp[i] =dp[i-1]+2+(i-1>dp[i-1]?dp[i-dp[i-1]-2]:0);
            }
            ans=max(ans,dp[i]);
        }
        return ans;
    }
```



```cpp
/*
	解法2：栈。
	栈中先存放一个哨兵-1，代表连续的有效的子串起点前面的一个元素。
	然后碰到左括号，就把其索引存入栈。
	碰到右括号，则将出栈栈顶元素：
        (1) 如果栈为空，表明当前的右括号没有的对应的左括号。将当前右括号的索引入栈作为哨兵。
        (2) 如果栈非空，则用当前索引减去栈顶元素的索引更新结果。
    这种方法应该空间上更有优势，因为有较小的可能所有的元素都入栈。
*/
```

```cpp
int longestValidParentheses(string s) {
        int n=s.size(),ans=0;
        stack<int> st;
        st.push(-1);
        for(int i=0;i<n;i++)
        {
            if(s[i]=='(')
                st.push(i);
            else
            {
                st.pop();
                if(st.empty())
                    st.push(i);
                else
                {
                    ans=max(ans,i-st.top());
                }
            }
        }
        return ans;
    }
```

