### leetcode [381. O(1) 时间插入、删除和获取随机元素 - 允许重复](https://leetcode-cn.com/problems/insert-delete-getrandom-o1-duplicates-allowed/)

解法：根据题意，要想实现前两个需求，必须要用到哈希表。

要想实现第三个需求，必须要用到数组。

关键在于如何将两者建立联系。这里采用在哈希中用集合存数组的索引的方式。

每回删除元素，将其与最后一个元素交换，并修改最后一个元素的索引值。然后将待删除的元素的索引和值从数组中删除即可。

```cpp
unordered_map<int,unordered_set<int>> mp;
    vector<int> v;
    RandomizedCollection() {
        srand(time(0));
    }
    bool insert(int val) {
        v.push_back(val);
        bool flag=true;
        if(mp[val].size())
            flag=false;
        mp[val].insert(v.size()-1);     //插入索引
        return flag;
    }
    bool remove(int val) {
        if(mp[val].empty())    //不包含该元素，返回false
            return false;
        int idx=*(mp[val].begin());     //获取val的索引
        mp[val].erase(idx);             //删除索引
        int e=v.back();                 //获取数组最后一个值
        if(idx==v.size()-1)
        {
            v.pop_back();
            return true;
        }
        swap(v[idx],v[v.size()-1]);    //交换到最后一个元素
        mp[e].erase(v.size()-1);     //删除索引
        mp[e].insert(idx);  
        v.pop_back();      
        return true;
    }
    int getRandom() {
        int ra=rand()%v.size();
        return v[ra];
    }
```

