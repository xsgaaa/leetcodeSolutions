### leetcode 42. 接雨水

解法：双指针。

![image-20200817100608852](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200817100608852.png)

```cpp
//如图，观察箭头处的三个地方。可知：能否接到雨水取决于其左右两边柱子的最大高度的最小值。

//如果左右两边柱子的高度都是很高，中间一定可以接满水

//因此用两个变量来记录左右两边的最大值。

//当左边比右边高时，移动右指针，然后如果当前值比右边的最大值小，记录结果

//当左边比右边低时，移动左指针，同理
```



```cpp
int trap(vector<int>& height) {
        int N=height.size();
        int l=0,r=N-1;
        int res=0;
        int leftmax=0,rightmax=0;
        while(l<r)
        {
            if(height[r]>height[l])
            {
                if(height[l]<leftmax)
                    res+=leftmax-height[l];//此时，leftmax必然小于rightmax。
                //如果出现一个l，有height[l]>height[r]，那么必然不会执行到这一步来
                leftmax=max(height[l],leftmax);
                l++;
            }
            else
            {
                if(height[r]<rightmax)
                    res+=rightmax-height[r];
                rightmax=max(rightmax,height[r]);
                r--;
            }
        }
        return res;
    }
```

