### leetcode [36. 有效的数独](https://leetcode-cn.com/problems/valid-sudoku/)

```cpp
/*
	解法：利用bisset位运算。
*/
```

```cpp
bool isValidSudoku(vector<vector<char>>& board) {
        bitset<9> rows[9],cols[9],mat[9];
        for(int i=0;i<9;i++)
        {
            for(int j=0;j<9;j++)
            {
                if(!isdigit(board[i][j]))   continue;

                int num=board[i][j]-'0';
                //验证行
                if(rows[i][num]==1)  return false;
                else rows[i][num]=1;
                //验证列
                if(cols[j][num]==1) return false;
                else cols[j][num]=1;

                int a1=i/3;
                int a2=j/3;
                //验证3*3矩阵
                if(mat[a1*3+a2][num]==1)    return false;
                else mat[a1*3+a2][num]=1;
            }
        }
        return true;
    }
```

