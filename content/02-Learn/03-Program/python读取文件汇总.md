- 读取 csv 格式：`pd.read_csv(data.csv)`
- 读取 docx 格式：
	- 1. 安装包 `pip install python-docx`
	- 2. 导入包 `from docx import Document`
	- 3. 导入数据 `doc = Document(file.docx)`
	- 4. 查看文档中文本对象 `doc.paragraph` （是一个列表，列表中是对象）
	- 5. 查看列表中对象的文本 `doc.paragraph[0].text` (是 doxc 文档的第一段话)
	- 更多读写操作参考 [python 使用 python-docx 读取和写入 word_python-docx读取field-CSDN博客](https://blog.csdn.net/qq_44614026/article/details/108223149)
- 读取 doc 格式：
	- 由于 python 本身无法读取 doc 文件，因此可采用批量另存为 docx 的方式，转为读取 docx
	- 注意，如果批量运行函数需要间隔，防止 word 程序没关闭完成`time.sleep(2)`
	- 更多参考[【python基础】——python读写doc/docx/txt/xls文件_python doc-CSDN博客](https://blog.csdn.net/weixin_40449300/article/details/79143971)

```python
import sys
import pickle
import re
import  codecs
import string
import shutil
from win32com import client as wc
import docx
 
 
def doSaveAas():
    word = wc.Dispatch('Word.Application')
    doc = word.Documents.Open(r'E:\code\xx.doc')        # 目标路径下的文件
    doc.SaveAs(r'E:\\code\hh.docx', 12, False, "", True, "", False, False, False, False)  # 转化后路径下的文件    
    doc.Close()
    word.Quit()
 
doSaveAas()
```