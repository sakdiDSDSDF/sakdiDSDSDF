>2025-02-27
>
>指导老师: ChatGPT

# github基本操作

>  其实我也不咋会。。。经常大部分都是问 chat 和 deepseek。目前基本上只用 git add ，commit , push , branch 这些。。。这是大概会提交代码。其他的啥都不会，该学一下总结一下了。

# 创建仓库

首先咱们创建一个仓库，有一个选项是添加 `README file` ，选了这个应该就会自动初始化仓库，否则仓库是空的。

我说怎么每次情况不一样呢。那咱们这里先不要选。因为以后选不选，操作都差不多。

其他的设置都先不用改，取好项目名字就行。

没有选添加 `README.md` 的话，仓库会是空的。

会显示这几行代码，每个人的不一样，第六行那里的项目地址不一样。

```bash
echo "# www" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/fwdzh/www.git
git push -u origin main
```

选ssh连接的话会有点不一样，这里咱们先用https连接。

这个是让咱们创建本地目录并和远程仓库连接推送文件的。

这个命令，我们可以点开本地文件夹，然后右键点击空白的地方，选择 `git bash here`，就会在这里启动git bash，可以在里面输入命令。也可以使用vscode 打开文件夹，在vscode 的终端中输入命令。

在vscode中可以使用 ==ctrl+`== 快捷键来打开终端，几行命令全复制过去就行。

不过第一次应该需要咱们配置用户信息。

```bash
Author identity unknown

*** Please tell me who you are.

Run

  git config --global user.email "you@example.com"
  git config --global user.name "Your Name"

to set your account's default identity.
Omit --global to set the identity only in this repository.

fatal: unable to auto-detect email address (got 'ilyha@skadi.(none)')
```

 我刚才把命令全粘过去出这个了。这是让咱们先配置用户信息。

```bash
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
```

把对应的引号里的内容，换成你的github绑定的邮箱，和github的用户名。

```bash
git config --global user.email "2895264580@qq.com"
git config --global user.name "fwdzh"
```

这是我的，你们改成自己的。

粘到终端去。这里加 --global是设置全局的，不加的话只设置当前目录的信息。

如果你提示443端口或22端口连不上，可以去搜索解决方法。我的另一篇博客有简单记了一下443端口连不上。

## **1. `echo "# www" >> README.md`**

```bash
echo "# www" >> README.md
```

📌 **作用**：

- 创建一个 `README.md` 文件，并在其中写入 `# www`。
- 如果 `README.md` 文件已存在，则在末尾追加 `# www`。
- 这个文件通常用于描述项目的基本信息，在 GitHub 上会自动显示为项目主页的介绍。

------

## **2. `git init`**

```bash
git init
```

📌 **作用**：

- 在当前目录下 **初始化一个 Git 仓库**，生成 `.git/` 隐藏目录。
- 之后的 Git 命令（如 `add`、`commit`、`push` 等）都会基于这个 Git 仓库进行操作。

💡 **执行后，当前目录就变成了一个 Git 仓库**。

------

## **3. `git add README.md`**

```bash
git add README.md
```

📌 **作用**：

- 将 `README.md` 文件加入 **暂存区**（staging area），准备提交。

💡 **只有被 `git add` 的文件才会被 `commit` 记录**。

------

## **4. `git commit -m "first commit"`**

```bash
git commit -m "first commit"
```

📌 **作用**：

- **提交代码**，把 `README.md` 从暂存区提交到本地仓库（本地 `main` 分支）。
- `-m "first commit"` 指定提交信息，描述这次提交的内容。

💡 **执行后，你的代码已经被记录在本地 Git 仓库**，但还没有推送到远程 GitHub。

------

## **5. `git branch -M main`**

```bash
git branch -M main
```

📌 **作用**：

- **将当前分支重命名为 `main`**（现代 Git 默认使用 `main` 作为主分支，而不是 `master`）。

💡 **如果你刚 `git init`，默认分支可能是 `master`，这个命令会改成 `main`**。

------

## **6. `git remote add origin https://github.com/fwdzh/www.git`**

```bash
git remote add origin https://github.com/fwdzh/www.git
```

📌 **作用**：

- **将远程 GitHub 仓库（`https://github.com/fwdzh/www.git`）添加为 `origin` 远程地址**。
- 之后可以使用 `origin` 作为别名进行 `git push` / `git pull`。

💡 **执行后，本地 Git 知道代码应该推送到哪个 GitHub 仓库**。

------

## **7. `git push -u origin main`**

```bash
git push -u origin main
```

📌 **作用**：

- **将本地 `main` 分支的代码推送到 GitHub 远程仓库**。
- `-u` 选项的作用：**设置 `origin/main` 为默认上游分支**，以后 `git push` 和 `git pull` 可以省略 `origin main`，直接用 `git push` / `git pull`。

执行完这些命令之后，我们的本地目录就会初始化为一个git仓库，可以使用git命令来拉取或推送代码。并且可以利用github pages方便地部署静态网页。

# 提交修改

运行完以上的代码，我们可以看到github的仓库已经有了README.md文件。

上面每个命令的解释我让chat生成的，也方便我理解。。。原来 `git push -u origin master` 也会设置默认分支。

以后咱们每次提交修改，只需要运行三个命令。

```bash
git add .
git commit -m "..."
git push
```

### 1.`git add`

📌 **作用**：

- 把 **当前目录下的所有修改**（新增、修改、删除的文件）**加入暂存区**，准备提交。

- 其中 

  ```
  .
  ```

   代表当前目录的所有文件，等价于：

  ```cpp
  git add --all
  ```

💡 **示例**：

- 如果你修改了 `main.cpp`，新增了 `utils.h`，删除了 `temp.txt`，执行 `git add .` 后，这些变更都会进入 **暂存区**，等待提交。

------

### **2. `git commit -m "..."`**

```
git commit -m "..."
```

📌 **作用**：

- **提交暂存区的修改到本地仓库**，并记录一条提交信息（`-m "..."`）。
- 这相当于**快照**，以后可以查看每次提交的历史，甚至回滚到某个版本。
- 把引号里的内容换成你想留言的话，但是不能为空。

💡 **示例**：

```
git commit -m "修复了登录界面加载慢的问题"
```

这样我们就能知道这次提交的主要改动内容。

------

### **3. `git push`**

```
git push
```

📌 **作用**：

- **把本地仓库的修改推送到远程仓库（GitHub）**。

- 由于之前 

  ```
  git push -u origin main
  ```

   绑定了默认上游分支，以后 

  ```
  git push
  ```

   就等价于：

  ```
  git push origin main
  ```

💡 **示例**：

- 本地修改的代码提交到 GitHub 上，团队成员或其他人就能看到更新。

------

## **完整流程**

1. **修改代码**，比如编辑 `index.html`。
2. **`git add .`** 把改动加入暂存区。
3. **`git commit -m "优化前端 UI"`** 提交修改。
4. **`git push`** 推送到 GitHub。

这样，每次提交都很简单高效 🎉。

# github pages

这是一个非常牛非常爽的功能，可以让咱们无需服务器就可以通过域名来访问我们的网站。

并且还可以添加自定义域名，使得我们无需加速器即可访问我们的页面。

### **启用 GitHub Pages**

如果你想让 GitHub 托管静态网站，比如个人博客、文档站点，步骤如下：

1. 进入你的仓库，点击 `Settings`

2. 左侧找到 `Pages`

3. 选择**部署来源（Branch）**，一般选 `main` 分支

4. 选择根目录 `/`

5. GitHub 会自动生成 URL，比如：

   ```bash
   https://你的用户名.github.io/你的仓库名/
   ```

### **上传静态网站**

如果你有 `index.html`，直接提交到仓库根目录：

```bash
git add .
git commit -m "添加网站"
git push
```

然后等几分钟，GitHub Pages 就会自动生成网站。

### 自定义域名

在settings->pages 页面，找到 custom domain 选项，在这里填入你的域名，即可通过自定义域名访问你的github pages页面。操作方式就是，先在你的域名那添加一个记录，记录值设置成 `username.github.io` ， username替换为你的用户名，然后再到github里设置自定义域名。记得勾选下面的强制https，这样就不会被提示不安全了。

稍微等一下，就可以在自定义域名里访问我们的页面了。

而且我们的每一个项目都可以设置一个单独的域名，只需要把对应的域名的记录值都改为 `username.github.io ` ，类型为 `CNAME` 类型。
