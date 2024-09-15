#rpy2
在python中使用R
1.下载R https://blog.csdn.net/Suegsp/article/details/132161875 本机下载版本R-4.1.3-win.exe
2.记录安装路径：安装的时候复制即可。本机路径 D:\Software\R-4.3.3
	> .libPaths()
	>  [1]"C:/Users/wujyu/AppData/Local/R/win-library/4.3" "D:/Software/R-4.3.3/library"
3.环境变量设置
	1）name: R_HOME  value:C:\\Program Files\\R\\R-4.1.3
	2）name: R_USER  value:D: \\Software\\R-4.3.3\\bin
	3）path:C:D:\\Software\\R-4.3.3\\bin\\x 64
4.rpy2下载
	【注】由于不是linux，所以不能直接使用pip install rpy2下载
	1）直接下载whl文件，根据自己的python版本选择： https://www.lfd.uci.edu/~gohlke/pythonlibs/#rpy2
	2）使用命令行模式找到whl文件所在目录，pip install xxx.whl
5.测试
	1）在python中运行from rpy2.robjects import r
6.rpy2语法
	1）单句a = r('c(1,2,3)')
	2）一段	rscript = """
		a <- c(1,2,3,4)
		b <- c(2,4,6,8)
		fit <- lm(b~a)
		summary(fit)
		"""
		print(r(rscript))

下载的R包路径 C:\Users\wujyu\AppData\Local\Temp\RtmpUFU2ie\downloaded_packages