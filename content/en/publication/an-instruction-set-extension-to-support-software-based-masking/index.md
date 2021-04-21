---
title: An Instruction Set Extension to Support Software-Based Masking
publication_types:
  - "3"
abstract: "In both hardware and software, masking can represent an effective
  means of hardening an implementation against side-channel attack vectors such
  as Differential Power Analysis (DPA). Focusing on software, however, the use
  of masking can present various challenges: specifically, it often 1) requires
  significant effort to translate any theoretical security properties into
  practice, and, even then, 2) imposes a significant overhead in terms of
  efficiency. To address both challenges, this paper explores use of an
  Instruction Set Extension (ISE) to support masking in software-based
  implementations of a range of (symmetric) cryptographic kernels including AES:
  we design, implement, and evaluate such an ISE, using RISC-V as the base ISA.
  Our ISE-supported first-order masked implementation of AES, for example, is an
  order of magnitude more efficient than a software-only alternative with
  respect to both execution latency and memory footprint; this renders it
  comparable to an unmasked implementation using the same metrics, but also
  first-order secure."
draft: false
featured: false
url_pdf: https://eprint.iacr.org/2020/773.pdf
authors:
  - Si Gao
  - Johann Großschädl
  - Ben Marshall
  - Dan Page
  - Thinh Pham
  - Francesco Regazzoni
tags:
  - Side-channel Attack
  - Masking
  - RISC-V
  - ISE
categories:
  - RISC-V

date: 2020-10-16T00:00:00.000Z
---
