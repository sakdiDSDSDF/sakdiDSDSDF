# 二分查找

https://www.bilibili.com/video/BV1np421o77o/?spm_id_from=333.1007.0.0&vd_source=e3dc19eb700a416c04efe110fff16163

```c++
#include<bits/stdc++.h>
using namespace std;
bool check(int x){
	......
}
int main(){
	int l=1,r=n+1;
	while(l<r){
		int mid=(l+r)>>1;
		if(check(mid)){
			r=mid;
		}
		else{
			l=mid+1;
		}
	}
	cout<<l<<endl;
	return 0;
}
```

