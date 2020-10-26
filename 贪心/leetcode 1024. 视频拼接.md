### leetcode [1024. 视频拼接](https://leetcode-cn.com/problems/video-stitching/)

> 你将会获得一系列视频片段，这些片段来自于一项持续时长为 T 秒的体育赛事。这些片段可能有所重叠，也可能长度不一。
>
> 视频片段 clips[i] 都用区间进行表示：开始于 clips[i][0] 并于 clips[i][1] 结束。我们甚至可以对这些片段自由地再剪辑，例如片段 [0, 7] 可以剪切成 [0, 1] + [1, 3] + [3, 7] 三部分。
>
> 我们需要将这些片段进行再剪辑，并将剪辑后的内容拼接成覆盖整个运动过程的片段（[0, T]）。返回所需片段的最小数目，如果无法完成该任务，则返回 -1 。
>

```cpp
/*
	解法：贪心算法。
	在clips[i][0]小于left的情况下，不断扩展right的值，并选择的最大的right进行下一次的扩展。
*/
int videoStitching(vector<vector<int>>& clips, int T) {
        sort(clips.begin(),clips.end());
        int left=0,cnt=0,i=0,right=0;
        int N=clips.size();
        while(left<T)
        {
            int cur=i;
            while(i<N && clips[i][0]<=left)
            {
                right=max(right,clips[i][1]);
                i++;
            }
            //注意边界条件，当i<N且i经过循环没有发生变化。或者i到达最右边了，仍然无法达到T,则返回-1。
            if(cur==i || (i==N && right<T)) return -1; 
            cnt++;
            left=right;
        }
        return cnt;
    }
```

