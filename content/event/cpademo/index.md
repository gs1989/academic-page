---
title: CPADemo
abstract: A graphic demo the shows how HW-CPA works on the first round of AES
location: " "
date: 2021-04-21T09:43:47.165Z
date_end: 2021-04-21T09:44:45.106Z
all_day: false
event: " "
event_url: " "
publishDate: 2021-04-21T09:43:47.189Z
draft: false
featured: false
image:
  filename: featured
  focal_point: Smart
  preview_only: false
---
This is a demo I wrote for teaching/demonstrating purpose. The underlying target is a trivial byte-wise AES implementation on ARM M3 core. The repository contains a small trace set: by default, the attack python script uses this one and shows how power analysis recovers the secret key by analysing the power traces. In theory the code should work for other trace set or implementations as well, although I have never tried that.

More details see: https://github.com/gs1989/DPAdemo

p.s. Please do not use this to validate your countermeasure etc.: this is basically the trivial attack invented 20 years ago; there are of course much better attacks existing...