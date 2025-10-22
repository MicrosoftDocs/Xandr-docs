---
title: Benefits of AST
description: In this article, understand the benefits of AST to legacy tags.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: seller-tag
ms.author: shsrinivasan
---

# Benefits of AST

AST offers a number of benefits to legacy tags, such as tinytag (`/ttj` or `/tt`).

- **Can reduce ad delivery latency, typically resulting in faster page load times**  
  
  AST loads tags asynchronously and attempts to consolidate ad slots into a single ad call, reducing both the bandwidth and overhead of multiple ad calls while allowing the page to load while ads are being rendered.  

- **Can provide advertisers more control when buying inventory** 
  
  When ad slots are consolidated, advertisers can make use of additional controls that Console provides, such as page-level frequency caps, roadblocks, or competitive exclusions.  

- **Can reduce time and effort needed to debug ads on a page** 
  
  AST fires events and provides methods to easily debug an ad call to let a seller determine why a campaign is not serving or to quickly identify details of an ad that served. These methods have a global scope, so tools can be easily built on top of AST to capture and log this information as needed. Additionally, details about the auction results are included in the ad call response as a JSON structure, so Fiddler traces can also easily capture necessary information.  

- **Can provide many ad experiences to advertisers** 
  
  Numerous experiences are made available when using AST. In addition to supporting standard banners, AST can simultaneously support rich media, native, or video. If a high value video or native campaign is not available, a banner can serve without any redirects or new auctions.  

- **Can simplify ad tagging and setup**  
  
  AST is flexible enough to support all ad formats and page integrations. Individual ad slots can be customized in the tag (providing dynamic configuration) or in Console (removing complexity from the tag). Additionally, custom ad rendering can be assigned to each ad slot and hosted with Xandr. This removes the reliance on the code on page but provides unique, page-specific customization of how an ad renders. This is useful for native ads or when selling multiple ad formats in parallel. Lastly, the same tag can be used in pre-bid setups with a single flag to turn pre-bid support on or off.  

- **Can maintain support for future ad serving features and ad formats**
  
  AST has been built to be flexible to support features we haven't even thought about yet. By adding options to the tag or within Console, AST will be able to deliver new formats or auction capabilities that we build in the future. As our primary tag, all features will be built and optimized to support AST; other tags will not always be updated.
