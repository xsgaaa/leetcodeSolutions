### leetcode [1074. 元素和为目标值的子矩阵数量](https://leetcode-cn.com/problems/number-of-submatrices-that-sum-to-target/)

解法：经典问题。求子矩阵的和。

首先计算二维前缀和：

```cpp
sum[i+1][j+1]=sum[i][j+1]+sum[i+1][j]+matrix[i][j]-sum[i][j];
```

之后**拍扁矩阵**，还是利用**前缀和**的思想。利用`O(n^3)`计算子矩阵的和。

注意`mp[0]=1`那里。由于从`k`从`1`开始，可以减少外层的循环一次，故需要提前保留个`0`。

```cpp
int numSubmatrixSumTarget(vector<vector<int>>& matrix, int target) {
        int N=matrix.size(),M=matrix[0].size();
        int sum[N+1][M+1];
        memset(sum,0,sizeof sum);
        for(int i=0;i<N;i++)
        {
            for(int j=0;j<M;j++)
            {//计算前缀和
                sum[i+1][j+1]=sum[i][j+1]+sum[i+1][j]-sum[i][j]+matrix[i][j];
            }
        }
        int ans=0;
        unordered_map<int,int> mp;
        int num=0;
        for(int i=1;i<=N;i++)
        {
            for(int j=0;j<i;j++)
            {
                mp.clear();
                mp[0]=1;//如果k从1开始的话，就要提前赋值，如果k从0开始，就不用赋值这个。
                for(int k=1;k<=M;k++)
                {
                    num=sum[i][k]-sum[j][k];
                    if(mp.count(num-target))
                        ans+=mp[num-target];
                    mp[num]++;
                }
            }
        }
        return ans;
    }
```

