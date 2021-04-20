---
title: RISC-V related
date: 2021-04-20T18:54:21.953Z
draft: false
featured: false
external_link: " "
image:
  filename: featured
  focal_point: Smart
  preview_only: false
---
Up till now, I have not yet led a RISC-V related project: I participate and contribute to such project, but usually it is Ben or Dan coordinated the entire project. This include:

* FENL: the leakage "barrier" instruction extension. This instruction helps users to "clear" a certain part of the micro-architecture, which makes masking implementation and leakage diagnose much easier.
* Masked Instruction extension, which supports various 2-share operations, like boolean to arithmetic, finite field multiplication/inversion etc. There exist several implementations of the unmasked/masked with standard instructions(ISA)/masked with the extended instruction(ISE) version of the same cipher (eg. AES/SM4). We are planing to publish the code afterwards.
* Some other masked/unmasked implementation code in RISC-V assembly: I might be writing a few other cipher's implementation this year, but right now it is not the top priority on my to-do list.