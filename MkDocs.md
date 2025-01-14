# MkDocs

看到很多大佬的博客都是这个 [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) , 我也想整一个，所以来学习一下。

其实很多内容可能会是我复制其他大佬的博客。

我之前弄的博客很乱，也没更新多久，就没有再弄了。现在想重新整一个。

现在是在windows上配置。

首先需要安装pip，在这之前要先安装python，[下载链接](https://www.python.org/downloads/windows/)。

好吧下载安装程序之后会自动安装好pip。

![image-20250114170449725](./assets/image-20250114170449725.png)

我直接下载了最新版的，可以下载其他版本，但是不要太低了。

### 安装

```bash
pip install mkdocs-material
```

在 cmd 或 powershell 输入以上内容。

我报error了

```bash
 error: Microsoft Visual C++ 14.0 or greater is required. Get it with "Microsoft C++ Build Tools": https://visualstudio.microsoft.com/visual-cpp-build-tools/
      [end of output]

  note: This error originates from a subprocess, and is likely not a problem with pip.
  ERROR: Failed building wheel for regex
  Building wheel for MarkupSafe (pyproject.toml) ... done
  Created wheel for MarkupSafe: filename=MarkupSafe-3.0.2-py3-none-any.whl size=9325 sha256=c4cb3dbadfedcb388ee37c84f33b807769309218ed97e3e46efc94903212e884
  Stored in directory: c:\users\ilyha\appdata\local\pip\cache\wheels\31\d7\9c\91ea0a7f1bd99970c6602ae982d137132c904433343f48095b
  Building wheel for pyyaml (pyproject.toml) ... done
  Created wheel for pyyaml: filename=PyYAML-6.0.2-cp314-cp314-win_amd64.whl size=45437 sha256=42903cee0a60f3f89009d1c5cb7a7351f4c6e357df99414dffa2f70b581cd9c8
  Stored in directory: c:\users\ilyha\appdata\local\pip\cache\wheels\16\d3\3b\1f603c475e2c00f8749b9c112c874a87093b6fc1ef4a11ce07
Successfully built MarkupSafe pyyaml
Failed to build regex
ERROR: ERROR: Failed to build installable wheels for some pyproject.toml based projects (regex)
```

缺少visual c++。好像是我自己删的，我看电脑上自带的本来有visual c++，我不喜欢就删了。

我现在下载一下然后看看重新安装。

[Microsoft C++ 生成工具 - Visual Studio](https://visualstudio.microsoft.com/zh-hans/visual-cpp-build-tools/)

好像无法下载。。。

我用手机上的edge也下载不了，但是自带的那个浏览器下载成功了。

是一个visual studio installer，而且下载进度一直不动。。。要不直接下载一个visual studio吧。

[Visual C++ Build Tools 2015](http://go.microsoft.com/fwlink/?LinkId=691126)

服了，一直说下载失败。。。

重启一下试试。

然后我又去了第一个，下载成功了。

但是这个是下载Visual Studio 2022的，我选了10GB的东西下载，好像不用下这么多的。只用选那个2015xxx的就行了，我选了C++桌面开发工具7GB，2015 开发工具4GB，应该只下那个就行的。

ok，安装完之后，运行刚才的pip xxxx，没有`error`了。

主要是我把电脑上那个Visual C++给删了，你们如果没删，应该不用这么麻烦。

感觉比Ubuntu的操作轻松很多，Ubuntu用这个pip系统报警告，不让用，得弄虚拟环境。配置Docker也非常麻烦，至少我是没弄成功的。

### 新建网站

在完成[Material for MkDocs的安装](https://mkdoc-material.llango.com/getting-started/)后，可以使用`mkdocs`相关命令来启动文档。转到要放置项目的目录，然后输入：

```powershell
mkdocs new .
```

以上操作会新建以下结构的文件：

```
.
├─ docs/
│  └─ index.md
└─ mkdocs.yml
```

#### 配置

##### 最小配置

只需要简单的添加以下几行内容到`mkdocs.yml`即可启用主题。请注意，由于有几种不同的安装方法，因此配置可能会略有不同：

```y
theme:
  name: material
```

*如果是从GitHub克隆的MkDocs from GitHub，那么应当列出所有主题的默认项，因为`mkdocs_theme.yml`不会作为`官方的描述文件`被自动载入*。

#### 预览

MkDocs包含一个试试预览的服务，所有可以在撰写文档的过程中进行实时预览。当文档修改保存后，这个服务会自动重建整个网站的文档。使用以下命令启动：

```
mkdocs serve
```

会输出

```
PS C:\blog> mkdocs serve
INFO    -  Building documentation...
INFO    -  Cleaning site directory
INFO    -  Documentation built in 1.69 seconds
INFO    -  [02:08:25] Watching paths for changes: 'docs', 'mkdocs.yml'
INFO    -  [02:08:25] Serving on http://127.0.0.1:8000/
INFO    -  [02:08:28] Browser connected: http://127.0.0.1:8000/
INFO    -  Shutting down...
```

按住ctrl然后点击那个链接，会在浏览器打开，可以预览网站。

#### 生成网站

当文档编辑完成后，可以通过以下命令将所有的Markdown文件生成一个静态网站：

```
mkdocs build
```

该目录中的内容就是项目文档/网站。因为是完全独立的，所以不需要操作数据库或者服务器。生成的网站可以托管在GitHub Pages、GitLab Pages、CDN网络或者其它的web服务器上。

这也太不错了吧，配置很简单。

### 发布网站

将网站托管在`git`库中的最大好处是能够在推送新更改时自动部署它。MkDocs使得这一操作更加简单。

#### GitHub Pages

如果已经在GitHub上托管代码，那么使用[GitHub Pages](https://pages.github.com/)来发布网站再方便不过了。

##### 使用GitHub Actions

使用[GitHub Actions](https://github.com/features/actions)可以自动部署网站。在库的根目录下新建一个GitHub Actions workflow，比如：`.github/workflows/ci.yml`，并粘贴入以下内容：

Material for MkDocs

```
name: ci
on:
  push:
    branches:
      - master
      - main
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-python@v2
        with:
          python-version: 3.x
      - run: pip install mkdocs-material
      - run: mkdocs gh-deploy --force
```

全部的内容基本都是看这个的[入门 - Material for MkDocs 中文文档](https://mkdoc-material.llango.com/getting-started/)，官方的文档，确实挺不错的。