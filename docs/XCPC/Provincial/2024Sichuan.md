> 2025-03-01 VP
>
> 这是我这学期第一次打到团队赛，也是今年第一次。另外两个小伙伴应该是以前从来没打过团队赛。打了三小时左右，但1时17分之后，就没有AC过了。还行啦，慢慢来，先一周一次团队赛保持下感觉好了。

# 2024四川省大学生程序设计竞赛

比赛链接: https://codeforces.com/gym/105222

榜单链接: https://board.xcpcio.com/provincial-contest%2F2024%2Fsichuan?group=official

赛时只通过了三题： E H L

H 可能稍微要推一会，E 单纯是题目描述非常迷惑。如果没有理解问题，感觉也是十多分钟能AC的。L 就排个序就行。。。这次真就只签了个到。后面的写不了了。

## E

要用 L 形来填满网格。但是并非填满。它题目，我们明明看着是如果还剩一个格子没有被覆盖，且没有覆盖的格子在第一行第 $m$ 列，那么这个也是一个合法的方案。但是实际上，说的是必须空一个格子不被覆盖，且必须在第  $1$ 行第 $m$ 列空着。

那么就很好判断了。直接就检查是不是三个一组，是不是每个格子都被覆盖。

幸好有样例第二个，不然真看不出来。

```cpp
constexpr int N = 500*500;
int cnt[N+1];

void solve()
{
    int n,m;
    cin>>n>>m;
    vector<string>s(n);
    for(int i=0;i<n;i++){
        cin>>s[i];
    }
    vector<vector<int>>C(n+1,vector<int>(m+1));
    int tot=0;
    for(int i=0;i<n;i++)
        for(int j=0;j<m;j++){
            if(s[i][j]=='C'){
                C[i][j]=++tot;
                cnt[tot]=0;
                if(i-1>=0&&s[i-1][j]=='D'){
                    C[i-1][j]=tot;
                }
                if(i+1<n&&s[i+1][j]=='U'){
                    C[i+1][j]=tot;
                }
                if(j-1>=0&&s[i][j-1]=='R'){
                    C[i][j-1]=tot;
                }
                if(j+1<m&&s[i][j+1]=='L'){
                    C[i][j+1]=tot;
                }
            }
        }
    // cout<<'\n';
    for(int i=0;i<n;i++)
        for(int j=0;j<m;j++){
            // cout<<C[i][j]<<" \n"[j+1==m];
            cnt[C[i][j]]++;
        }
    int all=0;
    for(int i=1;i<=tot;i++){
        // cerr<<cnt[i]<< '\n';
        all+=cnt[i];
        if(cnt[i]!=3){
            cout<<"No\n";
            return;
        }
    }
    // cerr<<all<<'\n';
    // if(all==n*m){
    //     cout<<"Yes\n";
    // }else 
    if(all==n*m-1&&s[0][m-1]=='.')
        cout<<"Yes\n";
    else
        cout<<"No\n";
}
```

## H

稍微推一下前面几个啊，然后就可以 guess 了，找规律。

```
//1 G ,1
//2 G ,2
//3 Y ,1
//4 G ,2
//5 G ,3 , 3 Y , 1 G
//6 Y ,2
//7 G ,3
//8 G ,4 
//9 Y ,3 , 7 Y , 3
//10 G
//11 G
```

这是我们推的，就是 $n$ 为多少，然后谁能赢，能拿到多少个石头。

写这么几个大概就能看出来，一定是可以直接确定谁能赢的。两个人都希望能拿走尽可能多的石头，所以如果你怎么选都是输，那肯定就是拿 2 个。

前面推的就是，显然 1 和 2 个石头时，先手必赢。如果是 3 个石头，那么先手的人一定会把他转换成 2 或 1，且另一个人先手，于是变成另一个人的必胜状态。所以就多推几个就可以猜啦。

```cpp
void solve()
{
    long long n;
    cin>>n;
    long long ans=(n-1)/3+1;
    if(n%3==0){
        cout<<"1 ";
        cout<<ans<<'\n';
    }else{
        cout<<"0 ";
        if(n%3==2) cout<<ans+1<<'\n';
        else cout<<ans<<'\n';
    }
}
```

## L

这个就是很签到啦。

就看把哪个放到第一个锅，哪个放第二个锅。

然后按值排序输出下标即可。

```cpp
void solve()
{
    int n;
    cin >> n;
    vector<pair<int, int>> v1, v2;
    for (int i = 1; i <= n; i++) {
        int a, b, c, d;
        cin >> a >> b >> c >> d;
        if (c == d) {
            if (a < b) {
                v1.push_back({ a, i });
            } else {
                v2.push_back({ b, i });
            }
        } else if (c)
            v1.push_back({ a, i });
        else
            v2.push_back({ b, i });
    }
    sort(v1.begin(),v1.end(),[](pair<int,int>x,pair<int,int>y){
        return x.first<y.first;
    });
    sort(v2.begin(),v2.end(),[](pair<int,int>x,pair<int,int>y){
        return x.first<y.first;
    });
    cout<<v1.size()<<' ';
    for(auto [_,i]:v1)
        cout<<i<<" ";
    cout<<'\n';
    cout<<v2.size()<<' ';
    for(auto [_,i]:v2)
        cout<<i<<" ";
}
```

