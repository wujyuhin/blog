#软件使用攻略 #obsidian 

[Obsidian基本使用-CSDN博客](https://blog.csdn.net/Castlehe/article/details/114290410)

# 1.更换字体

直接在电脑中双击ttf尾缀文件，下载对应字体，重启obsidian即可搜索到下载字体

# 2.使用note gallery

可以使用以下代码放在根目录下，即可记录目录中的笔记

```python
~~~~note-gallery
sort: desc
limit: 9
~~~~
```

# 3.外观

壁纸：在商店下载Vicious

字体：霞鹜文楷 [lxgw/LxgwWenKai: An open-source Chinese font derived from Fontworks' Klee One. 一款开源中文字体，基于 FONTWORKS 出品字体 Klee One 衍生。 (github.com)](https://github.com/lxgw/LxgwWenKai)

# 4. 多端同步

**windows 上的 obsidian 同步**

- 同时同步到两个云盘
	- 使用坚果云同步（放入同步文件夹后自动同步，需要点开坚果云 app 查看是否同步完成）
		- 不充会员只有 1 G 空间和 3 G 下载
	- 使用 remotely save 插件同步到 onedrive（需要手动点击插件栏上的圈圈）
		- 可惜只有个人版的，所以只有 5 G 空间
- ipad 上的 obsidian 同步
	- 同样使用 remotely save 插件同步到 onedrive（手动点击插件栏圈圈）
- 双端同步
	- 下载 air explorer
	- 分别登录两个账户即可同步
- 同步技巧
	- 如果只在电脑端修改 obsidian，则只需要点击手动同步 onedrive 即可，因为坚果云自动同步，这样两个云盘是一致的
	- 如果在 ipad 端修改 obsidian
		- 手动同步 ipad 的onedrive
		- 上电脑时要手动同步onedrive，理论上会将onedrive上下下来，然后自动同步到坚果云

# 5. 笔记的换行问题

因为如果在 obsidian 中，一个换行没问题，但是同步到 quartz 后就连在一起了

如果想要 quartz 换行，那么 obsidian 就需要两个回车了，不美观

使用 easy typing 插件, 没用还是不美观

没办法最终接受不美观，并且用 Linter 插件批量增加回车

策略：

原本的笔记正常写

写完之后复制到博客笔记库

然后对博客笔记库进行批量填充回车即可

# 6. 标注信息

模板如下：

> [!info] Title
> 
> This is a callout!

![[Pasted image 20240825101014.png]]

![[Pasted image 20240825101029.png]]

[Obsidian笔记最新版本的功能Callouts，提升方便性和美观程度_obsidian callout-CSDN博客](https://blog.csdn.net/weixin_45374670/article/details/124022120)

## 如何批量标注？

选中文本右键，增加标注
