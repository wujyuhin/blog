1.安装
	cmd使用命令 pip install opencv-python
	python使用命令 import cv2 as cv
2. 图像命令
	cv.imread('test.png',0)		# 加载灰色图像
	cv.imshow('image',img)		# image为窗口名称，img为图片的数字形式
	cv.imwrite('image.png',img)	# 将image数字形式保存为png格式，目前只能保存在当前文件夹，不能调路径 