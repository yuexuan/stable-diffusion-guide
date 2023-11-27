---
title: 环境搭建及准备
type: docs
weight: 1
prev: docs/infrastructure/
created: 2023-11-15T11:13:12+08:00
date: 2023-11-27T15:56:50+08:00
---
## 容易的开局
![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/5081a7eafd134a73962c344f81afee84~tplv-obj.image?lk3s=3de049d8&traceid=2023112317011619203B17AAEE0119D9DB&x-expires=2147483647&x-signature=w813o0nBiA%2ByEL%2FOCon78MzFI4c%3D)

不用担心他会很难，现在的操作页面已经做的很友善且易用。我们知道，AI绘画的最基本要求是显卡。至于你在那个操作系统上绘画，其实无关紧要。在这个教程里，从大众的普遍性，易用性，较高的容错性，我推荐使用window10及以上的系统，配合英伟达家的显卡。这样即使遇到问题，也能很容易的去找到解决方案。至于Mac OS系统，Linux系统为内核的GUI分发版本，使用AMD显卡的，如果愿意折腾，欢迎issue留言。我将会在博客版本中专门为你提供步骤。

那么问题来了，如果你没有显卡，或者显卡配置过低，又或者现在不是英伟达的显卡，是不是就没办法继续下去了呢？

当然不是啦，该教程的核心宗旨就是，为了没有计算机知识，也没有显卡的用户服务的。在这个链接里，我已经列出来AI绘画相关的网站，其中在显卡部分，也为你指明了方向，[AI绘图网站推荐](https://jinheyong.cn/zh-cn/blog/ai-art-create-website-guide/)， 对于什么都懒的折腾的用户，我十分推荐 https://rundiffusion.com/ 这个网站。虽然费用有点小贵（0.5刀/小时），但省去了折腾的时间，他提供了几种流行的开源webui。按使用时长收费，不使用时记得关闭。
  
因作者目前在中国环境，也没有显卡，我的所有教程都打算租赁[AutoDL算力云 | 弹性、好用、省钱。租GPU就上AutoDL](https://www.autodl.com/)上面的显卡来使用。关于如何购买和选择，使用租赁的显卡，以及遇到的坑，我后续会出相关博文，现在大家可以先凑合看下这篇文章，[【Stable diffusion教程】AutoDL云部署超详细步骤说明](https://zhuanlan.zhihu.com/p/629479857)，[手把手教你在云环境炼丹(部署Stable Diffusion WebUI) - 萤火架构 - 博客园](https://www.cnblogs.com/bossma/archive/2023/07/31/17593492.html)
  
## 配置推荐

说实话，很多人喜欢推荐最低的极限配置，我个人对此持有保留意见。我个人更倾向于合理的配置，我们的目的不是做一个技术极客，而是内容产出效率。来解决我们生产需要的实际问题。因此我给出一个最底线的配置，上限当然越多越好。

- CPU： AMD 或 Intel CPU。这个配置虽然要求不高，但不用轻易忽略，总不能用上个世纪的CPU。
- RAM：至少 16 GB DDR4 或 DDR5 RAM。
- 存储：256 GB 或更大的SATA 或 NVMe 固态驱动器。您需要至少 10 GB 的可用空间。通常，1 TB 驱动器提供每 GB 存储的最佳价格。（一般模型的尺寸都非常大，越大的存储空间，越方便存储更多的模型，使用固态硬盘要优先于传统的磁盘，在读写速率上有很大的提升）
- GPU：具有至少 16 GB GDDR6 内存的 GeForce RTX GPU。很多人会忽略带宽问题，带宽没有一个确定的标准，选择时注意越大越好。


![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/817f035424bd4b9eafe7d6087fa32428~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=MmriN0STqJve1ci6AzCX40YnUB8%3D)

下面是相对4090的出图速度：

|   |   |   |
|---|---|---|
|型号|出图速度  <br>（张/每分钟）|相对  <br>RTX 4090|
|RTX 3060 12GB|4.36|22.10%|
|RTX 2060 Super|4.38|22.20%|
|RTX 4060|4.67|23.67%|
|RTX 2070 Super|4.8|24.33%|
|RTX 3060 Ti|5.19|26.31%|
|RTX 2080 Super|5.36|27.17%|
|RTX 4060 Ti 8GB|6.28|31.83%|
|RTX 3070|6.61|33.50%|
|RTX 3070 Ti|6.94|35.17%|
|RTX 3080 10GB|8.89|45.06%|
|RTX 4070|9.09|46.07%|
|RTX 3080 Ti|10.01|50.73%|
|RTX 3090|10.55|53.47%|
|RTX 4070 Ti|10.71|54.28%|
|RTX 3090 Ti|11.01|55.80%|
|RTX 4080|13.48|68.32%|
|RTX 4090|19.73|100.00%|

以上可以看到，显卡对出图速率和效果有着不言而喻的重要性。

## 环境搭建

假设你已经看了前两节的内容，并准备好了学习用到的显卡，以及windows系统，那么相信你已经迫不及待的配置一个属于自己的Stable Diffusion控制台了。

本地安装，是指直接基于windows系统（该系统可以在你本地，也可以是在云上运行），进行一步步的环境搭建安装（我没有真实的本地环境，内容都是按照网络整理，步骤均没有问题）。

云环境，一般是显卡租赁平台提供一张显卡，以及docker容器类的运行环境，模型数据，图片数据，可以存放于网络云盘上。也是我后续会主要介绍的。

## 本地安装

1. 环境检查

看显卡、看内存、看硬盘、看CPU。其中最重要的是看显卡，显卡N卡（英伟达Nvida显卡，A卡用不了），最低10系起步，显存最低4G，6G及格；内存最低8G，16G及格；硬盘可用空间最好有个500G朝上，固态最佳，机械硬盘也没多大问题。CPU其实没太大要求，有好显卡的，CPU一般不会很差。

不会看自己显卡的，可以右键任务栏打开任务管理器，也可以快捷键打开，按顺序连续按住Ctrl、Alt和Delete键，有4G以上就可以，4G其实不是太够。

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/9764564ca995427b8449ab6703d04f2b~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=2FtFS0DGqAhcnfrY6%2FiZQLgNoEE%3D)

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/ef9aea54edf24f84a27a5a48dfeb508c~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=woDeU%2FpkT%2Fdwfeho6URLC%2B8oEpg%3D)

2. Python安装

去python官网，下载最新的python版本即可。https://www.python.org/downloads/

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/84904f4d0c814ae4b6a6f337583a5cf1~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=j1H1kH0g%2FjPCZuT%2FzwTzzll%2FX8U%3D)

当前最新的是3.12.0

windows版的Python安装包是exe文件，下载后只需要无脑点击即可，这里记得选中“Add python.exe to Path”，可以避免人工再去配置环境变量

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/5ebba74062614052b8ec66b3f1e3f1cc~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=6B%2BGwZOUXVENOwdBiAhqyldZRI4%3D)

这里为了方便，我们直接选择“Install Now”，默认会把必备的都装上

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/a3c06ed65f9a4cbeac71b1fc88043605~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=jbGf0y8wlS%2BVi8KiRbhOhe6l32M%3D)

安静等待安装~

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/c3cc817effb44c86977dbf4391b7fc66~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=bquTbyUYeo8wXldp9%2Bz%2BSqqwMo0%3D)

然后如果弹出下面这个框，点击“Disable path length limit”的按钮，然后点击close关闭。“Disable path length limit”是指，禁用系统的Path长度自动限制，能给我们避免很多的麻烦。禁用路径长度限制更改计算机配置，以允许包括Python在内的程序绕过260个字符的“最大路径”限制。这是说明你电脑对Python的一些限制，点击它然后确定权限就可以了

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/b731467ec66b4f029771c516393c3810~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=bbi3%2BO4TdiGjpMdjeaNpoABoy1Y%3D)

`Win` `R` 快速打开cmd，输入`python --version`可以验证是否正确安装

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/937d0526ad724f079598bb45e6687311~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=Klc1CFncvycJw4Y3dPA6dvMRBQ0%3D)

**环境变量****配置（非必要）**

1、如果忘了选中“Add python.exe to Path”，可能这里无法正确执行python命令，需要手动添加环境变量

2、右键我的电脑，点击属性，弹出如下界面

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/260170bd99274129946acec11c5fe556~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=ugJlb6CcLFy6HwqV%2FfHSOgPWT1w%3D)

3、点击高级系统设置，出现下图，选择环境变量

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/2d5576e0cc044a0aa35b01fb2c6b1a79~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=hYPkZXiai6%2Bd3jTmXkXxZidaWFE%3D)

4、找到系统变量里面的Path，编辑它，将python解释器所在路径粘贴到最后面，再加个分号，至此环境变量配置完成，再打开命令行输入python即可看到正确的显示。

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/67041cb493874855a361506e65df6de0~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=oPYBNm4mI5vgV0UwyCT3FkzrcLs%3D)

3. git安装
下载地址：[https://git-scm.com/download/win](https://git-scm.com/download/win)

Git作用是拉取远程Github仓库代码，可以让Stable Diffusion实时更新，第一时间使用全新功能。（webui更新非常快，有时候一个月发布十几次更新）

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/2bfc16a173ad4ac9a5a9f9cfb1aaf0f6~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=%2Fs9mIlEGD5%2Bvr9zR9nPU9um3v10%3D)

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/fac60217a0b34010a919ff22cdd003e9~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=XSGIpV6H8R5vuyjaIV9EUrjYeu0%3D)

安装完成后，通过CMD命令对运行环境进行检查。

【Win+R】唤出【运行】，输入“cmd”，回车，在命令行里输入

```Plain
git --version
```

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/b9e434184a2b4d8b960ca91725bf8071~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=RUi5%2BEVk4uM%2Bk0%2Ba3hlbXW9mM8Q%3D)

4.  cuda安装

下载地址：[https://developer.nvidia.com/cuda-toolkit-archive]() CUDA是NVIDIA显卡用来跑算法的依赖程序，先在“命令提示符”运行命令`nvidia-smi`查看自己显卡支持的 CUDA版本（升级驱动程序可以支持更高级的CUDA版本）

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/0d4eb345ff634832be94d54206ee20d5~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=aBZ5UvEvvBFPd5Yjtf7rajp8Jsw%3D)

接下来前往英伟达官网[https://developer.nvidia.com/cuda-toolkit-archive](https://developer.nvidia.com/cuda-toolkit-archive)，下载对应版本。 注意请下载你对应的版本号最高的版本，比如我的是11.5的，那就下11.5.2（这里最后的.2意思是，11.5版本的2号升级版）

CUDA驱动版本与CUDA ToolKit对应关系: [https://docs.nvidia.com/cuda/cuda-toolkit-release-notes/index.html#major-components](https://sspai.com/link?target=https%3A%2F%2Fdocs.nvidia.com%2Fcuda%2Fcuda-toolkit-release-notes%2Findex.html%23major-components)

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/8befe93a72f14ea19431fe7ff0217704~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=aEKOHKMWYt0cGC3DCUjuOu2LlXw%3D)

下载的时候注意下载exe_local（离线安装包），在线可能比较慢

安装完成之后，可以使用如下命令查看 CUDA 版本

```JavaScript
nvcc --version
```

5.  **Stable Diffusion** **web UI** **安装**
打开cmd，通过git下载stable diffusion webui

在磁盘中新建一个文件夹，如下图名为【AI】的文件夹，然后在这个文件夹里点击鼠标右键，选择【Git Bash Here】打开Git终端

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/d7562c6c926743c98e65fc1dc6e055c4~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=FPnuwCuYwugoRF3eldqszsIz92s%3D)

![](https://p26-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/273da55abf18478eac105158235abcbf~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=DFyHZeztJ5fqYyFsQgWXQy4qLcA%3D)

通过Git命令克隆下载代码，如下：

```Plain
git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui.git 
```

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/610774cf63a943f290a3173ad4e64482~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=m2nRALYfDCbl1iccsTn%2FDbPXT%2BE%3D)

你将会看到这样的一个文件夹。如果你下载遇到问题，提示网络失败，或者https安全校验等问题，你也可以直接去github[https://github.com/AUTOMATIC1111/stable-diffusion-webui.git ](https://github.com/AUTOMATIC1111/stable-diffusion-webui.git )网页下载后解压文件。（该方式不利于后续对webui的升级，不是太推荐）

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/2d90b65b76e746b3a65fbb513e8e7095~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=ja6Ql5H0cpnPDc4VI1wyqvwZN%2F4%3D)

6.  **运行webui-user.bat**

打开stable-diffusion-webui目录，你能看到，webui-user.bat这个文件，双击运行吧。

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/80e0fb8564284d278618be0f0772cdec~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=ZksM%2Ffyo0344riWQNHXoQHxU%2B04%3D)

运行过程，取决于你的网络环境。一般10~30min可以完成。

直到最后出现http://127.0.0.1:7860的地址，说明已经可以正常运行。（注意不要关闭这个窗口，关闭就退出了）

复制http://127.0.0.1:7860到浏览器打开（可以保存为书签，下次打开比较方便），然后就可以输入咒语生成图片了

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/79fbc07b66d149379f3fda174c6af350~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=I%2FsPo63dg3mfbUDioj1liqRZ29E%3D)

是不是觉得很麻烦？

麻烦就对了，这是编程人员的运行方式，其实上面的步骤，你都可以不用去理解的，知道他很复杂就行了，于是就有朋友提供了整合包。你可以一键安装他们。

## 整合包安装

秋葉aaaki

秋葉aaaki整合包介绍：[https://www.bilibili.com/video/BV1iM4y1y7oA](https://www.bilibili.com/video/BV1iM4y1y7oA)

整合包下载地址：[https://pan.baidu.com/s/1TK7UyX5lgNjdwdfcmYCI5Q](https://pan.baidu.com/s/1TK7UyX5lgNjdwdfcmYCI5Q) 提取码：c132

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/dec17d88bc5f4a70ae07fc0993eebc4a~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=4bhNXTTL%2FR2lk0VYH0MM2UjpuRY%3D)

或StabilityMatrix，[GitHub - LykosAI/StabilityMatrix: Multi-Platform Package Manager for Stable Diffusion](https://github.com/LykosAI/StabilityMatrix) 的启动器，下载安装即可。

![](https://p26-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/5509f272d2b64f2883cf58c236401aae~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=%2FP11iI76QvNmH8NpKVfIEjNJMOQ%3D)

这些启动器，均已集成了python环境，和模型。一键运行即可食用。

不管是自己手动安装，还是整合包安装，面对本机多变的环境，难免会遇到很多错误，或收集网络资料来解决，或根本不其可云，无法解决。那么我诚心的推荐你使用云环境，现在的云环境，基本上大多都集成了一键stable diffusion webui。只管付费运行即可。

## 云环境安装

【后续更新其他平台，目前先AutoDL】

[【Stable diffusion教程】AutoDL云部署超详细步骤说明](https://zhuanlan.zhihu.com/p/629479857)，

[手把手教你在云环境炼丹(部署Stable Diffusion WebUI) - 萤火架构 - 博客园](https://www.cnblogs.com/bossma/archive/2023/07/31/17593492.html)