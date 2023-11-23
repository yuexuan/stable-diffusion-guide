---
title: Env Preparation | Guide
type: docs
prev: docs/infrastructure/
created: 2023-11-15T11:13:12+08:00
date: 2023-11-23T17:51:11+08:00
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

![Comparison with RTX 4090](https://w5wc4ktwyr.feishu.cn/space/api/box/stream/download/asynccode/?code=NDJlZDQyOTI1YjJjNjdjMjBiMzQxMWJmOTA1N2VhYjNfR1l5N0pUenFBYzcyRTJBVlpmdmlya2RxbktKV05xTWxfVG9rZW46VWo5MGJBSGdQb3JDeGp4VkoyM2NKcmxvbjllXzE3MDA3MzAzODI6MTcwMDczMzk4Ml9WNA)

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
![](https://w5wc4ktwyr.feishu.cn/space/api/box/stream/download/asynccode/?code=YWI3N2UwYThiY2ZkOGMwMjk5YzYxMDRkMDkwNzgyZGFfZjBjRXdVVzJqQWZOQ3hsV0llSnZhVWdic3U2SVhzMG1fVG9rZW46TUc3RWI2WXpQb1Y3MmR4emdjQ2NGbzhLbk5iXzE3MDA3MzAzODI6MTcwMDczMzk4Ml9WNA)
![](https://w5wc4ktwyr.feishu.cn/space/api/box/stream/download/asynccode/?code=OWMzY2U2OTViZTY2YzY2ZWE3NDJjY2YxMTczMGY4OGZfQXdRQTlvNUlGc21yNHZ5SmZEd3NHdjZxWXZ3SHNDVTRfVG9rZW46WG4yMGJzb3lHb2w2Tlp4U0VyZWNacDM1blZmXzE3MDA3MzAzODI6MTcwMDczMzk4Ml9WNA)

2. Python Installation

Go to the Python official website and download the latest version: [Python Downloads](https://www.python.org/downloads/)
![](https://w5wc4ktwyr.feishu.cn/space/api/box/stream/download/asynccode/?code=ZDAzZDJmMDdkYjdlNWFmZDgzZmI2MTZlODI2MGMwODFfQ0hBMnBhUnhrTmxWQlliN1dNSG80TVpMVW52cnBWbXBfVG9rZW46S2sxdWJVaDFkb1BmV1R4dm5CZWM0UENNbktmXzE3MDA3MzAzODI6MTcwMDczMzk4Ml9WNA)

Choose the "Install Now" option and make sure to select "Add python.exe to Path" to avoid manual configuration.
![](https://w5wc4ktwyr.feishu.cn/space/api/box/stream/download/asynccode/?code=ZTA1MmNlNmRjMTQ1YTI2YTRmNTYxMmQyYzE3YjQ3MmRfSDFOdmZLUUUzVkQ1UGdKNG1hUDc4QWlHTU80VWViNk1fVG9rZW46QUk2SGJvQTFyb1RuY0p4emcxamM1SVcxbmJnXzE3MDA3MzAzODI6MTcwMDczMzk4Ml9WNA)

Once downloaded, click through the installation process.
![](https://w5wc4ktwyr.feishu.cn/space/api/box/stream/download/asynccode/?code=YzRlNTI1NWUxZDZkZTQzZmIyOWZhMjViNzQ0M2VmMjdfdGxmZXRRcnNPWmtVaFA4YUFhN0NJM2R6QkpNQ2d6QTdfVG9rZW46T0FHaWJMV09hb3J3OWp4R0RzZmNvYzVZbk5kXzE3MDA3MzAzODI6MTcwMDczMzk4Ml9WNA)
Next, open the command prompt by pressing `Win + R`, type `python --version`, and press Enter to verify the installation.
![](https://w5wc4ktwyr.feishu.cn/space/api/box/stream/download/asynccode/?code=MjdlMTNlMzgwY2RmNzU2M2Q0YWY0ZWYzNDI2OTAyYWVfSkNYVUJJR0NTQkhxZmtPbk9sbEZmRmNqQ1hmVExLZlZfVG9rZW46VWxHdWJNbW5Mb1RhWk94OXdudmNBTjE3bkNkXzE3MDA3MzAzODI6MTcwMDczMzk4Ml9WNA)
**Optional: Environment Variable Configuration**

1. If you forgot to select "Add python.exe to Path," you may need to manually add the environment variable.

2. Right-click on "This PC" or "My Computer," select Properties, and go to Advanced system settings.
        ![](https://w5wc4ktwyr.feishu.cn/space/api/box/stream/download/asynccode/?code=NjE1Nzg2ZWI1MmQ5NTk2ZTBhNTEzNmU3OTQ5ZDRjN2ZfaFpKeDZCSkpKYzk2amRGaWd1ajhOc1RFOVhOZ01Jc1FfVG9rZW46UktJSWJxczZUb29NTGd4N2l3ZmNoeFhYbjljXzE3MDA3MzAzODI6MTcwMDczMzk4Ml9WNA)
3. Click on Environment Variables.
    ![](https://w5wc4ktwyr.feishu.cn/space/api/box/stream/download/asynccode/?code=OWM0NTZiZjI1MWVkOWI1OGM1MWY4ZTVmYTFkZDk5MzVfMUNuQnNPdzBIbXI5dno3V3p5bUF2cUNqOVVOckJCcVdfVG9rZW46R2toYWJHNkMzb2xIRHF4VVVDQmNrZ0owbk1kXzE3MDA3MzAzODI6MTcwMDczMzk4Ml9WNA)
4. In the System variables section, find the Path variable, click Edit, and add the path to the directory where the Python interpreter is located. Remember to add a semicolon (;) before pasting.
    ![](https://w5wc4ktwyr.feishu.cn/space/api/box/stream/download/asynccode/?code=ZjU5MGNlMDZlNmIwZWU2ZWVkYzQyOWExMWY5ZGEzOGFfOHVYNExtR1VzaHBFSjY1QW5XNUxSOGJRbFV6UExKdUxfVG9rZW46UE5RMGIycXlsb1JNQ2p4Z1hmOWMxVUd5bkJmXzE3MDA3MzAzODI6MTcwMDczMzk4Ml9WNA)

![Environment Variable](https://w5wc4ktwyr.feishu.cn/space/api/box/stream/download/asynccode/?code=ZTA1MmNlNmRjMTQ1YTI2YTRmNTYxMmQyYzE3YjQ3MmRfSDFOdmZLUUUzVkQ1UGdKNG1hUDc4QWlHTU80VWViNk1fVG9rZW46S2sxdWJVaDFkb1BmV1R4dm5CZWM0UENNbktmXzE3MDA3MzAzODI6MTcwMDczMzk4Ml9WNA)

3. Git Installation

Download Link: [https://git-scm.com/download/win](https://git-scm.com/download/win)

Git is used to fetch code from remote Github repositories, allowing real-time updates for Stable Diffusion. This ensures timely access to new features, as the web UI is frequently updated, sometimes with more than ten releases in a month.

After downloading, install Git and check the runtime environment using the following CMD command:

[Win+R] to open [Run], type "cmd," press Enter, and in the command line, enter:

PlainCopy code

`git --version`

![Git Installation Check](https://w5wc4ktwyr.feishu.cn/space/api/box/stream/download/asynccode/?code=YjJkY2RjZjU5MTRlYjk1ZTM4ODhlMjE4NTc4NTVjNzRfNnpKSXlxTWQ3cmhRWGkxVkdqTUxPS2lMNWhEZ0o2SXpfVG9rZW46TzVEMWJVTWdrb3JPQnB4UUFpUWNuRlJDbnhiXzE3MDA3MzAzODI6MTcwMDczMzk4Ml9WNA)

![Git Installation Check](https://w5wc4ktwyr.feishu.cn/space/api/box/stream/download/asynccode/?code=NzFmMDEzZDFhYjNmODMyNzg3MWE5MTJkMWIyZWJlNzBfbG5mcENxTURmU3hoQTdTQm9ub0g5clNxd3B3M0J5anJfVG9rZW46VHBkU2JVMmdBb0w5dUJ4QnF1MGNHdW44bmtoXzE3MDA3MzAzODI6MTcwMDczMzk4Ml9WNA)

4. CUDA Installation

Download Link: [https://developer.nvidia.com/cuda-toolkit-archive](https://chat.openai.com/c/20717714-2e83-42ea-95d6-5578e8783599)

CUDA is a dependency program for NVIDIA graphics cards to run algorithms. First, run the command `nvidia-smi` in the command prompt to check your GPU's supported CUDA version. Updating the driver may enable support for a higher CUDA version.

![](https://w5wc4ktwyr.feishu.cn/space/api/box/stream/download/asynccode/?code=NTAyY2JlMDUwMTU4Yzg1NWZlYzNjZGM2YjFmMDY5ZGZfdklndHFJbzVKV3VQV3dwMDdVa2llWmtZV0NJelNGY0VfVG9rZW46SEhaMWJoeHVub0FJbDJ4WVB6TWM2OUtBbnllXzE3MDA3MzAzODI6MTcwMDczMzk4Ml9WNA)

Next, visit the NVIDIA official website [https://developer.nvidia.com/cuda-toolkit-archive](https://developer.nvidia.com/cuda-toolkit-archive) and download the corresponding version. Ensure you download the highest version number compatible with your GPU; for example, if you have version 11.5, download 11.5.2 (where .2 indicates the 2nd update for version 11.5).

CUDA Driver Version vs. CUDA Toolkit Compatibility: [https://docs.nvidia.com/cuda/cuda-toolkit-release-notes/index.html#major-components](https://sspai.com/link?target=https%3A%2F%2Fdocs.nvidia.com%2Fcuda%2Fcuda-toolkit-release-notes%2Findex.html%23major-components)

![CUDA Download](https://w5wc4ktwyr.feishu.cn/space/api/box/stream/download/asynccode/?code=ODgxZDg1NzgxMTczZmJlNzRmZDFjODQ4YTVjNDk5ZGJfMEVpaVdFc1d3N1VNMVJYUks1TUpMVFNWMjJORzJMeXFfVG9rZW46Q1ljZGJaOTMwb3dhZll4ZFZYemN5dnFDbjhmXzE3MDA3MzAzODI6MTcwMDczMzk4Ml9WNA)

When downloading, choose the 'exe_local' (offline installer) as online installation may be slower.

After installation, check the CUDA version with the following command:

JavaScriptCopy code

`nvcc --version`

5. Stable Diffusion Web UI Installation

Open CMD and download Stable Diffusion web UI using Git.

Create a new folder on your disk, e.g., named 'AI.' Right-click inside the folder and choose 'Git Bash Here' to open the Git terminal.

![Git Bash Here](https://w5wc4ktwyr.feishu.cn/space/api/box/stream/download/asynccode/?code=MWY0MmJlNDM4NGNjZGM0ZTJjY2I1MTc2OTUwM2RiNzVfZ3IzTzZNTGJSMThuVlBFMVNkVGM4Mmd0WlVEYUZaeXlfVG9rZW46SDEzSWIzNWpLbzE3QU94VnlzUGNZeDZrbmFiXzE3MDA3MzAzODI6MTcwMDczMzk4Ml9WNA)

![Git Clone](https://w5wc4ktwyr.feishu.cn/space/api/box/stream/download/asynccode/?code=YzYzMTViMzk5YmQ2MzM0M2JkZGFiMzI4N2NiODA0Njdfa2xYdFFCTWN2UWh6Tkt5NmhxSzF5UzQ3RUxMa21zbWtfVG9rZW46QWVLdGJETHVxb2w0TVN4ODNYbmM2bnN0bnNjXzE3MDA3MzAzODI6MTcwMDczMzk4Ml9WNA)

Clone the code using the Git command:

PlainCopy code

`git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui.git` 

![Git Clone](https://w5wc4ktwyr.feishu.cn/space/api/box/stream/download/asynccode/?code=ODIyODU4NWViZWFjMzA1YzhiNDJkYjgzYmI1OTMwM2ZfVmQyUUxGdTZwR3hXZVFoWTVORnFPMzk1NkxzMDRxVWpfVG9rZW46QkJDTWJ3Nkk0b2pQSGZ4Mmh5b2NIbGpsbnE2XzE3MDA3MzAzODI6MTcwMDczMzk4Ml9WNA)

You will see a folder like this. If you encounter issues with downloading, such as network failures or HTTPS security verification problems, you can also download and unzip the file directly from the GitHub page [https://github.com/AUTOMATIC1111/stable-diffusion-webui.git](https://github.com/AUTOMATIC1111/stable-diffusion-webui.git) (not recommended for future web UI upgrades).

![Web UI Folder](https://w5wc4ktwyr.feishu.cn/space/api/box/stream/download/asynccode/?code=NGU2N2YyNTA0MDdmNmZiNDc3NDg5Mjg5ZDZkYThiMTBfSWVCd1BCak5SMnN6ZkhwMEV0bE5VZHZIc01MVEV0YllfVG9rZW46Vjg2MGIwYjJvb2JXRmx4ZDg0NmNxYWdObnZoXzE3MDA3MzAzODI6MTcwMDczMzk4Ml9WNA)

6. Run webui-user.bat

Open the stable-diffusion-webui directory, and you will see the 'webui-user.bat' file. Double-click to run it.

![Run webui-user.bat](https://w5wc4ktwyr.feishu.cn/space/api/box/stream/download/asynccode/?code=ZjlhMGQxZmVjMmUzNTM1ZTUwNmIyNjQ2MjcxN2JjNDFfTU8xTFpjN3I5MHVtSFFUR0h1MXhaMzJ5SEl0aE91YWFfVG9rZW46UkhwMmJyVHg5b1NuNWp4dWtOeWMzM3R1bmVlXzE3MDA3MzAzODI6MTcwMDczMzk4Ml9WNA)

During the run, the duration depends on your network environment, usually taking 10-30 minutes to complete. Wait until you see the address [http://127.0.0.1:7860](http://127.0.0.1:7860/), indicating that it is running successfully. Do not close this window; closing it will exit the process.

Copy [http://127.0.0.1:7860](http://127.0.0.1:7860/) to your browser (you can save it as a bookmark for convenience), and now you can input commands to generate images.

![Web UI Running](https://w5wc4ktwyr.feishu.cn/space/api/box/stream/download/asynccode/?code=NDQyMjYwZjc0YmE1YjcyMjE1ZmQ3OWU3NDg3MjQzNmJfTDRCN3FkRjRrN3c2d0pZcGFhZFpjVDlyT1hmRG1kdjhfVG9rZW46RkN6dWJJMzFEb3FUc0V4em03M2NTTHhzbk5kXzE3MDA3MzAzODI6MTcwMDczMzk4Ml9WNA)

Feeling overwhelmed?

That's normal; this is the developer's way of running things. You don't necessarily need to understand all the steps, just know that it's a complex process. To simplify, some enthusiasts have provided integrated packages that you can install with a single click.

### Integrated Package Installation

**秋葉aaaki**

Check out the introduction to 秋葉aaaki's integrated package: [https://www.bilibili.com/video/BV1iM4y1y7oA](https://www.bilibili.com/video/BV1iM4y1y7oA)

Download Link:
[https://pan.baidu.com/s/1TK7UyX5lgNjdwdfcmYCI5Q](https://pan.baidu.com/s/1TK7UyX5lgNjdwdfcmYCI5Q) 
Extraction Code: c132

![秋葉aaaki Integrated Package](https://w5wc4ktwyr.feishu.cn/space/api/box/stream/download/asynccode/?code=NjA4NmE1NDJlNTJhNGI1YzAwNjYxZjUwZTk3NGNlNGFfdDVXdTIzaFJnY2RyMHhvSVVQZFJrQUp3ejZmS2M3MkJfVG9rZW46VXlmY2JEUlJDb3E1M3R4cjltN2M1M0VnbjBnXzE3MDA3MzAzODI6MTcwMDczMzk4Ml9WNA)
    
**StabilityMatrix**

Launcher from [GitHub - LykosAI/StabilityMatrix](https://github.com/LykosAI/StabilityMatrix). Download and install.

![StabilityMatrix Launcher](https://w5wc4ktwyr.feishu.cn/space/api/box/stream/download/asynccode/?code=MGRlODQzNTU0MWIxMDE1NDBmOWRhMzY2YzkzMTVhMTdfb29jUFR3TXBpZFVKRFZKYjJyemJ5YjZmdHpvajlRVUFfVG9rZW46QXVGVmJ1eDltb1ZIbzR4SlVucmNzR0V0bmFmXzE3MDA3MzAzODI6MTcwMDczMzk4Ml9WNA)


These launchers are integrated with Python environments and models. Simply run them with a single click.

Whether you choose manual installation, integrated packages, or cloud environments, errors may occur due to the variability of your local environment. In such cases, you may need to troubleshoot by collecting information online or, in some cases, find that it's beyond your expertise. In that case, I sincerely recommend using a cloud environment, where most platforms offer one-click Stable Diffusion web UI setups. Just pay and run