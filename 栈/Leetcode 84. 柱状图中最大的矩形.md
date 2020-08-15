### Leetcode 84. 柱状图中最大的矩形

解法：利用单调栈。构造一个单调递增的栈，记录数组元素的下标。当数组中的当前元素比栈顶的元素要小时，表明其左边的矩形的最大值可以确定下来了。

此外，注意边界问题的出现。此题用了两个哨兵在`heights`数组最前面和最后面分别加了个0。

![image-20200815143114590](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200815143114590.png)

```cpp
int largestRectangleArea(vector<int>& heights) {
        int N=heights.size();
        heights.insert(heights.begin(),0);
        heights.push_back(0);
        int res=0;
        stack<int> st;
        for(int i=0;i<N+2;i++)
        {
            while(!st.empty() && heights[st.top()]>heights[i])
            {
                int cur=st.top();st.pop();
                res=max(res,(i-st.top()-1)*heights[cur]);
            }
            st.push(i);
        }
        return res;
    }
```



