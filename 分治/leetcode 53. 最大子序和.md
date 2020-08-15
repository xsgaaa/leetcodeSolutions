### leetcode 53. 最大子序和

解法1：动态规划。计算前缀和，然后遍历前缀和，动态维护目前的最大值`maxval`和目前的最小前缀和`minval`。

```cpp
int maxSubArray(vector<int>& nums) {
        int n=nums.size();
        if(n==1)    return nums[0];
        int sum[n+1];
        memset(sum,0,sizeof sum);
        for(int i=0;i<n;i++)
            sum[i+1]=sum[i]+nums[i];
        int minval=0,maxval=INT_MIN;
        for(int i=1;i<=n;i++)
        {
            maxval=max(maxval,sum[i]-minval);
            minval=min(minval,sum[i]);
        }
        return maxval;
    }
```

解法二：

计算前缀和，利用归并排序进行分治。凡是存在这种明显的正序或者逆序的题，并且最终结果后面的数比前面数大的，都可以用归并。

```cpp
int res=INT_MIN;
    int maxSubArray(vector<int>& nums) {
        int n=nums.size();
        if(n==1)    return nums[0];
        int sum[n+1];
        memset(sum,0,sizeof sum);
        for(int i=0;i<n;i++)
            sum[i+1]=sum[i]+nums[i];
        mergeSort(sum,0,n+1);
        return res;
    }
    void mergeSort(int sum[],int l,int r)
    {
        if(r-l<=1)  return;
        int m=l+(r-l)/2;
        mergeSort(sum,l,m);
        mergeSort(sum,m,r);
        res=max(res,sum[r-1]-sum[l]);
        int tmp[r-l];
        int i=l,j=m,k=0;
        while(i<m && j<r)
        {
            if(sum[i]<sum[j])
                tmp[k++]=sum[i++];
            else
                tmp[k++]=sum[j++];
        }
        while(i<m)  tmp[k++]=sum[i++];
        while(j<r)    tmp[k++]=sum[j++];
        i=l,k=0;
        while(i<r)
            sum[i++]=tmp[k++];
        return;
    }
```

