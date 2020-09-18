### leetcode [384. 打乱数组](https://leetcode-cn.com/problems/shuffle-an-array/)

```cpp
/*
	解法：洗牌算法。
*/
```

```cpp
class Solution {
public:
    vector<int> v;
    vector<int> res;
    Solution(vector<int>& nums) {
        for(auto &i:nums) 
        {
            v.push_back(i);
            res.push_back(i);
        }  
    }
    
    /** Resets the array to its original configuration and return it. */
    vector<int> reset() {
        res.clear();
        for(auto &i:v)  res.push_back(i);
        return v;
    }
    
    /** Returns a random shuffling of the array. */
    vector<int> shuffle() {
        int N=v.size();
        for(int i=N-1;i>=0;i--)
        {
            int num=rand()%(i+1);
            swap(res[num],res[i]);
        }
        return res;
    }
};
```

