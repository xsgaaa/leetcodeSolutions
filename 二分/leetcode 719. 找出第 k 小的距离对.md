### leetcode [719. 找出第 k 小的距离对](https://leetcode-cn.com/problems/find-k-th-smallest-pair-distance/)

解法：第二次做这题，居然还做不出来。只能说这题太巧妙了。

基本思路就是二分。题目里说是绝对值了，而且不限制顺序。首先来一波排序。

然后就是二分的时候左右区间的确定是比较难的。压根没想到用这种二分方式。

最难的就是怎么计算`cnt`，即怎么计算距离小于`mid`。

```cpp
int smallestDistancePair(vector<int>& nums, int k) {
        sort(nums.begin(),nums.end());
        int N=nums.size();
        int lo=0,hi=nums.back()-nums[0];//枚举每一个差值很难，所以枚举最大差值和最小差值
        while(lo<hi)
        {
            int mid=lo+(hi-lo>>1);
            int i=0,cnt=0;
            //这一步甚为巧妙
            for(int j=0;j<nums.size();j++)
            {//统计距离小于等于mid的对数
                while(nums[j]-nums[i]>mid)
                    i++;
                cnt+=j-i;
            }
            if(k<=cnt)  hi=mid;
            else lo=mid+1;
        }
        return lo;
    }
```

