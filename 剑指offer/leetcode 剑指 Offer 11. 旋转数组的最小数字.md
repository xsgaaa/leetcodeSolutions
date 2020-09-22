### leetcode [剑指 Offer 11. 旋转数组的最小数字](https://leetcode-cn.com/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof/)

```cpp
/*
	解法:
	当nums[m]==nums[r],r--这是最为关键的一步
	其余的，跟普通的二分没有啥区别。
*/
```

```cpp
int minNumberInRotateArray(vector<int> rotateArray) {
        int l=0,r=rotateArray.size()-1;
        while(l<r)
        {
            int m=(l+r)/2;
            if(rotateArray[m]==rotateArray[r])
                r--;
            else if(rotateArray[m]>rotateArray[r])
            {
                l=m+1;
            }
            else
                r=m;
        }
        return rotateArray[l];
    }
```

