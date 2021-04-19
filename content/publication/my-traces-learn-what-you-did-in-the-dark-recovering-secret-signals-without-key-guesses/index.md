---
title: "My Traces Learn What You Did in the Dark: Recovering Secret
  Signals                Without Key Guesses"
publication_types:
  - "1"
abstract: In side channel attack (SCA) studies, it is widely believed that
  unprotected implementations leak information about the intermediate states of
  the internal cryptographic process. However, directly recovering the
  intermediate states is not common practice in today’s SCA study. Instead, most
  SCAs exploit the leakages in a “guess-and-determine” way, where they take a
  partial key guess, compute the corresponding intermediate states, then try to
  identify which one fits the observed leakages better. In this paper, we ask
  whether it is possible to take the other way around—directly learning the
  intermediate states from the side channel leakages. Under certain
  circumstances, we find that the intermediate states can be efficiently
  recovered with the well-studied Independent Component Analysis (ICA).
  Specifically, we propose several methods to convert the side channel leakages
  into effective ICA observations. For more robust recovery, we also present a
  specialized ICA algorithm which exploits the specific features of circuit
  signals. Experiments confirm the validity of our analysis in various
  circumstances, where most intermediate states can be correctly recovered with
  only a few hundred traces. Our approach brings new possibilities to the
  current SCA study, including building an alternative SCA distinguisher,
  directly attacking the middle encryption rounds and reverse engineering with
  fewer restrictions. Considering its potential in more advanced applications,
  we believe our ICA-based SCA deserves more research attention in the future
  study.
draft: false
featured: false
image:
  filename: featured
  focal_point: Smart
  preview_only: false
date: 2021-04-19T13:26:14.622Z
---
