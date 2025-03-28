## 对拍

> 2025-03-28
>
> 可能主要供我自己复制，经常需要对拍的时候再去之前用过的地方复制，不如早点传线上，再弄个 `snippets` ，之前弄过好几个，但都没了。最近得都存着。

只是放一下我的对拍的代码。

把对应的代码放文件里，文件名对应，运行对拍文件即可，需要在同一目录下。

### 对拍文件

这个文件名没有要求，叫啥都行。但是我的生成随机数现在用的C++，名字叫 `gen` ， 两份代码分别叫 `sol` 和 `std` 。如果你想改，把对应的名字全都修改就行。 `.in` `.out` 的文件名不必与前面的对应，叫啥都行，后缀用 `.txt` 之类的也可以。

```cpp
#include <bits/stdc++.h>
using namespace std;

int main()
{
    system("g++ -std=c++20 gen.cpp -o gen");
    system("g++ -std=c++20 sol.cpp -o sol");
    system("g++ -std=c++20 std.cpp -o std");
    int t = 10000;
    for (int i = 1; i <= t; i++) {
        system("gen > 1.in");
        system("sol < 1.in > sol.out");
        system("std < 1.in > std.out");
        if (system("fc sol.out std.out")) {
            return 0;
        } else
            printf("running on test %d\n", i);
    }
    return 0;
}
```

### 生成随机数

用于生成随机数据，需要设置编译参数 `-std=c++11` 或设置更高标准，C++11应该是可以用的，但是我好像没试过在那个蓝色 dev 用过。

`rand_integer(l,r)` 用于产生一个在 $[l,r]$ 之间的整数。需要生成随机字符串，你可以生成随机下标，或者其他思路。这个函数名你也可以改成任何你喜欢的。

也可以用 python 生成随机数据，可能也会比较简单。

```cpp
#include<bits/stdc++.h>
using namespace std;
using ll = long long;

mt19937_64 rng(time(NULL));
ll rand_integer(ll l, ll r)
{
    uniform_int_distribution<ll> dis(l, r);
    return dis(rng);
}
int main()
{
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    cout.tie(nullptr);
    
    return 0;
}
```

