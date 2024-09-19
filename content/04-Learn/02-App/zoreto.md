#软件使用 

# 结合大模型的插件Zotero -gpt

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