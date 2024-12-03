#环境配置

新版本的torch于torchvision对应[torch torchvision版本对应关系_python torch torchversion 对应版本-CSDN博客](https://blog.csdn.net/xcls2010/article/details/125553626)
重新下载对应本地版本[download.pytorch.org/whl/torch_stable.html](https://download.pytorch.org/whl/torch_stable.html)

# 一、安装CUDA

## 1.检查电脑有无独立显卡

任务管理器→性能：如果有NVIDIA 的GPU，则有独立的NVIDIA显卡。

  ![](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image002.jpg)![QQ图片20230709105049](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image004.png)

## 2.查看电脑NVIDIA支持的CUDA版本

在开始栏查找NVIDIA Control Panel，并打开→帮助→系统信息→组件：找到CUDA对应的版本，示例对应的CUDA是10.2版本。

 ![QQ图片20230709104802](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image006.png)→ ![QQ图片20230709104832](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image008.png)

## 3.下载CUDA

CUDA安装链接：[https://developer.nvidia.com/cuda-toolkit-archive](https://developer.nvidia.com/cuda-toolkit-archive)

打开链接→找到与自己电脑CUDA 版本对应的链接

![QQ图片20230709105809](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image010.png)

→依次点击绿键，直到出现Download，点击base installer对应的download即可。

![QQ图片20230709110020](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image012.png)

## 4.安装CUDA

→找到下载好的安装包双击下载；![QQ图片20230709112805](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image014.png)

→建议C盘，下文环境配置可以用和我一样的路径

![QQ图片20230709113053](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image016.png)

→在到这一步的时候选择精简版；

![QQ图片20230709113155](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image018.png)  
→勾选上选项；

![QQ图片20230709113226](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image020.png)

→两个选项均无需勾选，点击关闭，安装完成。

![QQ图片20230709113252](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image022.png)

## 5.CUDA环境变量配置（此处仅示范配置环境变量，因为换了电脑，所以cuda版本更换为11.3）

→CUDA安装完毕后，右击此电脑，点击属性，

![20190829173437193](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image024.jpg)

→选择高级系统设置

![QQ图片20230712121514](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image026.jpg)

→选择环境变量

![QQ图片20230712121758](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image028.jpg)

→点击新建

![](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image030.jpg)

→首先添加CUDA_PATH=C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.3

（注：这是我的安装位置，此处应默认你的安装路径，一般安装cuda之后默认自带）

![](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image032.jpg)

→然后添加CUDA_SDK_PATH= C:\ProgramData\NVIDIA Corporation\CUDA Samples\v11.3

(注：这是我的安装位置，此处应默认你的安装路径，你的可能是其他盘，和其他版本）

![](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image034.jpg)

→同样的方式添加以下四个变量（这四个变量不需要考虑路径是你的还是我的）

CUDA_LIB_PATH = %CUDA_PATH%\lib\x64

CUDA_BIN_PATH = %CUDA_PATH%\bin

CUDA_SDK_BIN_PATH = %CUDA_SDK_PATH%\bin\win64

CUDA_SDK_LIB_PATH = %CUDA_SDK_PATH%\common\lib\x64

→最终结果如下，总共六个路径。

![](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image036.jpg)

→选择系统变量PATH，点击编辑，弹出右边界面

 ![QQ图片20230712124359](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image038.jpg) ![](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image040.jpg)

→选择新建，在末尾添加以下八行，如果你安装默认路径直接抄，如果不是就找到对应路径：

%CUDA_LIB_PATH%

%CUDA_BIN_PATH%

%CUDA_SDK_LIB_PATH%

%CUDA_SDK_BIN_PATH%

C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.3\lib\x64

C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.3\bin

C:\ProgramData\NVIDIA Corporation\CUDA Samples\v11.3\common\lib\x64

C:\ProgramData\NVIDIA Corporation\CUDA Samples\v11.3\bin\win64

![](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image042.jpg)

→接下来，检验配置是否成功。Windows+R键启动cmd，

→输入cd C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.3\extras\demo_suite

（这是我的demo_suite的位置，如果安装的时候按在其他盘，请看自己demo_suite所在位置）

→→输入bandwidth.exe，出现Result=PASS

![](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image044.jpg)

→输入deviceQuery.exe,出现Result=PASS。

![](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image046.jpg)

以上两步均出现Result=PASS，表明CUDA环境设置成功。若出现问题，则往前查看自己路径是否输入错误。因为路径里面是有这两个可执行文件

![QQ图片20230712125141](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image048.jpg)

# 二、安装CUDNN

## 1.下载CUDNN

CUDNN下载链接：[https://developer.nvidia.com/rdp/cudnn-archive#a-collapse742-10](https://developer.nvidia.com/rdp/cudnn-archive#a-collapse742-10)

打开链接，找到对应版本链接→点击之后需要注册→注册完毕后，重新选择版本下载即可

（注：下图仅为示例，具体版本按照自己CUDA版本对应，我上面下的是CUDA10.2）

 ![QQ图片20230709111803](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image050.jpg) ![QQ图片20230709111852](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image052.jpg)

## 2.安装CUDNN

目的：将下载的CUDNN压缩包里面的文件，复制到CUDA的安装目录下

第一步：将cudnn解压

![QQ图片20230712130847](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image054.jpg)

第二步：将里面的四个文件复制到上面的v10.2

→按照刚刚下载的路径，找到NVIDIA GPU Computing Toolkit，依次打开到v10.2，放在一边。

CUDA的安装目录下

![](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image056.jpg)

→替换成功，此时CUDA和CUDNN操作完毕！

![QQ图片20230712170511](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image058.jpg)

# 三、安装anaconda

## 1.下载anaconda

Anaconda官网网址：[https://www.anaconda.com/dowmload](https://www.anaconda.com/dowmload) (下载很慢）

清华镜像版网址：[https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/](https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/) (下载快）

→选择相应版本下载

![QQ图片20230709115528](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image060.png)

## 2.安装anaconda

→双击下载好的软件安装

![QQ图片20230709143101](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image062.jpg)

→点击next

![QQ图片20230712133222](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image064.jpg)

→点击I Agree

![QQ图片20230712133226](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image066.jpg)

→选择just me，点击next

![QQ图片20230712133231](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image068.jpg)

→建议保存在内存较大的网盘

![QQ图片20230712133236](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image070.jpg)

→将所有选项都选上，点击Intall

![QQ图片20230712133240](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image072.jpg)

【注1】：如果这一步没有选择第一个选项，则需要自己手动设置环境变量，操作可参考下面的【注2】。

→点击next

![QQ图片20230712133245](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image074.jpg)

→next

![QQ图片20230712134032](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image076.jpg)

→Finish

![QQ图片20230712134036](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image078.jpg)

→出现以下界面安装完成

![QQ图片20230712134041](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image080.jpg)

## 3.检验anaconda安装成功

→快捷键Windows+r，出现cmd，点确定（或者直接在开始栏输入cmd）

![QQ图片20230709143605](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image082.jpg)

→输入conda info 查看python版本

→输入python 查看python版本

→如果版本相同，则安装成功！

![](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image084.jpg)

## 4.anaconda环境配置（选择性看）

如果在安装anaconda的时候出现红色字体不能勾选，则需要手动配置环境。

【注2】：如何手动设置环境变量？

→右击此电脑，点击属性→选择高级系统设置→选择环境变量

→选择Path，点击编辑

![](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image086.jpg)

→点击新建，输入Anaconda位置，

（注：Anaconda安装在哪里，就去哪里找位置。这里是安装在D盘）

![](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image088.png)

# 四.安装pycharm

## 1.下载pycharm

Pycharm官网网址：[https://www.jetbrains.com/pycharm](https://www.jetbrains.com/pycharm)

打开官网并滑动到底下，找到社区版下载

![](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image090.jpg)

## 2.安装pycharm

→双击下载好的软件

![QQ图片20230712135204](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image092.jpg)

→next

![QQ图片20230712135209](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image094.jpg)

→建议下载到内存较大的网盘，点击next

![QQ图片20230712135214](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image096.jpg)

→建议全部勾选上，点击next

![QQ图片20230712135218](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image098.jpg)

→Intall

![QQ图片20230712135222](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image100.jpg)

→next

![QQ图片20230712135227](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image102.jpg)

→建议选择立刻重启，点击Finish

![QQ图片20230712135231](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image104.jpg)

（注：anaconda和pycharm安装过程视频推荐观看：【【python编程环境安装】全网最详细python环境安装。pycharm和anaconda手把手安装教学。-哔哩哔哩】 [https://b23.tv/ANrm2N0](https://b23.tv/ANrm2N0)）  

# 五、安装torch和torchvision

## 1.下载torch和torchvision文件

→根据自己想用的python版本，找到对应torch和torchvision版本（跟我一样选用python3.6-3.9）

![423404ba8a224410b0aaf5f3e5c4de15](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image106.jpg)

→下载链接：[https://download.pytorch.org/whl/torch_stable.html](https://download.pytorch.org/whl/torch_stable.html)

打开链接，呈现如下画面

![d712466827f7454f89bfaf21fb6662e0](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image108.jpg)

→找对应的版本，

例如：cuda10.2和python3.7，匹配torch 1.10.2和torchvison 0.11.3。

红色箭头：cu102代表cuda 10.2

绿色箭头：代表torch 1.10.2与torchvision0.11.3

蓝色箭头：代表python是3.7版本

黑色箭头：代表Windows版本

 ![](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image110.jpg) ![](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image112.jpg)

→点击下载即可。

## 2.安装torch和torchvision

## 3.用conda创建虚拟环境

→打开anaconda prompt

![6066ef4c9bdf42ceb337d77a60e29df5](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image114.jpg)

→输入conda create -n Torch python=3.7（这里python版本对应自己的，此处是在创建名字为Torch的环境，且该环境声明的python版本为3.7）

![](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image116.jpg)

→输入y回车

![QQ图片20230712141549](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image118.jpg)

→环境创建完成后，再输入activate Torch，进入刚刚创建的Torch环境

![QQ图片20230712141553](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image120.jpg)

## 4.在创建的虚拟环境中安装torch和torchvision

→找到torch和torchvision路径，

我的路径是C:\Users\Lenovo\Downloads，大家找到自己对应的路径。

![QQ图片20230712144007](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image122.jpg)

→输入cd C:\Users\Lenovo\Downloads

→如果没有切换的话，再输入一次对应的盘符，我的盘符是C，所以输入C:

![](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image124.jpg)

→再输入pip install (torch文件名）

![](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image126.jpg)

→同样的输入pip install (torchvision的文件名)就可以安装torchvision了

→最后检验是否成功，

![](file:///C:/Users/wujyu/AppData/Local/Temp/msohtmlclip1/01/clip_image128.jpg)


# 六、升级 cuda
升级教程连接 [windows cuda更新教程_cuda 12.0-CSDN博客](https://blog.csdn.net/weixin_51066144/article/details/128105318)
## 1. 进入控制面板删除 cuda
![[Pasted image 20240411100003.png]]
## 2. 查看本机能支持的版本
右键进入 nividia-系统信息-组件-支持 cuda12.3
![[Pasted image 20240411100127.png]]
![[Pasted image 20240411100222.png]]

## 3. 下载相应版本 cuda
进入官网 [cuda官网](https://developer.nvidia.com/cuda-toolkit-archive), 
本机支持 12.3，因此下载 12.3.2 版本cuda
![[Pasted image 20240411100442.png]]
## 4. 安装 cuda
![[Pasted image 20240411102334.png]]
![[Pasted image 20240411102527.png]]
![[Pasted image 20240411102542.png]]
**反勾选 vs inteegration**
![[Pasted image 20240411103721.png]]

![[Pasted image 20240411102358.png]]

### 可能出现安装程序错误！
参考文章[英伟达NVIDIA驱动程序安装失败/解决N卡安装失败问题 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/110530306)


## 5. 下载对应cudnn 版本对应
cnDNN 历史版本下载地址 https://developer.nvidia.com/rdp/cudnn-archive
![[Pasted image 20240411101230.png]]
![[Pasted image 20240411101250.png]]
## 6. 复制文件
下载后共三个文件夹，分别复制到 cuda 对应文件夹内

## 7.检验是否安装 cuda 与 cudnn 成功
命令行查看安装版本
```
nvcc -V
```

进入到 cuda 的安装路径 `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v10.2\extras\demo_suite`，执行 `deviceQuery.exe`

同样进入 cudnn 路径 在 `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v10.2\extras\demo_suite` 目录下执行 `bandwidthTest.exe`，出现如下界面
# 升级 torchvision
## 查看自己 torch 版本
是 2.2.2 + cu121
![[Pasted image 20240411110236.png]]

## 打开 gitgub 查看对应 torchvision 版本
[pytorch/vision: Datasets, Transforms and Models specific to Computer Vision (github.com)](https://github.com/pytorch/vision)
![[Pasted image 20240411110124.png]]
## 下载版本
打开下载链接 [download.pytorch.org/whl/torch_stable.html](https://download.pytorch.org/whl/torch_stable.html)
直接锁定自己要的 python 版本的torchvision
![[Pasted image 20240411110355.png]]
# 升级 torch
## 在官网查看
进入官网 [PyTorch](https://pytorch.org/)，下滑
![[Pasted image 20240411105203.png]]

直接下载，pytorch 官网上的版本低是可以的，电脑安装的 cuda 能向下兼容
