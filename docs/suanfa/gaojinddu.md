# 高精度算法

## 加法代码

```c++
/*
   (｡･ω･｡)ﾉ♡  我喜欢斯卡蒂啊，我喜欢流萤啊
*/
#include<bits/stdc++.h>
#define INF 1e18
#define pb push_back
#define ll long long
using namespace std;
int main(){
    string a,b;
    cin>>a>>b;
    vector<int> A,B;
    for(int i=a.size()-1;i>=0;i--){
        A.pb(a[i]-'0');
    }
    for(int i=b.size()-1;i>=0;i--){
        B.pb(b[i]-'0');
    }
    int len=max(A.size(),B.size()),mi=min(A.size(),B.size());
    vector<int> ans;
    for(int i=0;i<len;i++){
        if(i<=mi-1){
            ans.pb(A[i]+B[i]);
        }
        else{
            if(A.size()==len) ans.pb(A[i]);
            else ans.pb(B[i]);
        }
    }
    for(int i=0;i<ans.size()-1;i++){
        if(ans[i]>=10){
            ans[i]=ans[i]%10;
            ans[i+1]++;
        }
    }
    for(int i=ans.size()-1;i>=0;i--){
        cout<<ans[i];
    }
    cout<<endl;
    return 0;
}
```

## 减法代码

```c++
/*
   (｡･ω･｡)ﾉ♡  我喜欢斯卡蒂啊，我喜欢流萤啊
*/
#include<bits/stdc++.h>
#define INF 1e18
#define pb push_back
#define ll long long
using namespace std;
int main(){
    string a,b;
    cin>>a>>b;
    string mx,mi;
    bool fuhao=false;
    if(a.size()>b.size()){
        mx=a;
        mi=b;
    }
    else if(a.size()<b.size()){
        mx=b;
        mi=a;
        fuhao=true;
    }
    else{
        bool ok=false;
        for(int i=0;i<a.size();i++){
            if(a[i]>b[i]){
                mx=a;
                mi=b;
                ok=true;
                break;
            }
            else if(a[i]<b[i]){
                mx=b;
                mi=a;
                ok=true;
                fuhao=true;
                break;
            }
        }
        if(!ok){
            cout<<0<<endl;
            return 0;
        }
    }
    vector<int> MX,MI;
    for(int i=mx.size()-1;i>=0;i--){
        MX.pb(mx[i]-'0');
    }
    for(int i=mi.size()-1;i>=0;i--){
        MI.pb(mi[i]-'0');
    }
    vector<int> ans;
    for(int i=0;i<MX.size();i++){
        if(i<=MI.size()-1){
            if(MX[i]>=MI[i]){
                ans.pb(MX[i]-MI[i]);
            }
            else{
                ans.pb(MX[i]+10-MI[i]);
                if(MX[i+1]!=0) MX[i+1]--;
                else{
                    MX[i+1]=9;
                    for(int j=i+2;j<MX.size();j++){            // 1009
                        if(MX[j]!=0){
                            MX[j]--;
                            break;
                        }
                        else{
                            MX[j]=9;
                        }
                    }
                }
            }
           // cout<<ans[i]<<endl;
        }
        else{
            ans.pb(MX[i]);
        }
    }
    if(fuhao){
        cout<<'-';
    }
    bool qiandao=false;
    for(int i=ans.size()-1;i>=0;i--){
        if(!ans[i]&&!qiandao) continue;
        else{
            qiandao=true;
            cout<<ans[i];
        }
    }
    return 0;
}
```

## 乘法代码

```c++
#include<iostream>
#include<cstring>
#include<cstdio>
#include<algorithm>
using namespace std;
char a1[10001],b1[10001];
int a[10001],b[10001],i,x,len,j,c[10001];
int main ()
{
    cin>>a1>>b1;//不解释，不懂看前面
    int lena=strlen(a1);//每个部分都很清楚
	int lenb=strlen(b1);//这只是方便你们复制
    for(i=1;i<=lena;i++)a[i]=a1[lena-i]-'0';
    for(i=1;i<=lenb;i++)b[i]=b1[lenb-i]-'0';
	for(i=1;i<=lenb;i++)
	for(j=1;j<=lena;j++)
	c[i+j-1]+=a[j]*b[i];
    for(i=1;i<lena+lenb;i++)
	if(c[i]>9)
	{
		c[i+1]+=c[i]/10;
		c[i]%=10;
	}
	len=lena+lenb;
    while(c[len]==0&&len>1)len--;
    for(i=len;i>=1;i--)cout<<c[i];
    return 0;
}
```

