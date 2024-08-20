---
title: LLMs for cybersecurity
date: 2024-08-19
permalink: /posts/2024/LLM4Cyber
tags:
  - Cybersecurity
description: "My perspective on LLMs for cybersecurity"
---

## TL;DR
Cyber-capabilities are a concern for LLMs for good reason. Most current benchmarks are simplifications of real world scenarios. So currently there is still some confusion on how we can view and discuss current capabilities of LLMs when it comes to cyberattack/security.

## Introduction
Cyber-capability of LLMs is dual-use as it benefits both attackers and defenders. Many are concerned that proliferation of cybersecurity/hacking expertise being much more accessible via LLMs, that barriers of entry for crime will be much easier. Such concerns are quite reasonable as underground forums have precedents of service models that do this, such as Exploit-as-a-service or Ransomware-as-a-service. As someone who has had my own [work](https://aclanthology.org/2023.acl-long.415/) become apparent inspiration to some [cybercrime enabling AI services](https://www.darkreading.com/application-security/gpt-based-malware-trains-dark-web), I know there will be markets, demands, and sellers that try to do this.

While I'm quite sure that the service in the previous link is a scam, it should demonstrate that when powerful models capable of highly technical cybercrime *do* become available, there will be a demand to abuse it. Therefore, it is of great importance that current and future generations of models to be evaluated in their capability to perform cybersecurity/cyberoffensive analysis.

Some of my personal takes on this problem.

1. Previously, cybersecurity domain knowledge was often considered a huge bottleneck for previous generations of models ([I even worked on addressing this!](https://aclanthology.org/2024.findings-naacl.3/)). However, current LLMs are generally quite knowledgeable even in the cybersecurity domain. I no longer believe evaluating for domain knowledge is an important measure to understanding the capabilities and potential threats regarding LLMs. The focus should shift on what tasks and problems they are able to solve.

2. Cybersecurity workflow is very complex. It can involve anything between analyzing code, network behavior, logs, threat group activity, etc. Many works tend to simplify the whole workflow when defining a single scope of "cybersecurity expertise". It would be helpful to identify a specific task or behavior to be analyzed (with high utility), in order to evaluate them properly.


### WMDP 
The [WMDP Dataset by Li et al.](https://arxiv.org/pdf/2403.03218) is a carefully crafted multi-choice question benchmark intended to assess knowledge connected to harmful capabilities of LLMs. The intention is to use expert-level knowledge as a **proxy** for harmful capabilities that can arise in biosecurity, cybersecurity, and chemical security. I think that for cybersecurity, it's difficult to construct MC questions that can reflect abilities we care/worry about like execution of exploits. "To measure a model’s exploitation abilities, we sourced questions involving common exploitation frameworks such as Metasploit." But whether familiarity with the Metasploit framework (which can be earned through training on the documentation) can lead to successful exploitation is unclear.

### CONSIDERATIONS FOR EVALUATING LARGE LANGUAGE MODELS FOR CYBERSECURITY TASKS
This [white paper by Gennari et al.](https://insights.sei.cmu.edu/documents/5848/Considerations_for_Evaluating_Large_Language_Models_for_Cybersecurity_Tasks.pdf) includes a great description of the complexity of cybersecurity expertise, and argues how many evaluations limited to knowledge probing can miss other considerations. Three levels of evaluations are proposed 1) Throetical Knowledge Evaluation (Domain Knowledge assessments), 2) Practical Knowledge Evaluation (Ability to provide solutions to self-contained scenarios), and 3) Applied Knowledge Evaluation (the complex work of achieving higher level objectives in open-ended situations). The distinction between 2 and 3 is important, and will indicate whether an LLM's problem-solving abilities extends beyond artificial textbook scenarios.

### Eyeballvul

~~ WIP