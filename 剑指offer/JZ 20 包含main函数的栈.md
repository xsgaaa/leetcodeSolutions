### [JZ 20 包含main函数的栈](https://www.nowcoder.com/practice/4c776177d2c04c2494f2555c9fcc1e49?tpId=13&&tqId=11173&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)

> ## 题目描述
>
> 定义栈的数据结构，请在该类型中实现一个能够得到栈中所含最小元素的min函数（时间复杂度应为O（1））。

```cpp
//一个普通栈+一个单调递减栈
stack<int> st;
stack<int> minval;
void push(int value) {
	st.push(value);
	if(minval.empty() || value<=minval.top())
	minval.push(value);
}
void pop() {
	int tmp=st.top();
	st.pop();
	if(tmp==minval.top())minval.pop();
}
int top() {
	return st.top();
}
int min() {
	return minval.top();
}
```

