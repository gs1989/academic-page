---
abstract: Ge et al. propose the augmented ISA (or aISA), a central tenetof which is the selective exposure of micro-architectural resources via a less opaqueabstraction than normal. The aISA proposal is motivated by the need for controlover such resources, for example to implement robust countermeasures against micro-architectural attacks. In this paper, we apply an aISA-style approach to challengesstemming fromanaloguemicro-architectural leakage; examples include power-basedHamming weight and distance leakage from relatively fine-grained resources (e.g.,pipeline registers), which are not exposed in, and so cannot be reliably controlledvia, a normal ISA. Specifically, we design, implement, and evaluate an ISE namedFENL: the ISE acts as a fence for leakage, preventing interaction between, and henceleakage from, instructions before and after it in program order. We demonstrate thatthe implementation and use of FENL has relatively low overhead, and represents aneffective tool for systematically localising and reducing leakage.
slides: Slides
url_pdf: "https://tches.iacr.org/index.php/TCHES/article/view/8545/8110"
publication_types:
  - "1"
authors:
  - Si Gao
  - Ben Marshall
  - Dan Page
  - Thinh Hung Pham
author_notes: []
publication: CHES 2020 (IACR Trans. Cryptogr. Hardw. Embed. Syst.)
summary: "A paper discussing a set of RISC-V extension instructions that facilitate leakage diagnosing"
url_dataset: ""
url_project: ""
publication_short: ""
url_source: ""
url_video: ""
title: "FENL: an ISE to mitigate analoguemicro-architectural leakage"
doi: 10.13154/tches.v2020.i2.73-98
featured: true
tags:
  - Information leakage
  - Side-channel attack
  - ISA
  - ISE 
  - Micro-architecture
categories:
  - RISC-V

image:
  caption: ""
  focal_point: ""
  preview_only: false
date: 2021-04-18T20:50:24.884Z
url_slides: ""
publishDate: 2020-03-02T00:00:00Z
url_poster: ""
url_code: ""
---
