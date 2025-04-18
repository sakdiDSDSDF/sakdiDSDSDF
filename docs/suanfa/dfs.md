# 深度优先搜索

采用递归＋回溯的方式实现的算法

```c++
void dfs(当前状态) {
    if (到达边界条件) {
        处理当前答案;
        return;
    }

    for (所有可能的选择) {
        做出选择;
        dfs(下一层状态);
        撤销选择; // 回溯
    }
}

```

## https://www.luogu.com.cn/problem/P1036

对于这个题目，我们是不需要专门写回溯那一步的，因为我们每次调用dfs函数的时候把改变的值作为参数传入了，所以说不需要手动写回溯步骤

```c++
/*
   (｡･ω･｡)ﾉ♡  我喜欢斯卡蒂啊，我喜欢流萤啊
*/
#include<bits/stdc++.h>
#define INF 1e18
#define pb push_back
#define ll long long
using namespace std;
int n,k,ans=0;
void dfs(int pos,int sum,int num,vector<int> x){
    if(num==k){
        //if(sum<2) return;
        for(int i=2;i*i<=sum;i++){
            if(sum%i==0) return;
        }
        ans++;
        return;
    }
    for(int j=pos+1;j<=n;j++){
        dfs(j,sum+x[j],num+1,x);
    }
}
int main(){
    cin>>n>>k;
    vector<int> x(n+1);
    for(int i=1;i<=n;i++){
        cin>>x[i];
    }
    dfs(0,0,0,x);
    cout<<ans<<endl;
    return 0;
}
```

## https://www.luogu.com.cn/problem/P1219

这道题目要写回溯是因为参数里不包含被改变的变量，所以我们需要手动回溯以达到能够让dfs返回上一级继续寻找其他可能性

```c++
/*
   (｡･ω･｡)ﾉ♡  我喜欢斯卡蒂啊，我喜欢流萤啊
*/
#include<bits/stdc++.h>
#define INF 1e18
#define pb push_back
#define ll long long
using namespace std;
vector<int> lie(169),shun(169),ni(169),ans(169);
int n;
int check=1,sum=0;
void change(int x,int y,int num){
    ans[x]=y;
    lie[y]=num;
    shun[x+y]=num;
    ni[(x-y)+n]=num;
}
void dfs(int i,int n){
    if(i>n){
        if(check<=3){
            for(int c=1;c<=n;c++){
                cout<<ans[c]<<" ";
            }
            cout<<endl;
            check++;
        }
        sum++;
        return ;
    }
    for(int j=1;j<=n;j++){
        if(lie[j]||shun[i+j]||ni[(i-j)+n]) continue;
        change(i,j,1);
        dfs(i+1,n);
        change(i,j,0);
    }
}
int main(){
    cin>>n;
    dfs(1,n);
    cout<<sum<<endl;
    return 0;
}
```

