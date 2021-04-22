---
title: 掩码实现
subtitle: "COSMIC: 开源掩码软件实现汇编"
date: 2021-04-20T09:25:03.069Z
draft: false
featured: false
tags:
  - 掩码
links:
  - url: https://github.com/sca-research/COSMIC
    name: Github(COSMIC)
    icon_pack: fab
    icon: github
image:
  filename: featured
  focal_point: Smart
  preview_only: false
---
掩码方案的实现绝非易事: 几乎所有的安全保障或者证明都需要依赖于相应的安全假设，而安全假设对于一般用户而言，或难以理解，或容易忽视，甚至无法实施。考虑到近几年来论文多辅以代码同时发表，这种情况有所改善。然而，除非论文中明确关注于某个具体实现的安全性，通常文中能找到诸如“若该方案用于任何其他平台(与文中不同)上，我们无法保证其实现的安全性”。

当然，我可以理解从工程角度看这样的安全声明非常苍白：毕竟选择掩码实现主要目的就是保证实现安全。但是，掩码安全抑或任何的实现安全，都是严格依赖于特定平台的：若不指定应用平台，作者不可能提供过高的安全保障。尽管如此，除了验证掩码方案的逻辑正确性和效率以外，在某个特定平台上进行安全分析在我看来仍是非常有意义的：即使分析结果依赖于特定平台，我们仍可以从中学到一些常识和陷阱，帮助开发者理解实现掩码中可能面临的挑战和问题。最终的目标可以是提出一套完整的基准度量，用于评估ELMO类仿真工具的有效性：但如前文所述，开发这样的基准需要消耗大量的时间和精力，目前我无法承担这样的工作量...

目前COSMIC项目目录中有3个掩码方案：全部都在我们常用的M0或M3平台上进行了测试。我手上仍有几个正确性无误，但安全性分析未完成的开源实现：若您有兴趣，请联系我。这里列出的掩码方案都是基于ARM平台：若涉及RISC-V平台，会放入RISC-V项目一并介绍。COSMIC中的每个方案均作为sub-module: 请注意，其中不少源自其他人的开源工程。若您希望用于非研究用途，请检查每个module中原作者的license要求。

* DPA课本中的1阶字节掩码AES汇编实现\[1]: 此方案使用两个字节的随机掩码分别保护S盒的输入和输出。每次加密前需根据掩码值计算所用的掩码表：具体方案描述详见("Scheme_Introduction.md"). 简而言之, 我并未找到简洁的实现方式能使得该方案在实测中1阶安全 ("Scheme_Introduction.md" 中介绍了各种容易出现的问题)。最终我选用的实现使用了4个额外的掩码，使得实测中通过了1阶TVLA; 显然二阶依然并不安全。

  以下两个实现源自Virginia Tech，均为基于C语言的实现：
* 一阶字节掩码AES实现: 可以看作上述方案的C语言版本 (未加入以上汇编实现中我加入的各种补丁）。该实现易于理解，但由于使用C语言，具体分析所有泄漏点较为困难(1阶不安全)。详见 https://github.com/gs1989/Masked-AES-Implementation
* 一阶share-slicing掩码AES: 该实现将多个share存储在同一个寄存器中(成为"share-slicing")。每个S盒均分解为多个加掩码的AND門，再用2-share的ISW乘法实现每个AND門。也就是说, 尽管该实现使用了share-slicing, 但并未使用针对share-slicing的掩码设计。我们在CHES 2020的文章中说明了此类实现方式在软件平台中需特别小心：所需的安全假设在底层硬件上实际不存在支持。安全分析可见https://github.com/gs1989/Masked-AES-Implementation, 或者参考论文发表页中的"Share-slicing: Friend or Foe?"

\[1]  Stefan Mangard, Elisabeth Oswald, Thomas Popp, Power analysis attacks - revealing the secrets of smart cards. Springer 2007
