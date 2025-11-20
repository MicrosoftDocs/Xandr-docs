---
title: Audit Best Practices
description: When working with Xandr audits, there are a couple of best practices to ensure that your creatives display properly during the audit process.
ms.date: 11/04/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Audit best practices

When working with Xandr audits, there are a couple of best practices to ensure that your creatives display properly during the audit process. 

**Allowlist - IPs and domains**

In order to ensure proper review, allow list our audit IPs and domains. This is also important for creative display, because a creative may fail to display if it includes geotargeting restrictions that limit where it can render.

- Western US:
  - Input 68.67.139.192 /26 (netblock)
  - Input 68.67.136.192 /26 (netblock)
  - Input 68.67.139.0   /26 (netblock)
  - 128.85.76.18/31
  - 28.24.139.140/31
  - 8.85.77.64/31
  - 2.208.223.42/31
- NY office:
  - Input 207.237.150.0 /24 (netblock)
  - 68.67.164.193
  - 68.67.164.194
  - 68.67.164.195
- Offshore:
  - 115.112.103.132
  - 123.201.61.176
  - 115.248.62.88
  - 118.185.207.40
  - 14.143.143.24
  - 118.185.184.184
  - 14.98.34.200
  - 182.74.78.216
  - 14.143.179.218
  - 223.31.25.162
  - 107.178.218.71
  - 169.47.132.71
  - 169.55.107.131
  - 111.93.148.126
  - 182.72.26.38
  - 14.98.201.134
  - 38.132.110.83
  - 35.238.185.16
  - 182.75.97.18
  - 216.73.161.182
  - 2.57.168.149
  - 157.97.121.97
  - 45.146.55.72
  - 136.144.42.114
- Domains:
  - `adnxs.net`
  - `adnxs.com`
  - `creative-preview-an.com`
  - `cq-preview.adnxs.net`
  - `new-audit.adnxs.net`
  - `cq-auditor.adnxs.net`


## Related topics

- [Creative Troubleshooting FAQ](creative-troubleshooting-faq.md)
