---
layout: default
title: "Fast, Simple, Fun - Video Understanding with <40M Parameters"
excerpt: "A very approachable jumping off point for video captioning. If you're GPU-poor (<24GB vram) this is for you."
tags: [video, nlp, multi-modal, foundational models, tutorial]
date: 2024-11-16
---

# Fast, Simple, Fun - Video Understanding with <40M Parameters

Recent advances in foundational models have dramatically lowered the barrier to entry for complex tasks like video understanding. This post explores how to build a capable video captioning model with less than 40 million trainable parameters, leveraging the power of pre-trained models like V-JEPA 2. If you're looking for an approachable, hands-on project that doesn't require a supercomputer, this is for you.

In some past articles, I’ve introduced V-JEPA 2\. If you’ve read those, you’re all caught up. If not, you can think of it as CLIP but for video, in a sense \- it’s a large-scale pretrained model that we can use as a foundational model out of the box for tasks within the same modality. The encoder works for video tasks out of the box, as the paper proved with their linear probe experiments, which saves us thousands of GPU-hours.

The authors of the [V-JEPA 2 paper](https://arxiv.org/abs/2410.17653) obtained SOTA performance for something-something v2 classification with a 4-layer probe on top of the encoder. This is a pretty standard way of evaluating the quality of embeddings produced by a foundation model. So I figured, let’s see what else they can do. 

This is meant to be a pretty approachable exercise. I’m not trying to do anything groundbreaking here, I’m really just curious about how quickly I can get to decent results. You don’t need that much compute available to reproduce this either, and the dataset is very accessible to everyone (no youtube downloads necessary). I’d love to extend this further if there’s interest.

Below are some examples of video clips with their corresponding predicted captions overlayed.

<div style="display: grid; grid-template-columns: repeat(2, 1fr); gap: 20px; justify-items: center; align-items: center; margin: 0 auto; max-width: 800px;">
  <div style="text-align: center;">
    <img src="{{ site.baseurl }}/assets/posts/2024-11-16-vjepa2-video-captioning/170354.gif" alt="Example 1" style="max-width: 100%; height: auto; display: block; margin: 0 auto;">
  </div>
  <div style="text-align: center;">
    <img src="{{ site.baseurl }}/assets/posts/2024-11-16-vjepa2-video-captioning/174998.gif" alt="Example 2" style="max-width: 100%; height: auto; display: block; margin: 0 auto;">
  </div>
  <div style="text-align: center;">
    <img src="{{ site.baseurl }}/assets/posts/2024-11-16-vjepa2-video-captioning/184590.gif" alt="Example 3" style="max-width: 100%; height: auto; display: block; margin: 0 auto;">
  </div>
  <div style="text-align: center;">
    <img src="{{ site.baseurl }}/assets/posts/2024-11-16-vjepa2-video-captioning/198826.gif" alt="Example 4" style="max-width: 100%; height: auto; display: block; margin: 0 auto;">
  </div>
</div>

---

## Some Basics

It’s worth clarifying that models like [VideoMAE](https://arxiv.org/abs/2203.12602) did exist before V-JEPA 2 came around, and you could probably do everything we talk about here with that as an encoder, it just might not work as well out of the box since it hasn’t been trained on such a mountain of data. A relevant detail from the VideoMAE paper is that video features are highly compressible, since most frame-to-frame details are redundant, so let’s keep that in mind. What this means is that I may not really need the entire (long) output sequence from the video encoder, I might just need 5-10% of it. 

Another relevant paper here is [BLIP-2](https://arxiv.org/abs/2301.12597). This made use of a so-called “Q-Former” as a bridge between a frozen vision model and a frozen language model, neither of which were designed with the opposite modality in mind. The Q-Former in this setup was the only trainable parameter, and it served two purposes: 

1. Learn queries that act as prefixes for the language model, and   
2. Compress the output sequence of the vision encoder.

So, we’d have as input to the text model a sequence consisting of \[Vision Tokens, Text Tokens\]. In BLIP-2’s setup, where the vision tokens are the output of the Q-Former. You might notice that what we’re doing here is basically prefix tuning from the perspective of the text model. 

This recipe is pretty simple to extend. The language model can be either encoder-decoder (BLIP-2's paper uses T5 Flan), or decoder-only. We'll be using decoder-only, since it's easy and we're really only looking for a baseline PoC today. ![Blip2 Vanilla]({{ site.baseurl }}/assets/posts/2024-11-16-vjepa2-video-captioning/blip2-vanilla.png)

## Extending to Video Captioning 

We can take the original architecture, and swap out the video encoder for V-JEPA 2's encoder. Now we have this:
![Blip2 Vanilla]({{ site.baseurl }}/assets/posts/2024-11-16-vjepa2-video-captioning/blip2-video.png)
You can find a full implementation [here](https://github.com/stevebottos/vjepa2-video-captioning). For the data, I went with [Something-Something v2](https://cv.gluon.ai/build/examples_datasets/somethingsomethingv2.html), and supplemented the training data with: [some additional captions that I synthetically generated](https://github.com/stevebottos/somethingsomethingv2-paraphrase) so that it behaved more like a video captioning dataset and less like an action recognition dataset. It’s still not much data, but it’s enough to prove a point.

There are a few details that are different from BLIP-2’s, most of which are imposed by the fact that I don’t have a ton of compute readily available right now:

- Since we’re dealing with video, we have to decide how many frames we want to deal with. V-JEPA 2 can handle up to 64 frames. I decided on 32 frames, which results in an output sequence length of 4096\. This is a pretty sane decision since our dataset spans 2-6 second clips, and uniformly sampling 32 frames of a 6-second clip is still \~5 frames per second, which is plenty.  
- I pre-compute V-JEPA 2 features and save them, then train on top of these features, so that I don’t have to deal with another model loaded on my GPU during training and so that I don’t have to wait for features to be computed at runtime. ***Ideally*** we wouldn’t do this, because we could augment the input videos during training, but I’m compute-poor right now.  
- We learn 64 queries instead of the original 32\. The additional queries come from the fact that we’re handling longer sequence lengths. ***Ideally*** we’d learn more queries, because 4096 \-\> 64 is very aggressive compression, more than than 5-10% rule of thumb that VideoMAE’s paper suggests.  
- If you’re using a relatively small dataset like I am, you can get away with a very small Q-Former, much smaller than they use in the paper. ***Ideally*** we’d have at least 10x the data that we do, and scale the Q-Former accordingly

You’ll find more details in the README in the github repo, with instructions on how to get started. End to end, you can get these results in \<24 hours (6-8 hours of preprocessing V-JEPA 2’s features, 10-12 hours of training on my 4070\)

## Some Additional Things to Try

I’m really curious about what the output embeddings from the Q-Former can be used for. Since they’re essentially compressed features, is it more practical to use them for embedding-related tasks than the output features of V-JEPA 2 directly? For example:

- Can we average across the 64-length sequence to produce one embedding? Can this embedding be used for tasks like clustering or similarity search?  
- Could we chunk a longer video into k-clips, each \<=6 seconds, as a way of comparing two movies for example, to see which scenes match with others?  
- Do the video embeddings start to look like text embeddings? For example, if we have a video of “a person jumping over a fence”, would we notice that some of the 64 video embeddings that we produce look like the text embeddings for that sentence? 

## Conclusion

This experiment demonstrates that it's possible to achieve compelling results in video captioning without extensive computational resources. By standing on the shoulders of giants and cleverly combining pre-trained models like V-JEPA 2 and the architectural principles of BLIP-2, we can create effective and efficient models. The results are promising, and the "Additional Things to Try" section opens up exciting avenues for future research.

