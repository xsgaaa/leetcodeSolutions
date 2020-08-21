### Leetcode [41. 缺失的第一个正数](https://leetcode-cn.com/problems/first-missing-positive/)

```cpp
解法：自哈希法。利用数组自身的索引作为键值，索引为i的位置的值固定位i+1。值为nums[i]的元素的下表应该是nums[i]-1。如果nums[i]满足要求。
```

```cpp
int firstMissingPositive(vector<int>& nums) {
        int N=nums.size();
        if(N==0)    return 1;//注意1
        for(int i=0;i<N;i++)
        {
            while(nums[i]>0 && nums[i]<=N && nums[i]!=nums[nums[i]-1])//注意2
                swap(nums[i],nums[nums[i]-1]);
        }
        for(int i=0;i<N;i++)
        {
            if(i+1!=nums[i])
                return i+1;
        }
        return N+1;	//注意3
    }
```

