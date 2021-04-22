---
title: RISC-V相关
date: 2021-04-20T18:54:21.953Z
draft: false
featured: false
image:
  filename: featured
  focal_point: Smart
  preview_only: false
tags:
  - RISC-V
---
迄今为止, 我并未主持过RISC-V相关的项目: 相关的研究一般是由Ben或Dan来主导，我参与/贡献其中的特定部分。此类研究包括:

* FENL:泄漏屏障指令扩展。该指令可以帮助用户清空某一特定的微架构组件，使得掩码实现的评估和调试更加简捷。
* 掩码指令扩展, 支持各类2-share操作, 如Boolean到算数掩码, 有限域乘法和求逆等等。在扩展指令/ISA加掩/不加掩条件下实现了多种算法，如AES和SM4。论文正式发表后计划会将代码公布.
* 其他掩码/非掩码RISC-V汇编的实现: 年内计划完成部分，但短时间内可能不会更新。
