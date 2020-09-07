### leetcdoe  [1004. 最大连续1的个数 III](https://leetcode-cn.com/problems/max-consecutive-ones-iii/)

```cpp
/*
	解法：滑动窗口。
	维护一个窗口[l,r]，其内部刚好有k+1个0。然后用r-l即可表示当其中k个0被转换成1后的个数。
*/
```

```cpp
class Solution {
public:
    int longestOnes(vector<int>& A, int K) {
        if(A.empty())   return 0;
        int l=0,r=0,cnt=0;
        int ans=0;
        while(r<A.size())
        {
            cnt+=A[r]==0;
            while(cnt>K)
            {
                ans=max(ans,r-l);
                cnt-=A[l]==0;
                l++;
            }
            r++;
        }
        ans=max(ans,r-l);
        return ans;
    }
};
```

