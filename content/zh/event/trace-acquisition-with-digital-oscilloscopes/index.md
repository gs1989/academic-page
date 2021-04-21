---
title: Trace acquisition with digital oscilloscopes
all_day: false
publishDate: 2021-04-21T09:36:32.368Z
draft: false
featured: false
---
Side channel acquisitions usually utilise a digital oscilloscope to capture traces, so in order to set up an experimental work bench, the first step is to communicate with your oscilloscope. 

My personal experience is this step can vary according to each vendor: for instance, Picoscope usually provides a brilliant API programming guide. As long as you understand what you need to do (and have some basic programming skills), performing measurements should not be hard (back in Bristol, we even try to let undergraduate students do this). One of the reason is perhaps Picoscope has no screen of its own, so everything must be transmit to PC through API. Lecroy on the other hand, manufactures those high-end scopes that not only have screen, but also a powerful PC itself. There are many methodologies provided and the hard bit often becomes finding which one is still working. Depending on your scope type, some might already become legacy. So the real challenge is finding the right way to do this from a 300-500 pages documents. With our scope at Bristol, it seems vbs stript is the best option at that time (not sure right now or with any new type of scope).

I will share some of my code here, in case it helps to build your own environment. As this has 0 innovation value, I only provide this as a reference, without any warranty. Fairly speaking, if you know exactly what you are doing, you should be able to write your own code quickly, without reading my code here.

* Acquisition script (python) for Lecroy oscilloscope: https://github.com/gs1989/Trace-Acquisition-for-Lecroy
* Acquisition project (c#) for Picoscope: https://github.com/gs1989/AcquisitionProject
