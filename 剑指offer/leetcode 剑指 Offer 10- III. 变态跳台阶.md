### nowcoder [变态跳台阶](https://www.nowcoder.com/profile/408614969/codeBookDetail?submissionId=89804941) 

```cpp
/*
	解法：第二类基本型DP。
*/
```

```cpp
class Solution {
public:
    int jumpFloorII(int number) {
        vector<int> dp(number+1);	
        dp[0]=1;
        dp[1]=1;
        for(int i=2;i<=number;i++)
        {
            for(int j=0;j<i;j++)
            {
                dp[i]+=dp[j];
            }
        }
        return dp[number];
    }
};
```

