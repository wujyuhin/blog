#requirements 
文件读取
1.csv
	pd.readcsv("filepath",usecols=['A','B'],encoding='utf-8').dropna()
2.txt
	1）逐行读取	
		with open('filepath','r',encoding='utf-8') as f:
			for line in f:
				逐行读取
	2）逐行写出
		with open('filepath','w',encoding='utf-8') as f:
			for item in items:
				f.write(...)

字符串拼接
1.普通拼接
	'*'.join(['1','2','3'])，表示用*把数字拼接在一起
2.路径拼接
	os.path.join(path1,path2)

重复扩展
	np.repeat(a,repeats,axis=None)
	repeats： 重复次数		
	axis = None 表示展开成1维
	axis=0 沿y轴重复
	axis=1 沿x轴重复

# apply_along_axis ()
>>> def my_func(a):  
...     \"\"\"Average first and last element of a 1-D array\"\"\"  
...     return (a[0] + a[-1]) * 0.5  
>>> b = np.array([[1,2,3], [4,5,6], [7,8,9]])  
>>> np.apply_along_axis(my_func, 0, b)  
array([4., 5., 6.])  
>>> np.apply_along_axis(my_func, 1, b)  
array([2.,  5.,  8.])