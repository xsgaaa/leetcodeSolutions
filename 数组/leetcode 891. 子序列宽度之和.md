### leetcode [891. 子序列宽度之和](https://leetcode-cn.com/problems/sum-of-subsequence-widths/)

解法：考虑每个数组元素对最终结果的贡献。

首先排序数组。假设数组当前的索引为`i`，则以其为走右边界的元素有`i`个，每个元素可选可不选，共有`2^i`种可能。以其为左边界的元素有`n-i-1`个，每个也是可选可不选，共有`2^(n-i-1)`种可能，用前者减去后者。然后累加结果。需要预处理出来`2`的阶乘的`table`。

![image-20200822111648437](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200822111648437.png)

```cpp
typedef long long ll;
    const int MOD=1e9+7;
    int sumSubseqWidths(vector<int>& A) {
        int N=A.size();
        sort(A.begin(),A.end());
        vector<ll> sum(N,0);
        sum[0]=1;
        for(int i=1;i<N;i++)
            sum[i]=(sum[i-1]<<1)%MOD;
        ll res=0;
        for(int i=0;i<N;i++)
        {
            int l=i;
            int r=N-i-1;
            res=(res+A[i]*(sum[l]-sum[r])+MOD)%MOD;
        }
        return res;
    }
```

