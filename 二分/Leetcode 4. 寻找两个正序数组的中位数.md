### Leetcode 4. 寻找两个正序数组的中位数

解法：二分法。这题是道比较难的题，边界情况特别复杂。

参考：https://leetcode-cn.com/problems/median-of-two-sorted-arrays/solution/he-bing-yi-hou-zhao-gui-bing-guo-cheng-zhong-zhao-/

![img](https://pic.leetcode-cn.com/50453678d4e9900786fda5a38f43ee5bf73ccd2b8d4152ec499d16c7cc661a00-4-binary-search-1.png)

![img](https://pic.leetcode-cn.com/dadba9cebeb89aee4f269c6ab613268060444c6be123c9195d0f26b5e433f969-4-binary-search-2.png)

![img](https://pic.leetcode-cn.com/2979a96c5172d7e5852b0940dd4414f8ba2b9d9666f9c011b324dd7c199edfeb-4-binary-search-3.png)

![img](https://pic.leetcode-cn.com/8b27f6804457aca51c38e21f0a19e22989c038b49165b30e09313cf5d40065aa-4-binary-search-4.png)

![img](https://pic.leetcode-cn.com/4431c982dc7104b7b03ec601ac1be2cedf5fb783f7bb32dc718dfb6e5d0b3194-4-binary-search-5.png)

![img](https://pic.leetcode-cn.com/8b4b5f880cd8d04c930537b690f09f8dae74f2b5e3397c605353ca9e0fa5472d-4-binary-search-6.png)

![img](https://pic.leetcode-cn.com/cc80aadda1ba02f93e5da4ae8b1194fb03d13f8a8ac7b582714a214c6d6698d2-4-binary-search-7.png)

![img](https://pic.leetcode-cn.com/a2b3f28158c773944c5d04eb22657c64fce25ad6da4a8a31eabd359e295f7765-4-binary-search-8.png)

![img](https://pic.leetcode-cn.com/00da76675cca8522e09f6cf1d35c1738d898bec1d509bc206454c6e09e7ac7ee-4-binary-search-9.png)

![img](https://pic.leetcode-cn.com/24fdacd8a4b0ba9db7ae9537bda02cb9e91f9aa25c95377e123fb8d4c90e3581-4-binary-search-10.png)

```cpp
double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        int N=nums1.size(),M=nums2.size();
        //必须把长度较大的数组放在后面
        //nums1=[1],nums2=[]时，如果nums1在前会出现错误
        if(N>M) return findMedianSortedArrays(nums2,nums1);
        int l=0,r=N;
        int mid=(M+N+1)/2;
        while(l<=r)
        {
            //m1和m2将数组划分成两部分
            //当（M+N）为奇数时，左边长度=右边长度+1
            //当为偶数时，左边长度=右边长度
            int m1=l+(r-l)/2;
            int m2=mid-m1;
            //防止边界溢出
            int num1LeftMax=m1==0?INT_MIN:nums1[m1-1];
            int num1RightMin=m1==N?INT_MAX:nums1[m1];
            int num2LeftMax=m2==0?INT_MIN:nums2[m2-1];
            int num2RightMin=m2==M?INT_MAX:nums2[m2];

            if(num1LeftMax<=num2RightMin && num2LeftMax<=num1RightMin)
            {
                if((M+N)%2==1)
                    return max(num1LeftMax,num2LeftMax);
                else
                    return (max(num1LeftMax,num2LeftMax)+min(num1RightMin,num2RightMin))/2.0;
            }
            else if(num1LeftMax>num2RightMin)
                r=m1-1;//nums1左边较大，减小
            else
                l=m1+1;//nums1右边较小，增大
        }
        return -1;
    }
```

