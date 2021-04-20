---
title: Masking implementations
subtitle: "COSMIC: a Complication of Open-Source Masked Implementations for
  Crypto-software"
date: 2021-04-20T09:25:03.069Z
draft: false
featured: false
categories:
  - Masking
links:
  - url: https://github.com/sca-research/COSMIC
    name: Github(COSMIC)
    icon_pack: fab
    icon: github
image:
  filename: featured
  focal_point: Smart
  preview_only: false
---
Implementing a masking scheme is never a trivial job: security claims are always based on some assumption that you might not understand, simply ignore, or even worse, have no control. The situation is slightly better in recent years, as many researchers publish their code along with their paper. That has been said, unless the paper is really focusing on the security of that implementation, often there will be a sentence saying "we do not guarantee the security of this implementation on your platform".

I get it this is a cumbersome claim for many engineers, after all, security is why you choose this implementation for. However, as masking security (or side channel security in general) strictly depends on the specific platform, there is a limit the authors can do. That has been said, I believe it is at least useful to provide security analysis on *some* platform (instead of ensuring only the functional correctness and efficiency measurement): even if the security problems are not portable, we might learn some pitfalls that might widely exist and helps engineers to limited the security challenges on their selected platforms. Of course, a final goal would be having a benchmark that helps to evaluate the efficacy of ELMO-like tools: unfortunately, it seems that requires much more time and effort than I can afford...

Currently, there is only 3 schemes that have been tested on our ARM M0/M3 cores. I did collected a few more, but did not find the time to analyse the leakage of those. If you were interested in other schemes, please contact me: I might still have something on my hard-drive. Note that here everything is for ARM (most likely for Thumb-16): if the project is RISC-V related, I will add it to the RISC-V project.

More specifically, COSMIC is a gateway of several masking implementations that I have tested. Each one is presented as sub-module, as I am not always the author of the code. If you were interested in using any, please check the license requirements lie in each forked module.

* Assembly-based 1st order byte-wise masking in the DPA book\[1]: this scheme uses 2 byte random mask to protected the Sbox input/output. All the masked table is pre-calculated before each encryption. I have wrote a detailed description in the repository ("Scheme_Introduction.md"). In short, I could not find an easy way to make this scheme 1st order secure ("Scheme_Introduction.md" explains various pitfalls). The final implementation uses 4 extra mask byte and passes 1st order T-test on our platform. However, 2nd order is not secure at all.

  Then we have two C-based implementations forked form Virginia Tech.
* First-order byte-wise masked AES: this can be seen as a C-version of the recommended scheme in the DPA book (without any patch we added in our assembly implementation). This can help you understand the scheme, yet the security analysis is harder, as the implementation is based on C. Details see https://github.com/gs1989/Masked-AES-Implementation
* First-order share-slicing masked AES: This specific implementation stores both shares in the adjacent positions within one register (a technique which we called "share-slicing"). Each Sbox is decompose to multiple masked AND, where each AND is implemented as a 2-share ISW multiplication. That is to say, the implementation uses share-slicing, but did not use more efficient multiplication gadget that is designed for that case. Either way, our paper on CHES 2020 shows this approach can be tricky in software implementations, as there is in fact no low-level designing restriction that support the security assumptions. Security analysis can be found in  https://github.com/gs1989/Masked-AES-Implementation, but also in my publication page of "Share-slicing: Friend or Foe?"

\[1]  Stefan Mangard, Elisabeth Oswald, Thomas Popp, Power analysis attacks - revealing the secrets of smart cards. Springer 2007
