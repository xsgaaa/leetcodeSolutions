### leetcode [面试题 17.19. 消失的两个数字](https://leetcode-cn.com/problems/missing-two-lcci/)

解法：自哈希。用数组索引作为键值，索引`i`处存放`i+1`的值。

```cpp
vector<int> missingTwo(vector<int>& nums) {
        nums.push_back(0);
        nums.push_back(0);
        int N=nums.size();
        for(int i=0;i<N;i++)
        {//为了防止nums[i]-1溢出，这里要判断nums[i]!=0
            while(nums[i]!=0 && nums[i]!=nums[nums[i]-1])
                swap(nums[i],nums[nums[i]-1]);
        }
        vector<int> ans;
        //索引i存放i+1的值
        for(int i=0;i<N;i++)
        {
            if(nums[i]==0)
                ans.push_back(i+1);
        }
        return ans;
    }
```

