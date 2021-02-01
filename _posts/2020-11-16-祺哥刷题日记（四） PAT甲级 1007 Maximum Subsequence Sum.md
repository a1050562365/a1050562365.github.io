# 题目
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201116232456524.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mzg0OTc2Mw==,size_16,color_FFFFFF,t_70#pic_center)
# 思路
之前在LeetCode曾经做过，一道很经典的dp题目，主要思路就是用一个数组存放以第i个元素结尾的最大子序列。
状态转移方程表示如下：
$$dp[i] = \begin{cases}
	num[i], dp[i-1] < 0\\
	dp[i-1]+num[i], else
	\end{cases}$$
# 代码

```cpp
#include<iostream>

using namespace std;

int main(){
    int k = 0;
    cin >> k;
    int num[k] = {0};
    int sum[k] = {0};   //以第k位置为结尾的和最大的子串
    int res = -100000;
    int max_index = -1;
    for(int i = 0; i < k; i++){
        cin >> num[i];
    }
    sum[0] = num[0];
    res = sum[0];
    if(k == 1 && res > 0){
        cout << res << " " << res << " " << res;
        return 0;
    }
    for(int i = 1; i < k; i++){
        if(sum[i - 1] < 0){
            sum[i] = num[i];
        } else{
            sum[i] = sum[i - 1] + num[i];
        }
        if(res < sum[i]){
            res = sum[i];
            max_index = i;
        }
    }
    if(max_index == -1){
        cout << 0 << " " << num[0] << " " << num[k - 1];
        return 0;
    }
    cout << res <<" ";
    for(int i = max_index; i >= 0; i--){
        res -= num[i];
        if(res == 0){
            cout << num[i] <<" ";
            break;
        }
    }
    cout << num[max_index];
    return 0;
}
```
# 注意
这道题还是有一些坑在里面的

 1. 输出的是元素，不是元素下标，憨憨看错题。
 2. 要注意边界情况，比如只有一个元素、所有元素都是负数等等，当时因为考虑不够完善导致最终代码东拼西补，非常臃肿，之后有时间会整理好更整洁的代码。