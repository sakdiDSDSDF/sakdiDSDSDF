## 生成任意数量指定难度的Codeforces题目

原来这么简单哈。。。

让ai生成了一下，然后改了一下。。。

```python
import requests
import random

# 在这里修改需要的用户名，rating 区间，题目数量

min_rating = 1400
max_rating = 1800
handles = ['Zhangwuji']
count = 5

def get_problems():  # 获取题目列表
    url = "https://codeforces.com/api/problemset.problems"
    res = requests.get(url)
    if res.status_code == 200:
        return res.json()['result']['problems']
    else:
        print(f"Error: 无法获取题目列表")
        return []

def get_solvedList(handles):  # 获取已通过题目列表
    solved_problems = set()
    for handle in handles:
        url = f"https://codeforces.com/api/user.status?handle={handle}"
        res = requests.get(url)
        if res.status_code == 200:
            x = res.json()['result']
            for y in x:
                if y['verdict'] == 'OK':  # 只记录通过的题目
                    z = y['problem']
                    solved_problems.add((z['contestId'], z['index']))
        else:
            print(f"Error: 无法获取用户 {handle} 的提交记录，请检查用户名是否正确。")
    return solved_problems

problemset = get_problems()
solved_problems = get_solvedList(handles)
problemcount = len(problemset)  # 题目总数

def get_valid():
    res=[]
    for now in problemset:
        rd = now['contestId']
        id = now['index']
        if 'rating' in now:
            rt = now['rating']
            if (rd,id) in solved_problems:
                continue
            if min_rating<=rt<=max_rating:
                res.append(now)
    return res

validproblems = get_valid()

def gen_List(need):
    return random.sample(validproblems,need)

def printproblems(problems):
    print(f"\n芝士{len(problems)}个rating在 [{min_rating}, {max_rating}] 的随机题目")
    for x in problems:
        rd = x['contestId']
        id = x['index']
        rt = x['rating']
        name = f"{rd}{id}"
        url = f"https://codeforces.com/contest/{rd}/problem/{id}"
        print(f"{name:7} {rt:5} {url}")

x = gen_List(count)
printproblems(x)
```

唉唉，搞这种纯浪费时间吧。。。

虽然挺好玩的。

[Duel](https://algorithm-duels.online/home) 这个算法单挑网站，昨晚知道的，，感觉很不错。打算在上面每天随机6个需要的难度的题目。。如果有一个人跟我一起练，可以在一样的房间，那就会每天写一样的题目，感觉会挺不错的。。。

大家新年快乐。祝大家身体健康，技术++。
