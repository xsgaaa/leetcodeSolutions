### Leetcode [406. 根据身高重建队列](https://leetcode-cn.com/problems/queue-reconstruction-by-height/)

```cpp
/*
	解法：利用插入排序的思想。
	既然要考虑前面比当前数大的个数，干脆将整个数组按照第一关键字h降序排列，第二关键字k升序排列。
	之后将数组元素依次插入到合适的位置。这样做的好处是，插入当前的元素(h,k)时，所有比h大的元素都有了
	合适的位置。
*/
vector<vector<int>> reconstructQueue(vector<vector<int>>& people) {
        sort(people.begin(),people.end(),[](const vector<int> & a,const vector<int> &b){
            return a[0]==b[0]?a[1]<b[1]:a[0]>b[0];
        });
        vector<vector<int>> ans;
        for(auto &p:people)
        {
            ans.insert(ans.begin()+p[1],p);
        }
        return ans;
    }
```

