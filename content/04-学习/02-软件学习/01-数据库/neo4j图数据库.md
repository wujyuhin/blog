1 节点规则
(代表元: 节点类别1:节点类别2{属性1:属性值1, 属性2: 属性值})

2 关系规则
[关系名: 关系类型{属性:属性值}]
3 语法
	i 添加节点
		create 节点

	ii 添加关系
		a 从已有节点添加关系
			match 节点1, 节点2 merge 节点1-关系->节点2
		b 新建节点添加关系
			create 节点1-关系->节点2
		c 部分节点已存在
			match 节点1 merge 节点1-关系->节点2
	iii 添加属性
		a 添加\修改节点属性
			match 节点1 set 节点1.属性名=属性值 
		b 移除节点属性
			match 节点1 remove 节点1.属性名
		c 查询属性值
			match 节点1 return 节点1.属性名
		d 添加\修改关系属性
			match 节点1-关系->节点2  set 关系.属性名=属性值

	iv 删除关系
		a 匹配关系，删除
			match 规则 delete 关系；
	v 删除节点
		a 确保与该节点链接的关系全部删除-方式1
			match (n)-[h]->节点 delete h;
			match 节点-[r]->(n) delete r;
			match 节点 delete 节点；
		b 解放关系，顺便删除节点
			match 节点 detach delete 节点

	vi 查询
		a 查询节点
			match 节点 return 节点
		b 查询关系
			match 节点1-关系->节点2 return 关系
		c 查询多层关系
			(a) 查找1-2层的关系
				match 节点1-[*1..2]->节点2 return 节点1, 节点2
				match (n:Person{name:"周星驰"})-[*1..2]->(m) return n,m
			(b) 只查找具有2层关系
				match 节点1-[*2]->节点2 return 节点1, 节点2

4 条件语句
	i 条件语句规则
		节点.属性名=属性值
	ii 条件语句一般用法
		match 规则 where 条件1 and\or 条件2

4.新建数据库
	i 在docker目录下改不了了，因为找不到配置文件修改
	ii 3.5版本neo4j修改配置文件 https://blog.csdn.net/m0_51544947/article/details/122361891
		（0）首先在cmd中 neo4j install-service 下载服务
		（a）打开neo4j路径下的conf文件，双击打开neo4j.conf
		（b）找到这部分
			# The name of the database to mount
			# dbms.active_database=graph.db
			增加一句即可新增一个数据库
			# The name of the database to mount
			# dbms.active_database=graph.db
			dbms.active_database=red.db
		（c）在cmd中重启 neo4j restart

5.查询多个关系的相关实体
	i MATCH (d:Person)-[r]-(e:Person) where type(r) in ['丫环','妻子','妾'] return d,e		