### leetcode [剑指 Offer 04. 二维数组中的查找](https://leetcode-cn.com/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof/)

```cpp
/*
	解法：利用数组的特性，采用双指针。
*/
```

```cpp
class Solution {
public:
    bool Find(int target, vector<vector<int> > array) {
        if(array.empty() || array[0].empty())    return false;
        int N=array.size();
        int M=array[0].size();
        int row=0,col=N-1;
        while(row<N && col>=0)
        {
            if(target==array[row][col])
                return true;
            else if(target<array[row][col])
                col--;
            else 
                row++;
        }
        return false;
    }
};
```

