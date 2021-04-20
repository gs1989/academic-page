---
slides: Beyond ELMO
url_pdf: ""
title: Beyond ELMO...
summary: ""
url_video: ""
date: 2021-04-19T18:41:50.241Z
categories: []
url_slides: ""
subtitle: my own perspective
tags:
  - ELMO
links:
  - icon: github
    icon_pack: fab
    name: ELMO Github
    url: https://github.com/sca-research/ELMO
  - url: http://reassure.eu/
    name: REASSURE project site
    icon_pack: fab
image:
  caption: ELMO workflow
  focal_point: Smart
  filename: featured.png
url_code: ""
---
Analysing power leakage is never a trivial task: users must deploy their code on the target platform, then construct a measurement setup where the power consumption can be reliably measured. 

Usually this first step is already challenging: not every cryptographic engineer (including myself) has a deep understanding of electrical engineering; some may have issues with using an oscilloscope as well.  Besides, from a development perspective, finding new issues when the design has already be deployed is far from ideal: tons of effort could end up in vain. 

Obviously, a better way to do this would be using a tool that can detect potential leakage in the early stage: for example, if the application is based on ARM processors, testing leakage right after the crypto-code has been written, before any realistic deployment on any device. This is not entirely a new idea though: many previous simulators did the same, including the one integrated in Riscure's Inspector. Depending on the methodology, this so-called simulator can be an algorithmic one (eg. abstract or C-based), or a circuit-level one (eg. SPICE-based). The former is fast, yet lacking various details, eg. assembly and architectural elements. The latter is more accurate, yet extremely slow and requires full circuit specification (i.e. full white-box access, not available for ARM). 

ELMO can be regarded as a trade-off option in-between:  ELMO reads ARM assembly and make-up the missing architectural effect through statistical profiling (with realistic measurements).  The following figure shows the workflow of ELMO. 

Details of ELMO (plus the paper) can be found in the Github repository (https://github.com/sca-research/ELMO). As this is what I took over from Dr. David McCann, I won't further introduce more technical details.

An obvious question to ask is about the "quality" of ELMO: unfortunally there isn't any existing metric to measure the "quality" (in fact, people might not even agree with each other on what does "quality" mean here...). This has been the core challenge I worked on in Bristol/Klagenfurt. More specifically, we have tried the following:

1) On another ARM M0 core: ELMO works for any set of code that based on 16-bit Thumb instructions, however, the power model is built with profiling one specific ARM M0 core (STM32F0). A natrual question to ask is how well does this model generalise to other ARM M0 cores, espeicially for cores from a different vendor. Thanks to Dr. Dan Page's SCALE project (https://github.com/danpage/scale), we get a stable measurement setup for another M0 core, NXP LPC1114. Following exactly the same approach, we have rebuilt the ELMO model on this core and release the specific model coefficient file in the repository. Detailed comparision results have been anounced in ARM Research Summit 2018 (slides: https://github.com/sca-research/ELMO/blob/master/Modeling_M0_leakage_generically.pdf) and CHES 2018 (the walk and explore section).

2) Simulation accuracy: if we simply define the "quality" as simulation accuracy, then the standard metric in machine learning should be checking the cross-validation results. We have done so on the new core (details see in https://github.com/sca-research/ELMO/blob/master/ELMOCrossValidation.xlsx): in short, the simulation accuracy is OK if we are targeting at the same chip and same measurement setup; but not OK otherwise. 

3) Other metrics: depending on the specific goal, users do not always care about the simulation accuracy. For instance, if the final output is a fixed-v.s.-random T-test, the goal is to find any leaky cycle and find out why: we do not neccessarily care about how much it leaks, as T statistic cannot be regarded as the magnitude of the leakage. In this case, we care about whether our tool captures all leakage in the realistic measurement. The tricky part is there is no metric for this right now in the community: this is one of our on-going effort and hopefully I can update this thread in a few months.

4) Benchmark: the above metric can be quite theorectical and hard to intepret. A trivial option is to have many masking code with known issues and then benchmark how many flaws the tool has found. Sounds easy, but the fact is there are not that many software masking code with "known issues". Many code still lie in the argorithmatic level (eg. written in C), which means any practical flaw from the assembly or micro-architecture is "out of the scope". You can always analyse yourself, but with a gray-box core where the low-level details are missing and a TVLA that only reports the leakage without any reasoning behind, constructing such a benchmark takes a lot of effort that is hardly appreciated by any major acadamic venue. We have spent some effort in this catogrory, which will be documented in as a seperated project (masking implementations).

 
