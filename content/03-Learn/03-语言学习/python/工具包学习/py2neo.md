#py2neo
```python
1.连接图模型
graph = Graph('http://localhost:7474', user='', password='')
2.节点规则
节点=Node(节点标签, 属性名1=属性值1, 属性名2=属性值2)
3.关系规则
关系=Relationship(节点1,关系类型,节点2)
4.语法
	i 增加节点
		graph.create(节点)
	ii 增加关系
		注：必须先创建节点
		b = Relationship(节点1, 关系类型, 节点2)
		graph.create(b)
	iii 节点修改
		a 增加/修改属性
			节点[属性名]=属性值
			graph.push(节点)
              	b 删除属性
			del a['age']
			graph.push(a)
		c 增加/移除标签
        			节点.add_label(标签1)
			节点.remove_label(标签1)
		d 批量增加节点标签
			节点.update_labels( [标签1, 标签2] )
		e 删除节点
			graph.delete(节点)  # 把关系一同删除
	v 关系修改
		a 增加/修改属性
			关系[属性名] = 属性值
			graph.push(关系)
     		b 删除属性
			del 关系[属性名]
			graph.push(关系)
		a 解除某个关系（修改关系使用）
			关系 = graph.match(nodes=[节点1, 节点2], r_type=关系, limit=None)
			graph.seperate(关系)
		b 删除指定类型的关系，并删除连接的两个节点
			graph.delete(关系)
	x 查询
		a 查询节点
			(1) 根据节点类型查询
			node = NodeMatcher(graph)
			node.match(节点类型1, 节点类型2, 属性1=属性值1, 属性2=属性值2)  # 特定属性值查询，结果为字典构成的可迭代
			a = node.match()
			for ai in a:
				#规则
		b 查询关系
			(1) 根据关系属性来查询
				relation = RelationshipMatcher(graph)
				a = relation.match(r_type='mate', strong=3) # 根据关系属性特定值匹配，匹配结果为字典构成的可迭代
				b = relation.match()                                       # 根据复杂规则遍历查找特定条件关系
				for bi in b:
					# 规则
			(2) 更具节点、关系类型来查询关系
				graph.match(nodes=[开始节点1, 结束节点2], r_type=关系, limit=None)
				结果是可迭代与对象，节点和关系都可以为None
		c 查询属性
			节点[属性名]
		d 查询节点标签
			节点._labels


其他
1. 提取某个节点的标签，并变成列表
	i a = 节点.labels   # 提取标签
	ii b = a._SetView__collection  # 提取标签格式 
	iii c = [i for i in b]  # 将可迭代对象化为列表

2.提取节点关系名称
	relation_matcher = RelationshipMatcher(g)
	rels = relation_matcher.match(r_type="朋友")
	a = [rel for rel in rels]
	a[0] # 这是两个节点和一个关系
	type(a[0]).__name__   # 这是a[0]关系的关系名

3.查找总共有哪些关系、或者节点标签
	i graph.schema.node_labels
	ii graph.schema.relationship_types
		
```




1.连接图模型
graph = Graph('http://localhost:7474', user='', password='')
2.节点规则
节点=Node(节点标签, 属性名1=属性值1, 属性名2=属性值2)
3.关系规则
关系=Relationship(节点1,关系类型,节点2)
4.语法
	i 增加节点
		graph.create(节点)
	ii 增加关系
		注：必须先创建节点
		b = Relationship(节点1, 关系类型, 节点2)
		graph.create(b)
	iii 节点修改
		a 增加/修改属性
			节点[属性名]=属性值
			graph.push(节点)
              	b 删除属性
			del a['age']
			graph.push(a)
		c 增加/移除标签
        			节点.add_label(标签1)
			节点.remove_label(标签1)
		d 批量增加节点标签
			节点.update_labels( [标签1, 标签2] )
		e 删除节点
			graph.delete(节点)  # 把关系一同删除
	v 关系修改
		a 增加/修改属性
			关系[属性名] = 属性值
			graph.push(关系)
     		b 删除属性
			del 关系[属性名]
			graph.push(关系)
		a 解除某个关系（修改关系使用）
			关系 = graph.match(nodes=[节点1, 节点2], r_type=关系, limit=None)
			graph.seperate(关系)
		b 删除指定类型的关系，并删除连接的两个节点
			graph.delete(关系)
	x 查询
		a 查询节点
			(1) 根据节点类型查询
			node = NodeMatcher(graph)
			node.match(节点类型1, 节点类型2, 属性1=属性值1, 属性2=属性值2)  # 特定属性值查询，结果为字典构成的可迭代
			a = node.match()
			for ai in a:
				#规则
		b 查询关系
			(1) 根据关系属性来查询
				relation = RelationshipMatcher(graph)
				a = relation.match(r_type='mate', strong=3) # 根据关系属性特定值匹配，匹配结果为字典构成的可迭代
				b = relation.match()                                       # 根据复杂规则遍历查找特定条件关系
				for bi in b:
					# 规则
			(2) 更具节点、关系类型来查询关系
				graph.match(nodes=[开始节点1, 结束节点2], r_type=关系, limit=None)
				结果是可迭代与对象，节点和关系都可以为None
		c 查询属性
			节点[属性名]
		d 查询节点标签
			节点._labels


其他
1. 提取某个节点的标签，并变成列表
	i a = 节点.labels   # 提取标签
	ii b = a._SetView__collection  # 提取标签格式 
	iii c = [i for i in b]  # 将可迭代对象化为列表

2.提取节点关系名称
	relation_matcher = RelationshipMatcher(g)
	rels = relation_matcher.match(r_type="朋友")
	a = [rel for rel in rels]
	a[0] # 这是两个节点和一个关系
	type(a[0]).__name__   # 这是a[0]关系的关系名

3.查找总共有哪些关系、或者节点标签
	i graph.schema.node_labels
	ii graph.schema.relationship_types





		