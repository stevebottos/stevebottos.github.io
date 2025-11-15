---
layout: default
title: "V-JEPA 2 Isn't Getting the Hype It Deserves"
excerpt: "Some thoughts about the potential power of Meta's V-Jepa 2."
tags: [video, multi-modal, foundational models]
date: 2024-11-09
---

# V-JEPA 2 Isn't Getting the Hype It Deserves

It’s hard to believe that it’s been nearly half a decade since OpenAI released CLIP. From a computer vision perspective, it felt like the landscape of the industry was about to change fundamentally forever. CNNs' dominance faded, massively pretrained Vision Transformers (ViTs) were the standard, gone were the days of imagenet-pretrained ResNets. Of course ChatGPT was released shortly after, and multimodal LLMs have dominated the spotlight ever since. In practice, though, massively pretrained ViTs continue to underpin the vision side of these systems — often serving as the primary visual feature extractor for the LLM, while still remaining ubiquitous in state of the art vision-only tasks.

Lately, though, I hear more and more chatter about world models, and it feels like eventually people will be talking about these rather than LLMs achieving AGI etc. As humans with our own actual intelligence, it seems obvious that a functioning world model/AGI would require the ability to encode the physical world not just spatially but also temporally. In June, Meta released V-JEPA 2, a significant contribution toward that goal. This seems like something worth being excited over, world models aside, and yet I haven’t heard much about it since its release.

Now, we certainly can provide a multimodal LLM with a series of frames, treating them as individual images and explaining that the frames are related to one another and in sequence, but these frames are still usually tokenized as discrete 2D chunks of information. The reasoning about their sequential/temporal relationship is an afterthought, whereas the 3D tubelet-based embeddings that models like V-JEPA 2 offer encode temporal information naturally. On top of that, it’s also easy to imagine how prohibitively expensive it would be to “stream” video to an LLM for analysis, then there are latency and privacy concerns… It just doesn’t seem to me like LLMs are going to dominate the vision space in general, especially not when it comes to applications involving video.

Forgetting applications like video question-answering and captioning, what about simple object detection — what if we want to tell a satellite from a star? If an object is rising or falling? Estimate impact force? Even simple tasks like this are impossible given a single frame. This isn’t to say that training on video data is particularly revolutionary, rather to illustrate that even simple tasks require sequential information.

To quickly recap:

* OpenAI’s CLIP was a breakthrough model \- pretrained on hundreds or millions of image-text pairs.  
* Spatial, single-frame information is adequate for some tasks, but it lacks the temporal information that multi-frame sequences convey.  
* This temporal information is not trivial, from the lofty realm of world models and AGI all the way down to simple object classification, there are use-cases that depend on temporal information.  
* Current technologies like LLMs can reason about a sequence of frames, but the manner in which they do so is more like leafing through an album rather than watching a video

**So why am I excited about V-JEPA 2?**

It’s worth remembering that 3D convolutional networks have been the backbone of video understanding for years — powering models like C3D, I3D, and SlowFast. These architectures use true 3D kernels that capture space and time jointly, making them the go-to choice for action recognition and motion-based detection. Transformer-based video models, by contrast, have mostly relied on 2D ViTs pretrained on images (often CLIP) and then fused temporal information afterward. They “tokenize” frames, not motion.

V-JEPA 2 changes that. For the first time, we have a massive-scale (1B+ parameter), openly available Vision Transformer that operates directly on spatiotemporal tubelets—effectively a 3D ViT—pre-trained for general-purpose world understanding. Just as CLIP revolutionized image understanding by unlocking general-purpose 2D representations, V-JEPA 2 has the potential to do the same for video, bringing genuine temporal reasoning into the foundation model era.

The key word here is “potential”. While there is some research happening, It’s not yet widely established that the embeddings produced by the model’s encoder layer are semantically rich enough to be used out of the box — that is, without any additional training — but it seems promising. I can think of a bunch of fun experiments, I hope to try some of them if time permits and report back with what I find.
