---
title: CPADemo
abstract: A graphic demo the shows how HW-CPA works on the first round of AES
all_day: false
publishDate: 2021-04-21T09:43:47.189Z
draft: false
featured: false
---
This is a demo I wrote for teaching/demonstrating purpose. The underlying target is a trivial byte-wise AES implementation on ARM M3 core. The repository contains a small trace set: by default, the attack python script uses this one and shows how power analysis recovers the secret key by analysing the power traces. In theory the code should work for other trace set or implementations as well, although I have never tried that.

More details see: https://github.com/gs1989/DPAdemo

p.s. Please do not use this to validate your countermeasure etc.: this is basically the trivial attack invented 20 years ago; there are of course much better attacks existing...
