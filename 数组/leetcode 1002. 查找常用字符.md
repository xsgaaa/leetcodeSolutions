### leetcode [1002. 查找常用字符](https://leetcode-cn.com/problems/find-common-characters/)

> 给定仅有小写字母组成的字符串数组 A，返回列表中的每个字符串中都显示的全部字符（包括重复字符）组成的列表。例如，如果一个字符在每个字符串中出现 3 次，但不是 4 次，则需要在最终答案中包含该字符 3 次。
>
> 你可以按任意顺序返回答案。
>
>  
>
> 示例 1：
>
> 输入：["bella","label","roller"]
> 输出：["e","l","l"]
> 示例 2：
>
> 输入：["cool","lock","cook"]
> 输出：["c","o"]

```cpp
/*
	解法:统计每个单词中26个字符出现的频率，然后求其最小值作为个数即可。
*/
vector<string> commonChars(vector<string>& A) {
        int N=A.size();
        int cnt[N][26];
        memset(cnt,0,sizeof cnt);

        for(int i=0;i<N;i++)
        {
            for(int j=0;j<A[i].size();j++)
            {
                cnt[i][A[i][j]-'a']++;
            }
        }
        vector<string> res;
        for(int i=0;i<26;i++)
        {
            int minv=INT_MAX;
            for(int j=0;j<N;j++)
            {
               minv=min(minv,cnt[j][i]); 
            }
            for(int j=0;j<minv;j++)
            {
                res.emplace_back(1,'a'+i);
            }
        }
        return res;
    }
```

