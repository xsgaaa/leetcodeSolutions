### leetcode [1330. 翻转子数组得到最大的数组值](https://leetcode-cn.com/problems/reverse-subarray-to-maximize-array-value/)

解法：见注释。

```cpp
//解题思路：假设区间[i+1,j]是要翻转的区间
    //那么翻转之后的数组值为：total为未翻转之前的值
    //total-abs(nums[i]-nums[i+1])-abs(nums[j]-nums[j+1])+abs(nums[i]-nums[j])+abs(nums[i+1]-nums[j+1])
    //total的值是不变的，主要看后面这块
    //设L[i]、H[i]分别为为nums[i]和nums[i+1]中的较小值和较大值
    //设L[j]、H[j]分别为为nums[j]和nums[j+1]中的较小值和较大值
    //那么有两种情况：
    //      1.假设区间L[i]...H[i]与区间L[j]...H[j]有重叠：
    //      翻转前：
    //      L[i]..........H[i]
    //              L[j]..............L[j]
    //      翻转后：
    //      L[i]....L[j]
    //                    H[i]........L[j]
    //      此时可以看出区间的值可能会变小
    //      2.假设区间L[i]...H[i]与区间L[j]...H[j]没有重叠
    //      翻转前和上面翻转后的情形类似，翻转后和上面翻转前的情形类似
    //      此时，翻转后的值应该增加重叠区间的2倍。
    //以上面的分析作为突破口：求翻转前区间左端点的最大值和区间右端点的最小值
    //然后两者相减计算重叠区域的长度乘以2加上total即可
    //注意有可能[0,i]区间会被翻转，或者[i,n-1]区间被翻转，此时需要特殊处理。
    int maxValueAfterReverse(vector<int>& nums) {
        int n=nums.size();
        int sum=0;
        int gain=0;//统计边界值，当nums[0]或者nums[n-1]成为要翻转的子数组的边界
        int lo=INT_MAX;     //用于求区间的右端点的最小值
        int hi=INT_MIN;     //用于求区间左端点的最大值
        for(int i=0;i<n-1;i++)
        {
            int n1=nums[i];
            int n2=nums[i+1];
            sum+=abs(n1-n2);//计算翻转前的最大值
            gain=max(gain,abs(nums[n-1]-n1)-abs(n1-n2));    //求[i,n-1]翻转最大值
            gain=max(gain,abs(nums[0]-n2)-abs(n1-n2));      //求[0,i]翻转最大值
            lo=min(lo,max(n1,n2));
            hi=max(hi,min(n1,n2));
        }
        return sum+max(gain,(hi-lo)*2);
    }
```



