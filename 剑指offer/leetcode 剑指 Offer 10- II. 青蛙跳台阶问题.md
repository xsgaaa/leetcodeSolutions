### leetcode [剑指 Offer 10- II. 青蛙跳台阶问题](https://leetcode-cn.com/problems/qing-wa-tiao-tai-jie-wen-ti-lcof/)

```cpp
/*
	解法：同斐波那契数列。
*/
```

```cpp
class Solution {
public:
    //空间复杂度O(n),时间复杂度O(n)
    int jumpFloor(int number) {
        int nums[number+1];
        memset(nums,0,sizeof nums);
        nums[0]=1;
        nums[1]=1;
        for(int i=2;i<=number;i++)
        {
            nums[i]=nums[i-1]+nums[i-2];
        }
        return nums[number];
    }
};
//空间复杂度o(1)
int jumpFloor(int number) {
        if(number==1)    return 1;
        int first=1,second=1;
        int third=0;
        for(int i=2;i<=number;i++)
        {
            third=first+second;
            first=second;
            second=third;
        }
        return third;
    }
```

