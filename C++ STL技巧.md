## STL技巧

### 1.fill()函数

> 可以把数组或容器中的某一段区间赋为某个相同的值。与memset有近似之处.
> 例如：

```
    int a[3] = {1,2,3};
	fill(a,a+3,3);
```

### 2.string中的find()函数

> (1) string中find()返回值是字母在母串中的位置（下标记录），如果没有找到，那么会返回一个特别的标记npos。（返回值可以看成是一个int型的数）

```cpp
string s("1a2b3c4d5e6f7jkg8h9i1a2b3c4d5e6f7g8ha9i");
string flag;
string::size_type position;
//find 函数 返回jk 在s 中的下标位置
position = s.find("jk");
if (position != s.npos)  //如果没找到，返回一个特别的标志c++中用npos表示，我这里npos取值是4294967295，
{
    printf("position is : %d\n" ,position);
}
else
{
    printf("Not found the flag\n");
}
```

> (2)返回子串出现在母串中的首次出现的位置，和最后一次出现的位置。

```cpp
flag = "c";
position = s.find_first_of(flag);
printf("s.find_first_of(flag) is :%d\n",position);
position = s.find_last_of(flag);
printf("s.find_last_of(flag) is :%d\n",position);
```

> (3) 查找某一给定位置后的子串的位置

**这个用的特别多，配合第五条，拆分整个字符串。**

```cpp
//从字符串s 下标5开始，查找字符串b ,返回b 在s 中的下标
position=s.find("b",5);
cout<<"s.find(b,5) is : "<<position<<endl;
```

> (4). 查找所有子串在母串中出现的位置

```cpp
flag="a";
position=0;
int i=1;
while((position=s.find(flag,position))!=string::npos)
{
    cout<<"position  "<<i<<" : "<<position<<endl;
    position++;
    i++;
}
```

> (5).反向查找子串在母串中出现的位置，通常我们可以这样来使用，当正向查找与反向查找得到的位置不相同说明子串不唯一。

```cpp
//反向查找，flag 在s 中最后出现的位置
flag="3";
position=s.rfind (flag);
printf("s.rfind (flag) :%d\n",position);
```

### 3.string中的substr()函数

> 函数定义如下：

```cpp
string substr (size_t pos = 0, size_t len = npos) const;
```

通常都是两个参数同时用，其实后面一个参数可以省略不写。表示直接获取`pos`到字符串末尾的子串。

