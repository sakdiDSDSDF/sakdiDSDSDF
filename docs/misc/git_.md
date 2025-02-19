---
2025-02-19
---
### github.io

今天算是发现 `username.github.io` 有什么不同之处了。。。

建了一个新项目，想着弄个子域名解析那个项目的pages，但是发现不可以。

因为普通项目的pages的路径它是username.github.io/repo , 这并不是一个域名，所以不能解析。。。

但是可以通过我这个域名绑定了 `github.io` ，所以其他项目会解析到 custom domain/repo ，也算还行吧。

感觉必须得再注册一个github账号了，不然我的主域名一直没有可以解析的东西，感觉这样不太好。

### git连接443端口失败

我记得之前我是22端口失败，然后去浏览器和问chat，改了host文件，好了一段时间。

今天新建一个项目就443端口连接失败，查了一下加了个代理就好了。

```bash
git config --global http.proxy http://127.0.0.1:33210
git config --global https.proxy https://127.0.0.1:33210
```

把ip和端口换成自己的，输这个命令，给git设置代理，然后就好了。

但是很奇怪的是，我之前应该没设过代理，为啥其他文件夹一直git push都没有问题呢。。。而且不开加速器貌似也能push。

