### leetcode 11. 盛最多水的容器

解法：双指针。

原理同 leetcode 42题 接雨水 https://leetcode-cn.com/problems/trapping-rain-water/

```cpp
//容器能接的水量取决于容器左右端点的最小值与容器宽度的乘积。

//因此，利用双指针分别从左右两端开始遍历。
//当左端的高度小于右端的高度时，移动左指针。并计算结果。
//当右端的高度小于左端的高度时，移动右指针。
```

```cpp
int maxArea(vector<int>& h) {
        int N=h.size();
        int l=0,r=N-1;
        int res=0;
        while(l<r)
        {
            if(h[l]<h[r])
            {
                res=max(res,h[l]*(r-l));
                l++;
            }
            else
            {
                res=max(res,h[r]*(r-l));
                r--;
            }
        }
        return res;
    }
```

