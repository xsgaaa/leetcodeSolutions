### leetcode [75. 颜色分类](https://leetcode-cn.com/problems/sort-colors/)

> 给定一个包含红色、白色和蓝色，一共 n 个元素的数组，原地对它们进行排序，使得相同颜色的元素相邻，并按照红色、白色、蓝色顺序排列。
>
> 此题中，我们使用整数 0、 1 和 2 分别表示红色、白色和蓝色。
>
> 注意:
> 不能使用代码库中的排序函数来解决这道题。
>
> 示例:
>
> 输入: [2,0,2,1,1,0]
> 输出: [0,0,1,1,2,2]
> 进阶：
>
> 一个直观的解决方案是使用计数排序的两趟扫描算法。
> 首先，迭代计算出0、1 和 2 元素的个数，然后按照0、1、2的排序，重写当前数组。
> 你能想出一个仅使用常数空间的一趟扫描算法吗？

```java
//将0交换到开头，将2交换到末尾，但要注意如果当前位置为2，交换之后，nums[i]可能仍然为2，如果此时i++,可能得不到正确的结果
//所以当nums[i]==2时，需要不停的测试和交换
public void sortColors(int[] nums) {
        int N=nums.length;
        int p0=0,p2=N-1;
        for(int i=0;i<N;i++)
        {
            while(i<p2 && nums[i]==2)
            {
                int temp=nums[p2];
                nums[p2]=nums[i];
                nums[i]=temp;
                p2--;
            }
            if(nums[i]==0)
            {
                int temp=nums[p0];
                nums[p0]=nums[i];
                nums[i]=temp;
                p0++;
            }
        }
    }
```

