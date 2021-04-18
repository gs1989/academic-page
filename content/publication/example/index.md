---
abstract: Masking is a well-loved and widely deployed countermeasure against
  side-channel attacks, in particular in software. Under certain assumptions
  (w.r.t. independence and noise level), masking provably prevents attacks up to
  a certain security order and leads to a predictable increase in the number of
  required leakages for successful attacks beyond this order. The noise level in
  typical processors where software masking is used may not be very high, thus
  low masking orders are not sufficient for real world security. Higher order
  masking however comes at a great cost, and therefore a number of techniques
  have been published over the years that make such implementations more
  efficient via parallelisation in the form of bit or share slicing. We take two
  highly regarded schemes (ISW and Barthe et al.), and some corresponding open
  source implementations that make use of share slicing, and discuss their true
  security on an ARM Cortex-M0 and an ARM Cortex-M3 processor (both from the LPC
  series). We show that micro-architectural features of the M0 and M3 undermine
  the independence assumptions made in masking proofs and thus their theoretical
  guarantees do not translate into practice (even worse it seems unpredictable
  at which order leaks can be expected). Our results demonstrate how difficult
  it is to link theoretical security proofs to practical real-world security
  guarantees.
slides: example
url_pdf: ""
publication_types:
  - "1"
authors:
  - Si Gao
  - Ben Marshall
  - Dan Page and Elisabeth Oswald
author_notes: []
publication: CHES 2020 (IACR Trans. Cryptogr. Hardw. Embed. Syst.)
summary: ""
url_dataset: ""
url_project: ""
publication_short: ""
url_source: ""
url_video: ""
title: "Share-slicing: Friend or Foe?"
doi: 10.13154/tches.v2020.i1.152-174
featured: true
tags:
  - Masking Side-Channel Analysis
categories:
  - Masking assumptions
projects:
  - REASSURE(http://reassure.eu/)
image:
  caption: ""
  focal_point: ""
  preview_only: false
date: 2021-04-18T15:34:24.884Z
url_slides: ""
publishDate: 2017-01-01T00:00:00Z
url_poster: ""
url_code: ""
---
