### leetcode [644. 最大平均子段和 II](https://leetcode-cn.com/problems/maximum-average-subarray-ii/)

解法：滑动窗口+二分+前缀和。

都是以前的老套路，组合到一起，又不会了。

首先二分：看到这个条件就应该知道是对平均值进行二分。

![image-20200821172805943](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200821172805943.png)

注意`check`之后，要么左边界等于`m`，要么右边界等于`m`。这和整数二分不一样。

题目说是求连续子序列的平均值，这里并没有直接求。而是利用区间内的每一个数减去均值。

然后就相当于计算前缀和，只要`sum-prevmin>=0`，满足要求，就可以找到大于等于`m`的均值。

因为题目里要求最大的和，所以当满足要求是时，要扩大`l`。

```cpp
 bool check(vector<int> &nums,int k,double m)
    {
        double sum=0;
        for(int i=0;i<k;i++)
        {
            sum+=nums[i]-m;
        }
        if(sum>=0)  return true;
        double prev=0,prevmin=0;
        for(int i=k;i<nums.size();i++)
        {
            sum+=nums[i]-m;
            prev+=nums[i-k]-m;
            prevmin=min(prev,prevmin);
            if(sum>=prevmin)
                return true;
        }
        return false;
    }
    double findMaxAverage(vector<int>& nums, int k) {
        int minval=INT_MAX,maxval=INT_MIN;
        for(auto & n:nums)
        {
            minval=min(minval,n);
            maxval=max(maxval,n);
        }
        double l=minval;
        double r=maxval;
        while(r-l>=1e-5)
        {
            double m=(l+r)/2;
            if(check(nums,k,m))
                l=m;
            else
                r=m;
        }
        return l;
    }
```

