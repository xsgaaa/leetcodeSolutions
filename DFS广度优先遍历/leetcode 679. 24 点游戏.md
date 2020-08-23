### leetcode [679. 24 点游戏](https://leetcode-cn.com/problems/24-game/)

解法：利用双端队列+`DFS`。下图是双端队列模拟的图，假设队列中此时有{a,b,c,d}四个元素，那么一轮go计算之后，数据顺序不会变化，而且尝试了所有的可能。

![image-20200822090548615](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200822090548615.png)

```cpp
 bool judgePoint24(vector<int>& nums) {
        deque<double> q;
        //插入双端队列
        for(int &n :nums)   q.push_back(n);
        return go(q);
    }
private:
    bool go(deque<double> & q)
    {
        int N=q.size();
        if(N==1)
        {//递归终止条件，判断是否等于24
            return fabs(q.front()-24)<eps;
        }
        //接下来的两层循环保证了计算前后数据的顺序保持不变
        //而且尝试了数据中元素的所有的肯能性
        for(int i=0;i<N;i++)
        {//先弹出来一个元素
            double a=q.front();q.pop_front();
            for(int j=1;j<N;j++)
            {//再弹出来一个元素
                double b= q.front();q.pop_front();
                if(gen(q,a+b) || gen(q,a-b) || gen(q,a*b)|| (b?gen(q,a/b):false))
                    return true;//只要有一个成功就返回true
                q.push_back(b); //插入到队尾
            }
            q.push_back(a);     //插入到队尾
        }
        return false;
    }
    bool gen(deque<double> &q, double v)
    {
        q.push_back(v);//将go中计算的结果保存在队列中
        bool flag=go(q);    //计算下一轮元素减少之后的结果
        q.pop_back();   //由于顺序没有变化，弹出
        return flag;
    }
    double eps=1e-5;    //判断浮点数是否相同的标志
```



### 

