---
layout: default
title: "Some RAG Systems and Their Problems"
excerpt: "Text RAG is manageable. Document RAG means bolting on OCR and layout models that work well but add real overhead. Visual RAG skips the extraction step entirely, but trades it for a cost and precision problem of its own."
tags: [vision, text, RAG, engineering]
date: 2026-07-11
---

# Some RAG Systems and Their Problems 
I want to break this down into three flavors of RAG. **Text RAG**: your content is already text, code files, transcripts, that kind of thing. **Document RAG**: you're starting from PDFs, so you have to extract the content before you can do anything with it. **Visual RAG**: you skip extraction entirely and embed the page images directly. All of these options have their own pros and cons, this is my attempt at working through them.

## Text RAG
Let's say you have a corpus of text-only content (code, transcriptions, etc...). You want to allow your users to ask questions about that content, and get a precise answer that's grounded in the source instead of hallucinated. A simple solution looks something like this:

![A typical text RAG pipeline: an offline indexing path that chunks and embeds text content into a vector DB, and an online query path that embeds the user query, searches the vector DB, and feeds the retrieved content plus query to an LLM for the answer.](/assets/posts/rag-issues/rag-flow.svg)

RAG systems can get a lot more complex than this and I've by no means seen all that there is to see in this domain, but even this simple setup is a lot of work to maintain and is pretty brittle. At least in applications that I've worked on, off-the-shelf pretrained models don't do a great job at embedding content in a nuanced way, so you need to train that. Even then, you might rely on a reranker to deliver precise results per the user's query. You also have to manage or pay for the vector db. This is clearly a lot of work already but it's manageable.

## Document RAG
A big wrinkle is that **most content is not text-native.** What if you have pdf documents? Now in addition to everything pictured above you have to:
- extract the doc's content, using something like [Docling](https://github.com/docling-project/docling). This means more models (layout detectors, OCR). These are usually pretty good but again struggle with unique content 
- now you can either: 
  - use the OCR-extracted text only, or 
  - decide to use the visual content (figures, maybe equations and tables) as well. This introduces a whole other modality into your system - now you need to embed and retrieve visual content. It's doable, but it's adding moving parts to an already complicated system 

This is all to say, it's magnitudes more work than Text RAG, and every added model is another place for the pipeline to break on content it wasn't tuned for. It doesn't feel like an elegant solution, it feels like several imperfect systems chained together. Maybe this is as good as it gets, but I think there's room for improvement.

## Visual RAG 
A couple of years ago some researchers released [ColPali](https://arxiv.org/pdf/2407.01449) which is a step forward in terms of simplifying the system I described above. The pitch is straightforward: skip extraction entirely and you fix Document RAG's brittleness, while landing closer to Text RAG's simplicity than Document RAG ever did.

![Figure 1 from the ColPali paper, comparing the standard OCR/layout-detection/captioning retrieval pipeline against ColPali's approach of embedding page images directly with a vision LLM - ColPali is both faster offline (0.39s/page vs 7.22s/page) and more accurate (0.81 vs 0.66 NDCG@5).](/assets/posts/rag-issues/colpali.png)

There's some pretty active work in this field and it's genuinely exciting. The system itself looks like Text RAG again, not Document RAG: the ColPali figure above benchmarks against Document RAG's OCR pipeline, but the pipeline it's proposing skips extraction entirely, so structurally it's Text RAG with a different modality. There is another benefit over Text RAG in that there is no chunking involved. PDFs as images are embedded directly. 

One big caveat: Now the LLM that synthesizes the answer needs to be able to accept visual content, which limits options. Additionally, while ColPali and its successors are great at inter-page retrieval, they are not great at *intra*-page retrieval. You can't reliably crop what's relevant on a page. This is an issue for a few reasons:  
- visual tokens into an LLM are far more costly than text tokens, and full pages can easily be in the ballpark of ~1.5k tokens  
- downsampling full pages to mitigate token spend results in degradation of quality 
- pages often contain a significant amount of distracting information that dilutes context and degrades response quality 

There was actually a [study related to the last point](https://arxiv.org/abs/2511.15090), and it makes the same claim from the model's side: otherwise capable vision-language models are bad at localizing what's relevant on a page, which is why they perform best when handed a cropped region, worse with a full page, and worse still with a whole document. 

![Table 3 from the paper: as evidence granularity narrows from Document to Page to Region, QA accuracy climbs for nearly every model tested - cropping to the relevant region isn't just nice-to-have, it measurably improves answer quality.](/assets/posts/rag-issues/sciegqa-results.png)

Pay attention specifically to Task 2. Notice that the VQA performance delta between the smaller and larger models compresses once you offer a page or a crop? That's the cost story too: narrow the retrieval enough and a cheaper model closes the gap on a more expensive one.

## Where this leaves us
Zoom out and the ordering in that table (crop > page > document) is really just a restatement of the problem: every extra page you hand the model is more surface area for irrelevant content to compete with the actual answer, so retrieval quality degrades as page count grows.

That reframes what "Visual RAG's cost problem" actually is. It's not just that visual tokens are expensive but rather that the retrieval granularity is stuck at the page level, so you're always paying for, and getting distracted by, more than you need. Region-level retrieval is the real fix, but ColPali-style models aren't there yet for reliable intra-page cropping. Until they are, the practical lever is the one you already have: retrieve fewer, more targeted pages rather than dumping whole documents into context.

So the pitch isn't "Visual RAG solves everything" - it's that it clears Document RAG's extraction mess for free, comes closer to Text RAG's simplicity than Document RAG ever did, and its one real weakness (page-level rather than region-level retrieval) is a tractable engineering problem rather than a fundamental one. That's a good trade, and it's the direction I'd bet on.

## What next? 
I posted a bit about this on my X account, in the linked post I outline a system in which you'd use a small, lightweight model I'm calling a "Seeker" that knows how to find relevant content *within* a page after ColPali's retrieval step, essentially a reranker but for visual content. 
<div style="display: flex; justify-content: center;">
<blockquote class="twitter-tweet"><p lang="en" dir="ltr">I feel like instead of either: <br>- PDF -&gt; extract to text+figs -&gt; text RAG<br>- PDF -&gt; image embeddings -&gt; retrieve whole pages<br>... You could do something like this? <a href="https://t.co/IRKvugHmdd">pic.twitter.com/IRKvugHmdd</a></p>&mdash; steve (@steve4thinking) <a href="https://x.com/steve4thinking/status/2074262898357231786?ref_src=twsrc%5Etfw">July 6, 2026</a></blockquote>
</div>
<script async src="https://platform.x.com/widgets.js" charset="utf-8"></script>
Open-vocabulary detection isn't really a new thing, models like Grounding DINO and OWL-ViT are pretty good at this already for objects. They're not really designed for small objects like text, though, and they're not trained to make semantic connections between query<->content. There's a drought of data for this sort of thing, I'm building a dataset to fix that, it's available through [my huggingface](https://huggingface.co/datasets/stevebottos/publaynet-grounding-v1), but at the time of writing it's still a big WIP. 

