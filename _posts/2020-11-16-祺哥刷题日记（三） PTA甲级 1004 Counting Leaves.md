# 题目
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201116231823116.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mzg0OTc2Mw==,size_16,color_FFFFFF,t_70#pic_center)
题目很长，大致的意思就是输入家谱信息，输出每代人中没有后代的人的个数。
# 思路
看到题目中第一行的**tree**，就可以很自然地想到使用树来存储家谱，相关的算法也不过就是与树相关的算法。
找到每一代没有后代的人数，首先要知道每个人的代数，也就是在家谱树中所在的层数，所以可以使用dfs算法解决问题。

# 代码

```cpp
#include<iostream>
#include<vector>
#include<algorithm>

using namespace std;

typedef struct people{
    int level = 0;
    vector<int> children;
}people;
vector<people> family(100);    //存储家谱
vector<int> leaves(100);
int maxLevel = 0;

int transID2Int(string ID){
    return (ID[0] - '0') * 10 + (ID[1] - '0') - 1;
}

void dfs(int p, int depth){
    if(family[p].children.size() == 0){
        maxLevel = max(depth,maxLevel);
        leaves[depth] ++;
        return;
    }
    else{
        family[p].level += depth;
        depth ++;
        for(int i = 0; i < family[p].children.size(); i++){
            dfs(family[p].children[i],depth);
        }
    }
}
int main(){
    int n, m, k;
    string parent, child;
    cin >> n >> m;
    //建立家谱
    for(int i = 0; i < m; i++){
        cin >> parent >> k;
        for(int j = 0; j < k; j++){
            cin >> child;
            int childNum = transID2Int(child);
            family[transID2Int(parent)].children.push_back(childNum);
        }
    }
    dfs(0,0);
    
    cout<<leaves[0];
    for(int i=1;i<=maxLevel;i++){
        cout<<" "<<leaves[i];
    }
    
    return 0;
}
```