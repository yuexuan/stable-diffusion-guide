---
title: Env Preparation | Guide
type: docs
weight: 1
prev: docs/infrastructure/
created: 2023-11-15T11:13:12+08:00
date: 2023-11-27T15:56:21+08:00
---
## Easy Start

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/5081a7eafd134a73962c344f81afee84~tplv-obj.image?lk3s=3de049d8&traceid=2023112317011619203B17AAEE0119D9DB&x-expires=2147483647&x-signature=w813o0nBiA%2ByEL%2FOCon78MzFI4c%3D)

Don't worry; it's not going to be too difficult. The current operating interface is user-friendly and easy to use. We know that having a good graphics card is crucial for AI drawing. The choice of the operating system is not critical; however, for the sake of general popularity, ease of use, and higher fault tolerance, I recommend using Windows 10 or later, paired with an NVIDIA graphics card. This way, even if you encounter problems, finding solutions will be relatively easy. For users on macOS or Linux systems with AMD graphics cards, if you're willing to tinker a bit, feel free to leave an issue. I'll provide step-by-step instructions in a dedicated blog post.

Now, the question is, what if you don't have a graphics card, or your graphics card is too low-end, or it's not an NVIDIA card? Does that mean you can't proceed?

Of course not! The core principle of this tutorial is to cater to users without much computer knowledge or a dedicated graphics card. In [this link](https://jinheyong.cn/zh-cn/blog/ai-art-create-website-guide/), I have listed AI drawing-related websites, including guidance on graphics cards. For users who don't want to bother with configurations, I highly recommend [rundiffusion.com](https://rundiffusion.com/). Although it's a bit expensive ($0.5/hour), it saves you the hassle, providing several popular open-source web UIs. They charge based on usage time, so remember to close it when not in use.

Since I'm currently in a Chinese environment and don't have a graphics card, I plan to use the graphics cards on [AutoDL](https://www.autodl.com/). I will write related blog posts about purchasing and selecting leased graphics cards, as well as the pitfalls you may encounter. For now, you can take a look at [this article](https://zhuanlan.zhihu.com/p/629479857) and [this blog post](https://www.cnblogs.com/bossma/archive/2023/07/31/17593492.html) for detailed steps on deploying Stable Diffusion WebUI on the AutoDL cloud.

## Recommended Configurations

To be honest, many people like to recommend the minimum configurations, but I personally reserve judgment on this. I lean towards reasonable configurations because our goal is not to be a tech geek but to enhance content production efficiency to solve real-world problems. So, here's the minimum baseline configuration, and the more, the better.

- CPU: AMD or Intel CPU. While the requirement for this configuration is not high, don't overlook it. You shouldn't use a CPU from the last century.
- RAM: At least 16 GB DDR4 or DDR5 RAM.
- Storage: 256 GB or larger SATA or NVMe solid-state drive. You need at least 10 GB of available space. Typically, a 1 TB drive offers the best price per GB of storage. (Since the sizes of general models are quite large, more storage space is convenient for storing more models. Using an SSD is preferable to a traditional disk, providing a significant improvement in read and write speeds.)
- GPU: GeForce RTX GPU with at least 16 GB GDDR6 memory. Many people overlook bandwidth issues, and there is no specific standard for bandwidth, so choose the largest available.

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/817f035424bd4b9eafe7d6087fa32428~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=MmriN0STqJve1ci6AzCX40YnUB8%3D)


Here's the relative rendering speed compared to the RTX 4090:

|Model|Rendering Speed (Images/Minute)|Relative to RTX 4090|
|---|---|---|
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

As you can see, the graphics card plays a crucial role in rendering speed and quality.

## Environment Setup

Assuming you've read the previous sections and have prepared to learn how to use a graphics card, let's dive into setting up your own Stable Diffusion console.

**Local Installation**

1. Environment Check

Check your graphics card, memory, hard drive, and CPU. The most crucial element is your graphics card—NVIDIA (Nvidia graphics card) starting from the 10 series, with a minimum of 4GB graphics memory (6GB is better). Memory should be at least 8GB (16GB is better), and your hard drive should ideally have 500GB or more, with SSD being the best choice. The CPU doesn't have strict requirements, as long as it's not outdated.

If you don't know how to check your graphics card, you can open the task manager by right-clicking on the taskbar or using the shortcut `Ctrl + Alt + Delete` and holding them down in sequence. If you have 4GB or more, you're good to go.
![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/9764564ca995427b8449ab6703d04f2b~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=2FtFS0DGqAhcnfrY6%2FiZQLgNoEE%3D)
![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/ef9aea54edf24f84a27a5a48dfeb508c~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=woDeU%2FpkT%2Fdwfeho6URLC%2B8oEpg%3D)

2. Python Installation

Go to the Python official website and download the latest version: [Python Downloads](https://www.python.org/downloads/)
![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/84904f4d0c814ae4b6a6f337583a5cf1~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=j1H1kH0g%2FjPCZuT%2FzwTzzll%2FX8U%3D)

Choose the "Install Now" option and make sure to select "Add python.exe to Path" to avoid manual configuration.
![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/a3c06ed65f9a4cbeac71b1fc88043605~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=jbGf0y8wlS%2BVi8KiRbhOhe6l32M%3D)

Once downloaded, click through the installation process.
![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/c3cc817effb44c86977dbf4391b7fc66~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=bquTbyUYeo8wXldp9%2Bz%2BSqqwMo0%3D)
![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/b731467ec66b4f029771c516393c3810~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=bbi3%2BO4TdiGjpMdjeaNpoABoy1Y%3D)
Next, open the command prompt by pressing `Win + R`, type `python --version`, and press Enter to verify the installation.
![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/937d0526ad724f079598bb45e6687311~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=Klc1CFncvycJw4Y3dPA6dvMRBQ0%3D)
**Optional: Environment Variable Configuration**

1. If you forgot to select "Add python.exe to Path," you may need to manually add the environment variable.

2. Right-click on "This PC" or "My Computer," select Properties, and go to Advanced system settings.
        ![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/260170bd99274129946acec11c5fe556~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=ugJlb6CcLFy6HwqV%2FfHSOgPWT1w%3D)
3. Click on Environment Variables.
   ![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/2d5576e0cc044a0aa35b01fb2c6b1a79~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=hYPkZXiai6%2Bd3jTmXkXxZidaWFE%3D)
4. In the System variables section, find the Path variable, click Edit, and add the path to the directory where the Python interpreter is located. Remember to add a semicolon (;) before pasting.
    ![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/67041cb493874855a361506e65df6de0~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=oPYBNm4mI5vgV0UwyCT3FkzrcLs%3D)

3. Git Installation

Download Link: [https://git-scm.com/download/win](https://git-scm.com/download/win)

Git is used to fetch code from remote Github repositories, allowing real-time updates for Stable Diffusion. This ensures timely access to new features, as the web UI is frequently updated, sometimes with more than ten releases in a month.
![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/2bfc16a173ad4ac9a5a9f9cfb1aaf0f6~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=%2Fs9mIlEGD5%2Bvr9zR9nPU9um3v10%3D)

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/fac60217a0b34010a919ff22cdd003e9~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=XSGIpV6H8R5vuyjaIV9EUrjYeu0%3D)
After downloading, install Git and check the runtime environment using the following CMD command:

[Win+R] to open [Run], type "cmd," press Enter, and in the command line, enter:

PlainCopy code

`git --version`

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/b9e434184a2b4d8b960ca91725bf8071~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=RUi5%2BEVk4uM%2Bk0%2Ba3hlbXW9mM8Q%3D)



4. CUDA Installation

Download Link: [https://developer.nvidia.com/cuda-toolkit-archive](https://chat.openai.com/c/20717714-2e83-42ea-95d6-5578e8783599)

CUDA is a dependency program for NVIDIA graphics cards to run algorithms. First, run the command `nvidia-smi` in the command prompt to check your GPU's supported CUDA version. Updating the driver may enable support for a higher CUDA version.

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/0d4eb345ff634832be94d54206ee20d5~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=aBZ5UvEvvBFPd5Yjtf7rajp8Jsw%3D)

Next, visit the NVIDIA official website [https://developer.nvidia.com/cuda-toolkit-archive](https://developer.nvidia.com/cuda-toolkit-archive) and download the corresponding version. Ensure you download the highest version number compatible with your GPU; for example, if you have version 11.5, download 11.5.2 (where .2 indicates the 2nd update for version 11.5).

CUDA Driver Version vs. CUDA Toolkit Compatibility: [https://docs.nvidia.com/cuda/cuda-toolkit-release-notes/index.html#major-components](https://sspai.com/link?target=https%3A%2F%2Fdocs.nvidia.com%2Fcuda%2Fcuda-toolkit-release-notes%2Findex.html%23major-components)

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/8befe93a72f14ea19431fe7ff0217704~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=aEKOHKMWYt0cGC3DCUjuOu2LlXw%3D)

When downloading, choose the 'exe_local' (offline installer) as online installation may be slower.

After installation, check the CUDA version with the following command:

JavaScriptCopy code

`nvcc --version`

5. Stable Diffusion Web UI Installation

Open CMD and download Stable Diffusion web UI using Git.

Create a new folder on your disk, e.g., named 'AI.' Right-click inside the folder and choose 'Git Bash Here' to open the Git terminal.

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/d7562c6c926743c98e65fc1dc6e055c4~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=FPnuwCuYwugoRF3eldqszsIz92s%3D)

![](https://p26-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/273da55abf18478eac105158235abcbf~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=DFyHZeztJ5fqYyFsQgWXQy4qLcA%3D)

Clone the code using the Git command:

PlainCopy code

`git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui.git` 

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/610774cf63a943f290a3173ad4e64482~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=m2nRALYfDCbl1iccsTn%2FDbPXT%2BE%3D)

You will see a folder like this. If you encounter issues with downloading, such as network failures or HTTPS security verification problems, you can also download and unzip the file directly from the GitHub page [https://github.com/AUTOMATIC1111/stable-diffusion-webui.git](https://github.com/AUTOMATIC1111/stable-diffusion-webui.git) (not recommended for future web UI upgrades).

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/2d90b65b76e746b3a65fbb513e8e7095~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=ja6Ql5H0cpnPDc4VI1wyqvwZN%2F4%3D)

6. Run webui-user.bat

Open the stable-diffusion-webui directory, and you will see the 'webui-user.bat' file. Double-click to run it.

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/80e0fb8564284d278618be0f0772cdec~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=ZksM%2Ffyo0344riWQNHXoQHxU%2B04%3D)

During the run, the duration depends on your network environment, usually taking 10-30 minutes to complete. Wait until you see the address [http://127.0.0.1:7860](http://127.0.0.1:7860/), indicating that it is running successfully. Do not close this window; closing it will exit the process.

Copy [http://127.0.0.1:7860](http://127.0.0.1:7860/) to your browser (you can save it as a bookmark for convenience), and now you can input commands to generate images.

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/79fbc07b66d149379f3fda174c6af350~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=I%2FsPo63dg3mfbUDioj1liqRZ29E%3D)

Feeling overwhelmed?

That's normal; this is the developer's way of running things. You don't necessarily need to understand all the steps, just know that it's a complex process. To simplify, some enthusiasts have provided integrated packages that you can install with a single click.

## Integrated Package Installation

**秋葉aaaki**

Check out the introduction to 秋葉aaaki's integrated package: [https://www.bilibili.com/video/BV1iM4y1y7oA](https://www.bilibili.com/video/BV1iM4y1y7oA)

Download Link:
[https://pan.baidu.com/s/1TK7UyX5lgNjdwdfcmYCI5Q](https://pan.baidu.com/s/1TK7UyX5lgNjdwdfcmYCI5Q) 
Extraction Code: c132

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/dec17d88bc5f4a70ae07fc0993eebc4a~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=4bhNXTTL%2FR2lk0VYH0MM2UjpuRY%3D)
    
**StabilityMatrix**

Launcher from [GitHub - LykosAI/StabilityMatrix](https://github.com/LykosAI/StabilityMatrix). Download and install.

![](https://p26-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/5509f272d2b64f2883cf58c236401aae~tplv-obj.image?lk3s=3de049d8&traceid=2023112318141748BF73F48B0FFF1EBAE2&x-expires=2147483647&x-signature=%2FP11iI76QvNmH8NpKVfIEjNJMOQ%3D)

These launchers are integrated with Python environments and models. Simply run them with a single click.

Whether you choose manual installation, integrated packages, or cloud environments, errors may occur due to the variability of your local environment. In such cases, you may need to troubleshoot by collecting information online or, in some cases, find that it's beyond your expertise. In that case, I sincerely recommend using a cloud environment, where most platforms offer one-click Stable Diffusion web UI setups. Just pay and run