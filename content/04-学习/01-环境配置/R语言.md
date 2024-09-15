# rtools 报错
step 1：bug 是什么
```R
WARNING: Rtools is required to build R packages but is not currently installed. Please download and install the appropriate version of Rtools before proceeding:
```

step 2：原因
这是 rtools 没有安装或者版本不匹配，需要下载 rtools
[RTools: Toolchains for building R and R packages from source on Windows (r-project.org)](https://cran.r-project.org/bin/windows/Rtools/)

step 3：下载对应的 rtools

我下的是 R 4.3.3，所以下载
![[Pasted image 20240409162107.png]]

![[Pasted image 20240409162305.png]]

# Lib 没有指定问题

## 永久指定下载包的路径
因为我的 R 语言下载在 D 盘，想要下载包到 D 盘的library
```R
.libPaths ()
.libPaths ("D:/Software/R-4.3.3/library")
```
