---
layout: post
title: "Basic Security issues which programmers need to know"
category: 
tags:
- Security
---
{% include JB/setup %}


* 不要信任用户的输入信息！
* 验证所有来自非信任源的输入信息，是使用白名单，不是黑名单。
* 从一开始就要策划安全。安全并不是可以在最后来做的。
* 保持简单。复杂性会增加安全漏洞的可能性。
* 最低限度保持你程序的攻击面(attack surface)[http://en.wikipedia.org/wiki/Attack_surface]。
* 确保程序有“自动防故障装置”(Fail-safe)[http://en.wikipedia.org/wiki/Fail-safe]
* 采用深度防御(defence in depth)[https://buildsecurityin.us-cert.gov/bsi/articles/knowledge/principles/347-BSI.html]
* 坚持最小特权原则(least privilege)[https://buildsecurityin.us-cert.gov/bsi/articles/knowledge/principles/351-BSI.html]
* 采用威胁建模(threat modelling)[http://www.owasp.org/index.php/Threat_Risk_Modeling]（Web程序更应如此）
* 权限分离(Compartmentalize)[http://www.cgisecurity.com/owasp/html/ch04s09.html]
* 没有不透风的墙，在代码中隐藏秘密都无法长久。
* Don’t write your own crypto / 不要自己编写一种加密方法 
* 采用加密（crypto），并不意味着你就安全了（攻击者会寻找弱点）
* 注意缓冲区溢出，并了解如何防范
