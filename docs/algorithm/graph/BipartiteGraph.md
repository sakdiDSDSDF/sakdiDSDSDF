---
2025年2月20日
---

# 二分图

二分图(Bipartite graph) 是一种特殊的图，可以将图里的所有点分为两个集合 $V1$ ， $V2$ ，这张图上的所有边都是一个点在 $V1$ 中 ，一个点在 $V2$ 中。

## 性质

如果两个集合种的点分别染成黑色和白色，二分图种的每一条边一定都是连接一个黑色点和一个白色点。即二分图中，每个点的相邻点一定都是颜色相反的。

二分图不存在长度为奇数的环。

可以通过 DFS 或 BFS 来判定二分图。

## 应用

二分图性质

[CF1949I](https://codeforces.com/contest/1949/problem/I)

这个就是去判定每个连通块是否是二分图。

```cpp
void solve()
{
    int n;
    cin>>n;
    vi x(n+1),y(n+1),r(n+1);
    for(int i=1;i<=n;i++)
        cin>>x[i]>>y[i]>>r[i];
    vector<vi>adj(n+1,vi());
    auto calc=[&](int x){
        return 1ll*x*x;
    };
    for(int i=1;i<=n;i++)
        for(int j=i+1;j<=n;j++){
            if(calc(x[i]-x[j])+calc(y[i]-y[j])==calc(r[i]+r[j])){
                adj[i].push_back(j);
                adj[j].push_back(i);
            }
        }
    vi s(n+1,-1);
    for(int i=1;i<=n;i++){
        if(s[i]!=-1) continue;
        bool ok=true;
        int x=0,y=0;
        auto dfs=[&](auto &&self,int u)->void{
            if(s[u]) x++;
            else y++;
            // cerr<<u<<'\n';
            for(auto v:adj[u]){
                if(s[v]!=-1){
                    if(s[v]==s[u]) ok=false;
                    continue;
                }
                s[v]=s[u]^1;
                self(self,v);
            }
        };
        s[i]=0;
        dfs(dfs,i);
        if(ok&&x!=y){
            cout<<"YES\n";
            return;
        }
    }
    cout<<"NO\n";
}
```

### 二分图最大匹配

从二分图里选出若干条边，每条边都不相交，且边的数量最多，就是二分图的最大匹配。

#### [P3386 【模板】二分图最大匹配 - 洛谷](https://www.luogu.com.cn/problem/P3386)

```cpp
void solve()
{
    int n,m,e;
    cin>>n>>m>>e;
    vector<vi>adj(n+1,vi());
    for(int i=1;i<=e;i++){
        int u,v;
        cin>>u>>v;
        adj[u].push_back(v);
    }
    vector<int>match(m+1);
    int ans=0;
    for(int i=1;i<=n;i++){
        vector<bool>sel(m+1);//记有没有被选过
        auto dfs=[&](auto &&self,int u)->bool{
            for(auto v:adj[u]){
                if(!sel[v]){
                    sel[v]=true;
                    if(!match[v]||self(self,match[v])){
                        match[v]=u;
                        return true;
                    }
                }
            }
            return false;
        };
        if(dfs(dfs,i))
            ans++;
    }
    cout<<ans<<'\n';
}
```

选取左边一个点，看能不能找到一个右侧的点和它匹配。如果已经匹配，则看能不能让它已匹配的点去尝试匹配别的点，如果可以匹配，那么直接答案+1。

#### [P1129 [ZJOI2007] 矩阵游戏](https://www.luogu.com.cn/problem/P1129)

同样是一道模板题，但是需要一些额外的思考，是一个蓝题。

> 这是我们算法课老师找的一道题。。。但那个时候其实没看出来也是跟二分图有关，看了下题解才知道。。

因为同一列的 $1$ , 我们并不能使他们分开，它们始终只能在一列上，同理，一行上的 $1$ ，它们始终只能在同一行。

所以我们最后要求对角线上全是 $1$ ， 我们只需要去调整行或者列，并且是一样的。

那么这个问题就转换成了，我们要把这 $n$ 行，每一行去匹配一个位置，由于我们需要对角线上全是 $1$ ， 所以我们每一行必须保证它移动之后，对角线上有 $1$ ， 即至少有一个 $1$ 的列数等于它所在的行数。所以就转换成了一个二分图匹配问题。

```cpp
void ChatGptDeepSeek()
{
    // 如果有多个1在同一行
    // 我们是没有办法让他们不在同一行的
    // 因为我们每次只能移动一整行 或者去调整列
    // 所以我们只需要去调整行或者列 因为一列上的多个的1 我们也没办法分开他们
    int n;
    cin >> n;
    vector<vector<int>> a(n + 1, vector<int>(n + 1));
    vector<vector<int>> adj(n + 1, vector<int>());
    for (int i = 1; i <= n; i++)
        for (int j = 1; j <= n; j++) {
            cin >> a[i][j];
            if (a[i][j]) {
                adj[i].push_back(j);
            }
        }
    vector<int> matched(n + 1);
    vector<bool> sel(n + 1);
    auto dfs = [&](auto&& self, int u) -> bool {
        for (auto v : adj[u]) {
            if (matched[v] && !sel[v]) {
                sel[v] = true;
                if (self(self, matched[v])) {
                    matched[v] = u;
                    return true;
                }
            } else if (!sel[v]) {
                sel[v] = true;
                matched[v] = u;
                return true;
            }
        }
        return false;
    };
    for (int i = 1; i <= n; i++) {
        sel = vector<bool>(n + 1);
        if (!dfs(dfs, i)) {
            cout << "No\n";
            return;
        }
    }
    cout << "Yes\n";
}
```

前两天才补的，写得有点烂hhh。

### ...