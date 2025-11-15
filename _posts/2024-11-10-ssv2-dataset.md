---
layout: default
title: "Something-Something-V2-Paraphrased"
excerpt: "A small contribution to the community. Adds caption-like variety samples to SSV2 dataset."
tags: [video captioning, novel dataset, LLMs, VLMs]
date: 2024-11-10
---
# Something-Something-V2, Paraphrased

Video captioning datasets are usually frustrating to work with. Many rely on YouTube links that frequently go dead, and some struggle to capture both spatial AND temporal nuances. This makes robust, readily-available datasets incredibly valuable for research and development.

Lately I've been turning to the Something-Something-V2 (SSv2) dataset. While it's primarily designed with action recognition in mind, its strong emphasis on both spatial and temporal details makes it an excellent resource for video captioning tasks.

To enhance its utility for this purpose, I've put together a complete set of synthetic paraphrased captions for the SSv2 training set. This effort introduces significant linguistic diversity, which is key for training more robust and generalized captioning models.

A few key stats on the paraphrased dataset:
- 2.4 million+ new captions generated
- An average of 14 paraphrases for each original video label
- Vocabulary expanded from ~8,000 unique words to over 31,000

This enrichment helps models learn a wider range of descriptive language for the same visual concepts. I'm finding this approach helpful for iterating on video captioning tasks that require a nuanced understanding of actions in space and time. 

You can find the full dataset and details here: https://github.com/stevebottos/somethingsomethingv2-paraphrase
