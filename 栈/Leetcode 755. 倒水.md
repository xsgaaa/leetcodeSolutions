### Leetcode 755. 倒水

解法： 单调栈。

![image-20200817154313885](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200817154313885.png)

```cpp
//利用单调栈的思想
//首先向左找到递减序列。然后向右找到最右边的和递减序列末位置相同的元素，如果其索引不能等于K,则高度加一，继续。
//如果上一步没有成功，向右找一个递减序列。然后再向左找与递减序列末尾相同的元素的值，找到最左边的那个，将其索引对应的位置加1即可.
//原理可见上图。
```



```cpp
vector<int> pourWater(vector<int>& heights, int V, int K) {
        int N=heights.size();
        while(V--)
        {
            int j=K;
            while(j-1>=0 && heights[j]>=heights[j-1]) j--;
            while(j<K && heights[j]==heights[j+1])  j++;
            if(j!=K)
            {
                heights[j]++;
                continue;
            }
            j=K;
            while(j+1<N && heights[j]>=heights[j+1]) j++;
            while(j>K && heights[j]==heights[j-1]) j--;
            heights[j]++;
        }
        return heights;
    }
```



