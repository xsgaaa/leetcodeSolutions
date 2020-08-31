### leetcode [488. 祖玛游戏](https://leetcode-cn.com/problems/zuma-game/)

```cpp
/*
	解法：深度优先搜索。
	这题本身有些问题，下面的代码可以通过OJ所有的测试用例。
*/
```

```cpp
int findMinStep(string board, string hand) {
        int arr[26];
        memset(arr,0,sizeof arr);		//注意，局部数组，一定要初始化
        for(auto &c:hand)   arr[c-'A']++;	//统计手中球的数量
        board+='#';							//确定终止符号
        int res=dfs(board,arr,false);
        return res==0x3f3f3f3f?-1:res;		
    }
private:
    int dfs(string board,int arr[],bool remove)
    {
        board=remove?removeStr(board):board;	//判断是否需要移除连续重复的球
        if(board.size()==1 && board[0]=='#')    return 0;	//递归终止条件
        int j=0;
        int res=0x3f3f3f3f;
        for(int i=0;i<board.size();i++)
        {//这个跟下面移除字符串的代码有些类似，利用双指针法
            if(board[i]==board[j])  continue;
            int put=3-(i-j);	//put为可以放置的个数
            if(put>=0 && arr[board[j]-'A']>=put)
            {
                arr[board[j]-'A']-=put;
                string next=board.substr(0,j)+board.substr(i,board.size()-i);
                res=min(res,dfs(next,arr,true)+put);	//重组成新的串，并制定要移除重复的球
                res=min(res,dfs(next,arr,false)+put);	//重组成新的串，并制定不要移除串中重复的球
                arr[board[j]-'A']+=put;
            }
            j=i;
        }
        return res;
    }
    string removeStr(string board)
    {
        int j=0;//利用双指针法来判断重复的区间的元素,j是左边界,i是右边界
        for(int i=0;i<board.size();i++)
        {
            if(board[j]==board[i])  continue;	//元素一致，继续
            if(i-j>=3)		//元素长度大于等于3可以进行移除，返回移除后的字符串
                return removeStr(board.substr(0,j)+board.substr(i,board.size()-i));
            j=i;	//如果连续区间的长度不足3，则把走边界进行切换
        }
        return board;
    }
```

