### leetcode [154. 寻找旋转排序数组中的最小值 II](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array-ii/)

解法：二分法。但注意出现重复元素的情况。

```cpp
int findMin(vector<int>& nums) {
        int l=0,r=nums.size()-1;
    	//如果数组单调递增，那么直接二分查找。
        while(l<r)
        {
            int m=l+(r-l>>1);
            if(nums[m]<nums[r])	//因为nums[m]可能刚好为最小，所以r=m
                r=m;
            else if(nums[m]>nums[r])	//这种情况下最小值必然在m右边
                l=m+1;
            else	
                r--;//逐步减少r。当减少r时，此时计算得到的m可能也会向左边偏。
        }
        return nums[l];
    }
```

