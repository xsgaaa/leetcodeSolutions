### leetcode [782. 变为棋盘](https://leetcode-cn.com/problems/transform-to-chessboard/)

```cpp
解法：首先统计四个角的元素相异或的结果，说实话，这个真看不出来。
rowSum,colSum分别用来统计第0行和第0列中1的数量，如果1的数量不满足要求，则返回-1。
rowSwap，colSwap分别用来表示变成010101...这种排列所要变换的次数。
当N为奇数时，由于交换一次需要消耗两个次数。故次数需要为偶数。
当N为奇数时，可以有两种变换情况，取最小值。
最后再对rowSwap和colSwap相加取均值即为最终结果。
```

```cpp
int movesToChessboard(vector<vector<int>>& board) {
        int N=board.size();
        for(int i=0;i<N;i++)
        {
            for(int j=0;j<N;j++)
            {   //以[0,0]为左上角的四边形的四个顶点要么是四个0，要么是4个1，要么是两个0，或者两个1
                //其异或结果必定为0
                if(board[0][0]^board[0][j]^board[i][0]^board[i][j]) return -1;
            }
        }
        int rowSum=0,colSum=0,rowSwap=0,colSwap=0;
        for(int i=0;i<N;i++)
        {
            rowSum+=board[0][i];    //计算第0行的1的个数
            colSum+=board[i][0];    //计算第0列1的个数
            rowSwap+=board[i][0]==i%2;  //统计第0列错位的个数
            colSwap+=board[0][i]==i%2;  //计算第0行错位的个数
        }
        //如果N为奇数，那么1的数量为N/2或者(N+1)/2;如果N为偶数，那么1的数量必为N/2
        //这样才能满足相间的要求
        if(N/2>rowSum || rowSum>(N+1)/2)   return -1;
        if(N/2>colSum || colSum>(N+1)/2)   return -1;

        if(N%2)
        {//N为奇数，由于每次交换会改变两个错位
            if(rowSwap%2)//所以当为奇数时，需要转换成偶数，才能满足题目要求
                rowSwap=N-rowSwap;
            if(colSwap%2)//同理
                colSwap=N-colSwap;
        }
        else
        {//N为偶数，有两种棋盘：010101 或 101010。
            rowSwap=min(N-rowSwap,rowSwap);//计算变为两种棋盘的可能性种最小的那一个
            colSwap=min(N-colSwap,colSwap);
        }
        return (rowSwap+colSwap)/2;
    }
```

