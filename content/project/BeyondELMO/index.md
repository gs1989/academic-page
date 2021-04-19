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

ELMO can be regarded as a trade-off option in-between:  ELMO reads ARM assembly and make-up for the missing architectural effect through statistical profiling (with realistic measurements).  The following figure shows the workflow of ELMO. 

Details of ELMO can be found in the Github repository (https://github.com/sca-research/ELMO). As this is what I took over from Dr. David McCann, I won't further introduce more technical details.
