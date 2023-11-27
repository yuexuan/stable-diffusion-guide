---
title: WebUI intro Model
type: docs
weight: 2
prev: docs/infrastructure/
created: 2023-11-15T11:13:12+08:00
date: 2023-11-27T15:55:46+08:00
---

In this section, we will focus on introducing the various features and concepts of the AUTOMATIC1111 version's web UI. The page you see when entering the web UI generally looks like this. Your version may differ slightly, but most cloud deployments come with built-in data models and basic plugins. (Here, I'll take a shortcut and use a demo deployed on Hugging Face, [https://huggingface.co/spaces/lianzhou/stable-diffusion-webui](https://huggingface.co/spaces/lianzhou/stable-diffusion-webui), which should be sufficient for explaining the content of this section.)

![Web UI](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/e92aff5b48fe4fc7a5d9062c6ea3c97d~tplv-obj.image?lk3s=3de049d8&traceid=20231127152715CA67B3484C26416A9B70&x-expires=2147483647&x-signature=ZMrZVSn%2FLadLlCTWZ0kfAPkVqo0%3D)

This section provides a conceptual overview without hands-on operations. Specific operations will be covered in each corresponding topic.

In the first column, there is a 'Stable Diffusion checkpoint,' which allows users to choose the base model. But what is a model?

In the field of AI graphics, developers strive to make machines exhibit intelligent behavior. They use machine learning to enable computers to learn from data and perform various tasks according to human expectations. In AI art, training algorithmic programs on various images results in files called 'models.' Simply put, a model is a trained program file. Unlike a typical image database, models store parsed image features, not visible raw images. A model acts like a super brain, predicting and automatically extracting corresponding fragmented information based on input prompts, ultimately outputting an image. Although the actual workings of a model are much more complex, as users, we don't need to delve into the intricacies of technical algorithms; understanding the basic concept is sufficient.

## Base Model

This is a concept representing the versions used by Stable Diffusion. You can find information on available versions in the filter bar on Civitai.com. Interestingly, in machine learning, the idea that newer versions are always better is losing its validity. For example, in certain scenarios, SDXL1.0 may not perform as well as SD1.5. Choosing an appropriate base model can be crucial in the image generation process.

![Base Model](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/2dbd52eb234f4e14862a2e8d2f9bcda3~tplv-obj.image?lk3s=3de049d8&traceid=20231127152715CA67B3484C26416A9B70&x-expires=2147483647&x-signature=u%2FF%2F1OmrVM3Vni1b6GSyrmR8Svk%3D)

## Checkpoint

Checkpoint is the most crucial model in Stable Diffusion, with a large size ranging from 2GB to 7GB. It serves as the main model, and almost all operations depend on it. All main models are based on training with the Stable Diffusion model, so they are sometimes referred to as Stable Diffusion models.

The main model usually has file extensions like _*.ckpt, *_.pt, *.pth, or *.safetensors. To manage models, you need to go to the models/Stable-diffusion directory under the WebUI directory.

_*.ckpt, *_.pt, *.pth extensions indicate models built on the PyTorch deep learning framework. As these models use Pickle technology for saving and loading, there may be potential program vulnerabilities that can be exploited, so caution is advised. The *.safetensors extension is an open-source model format developed by Hugging Face, known for supporting lazy loading, fast loading speed, universality, and resistance to DOS attacks. Popular models often have this format, so it is recommended to prioritize downloading models in this format.

In the C station, you can filter model types by selecting Checkpoint.

![Checkpoint](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/ab05beea9b9b4a2aaef5b516ac881f05~tplv-obj.image?lk3s=3de049d8&traceid=20231127152715CA67B3484C26416A9B70&x-expires=2147483647&x-signature=tmG0vcDEquAaLodd6Jbgg8pdtmI%3D)

For information on selecting model versions, we will continue to cover it in subsequent sections.

## LoRA and LyCORIS

Before delving into LoRA models, let's understand what LoRA is and why it's needed. Knowing this is crucial because we already have the main model.

LoRA stands for Low-Rank Adaptation, introduced by Microsoft's Hu and others in a paper published on ArXiv in 2021 (later presented at ICLR 2022). In simple terms, LoRA is a method of fine-tuning large models to adapt them to specific domains while minimizing the loss of model performance.

For instance, GPT-3 has 175 billion parameters, and to make it perform specific tasks in a certain domain, fine-tuning is required. However, direct fine-tuning of GPT-3 is costly and challenging.

LoRA's approach is to freeze the pre-trained model's weight parameters and inject trainable layers into each Transformer block (the 'T' in GPT). Since there is no need to recompute gradients for the model's weight parameters, the training computational load is significantly reduced.

The specifics of this topic are quite technical, and for those interested, more detailed explanations can be found elsewhere. [Here's a link for further reading](https://spaces.ac.cn/archives/9590).

In Stable Diffusion, you can think of LoRA as a patch for the main model. It can help fix character poses, identify objects or positions in images, apply specific styles for certain domains, or even convey a certain feeling. You can use multiple LoRA models in combination by setting different weights to create artwork.

Similar to the main model, LoRA models are preferably in the *.safetensors format, but their size is much smaller, typically ranging from 4MB to 300MB. To manage models, you can navigate to the models/LoRA directory under the WebUI.

In the C station, you can filter model types by selecting LoRA or LyCORIS.

![LoRA](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/6cacedee6d184379b8a65dd69186c8ed~tplv-obj.image?lk3s=3de049d8&traceid=20231127152715CA67B3484C26416A9B70&x-expires=2147483647&x-signature=RHjeaOhML9Uv%2B6OVP0S2QuuQgBw%3D)

Of course, you can also choose specific style models within the classification.

When using it in the WebUI, you can activate LoRA by clicking the red light on the left, then clicking 'Use' in the LoRA menu. Alternatively, you can use prompts directly.

![Using LoRA](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/e77b5bde4bb84e40a7bd292d69f18c05~tplv-obj.image?lk3s=3de049d8&traceid=20231127152715CA67B3484C26416A9B70&x-expires=2147483647&x-signature=ZFBRwLYhvEfnql5sZUG16NgDcwM%3D)

## VAE

VAE models are generally used for correcting image brightness and saturation, image correction, and fill lighting. They are applied when drawing to address issues like low brightness or grayness in images. Typically, VAE models are already integrated into checkpoints and can be understood as filters for images.

For example, a comparison of Anything's large model with and without VAE.

![VAE Comparison](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/89f6fea6ff16487099acd1a22092f530~tplv-obj.image?lk3s=3de049d8&traceid=20231127152715CA67B3484C26416A9B70&x-expires=2147483647&x-signature=KzUsQFHr1XcAVy2VbVItbg0cnSk%3D)

VAE models have file extensions *.pt or *.safetensors, with sizes usually at 335MB or 823MB. The model's directory is models/VAE.

When using VAE, you need to go to the Settings page and find the SD VAE menu to toggle it.

![VAE Settings](https://p6-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/5841fc3a23af457eb2e8aed43ba3ffd2~tplv-obj.image?lk3s=3de049d8&traceid=20231127152715CA67B3484C26416A9B70&x-expires=2147483647&x-signature=EdtGX4GRBLcuS95SU%2FIkz4%2FMvio%3D)

However, this can be cumbersome, so it is recommended to add 'sd_vae' to the Quicksettings list configuration for easy switching.

![VAE Switching](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/d5e76f69919844949d4c8bf010d5c02a~tplv-obj.image?lk3s=3de049d8&traceid=20231127152715CA67B3484C26416A9B70&x-expires=2147483647&x-signature=OwaytQYhBuFUBR2utMjYhxcUIAM%3D)

Now you can switch it at the top of the WebUI.

![VAE Switch](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/5158897f4e3e469bb8c1c196a6b39c6f~tplv-obj.image?lk3s=3de049d8&traceid=20231127152715CA67B3484C26416A9B70&x-expires=2147483647&x-signature=muetw6xLPc0FiKNJGqev8XzGZIY%3D)

## Hypernetworks

Hypernetworks are a fine-tuning technique initially developed by Novel AI. Hypernetworks are small networks attached to the stable diffusion model, used to modify the style of the diffusion model.

Hypernetworks have file extensions *.pt or *.safetensors, with sizes typically ranging from 20MB to 200MB. The model's directory is WebUI/models/hypernetworks.

When using Hypernetworks, you can also use the red light in the same way.

![Hypernetworks](https://p9-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/ab71698580a8477487266c9f64567b0f~tplv-obj.image?lk3s=3de049d8&traceid=20231127152715CA67B3484C26416A9B70&x-expires=2147483647&x-signature=Nq5jhLGIPxiTuVG4XVzmShkzKQY%3D)

(Note: This is mentioned here but is essentially not needed much after the introduction of LoRA.)

The above information is structured and presented as an introduction. Subsequent sections will provide more details on specific operations.

## Textual Inversion

Textual Inversion is a text encoder model primarily used to enhance text understanding. It's also commonly referred to as an Embedding model. The understanding of the prompts we use when creating art is crucial for this model.

The Textual Inversion model has file extensions *.pt or *.safetensors, with a very small size, usually just a few kilobytes. The model's directory is not in the 'models' folder but rather in the 'embeddings' directory in the WebUI.

When using it, you can either utilize Textual Inversion in the red light section or employ it through prompt calls.

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/36c22a6c19e641a29899ebeb1313a35c~tplv-obj.image?lk3s=3de049d8&traceid=20231127152715CA67B3484C26416A9B70&x-expires=2147483647&x-signature=C2%2FzzgMAuwbtHZdfV0v5TlLcUgk%3D)

On the C site, you can filter the model type as 'Embedding' to find it.

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/a34ab2c7fcda405e90bbf6bad22b56e7~tplv-obj.image?lk3s=3de049d8&traceid=20231127152715CA67B3484C26416A9B70&x-expires=2147483647&x-signature=eML%2BoFaeQLmmf%2Fx3H5YESSTSD50%3D)

## ControlNet

ControlNet, identified by the file extension *.safetensors, is a class of models. The model's directory is 'models/ControlNet,' and the model file is very small, typically only a few kilobytes, but it's powerful. A detailed introduction to it will be covered in a dedicated topic, and here, we'll just mention it briefly. The installation method requires a plugin.

There are many online resources for detailed information. I'll share a few articles for everyone to check out.

[Advanced Tutorial on Stable Diffusion! A Comprehensive Guide to Practical ControlNet](https://www.uisdc.com/controlnet)

[Complete Guide to Stable Diffusion ControlNet](https://zhuanlan.zhihu.com/p/646913973)

[Advanced Tutorial on Stable Diffusion! A Comprehensive Guide to Practical ControlNet](https://www.uisdc.com/controlnet)

## CodeFormer

CodeFormer is an excellent open-source project [sczhou/CodeFormer](https://github.com/sczhou/CodeFormer), widely used in various projects. Its paper ([arxiv.org/abs/2206.11253](https://arxiv.org/abs/2206.11253)) was accepted by the Neural Information Processing Systems conference (NeurIPS) in 2022. Since the code was released in June 2022, the number of stars quickly rose to nearly ten thousand, indicating high recognition in the open-source community.

It can be used to enhance image resolution, convert black and white photos to color, and perform tasks like facial restoration.

It's already integrated into the WebUI and can be accessed in the Extras menu. If you need to modify the CodeFormer version, you can place the model in the 'models/codeformer' directory.

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/2177623d71b34bf2b56957a279c087c1~tplv-obj.image?lk3s=3de049d8&traceid=20231127152715CA67B3484C26416A9B70&x-expires=2147483647&x-signature=PdeCNL%2F6%2FGgT3VCyU3aNqqdIz%2F4%3D)

## Summary and Comparison

||||||
|---|---|---|---|---|
|Model Name|Function|File Extension|Size|Folder in WebUI|
|Checkpoint|Main Model|*.ckpt or *.safetensors|2GB - 7GB|models/Stable-diffusion|
|LoRA and LyCORIS|Fine-tuning models, typically used for controlling art style, character generation, pose control, etc.|.safetensors|2GB - 7GB|models/Stable-diffusion|
|Textual Inversion|Text encoder model|*.pt or *.safetensors|KB level|embeddings|
|Hypernetworks|Adjusts model neural network weights for style fine-tuning|*.pt or *.safetensors|20MB - 200MB|models/hypernetworks|
|ControlNet|Powerful control model for image, action, color depth, and color control|.safetensors|KB level|models/ControlNet|
|VAE|Corrects image brightness, saturation, scene correction, and fill light|*.pt or *.safetensors|335MB or 823MB|models/VAE|
|CodeFormer|Restoration model for tasks like facial restoration and resolution enhancement|-|-|models/codeformer|

Alright, after introducing the models above, sometimes it's challenging to figure out where a specific model belongs. Fortunately, some thoughtful individuals have created a small website for you: [https://spell.novelai.dev/](https://spell.novelai.dev/). Simply drag the model in, and you'll get all the information you need.

![](https://p3-sign.toutiaoimg.com/tos-cn-i-6w9my0ksvp/c93a09104ba1402a9811c53f5b601fd8~tplv-obj.image?lk3s=3de049d8&traceid=20231127152715CA67B3484C26416A9B70&x-expires=2147483647&x-signature=JGwEnB4MzhS6LfdM1zUxvlq1kSo%3D)