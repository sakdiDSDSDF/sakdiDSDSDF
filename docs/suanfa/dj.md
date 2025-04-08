# 迪杰斯特拉

核心思想就是每次选择当前能选择的权值最小的点，然后找它的邻接点，从邻接点里接着找最小的，循环下去，直到所有点的最小值都已经确立

https://atcoder.jp/contests/abc362/tasks/abc362_d

```c++
#include<bits/stdc++.h>
#define INF 1061109567
#define pb push_back
#define ll long long
using namespace std;
int main(){
    int n,m;
    cin>>n>>m;
    vector<ll> a(n);
    for(int i=0;i<n;i++){
        cin>>a[i];
    }
    vector<ll> b(m),u(m),v(m);
    for(int i=0;i<m;i++){
        cin>>u[i]>>v[i]>>b[i];
        u[i]--,v[i]--;
    }
    vector<vector<pair<ll,ll>>> table(n);
    for(int i=0;i<m;i++){
        table[u[i]].pb({v[i],b[i]});
        table[v[i]].pb({u[i],b[i]});
    }
    priority_queue<pair<ll,ll>,vector<pair<ll,ll>>,greater<pair<ll,ll>>> pq;
    vector<ll> dist(n,1e18);
    dist[0]=a[0];
    pq.push({dist[0],0});
    while(!pq.empty()){
        auto[d,u]=pq.top();
        pq.pop();
        if(d>dist[u]) continue;
        for(auto x:table[u]){
            ll v=x.first;
            ll newdis=x.second+dist[u]+a[v];
            if(newdis<dist[v]){
                dist[v]=newdis;
                pq.push({newdis,v});
            }
        }
    }
    for(int i=1;i<n;i++){
        cout<<dist[i]<<" ";
    }
    cout<<endl;
    return 0;
}
```

https://www.luogu.com.cn/problem/P4779

https://www.luogu.com.cn/problem/P3905

迪杰斯特拉算法注意事项

第一是对于无向图，我们在邻接表存图的时候要双向存入，1到2存一遍，2到1也要存一遍

第二是在创立dist数组存答案的时候，要先将其内的元素赋值为一个很大的数，再对起点进行单独赋值，如果有点权，起点赋值为点权，否则为0

第三是在算法的核心部分当现在所选择的点是最小值进入找邻边和邻点的时候，到邻接点的权值在赋值时加的是之前路径的权值和，即dist[u]