---
title: AI艺术发展史
type: docs
weight: 1
prev: /
next: docs/infrastructure/
created: 2023-11-15T11:13:12+08:00
date: 2023-11-28T10:39:18+08:00
---

AI艺术的发展史，其实并没有什么好描述的，他没有民族战争那样可歌可泣，催人泪下的故事，也没有爱情小说那样凄凉婉转，肝肠寸断的情爱故事，更没有惊心动魄，峰回路转的侦探惊悚感。他有的只是一群热爱生活，热爱科学技术，充满想象力的朋友们，根据现实生活中，实际的生产需求需要，一步一个脚印，经历成百数千次，数万次失败，迭代而来的。
我们在此感谢那些失败者，他们为AI画图的路尝试了不可行的方向，虽然他们不会出现在历史长河的名单中，但依然值得感谢。

## AARON，理想者赞歌

一个英国的艺术创作者，[Harold Cohen](https://en.wikipedia.org/wiki/Harold_Cohen_(artist) )于上个世纪60~70年代，创造了[AARON](https://en.wikipedia.org/wiki/AARON)，他是一个以传统编码的方式，去操作一个物理机器，进行绘画。尽管他的画作非常有限，但还是可以绘画出一些抽象画作，像下面这副画，这应该算作作者的自画像，如果类别AI界的梵高，我想也说的过去。
<img
      alt="Another emotionally-aware portrait"
      loading="lazy"
      decoding="async"
      src="/images/Another emotionally-aware portrait.png"
    />
假如不是AI大模型的出现，也许我们现在依然停留在这个阶段。随着Harold的离开，AARON也走进了历史。想要了解更多AARON的艺术创作，可以看看,[Creative AI: The robots that would be painters](https://newatlas.com/creative-ai-algorithmic-art-painting-fool-aaron/36106/), [harold-cohen-aaron](https://outland.art/harold-cohen-aaron/)

## 神奇的2012
2012是一个神奇的年份，那是一个玛雅人预测人类文明的末日（一个关于2012的灾难片）。我想玛雅人只看见了悲痛，却没有看见希望。那一年或许是真正意义上的AI元年。从那年开始，热衷于AI技术的朋友们，不用在黑暗的道路上摸索，他们看到的黑暗中唯一的火炬，GPU+大数据。
这一年，[Geoffrey Hinton](https://en.wikipedia.org/wiki/Geoffrey_Hinton)和他的学生们，采用英伟达的GPU来训练他们的神经网络模型[AlexNet](https://en.wikipedia.org/wiki/AlexNet),在两张GTX 580显卡的支持下，1400万张图片的训练只花了一个周，AlexNet顺利夺冠。后续被Google收购，三年后推出AlphaGo，一举成名。

同年，谷歌大脑(Google Brain)团队成员Jeff Dean和吴恩达等通过深度学习技术，在YouTube视频中“认出”了猫。
<img
      alt="Another emotionally-aware portrait"
      loading="lazy"
      decoding="async"
      src="/images/learned to detect cats.png"
    />
你认出来了吗？这可是他们耗资100万美元，集结1000台电脑、16000个CPU，耗时3天画出来的。

感兴趣的同学可以看看，[2012，改变人类命运的180天](https://36kr.com/p/2421889040802823)

## 2015，机器视觉创造的始祖

Google在上一局成为了大赢家，这一局，自然也不甘落后，他们域2015年开源了deep dream，他们的实现模式很简单，就是将一张图片进行艺术化处理，像下面这样,是不是很超现实？
<img
      alt="Deep Dream Art"
      loading="lazy"
      decoding="async"
      src="/images/Deep Dream Art.png"
    />
他们的故事，可以看看[揭秘谷歌Deep Dream的前世今生](https://www.jiqizhixin.com/articles/2015-12-26-2).

在deep dream火爆的前一年，2014，由加拿大蒙特利尔大学的[Ian Goodfellow](https://en.wikipedia.org/wiki/Ian_Goodfellow)提出的GAN（Generative Adversarial Network）模型，却无意间成为了机器视觉的做图片生产的主流.下面是一张不存在的人，你会惊讶吗？
<img
      alt="this person does not exist"
      loading="lazy"
      decoding="async"
      src="/images/thispersondoesnotexist.jpg"
    />
GAN的原理是通过训练两个深度神经网络模型，一个生成器（Generator）和一个判别器（Discriminator），使得生成器可以生成与真实数据相似的新数据样本，并且判别器可以准确地区分生成器生成的假样本和真实数据。在训练过程中，生成器不断尝试生成更加逼真的样本，而判别器则不断提高自己对真实样本和生成样本的区分能力。这两个模型相互对抗、相互协作，最终实现了高质量的数据生成效果。
通过学习高质量内容，可以在一定程度上进行去噪处理。因此GAN不仅仅可以用来生成图片，还可以用来生成视频，音乐，设计稿等等。所以基于GAN模型为基础，后续的爱好者们相继研发了许多流行的架构，如DCGAN，StyleGAN，BigGAN，StackGAN，Pix2pix，Age-cGAN，CycleGAN，[GAN ZOO](https://github.com/hindupuravinash/the-gan-zoo)，每一种模型，都有去解决特定领域的问题。

在后期的发展中，DeepFakes也被推上了热门，换脸的游戏，总会让人津津乐道的去参与。

当然，GAN模型也有着非常大的局限性，那就是对于生成的内容很难去提升分辨率。比如生成一张512px的图片或许还不错，再到1024px便已经再难维继了。再者就是，生成的内容，局部不可控，我们输入prompt之后，剩下的只剩下等待，我们没办法控制，生成的内容，比如人的皮肤再白一些，光线再暗些。不管怎么样，GAN，在那个时代，绝对是无可代替的。

如果，我是说如果，没有Google开源了transform大模型，没有微软的LoRA，也就没有后来的王者Stable Diffusion，那么我们依然还要再GAN模型的世界里模式，我们甚至需要为每一个想要生成的结果做一个GAN的专属模型，这是普通消费者无法承受的，他属于AI工作者的专利。

如果你对GAN的发展史感兴趣，不妨阅读一下， [生成对抗网络(GAN)的发展史](https://zhuanlan.zhihu.com/p/63428113)，[Generative Adversarial Networks - The Story So Far]https://blog.floydhub.com/gans-story-so-far/

2015年的故事还未结束，依然是这一年，ImageNet图像识别大赛，似乎才刚开始，就要结束了。AI的识别率错误率已经超过人类。[图说2016深度学习十大指数级增长](https://36kr.com/p/1721287491585)

图像分类还在继续，也依然在超越人类，直到，2021 年 1 月Open AI团队（没错，就是那个以ChatGPT闻名世界的团队），开源了新的深度学习模型 CLIP（Contrastive Language-Image Pre-Training). 这是一个当今最先进的图像分类人工智能。他对后面一年，AIGC概论的大爆发，功不可没。


## Stable Diffusion无冕之王

<img
      alt="Space Opera Theater"
      loading="lazy"
      decoding="async"
      src="/images/Space Opera Theater.png"
    />
常常徘徊在互联网里的你，对上面这副图肯定不会陌生，没错，他便是在科罗拉多州博览会(Colorado State Fair)的美术比赛中，获得了第一名的作品——空间歌剧院，是由AI来生成的。
AI绘图的概念，仿佛一下子贯穿了整个世界，这太不可思议了，对那些重未接触AI的人来说。

前文提到GAN,在发展多年后，所面临的瓶颈依然无法解决，此时，有人会想，我们能否反其道而行呢？即 Diffusion Model (扩散模型)
<img
      alt="Image addition noise"
      loading="lazy"
      decoding="async"
      src="/images/Image addition noise.png"
    />
就是把原图用马尔科夫链将噪点不断地添加到其中，最终成为一个随机噪声图像，然后让训练神经网络把此过程逆转过来，从随机噪声图像逐渐还原成原图，这样神经网络就有了可以说是从无到有生成图片的能力。而文本生成图片就是把描述文本处理后当做噪声不断添加到原图中，这样就可以让神经网络从文本生成图片。
Diffusion Model (扩散模型) 让训练模型变得更加简单，只需大量的图片就行了，其生成图像的质量也能达到很高的水平，并且生成结果能有很大的多样性，这也是新一代 AI 能有难以让人相信的“想象力”的原因。这也就是他在诞生短短 2 年内，就把 AI 生成艺术带到了可用的程度。

虽然，Diffusion Model在2015年就已经提出来了，但真正将他带入工业界的， 却是openAI 公布了 [Dall-E](https://openai.com/blog/dall-e/)。尽管，dall-e未开源，初代产品表现的并非让人感到惊讶或者兴奋，但他却为整个AI绘画界，指明了方向，那就是 CLIP + Diffusion；

于是乎，各家的diffusion模型，也粉墨登场，抢占未来，哪怕是一个名字。

2022 年 8 月 [stability.ai](https://stability.ai/) 开源了 [Stable Diffusion](https://github.com/CompVis/stable-diffusion)，没错，是的，他来了。关于stable diffuison的版本，可以参考，[StableDiffusion模型发展历史](https://www.cnblogs.com/chester-cs/p/17411578.html).

商业产品都基于Stable Diffusion的名气 [NovelAI](https://novelai.net/)，我就不多赘述了。

最后，再补充一个《空间歌剧院》作品，所用到的软件，[Mid Djourney](https://www.midjourney.com/home)，其底层也是基于diffusion。

那么，还等什么，开始我们的Stable Diffusion学习之旅吧。