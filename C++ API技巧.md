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

### 4.[ C/C++ 取整函数ceil(),floor()](https://www.cnblogs.com/zjutlitao/p/3558218.html)

> 使用floor函数。floor(x)返回的是小于或等于x的最大整数。如：     

```cpp
floor(10.5) == 10    
floor(-10.5) == -11
```

> 使用ceil函数。ceil(x)返回的是大于x的最小整数。如：     

```cpp
ceil(10.5) == 11    
ceil(-10.5) ==-10
```

> floor()是向负无穷大舍入:

```cpp
floor(-10.5) == -11;
```

>
> ceil()是向正无穷大舍入:

```cpp
ceil(-10.5) == -10
```

> fix朝零方向取整，如:

```cpp
fix(-1.3)=-1; fix(1.3)=1;
```

>
> round四舍五入到最近的整数，如

```cpp
round(-1.3)=-1;round(-1.52)=-2;round(1.3)=1;round(1.52)=2
```

### 5.C++ advanced(), prev(),next()

> advance() 函数用于将迭代器前进（或者后退）指定长度的距离，其语法格式如下：

```cpp
void advance (InputIterator& it, Distance n);
```

> 其中 it 指的是目标迭代器，n 通常为一个整数。
>
> 注意，advance() 函数本身不会检测 it 迭代器移动 n 个位置的可行性，如果 it 迭代器的移动位置超出了合理范围，it 迭代器的指向将无法保证，此时使用 *it 将会导致程序崩溃。
>
> advance() 函数移动的是源迭代器。
>
> 例子:

```cpp
forward_list<int> mylist{1,2,3,4};
forward_list<int>::iterator it = mylist.begin();
advance(it, 2);
cout << "*it = " << *it;
*it = 3 		//结果
```

> prev 原意为“上一个”，但 prev() 的功能远比它的本意大得多，该函数可用来获取一个距离指定迭代器 n 个元素的迭代器。

```cpp
template <class BidirectionalIterator>
    BidirectionalIterator prev (BidirectionalIterator it, typename iterator_traits<BidirectionalIterator>::difference_type n = 1);
```

> 其中，it 为源迭代器，其类型只能为双向迭代器或者随机访问迭代器；n 为指定新迭代器距离 it 的距离，默认值为 1。该函数会返回一个距离 it 迭代器 n 个元素的新迭代器。
>
> 注意，当 n 为正数时，其返回的迭代器将位于 it 左侧；反之，当 n 为负数时，其返回的迭代器位于 it 右侧。

```cpp
std::list<int> mylist{ 1,2,3,4,5 };
std::list<int>::iterator it = mylist.end();
//获取一个距离 it 迭代器 2 个元素的迭代器，由于 2 为正数，newit 位于 it 左侧
auto newit = prev(it, 2);
cout << "prev(it, 2) = " << *newit << endl;
prev(it, 2) = 4			//结果
```

> next()函数和 prev 相反，next 原意为“下一个”，但其功能和 prev() 函数类似，即用来获取一个距离指定迭代器 n 个元素的迭代器

```cpp
template <class ForwardIterator>
    ForwardIterator next (ForwardIterator it, typename iterator_traits<ForwardIterator>::difference_type n = 1);
```

> 其中 it 为源迭代器，其类似可以为前向迭代器、双向迭代器以及随机访问迭代器；n 为指定新迭代器距离 it 的距离，默认值为 1。该函数会返回一个距离 it 迭代器 n 个元素的新迭代器。
>
> 需要注意的是，当 it 为前向迭代器时，n 只能为正数，该函数最终得到的新迭代器位于 it 右侧；当 it 为双向迭代器或者随机访问迭代器时，若 n 为正数，则得到的新迭代器位于 it 右侧，反之位于 it 左侧。

```cpp
 std::list<int> mylist{ 1,2,3,4,5 };
std::list<int>::iterator it = mylist.begin();
//获取一个距离 it 迭代器 2 个元素的迭代器，由于 2 为正数，newit 位于 it 右侧
auto newit = next(it, 2);
cout << "next(it, 2) = " << *newit << endl;
next(it, 2) = 3					//结果
```

