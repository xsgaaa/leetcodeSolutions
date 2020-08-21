### leetcode 238. 除自身以外数组的乘积

解法：计算前缀和后缀之积。

```cpp
//首先，从左往右计算前缀积。类似于前缀和的思想。
//然后,从右往左计算后缀积，与前缀积相乘，得到结果。
```

```cpp
vector<int> productExceptSelf(vector<int>& nums) {
        int N=nums.size();
        vector<int> l(N,0);
        for(int i=0;i<N;i++)
        {
            if(i==0){
                l[i]=1;
                continue;
            }
            l[i]=l[i-1]*nums[i-1];
        }
        vector<int> res(N,0);
        int r=1;
        for(int i=N-1;i>=0;i--)
        {
            if(i==N-1)
            {
                res[i]=r*l[i];
                continue;
            }
            r =r* nums[i+1];
            res[i]=r*l[i];
        }
        return res;
    }
```

