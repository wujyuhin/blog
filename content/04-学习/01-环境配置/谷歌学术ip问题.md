
此次屏蔽的方法主要屏蔽Google部分IP地址的443端口，包括google.com.hk，accounts.google.com的部分IP的443端口被封，导致部分中国用户无法访问Google搜索和Gmail，由于Google的IP地址非常多，而被屏蔽的只是其中部分IP，因此只有部分用户受到了影响。
解决的方法很简单，把如下IP添加到：C:\WINDOWS\system32\drivers\etc\hosts文件里：

203.208.46.146 www.google.com.hk

203.208.46.177 www.google.com.hk

203.208.46.178 www.google.com.hk

209.116.186.251 www.google.com.hk


具体做法新建 hosts.txt，添加上述 ip，然后覆盖原路径文件