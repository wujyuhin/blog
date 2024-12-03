dataframe数据
1.数据排序 data.sort_value('order_id')

某列列名作为列索引

所有列名转换成小写字母
data = data.rename(columns=lambda x : x.lower())

多重标题行数据读取
data = pd.read.excel(path,header=[0, 1])

dataframe根据某学生外连接
data = pd.merge(d1,d2,on=['姓名'],how='outer')
其他参数how = ['outer','left','right'],默认内连接


多重列索引使用reindex会自动排序，根据一级索引为主顺序，剩下的排序
data.reindex(index=[0,1,2..],columns=['name1','name2'],level=0)