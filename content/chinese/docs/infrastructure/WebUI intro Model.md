---
title: WebUI 介绍|模型篇
type: docs
weight: 2
prev: docs/infrastructure/
created: 2023-11-15T11:13:12+08:00
date: 2023-11-27T15:57:24+08:00
---

本节重点来介绍一下，AUTOMATIC1111版本的webui的各个功能和概念。进入webui的页面大概都是这个样子的，你们的版本可能和我的略有区别，使用云端部署，大多都内置了一些常用的数据模型，和基础插件。（这里容我偷个懒，我用的是部署在huggingface上的一款demo，https://huggingface.co/spaces/lianzhou/stable-diffusion-webui, 用来讲解本节的内容应该够用了）

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/e92aff5b48fe4fc7a5d9062c6ea3c97d~tplv-obj.image?lk3s=3de049d8&traceid=20231127152715CA67B3484C26416A9B70&x-expires=2147483647&x-signature=ZMrZVSn%2FLadLlCTWZ0kfAPkVqo0%3D)

本节只有概念介绍，没有操作，具体的操作将会放在每一个具体内容中

在入目的第一栏中，有一个Stable Diffusion checkpoint，这里就是提供给用户进行基础模型的选择。那么什么是模型呢？

一般在AIGC领域，研发人员致力于使机器展现智能行为。他们采用机器学习的方法，让计算机从数据中学到知识，并按照人类的期望执行各种任务。在AI绘画中，通过对算法程序进行训练，让机器学习各种图片的信息特征，形成了被称为"模型"的文件。简单来说，模型就是经过训练学到的程序文件。与普通的图片数据库不同，模型中储存的不是可视的原始图片，而是经过解析的图像特征代码。模型就像是一个超级大脑，根据提示内容预测并自动提取相应的碎片信息，最终输出一张图片。虽然模型的实际运行原理比这复杂得多，但作为使用者，我们不需要深入学习复杂的技术算法，只需了解其大致概念即可。

## Base Model (基础模型)

这是没有的概念，我们为了表述Stable Diffusion使用到的版本，当下有哪些版本，我们可以在Civitai.com的筛选栏里看到，随着时间的增加，版本也逐步在增多。这里有个地方非常重要，在传统的软件里，我们都认为版本越新越好，但在机器学习里，这个理念正在失效。比如，SDXL1.0的版本，在某些场景里，还不如SD1.5的表现。选择一个合适的基础模型，有时候在图片生成的过程中，是非常重要的。

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/2dbd52eb234f4e14862a2e8d2f9bcda3~tplv-obj.image?lk3s=3de049d8&traceid=20231127152715CA67B3484C26416A9B70&x-expires=2147483647&x-signature=u%2FF%2F1OmrVM3Vni1b6GSyrmR8Svk%3D)

## Checkpoint （检查点）

Checkpoint 是 Stable Diffusion 中最重要的模型，体积庞大，一般在 2G - 7G 之间，也是主模型，几乎所有的操作都要依托于主模型进行。而所有的主模型都是基于 Stable Diffusion 模型训练而来，所以有时会被称为 Stable Diffusion 模型。

主模型后缀一般为 _*.ckpt、*_.pt、*.pth 或者 *.safetensors。而要管理模型我们需要进入 WebUI 目录下的 models/Stable-diffusion 目录下。

_*.ckpt、*_.pt、*.pth 等后缀名表示的是基于 pytorch 深度学习框架构建的模型，因为模型保存和加载底层用到的是 Pickle 技术，所以存在可被用于攻击的程序漏洞，因此这几款模型后缀的文件中可能会潜藏着病毒代码。

*.safetensors"后缀名，是由 huggingface 研发的一种开源的模型格式，他具有支持懒加载，加载速度快，通用性强，可以防dos攻击等优点，一般热门模型都有改格式，所以下载模型时，尽量优先下载该格式文件。

在C站中，模型类型选择Checkpoint，即可筛选。

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/ab05beea9b9b4a2aaef5b516ac881f05~tplv-obj.image?lk3s=3de049d8&traceid=20231127152715CA67B3484C26416A9B70&x-expires=2147483647&x-signature=tmG0vcDEquAaLodd6Jbgg8pdtmI%3D)

关于模型版本的选择，我们后续会持续介绍。

## LoRA和 LyCORIS

介绍LoRA模型之前，我们先了解一下什么是LoRA，我想对你理解为何需要他，是非常重要的。毕竟我们已经有了主模型了。

LoRA是Low-Rank Adaptation的缩写，是微软的Hu等人于2021年挂在ArXiv上（后又发表在ICLR2022上）的一篇论文《[LoRA: Low-Rank Adaptation of Large Language Models](https://arxiv.org/pdf/2106.09685.pdf)》中提出的，通俗来讲，是一种**降低模型可训练参数**，又**尽量不损失模型表现**的**大模型微调**方法。

比如，GPT-3有1750亿参数，为了让它能干特定领域的活儿，需要做微调，但是如果直接对GPT-3做微调，成本太高太麻烦了。

LoRA的做法是，冻结预训练好的模型权重参数，然后在每个Transformer（Transforme就是GPT的那个T）块里注入可训练的层，由于不需要对模型的权重参数重新计算梯度，所以，大大减少了需要训练的计算量。

太专业的内容，我在此处就不描述了，感兴趣的同学可以看看别人的解释。[梯度视角下的LoRA:简介、分析、猜测及推广 - 科学空间|Scientific Spaces](https://spaces.ac.cn/archives/9590)

在Stable Diffusion里面，你可以把他当主模型的补丁来理解，他可以帮助你固定人物姿势，确认图片中的物品或位置，特定领域的风格，甚至是一种感觉。你也可以多个LoRA模型进行组合使用，通过设定不同的权重来作画。

和主模型一样，主推*.safetensors后缀格式，但体积较主模型要小得多，一般在 4M - 300M 之间。

需要管理模型时可以进入 WebUI 目录下的 models/LoRA 目录下。

在C站中，模型类型选择LoRA或者LyCORIS，即可筛选。

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/6cacedee6d184379b8a65dd69186c8ed~tplv-obj.image?lk3s=3de049d8&traceid=20231127152715CA67B3484C26416A9B70&x-expires=2147483647&x-signature=RHjeaOhML9Uv%2B6OVP0S2QuuQgBw%3D)

当然，你也看在分类中，选择特定的风格模型。

在 WebUI 中使用时，可通过点击左侧的小红灯，然后在 LoRA 菜单中点击使用。或直接使用 Prompt 调用。

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/e77b5bde4bb84e40a7bd292d69f18c05~tplv-obj.image?lk3s=3de049d8&traceid=20231127152715CA67B3484C26416A9B70&x-expires=2147483647&x-signature=ZFBRwLYhvEfnql5sZUG16NgDcwM%3D)

## VAE

VAE 模型一般用于图片亮度和饱和度的修正、画面校正和以及补光等。一般在绘图时如果出现图片亮度过低、发灰等问题时就需要用到。这种模型一般已经被集成到checkpoint里了，可以理解为其可作用为图片的滤镜。

比如，Anything大模型里附加VAE和没有VAE的对比效果。

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/89f6fea6ff16487099acd1a22092f530~tplv-obj.image?lk3s=3de049d8&traceid=20231127152715CA67B3484C26416A9B70&x-expires=2147483647&x-signature=KzUsQFHr1XcAVy2VbVItbg0cnSk%3D)

VAE 模型的后缀为 *.pt 或 *.safetensors，体积一般为 335M 或 823M。模型的目录为 models/VAE。

使用时需要到 Settings 页面找到 SD VAE 菜单切换。

![](https://p6-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/5841fc3a23af457eb2e8aed43ba3ffd2~tplv-obj.image?lk3s=3de049d8&traceid=20231127152715CA67B3484C26416A9B70&x-expires=2147483647&x-signature=EdtGX4GRBLcuS95SU%2FIkz4%2FMvio%3D)

但是这样使用过于繁琐，所以如果使用到建议在 Quicksettings list 配置中添加 sd_vae。

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/d5e76f69919844949d4c8bf010d5c02a~tplv-obj.image?lk3s=3de049d8&traceid=20231127152715CA67B3484C26416A9B70&x-expires=2147483647&x-signature=OwaytQYhBuFUBR2utMjYhxcUIAM%3D)

这样就可以在 WebUI 的顶部进行切换。

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/5158897f4e3e469bb8c1c196a6b39c6f~tplv-obj.image?lk3s=3de049d8&traceid=20231127152715CA67B3484C26416A9B70&x-expires=2147483647&x-signature=muetw6xLPc0FiKNJGqev8XzGZIY%3D)

## Hypernetworks

hypernetworks是一种fine tune的技术，最开始由novel AI开发。hypernetworks是一个附加到stable diffusion model上的小型网络，用于修改扩散模型的风格。

Hypernetworks 的后缀为 *.pt 或者 *.safetensors，体积一般在 20M - 200M 之间。模型的目录为 WebUI 下的 models/hypernetworks。

在使用时同样可以使用小红灯中的 Hypernetworks。

![](https://p9-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/ab71698580a8477487266c9f64567b0f~tplv-obj.image?lk3s=3de049d8&traceid=20231127152715CA67B3484C26416A9B70&x-expires=2147483647&x-signature=Nq5jhLGIPxiTuVG4XVzmShkzKQY%3D)

（这个仅是为了提一下，有了LoRA之后，基本用不到了）

## Textual Inversion

Textual Inversion 是文本编码器模型，主要用来调教文本理解能力。也是我们常说的Embedding模型。对理解我们的作画时填入的提示词（prompt）非常重要。

Textual Inversion 后缀为 *.pt 或者 *.safetensors，体积非常小，一般只有几 kb。模型所在的目录不在 models 下，而是在 WebUI 中的 embeddings 目录下。

在使用时同样可以使用小红灯中的 Textual Inversion，也可以使用 Prompt 调用。

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/36c22a6c19e641a29899ebeb1313a35c~tplv-obj.image?lk3s=3de049d8&traceid=20231127152715CA67B3484C26416A9B70&x-expires=2147483647&x-signature=C2%2FzzgMAuwbtHZdfV0v5TlLcUgk%3D)

在C站中，模型类型中筛选 Embedding可得到。

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/a34ab2c7fcda405e90bbf6bad22b56e7~tplv-obj.image?lk3s=3de049d8&traceid=20231127152715CA67B3484C26416A9B70&x-expires=2147483647&x-signature=eML%2BoFaeQLmmf%2Fx3H5YESSTSD50%3D)

## ControlNet

ControlNet 类模型的后缀为 *.safetensors。模型的目录为 models/ControlNet，模型文件很小，通常只有几KB，但很强大。我将会对他进行专题介绍。这里仅是提一下。他的安装方式需要通过插件安装。

网上介绍的有很多，我这里就不专门描写了。我贴几篇文章，大家看看，就知道了。

[Stable Diffusion进阶教程！超详细的 ControlNet 实用入门指南](https://www.uisdc.com/controlnet)

[Stable Diffusion ControlNet 完全指南](https://zhuanlan.zhihu.com/p/646913973)

[Stable Diffusion进阶教程！超详细的 ControlNet 实用入门指南](https://www.uisdc.com/controlnet)

## CodeFormer

CodeFormer 是一个很棒的开源项目[sczhou/CodeFormer](https://github.com/sczhou/CodeFormer)，被应用在许多项目中，它的论文（[arxiv.org/abs/2206.11253](https://arxiv.org/abs/2206.11253)）在 2022 年被 “经信息处理系统大会”（NeurIPS）接收后，自 2022 年 6 月代码开始放出至今的一年出头的时间里，Star 数量迅速升到了接近万星的水平，足见开源社区的认可程度。

因为他可以提高图片的分辨率、将黑白照片修改成彩色照片、人脸修复等等。

在 WebUI 中已经默认被整合，可以在 Extras 菜单中使用。如果需要修改 CodeFormer 版本可以将模型放到 models/codeformer

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/2177623d71b34bf2b56957a279c087c1~tplv-obj.image?lk3s=3de049d8&traceid=20231127152715CA67B3484C26416A9B70&x-expires=2147483647&x-signature=PdeCNL%2F6%2FGgT3VCyU3aNqqdIz%2F4%3D)

## 总结比较

|   |   |   |   |   |
|---|---|---|---|---|
|模型名称|作用|后缀名|大小|在 WebUI 中的文件夹|
|Checkpoint|主模型|.ckpt 或 .safetensors|2G - 7G|models/Stable-diffusion|
|LoRA 和 LyCORIS|微调模型，一般用于控制画风、控制生成的角色、控制角色的姿势等等|.safetensors|2G - 7G|models/Stable-diffusion|
|Textual Inversion|文本编码器模型|.pt 或 .safetensors|KB 级别|embeddings|
|Hypernetworks|调整模型神经网络权重，进行风格的微调|.pt 或 .safetensors|20M - 200M|models/hypernetworks|
|ControlNet|强大的控制模型，可以进行画面控制、动作控制、色深控制、色彩控制等等|.safetensors|KB 级别|models/ControlNet|
|VAE|图片亮度和饱和度的修正、画面较正和以及补光等|.pt 或 .safetensors|335M 或 823M|models/VAE|
|CodeFormer|修复模型，修复人脸、提高分辨率等|-|-|models/codeformer|

好了，介绍完上面的模型分类，有时候一个模型给你的时候，你很难从名字上分辨出来，他应该放在哪儿，细心的朋友们，已经帮你做了一个小网站，[https://spell.novelai.dev/](https://spell.novelai.dev/) ，把模型拖入就可以看到了。

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/c93a09104ba1402a9811c53f5b601fd8~tplv-obj.image?lk3s=3de049d8&traceid=20231127152715CA67B3484C26416A9B70&x-expires=2147483647&x-signature=JGwEnB4MzhS6LfdM1zUxvlq1kSo%3D)
