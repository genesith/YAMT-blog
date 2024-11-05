---
title: Tokenization Matters?
date: 2024-10-29
permalink: /posts/2024/TokenizationMatters
tags:
  - Tokenization
description: "My perspective on Tokenization"
---

## TL;DR
Tokenization matters!

## Introduction
It's become a [fairly mainstream idea](https://youtu.be/zduSFxRajkE?t=6711) that many model errors can be blamed on tokenization. More modern examples can include the "9.11 is larger than 9.9" and "there are 2 r's in strawberry".
I'm not so sure about this view. I think that for every scenario where a model failure can be attributed to bad tokenization, there's hundreds of scenarios where they succeed *despite* bad tokenization.

But the influence of tokenization is very real, and possibly underappreciated.
I noticed a common frustration across multiple works that is quite evident from their titles. [Tokenization Matters:...](https://aclanthology.org/2024.findings-naacl.113/), [Tokenization counts:...](https://arxiv.org/abs/2402.14903), [Tokenization Matters!...](https://arxiv.org/abs/2405.17067), and of course [wHy DoNt YoU jUsT uSe ThE lLaMa ToKeNiZeR??](https://huggingface.co/blog/catherinearnett/dangers-of-tokenizer-recycling).
Clearly, many believe the effects of tokenization is being overlooked. I tend to agree!
As model training runs become more and more extravagant, we should be paying attention to how the tokenizer shapes the model.
Keep in mind that once a model is trained with a particular tokenizer, it is not trivial to [substitute tokenizers](https://arxiv.org/abs/2405.07883) afterwards.

It's also very challenging to evaluate tokenizers. There are some intrisic evaluations such as fertility and compression effectiveness, but they are [not perfect indicators of performance](https://arxiv.org/pdf/2402.18376). On the other hand, downstream performance evaluations will require fully training a corresponding model (which would be subject to their own hyperparameters), making it prohibitively costly.

## Some thoughts

Some quick writeups of my personal thoughts regarding tokenization.

1. The tokenizer has so many design choices, and many current implementations may be underengineered. Even great models have some odd tokenizer oversights. Many heuristic tricks are inherited from much older models (e.g., reusing GPT2's regex), while new tricks are... [confusing](https://tokencontributions.substack.com/p/pre-tokenization-on-punctuation-in).

2. I am very optimistic about [tokenizer transfer](https://arxiv.org/abs/2405.07883), as it will enable efficient specialist models from well-trained base models. At the moment, we know so little about what's in a token representation. I think we're getting closer though, like [understanding the method in which tokens become words](https://footprints.baulab.info/).

3. LLMs are still remarkably robust to suboptimal tokenization. I think this has allowed tokenization to go underappreciated, since the good ol' "stack more layers/training data" seems to be good enough in preventing problems. However, slightly more [adversarial scenarios of tokenization](https://arxiv.org/abs/2405.17067) will fully mislead models. We should think about what does/doesn't happen in training, and how it can shape behaviors such as [bias](https://aclanthology.org/2024.findings-naacl.113/) or [fragility](https://arxiv.org/abs/2410.23684).

4. Curently, tokenizers are mostly linguistics-agnostic. For instance, the BPE algorithm is purely optimized for data compression. Admittedly, this works [very well](https://aclanthology.org/2024.findings-acl.134/), but surely it is [not optimal](https://aclanthology.org/2020.findings-emnlp.414/)? I am becoming more convinced that [tokenization is more than compression](https://arxiv.org/abs/2402.18376), and feel [morpheme-backed subwords](https://aclanthology.org/2024.acl-long.804/) are bound to be better. Point 3 makes this very tricky to verify though.

5. To make safer models, we will need safer tokenizers. Most tokenizers have a bunch of [undertrained tokens](https://arxiv.org/abs/2405.05417) that can cause model errors or aid in jailbreaks. I really appreciate this paper; it kickstarted a lot of systematic tokenizer analysis. But I am of the opinion that undertrained tokens are only one type of vulnerability rooted in the tokenizer. I discovered one such [vulnerability](https://arxiv.org/abs/2410.23684) in byte-level BPE tokenizers recently.



# Multilingual (Korean) tokenization
I have been thinking a lot about multilingual tokenization, mostly kickstarted by some intutions afforded by seeing how bad Korean tokenization is.
Modern Korean characters are represented by 3 bytes in UTF-8. It's a shame that these 3 bytes have almost no relation to the character. This is especially upsetting since Korean characters are made of 3 syllables anyway, and it would most likely improve if we used the syllables (jamo) as tokenization blocks instead of bytes.
I am very surprised that no major Korean company has put out a model with Jamo Korean tokenization, since this research direction has been [established](https://aclanthology.org/2020.lrec-1.429.pdf) in [literature](https://koreascience.kr/article/JAKO202111037333482.page).

Other languages with multi-byte characters suffer from similar problems, and I wonder how much is being overlooked because they are not immediately obvious to many in the English-centric research community.
Having multiple bytes to represent a character puts a lot of burden on the tokenizer and the model, opening up to lots of potential [fragility](https://arxiv.org/abs/2410.23684).
Some languages, like Korean, may have characters with compositional structures that are lost after being processed by the grinder that is UTF-8.
I think many languages could benefit from specialized tokenizers that utilize linguistic features of the language. Tokenizer transfer would be very important in this case.