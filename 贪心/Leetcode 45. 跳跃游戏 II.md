#### Leetcode [45. 跳跃游戏 II](https://leetcode-cn.com/problems/jump-game-ii/)

解法：贪心。

```cpp
int jump(vector<int>& nums) {
        int N=nums.size();
        int i=0,cnt=0;
        while(i<N-1)   
        {//因为N-1就是最终位置了。所以要小于N-1
            if(i+nums[i]>=N-1)
            {//计算这步能走的最远的距离是否到达终点
                cnt++;
                break;
            }
            //在能跳的范围内找最大的。
            int hi=i+nums[i],j=i+1,idx=i+1;
            for(;j<=hi;j++)
            {
                if(idx+nums[idx]<j+nums[j])
                {//更新最大值索引
                    idx=j;
                }
            }
            i=idx;  //直接跳到最大值索引那去
            cnt++;  //步数加1
        }
        return cnt;
    }
```

