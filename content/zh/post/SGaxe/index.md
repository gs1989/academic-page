---
title: SGAxe
subtitle: ""
date: 2021-05-04T00:00:00.000Z
summary: 对于Intel SGX的一种攻击
draft: false
featured: false
authors: []
lastmod: 2020-12-13T00:00:00.000Z
tags: []
categories: [论文阅读]
projects: []
image:
  caption: ""
  focal_point: ""
  placement: 2
  preview_only: false
---
读了“SGAxe: How SGX Fails in Practice”一文(https://sgaxe.com/)，做一个简单总结。因为不是我目前的主要研究点，读得比较粗略，没有详读背后Intel SGX的详细技术文档，有理解不对的地方欢迎指正。

文章本身主要讲的是用CacheOut技术攻击某个存储在enclave中的密钥，进而伪造证据，通过Intel remote attestation。概念上说CacheOut并不新鲜：毕竟SGX本身大致起到的作用无非是一个虚拟TPM。“虚拟”二字决定了其安全上限：不同于真实TPM，SGX没有独立的执行环境，所有的资源调用都和操作系统共享，仅仅通过访问控制来禁止非法访问enclave中的内容。Enclave中的内容实际是以明文方式存储在内存中的(理解来源于https://www.youtube.com/watch?v=mPT_vJrlHlg， 不清楚是否Intel的技术文档中有明确这一点)，因此当体系结构中出现任何不被访问控制禁用的元件，如Cache，就可能被利用时间信息读出。这一点从SGX出现开始就是明确的，多年来也一直有攻击问世。

这篇论文中比较吸引眼球的部分其实是对攻击出的密钥的利用，完成了伪造报告通过Intel验证的过程。但是就我的理解，做到的实际并不如字面描述一般有威胁性：如文中Figure 4所示，所盗出的密钥实际是Intel专为该处理器验证使用的，且Intel可以将该密钥相关的验证禁用。当然，理论上攻击者总可以重复这一过程获取新的可用验证密钥;但该密钥始终并非图中两个根密钥，不是长期的固定密钥(文中的描述两个根密钥是硬编码处理的，因此无法用cache攻击)。

文中后续给出了三个已知的应用场景：由于不够熟悉，加上文中描述也不够详尽，不好判断影响大小。直观上感觉其中不少问题需要考虑应用的需要和Intel remote attestation提供的是否对应。例如，文中提到在unlinkable状态下，Intel remote attestation不提供身份的鉴别。也就是用白话描述出来“Intel保证某个intel芯片在enclave中诚实执行了这段代码，但不确定是哪一个，也不一定是目前的交互方”。个人怀疑这样的性质本身对于部分应用场景就是不够的：也就是说，即使没有cache攻击，一些应用场景可能也会有问题。由于行业里产品和模块往往会造成开发人员知识的分层，使得下层与上层间的理解出现偏差; 商业上的广告和标题党很多时候还会加剧这种威胁。

尽管SCA是我个人的主要研究点，SGX不能抵抗side channel说不上太大的问题。然而， 在技术文档上直接写“side channel威胁请开发者自行负责”这句话依然是不合适的: 现有的开发环境中（即使是学术研究中也一样），对于side channel一词的指带是没有明确定义的。按照实践的难易，可以简单做下述划分（当然这一点不同的角度也有不同的观点，请结合自身应用再做考量）：
- T0: 剖片，冷冻读取 （这种必须从物理环境入手，无法靠设计解决）
- T0.1: 各类故障，如激光。细分还会有不同的力度和条件，比如Rowhammer(https://github.com/google/rowhammer-test)就不需要侵入，实践起来就容易一些（SGX显然也无法抵抗此类攻击）
- T1: Power/EM: 需要近距离采集测量，但获取的信息量可能很大 （仅靠访问控制不能抵抗）
- T2: Cache timing: 需测量同设备上的运行时间，比特率低，怕运行噪音 (访问控制对Cache的力度不够，目前无法抵抗)
- T3: 算法timing: 算法级实践差异，可能局域网攻击， 如Lucky13(http://www.isg.rhul.ac.uk/tls/Lucky13.html)
- T4: Padding oracle: 方案漏洞，单比特确定信息，可远程

“开发者自行负责”在这里显得非常尴尬：T0-T1 SGX无法处理，但开发者通过代码同样无法处理。只能以来对应用环境本身的限制。也就是说，使用之前，开发者应确定自己的应用环境没有太大的来自T0/T1的威胁。T2级上文中所用，开发者很难自行影响，而SGX目前也无法保护。T3/T4往往涉及到使用的算法和实现，确实可以由开发者保障，但这里的保障又于T0/T1不同：这里需要的只是选择目前认可的算法和实现代码。实际开发过程中，我很怀疑是否所有开发者从intel的一句话理解到这些。

更可能的情况是，开发者会忽略以上所有技术细节，甚至忽略影响更大的环节(如SGX不能保护外设，如键盘的输入过程)，片面地从一些安全描述出发，进行方案的设计和实施，例如“SGX提供独立安全隔离的执行环境”。在应用需求不明的条件下，片面地使用这样的描述作为方案设计的基础非常危险。使用SGX设计方案之前，也许可以考虑以下几个问题：
- “虚拟”的优势是什么？独立的TPM/UKey售价并不高(相比高端intel CPU)，连成LAN的通信速度/PC接口传输也未必慢 (云环境？成本？可移植性？)
- “虚拟”的代价是否可接受？特别是上述攻击中，是否能保证环境中同一个CPU上运行的其他程序不会盗取enclave中的内容？若会盗取，有多大的威胁？
- 系统的其他部分与SGX是否兼容？例如，password的输入必须在一台安全的设备上完成, 而输入后直接在相同设备上调用SGX，其意义是？既然设备已经假定安全，SGX假定系统不安全的努力是否浪费？


##

