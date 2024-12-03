#软件使用 

# 1.Zotero -gpt

1.首先打开仓库 [MuiseDestiny/zotero-gpt：GPT 认识 Zotero。 (github.com)](https://github.com/MuiseDestiny/zotero-gpt)，在里面下载好文件并安装

2.进入配置界面

![[Pasted image 20240825155842.png]]

![[Pasted image 20240825155937.png]]

![[Pasted image 20240825160214.png]]

3.进行配置（chatgpt 网络信号不好，用了发现配额不足）
- Api 处配置双击修改为`httphttps://dashscope.aliyuncs.com/compatible-mode/v1`
- Model 处配置双击修改为 `qwen-turbo`
- SecreKey 处配置双击修改为你的灵积平台 qwen-turbo 的密钥（需要去阿里云模型服务灵积申请）

> [!Tip] 注意
> 可以使用其他模型，Kimi、文心一言之类的，只要把上述三个配置修改即可。Api 一般在大模型相关的文档中会写，密钥需要自己创建，模型一般也能在管理界面看到。

![[Pasted image 20240825160149.png]]

4.最后可以根据文献内容直接与大模型交互

![[Pasted image 20240825160810.png]]

# 2.Zotero style

## 下载安装

下载链接 [zotero style](https://github.com/MuiseDestiny/zotero-style?tab=readme-ov-file)，打开 zotero，然后添加 style 插件

![[Pasted image 20240901170404.png]]

![[Pasted image 20240901170447.png]]

## 使用期刊标签

1.打开网站注册：[easyScholar | 显示期刊等级\SCI分区](https://www.easyscholar.cc/)

2.点击个人信息，弹出以下界面，复制密钥

![[Pasted image 20240901171320.png]]

3. 打开 zotero，在标题栏右键-点击期刊标签，就会多出来期刊标签

![[Pasted image 20240901170618.png]]

4.然后再期刊标签标题处右键-点击列设置，会弹出以下内容，将刚刚复制的密钥粘贴

![[Pasted image 20240901170809.png]]
![[Pasted image 20240901171417.png]]
