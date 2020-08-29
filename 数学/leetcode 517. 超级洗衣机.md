### leetcode [517. 超级洗衣机](https://leetcode-cn.com/problems/super-washing-machines/)

```cpp
/*
	解法：数学。
	先计算总和，判断总和是不是n的倍数。
	然后遍历数组，用当前值减去平均值，之后进行两步操作：
		(1)累加上述值，并记录到目前为止累加得到的值的绝对值的最大值。
			如果值为负，表示累加到当前位置，前面总共缺少的衣服数量，这必然需要后面将衣服移到前面来。
			如果值为正，表示累加到当前位置，前面总共多余的衣服数量，这必然需要前面将衣服移到后面去。
		(2)记录到目前为止上述值的最大值。
			表示某个洗衣机的衣服要移动的最大次数
		将上述两步得到的最大值取最值即可。
*/
```

```cpp
int findMinMoves(vector<int>& machines) {
        vector<int> &m=machines;
        int n=m.size();
        int sum=accumulate(m.begin(),m.end(),0);
        if(sum%n!=0)    return -1;
        int avg=sum/n;
        int maxSum=0;int res=0;
        sum=0;
        for(auto &i:m)
        {
            i-=avg;
            sum+=i;
            maxSum=max(maxSum,abs(sum));
            res=max(res,i);
        }
        return max(res,maxSum);
    }
```

