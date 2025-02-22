---
2025-02-22
---

## windows双系统删除ubuntu arch

首先在磁盘管理里删掉ubuntu在的分区

然后再把grub引导删掉

首先打开cmd或powershell，输入diskpart

再list volume，找到EFI分区，大小可能是300M左右，通常是FAT32格式

select volume 1，看EFI分区具体的编号，然后选择，然后给他分配盘符

assign letter=Z

然后这个分区被我们挂载到了这个盘，我们可以管理员身份打开VS Code

然后直接用VS Code打开这个盘，就可以看到文件目录，然后把EFI/下的ubuntu或arch文件夹删除

然后再remove letter=Z，再重启电脑，应该就看不到grub引导了

我先试试

``` bash
diskpart
list volume
select volume 1 #看具体哪个是EFI分区
assign letter=Z #给EFI分区分配盘符
然后去删除EFI/下的ubuntu或arch文件夹，可以使用管理员VS Code打开这个盘
remove letter=Z #删除盘符
exit
```
