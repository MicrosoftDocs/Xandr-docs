---
title: Microsoft Monetize - External DSPs Using Buyer Seat IDs
description: Explore the DSP eligibility, verify Buyer Seat IDs, confirm migration status, and ensure correct Microsoft Ads member IDs for ineligible seats.
ms.date: 10/28/2023
---

# Microsoft Monetize - External DSPs using buyer seat IDs

Not every buyer seat ID that you'll see when creating deals is currently eligible for deal creation. Before you create a custom deal with an external DSP using buyer seat IDs, you should check the Buyer Seat Migration Status reference table and communicate with the buyer to ensure you're using the correct IDs.

The following DSPs have either fully or partially migrated to use buyer seat ID bidding on Microsoft Advertising, or they're in the process of migrating. When you set up a custom deal, you will see a combination of Microsoft Advertising member IDs and seat IDs when selecting a buyer.

Before you try to set up a deal using a buyer seat ID, please use the Seat ID Deal Status column in the table to verify eligibility. If your external DSP is marked Not Eligible, you should continue to set up deals using the Microsoft Advertising member ID.

> [!NOTE]
> External DSPs not identified in this table have not yet migrated to buyer seat IDs.

For more information, see [Understanding Buyer Seat IDs](understanding-buyer-seat-ids.md).

| Bidder ID|Bidder Name|Seat ID Bidding Status|Seat ID Deal Status|Supports Deal Buyer Entity ID|Category|
|--|--|--|--|---|---|
| 8   |MediaMath | Bidding with seats on 100% of traffic | Eligible for Seat ID Deals |N/A|N/A|
| 13  |OwnerIQ |N/A|N/A |1|members|
| 17  |Roku OneView|N/A|N/A|1|members|
| 18  |Zeta | Bidding with seats on 100% of traffic |3|members_and_seats| Eligible for Seat ID Deals|
| 20  |Amobee(formerly known as Turn)|N/A|N/A|Bidding with seats on 100% of traffic|Eligible for Seat ID Deals|
| 33  |Peer39 |N/A |N/A |1 |members|
| 34  |Epsilon/Conversant |3|members_and_seats|Bidding with seats on 100% of traffic|Eligible for Seat ID Deals|
| 44  |Quantcast | Bidding with seats on 100% of traffic | Eligible for Seat ID Deals |N/A|N/A|
| 48  |Proximic|N/A|N/A|1|members|
| 52  |Criteo|N/A|N/A|1|members|
| 54  |iPromote | 3 | members_and_seats| Bidding with seats on 100% of traffic | Eligible for Seat ID Deals|
| 65  |eyeReturn|N/A|N/A|1|members|
| 66  |Simpli.fi|N/A|N/A|1|members|
| 74  |ClickDistrict (Platform 161 / Verve DSP)|N/A|N/A|1|members|
| 78  |Accordant Media, LLC|N/A|N/A|1|members|
| 82  | The Trade Desk | Bidding with seats on 100% of traffic | Eligible for Seat ID Deals |N/A|N/A|
| 87  |Buzzlogic|N/A|N/A|1|members|
| 89  |Grapeshot|N/A|N/A|1|members|
| 91  | Adform | Bidding with seats on 100% of traffic | Eligible for Seat ID Deals ||N/A|N/A|
| 94  |AdGear|N/A|N/A|1|members|
| 96  | Media.net |3 | members_and_seats  Bidding with seats on 100% of traffic | Eligible for Seat ID Deals |
| 98  |DoubleVerify|N/A|N/A|1|members|
|100  |sociomantic|labs GmbH|N/A|N/A|1|members|
|101  |DV360 (formerly known as DBM)|Bidding with seats on 100% of traffic|Eligible for Seat ID Deals||N/A|N/A|
|107  |Bidtheatre|N/A|N/A|1|members|
|112  |Delta Projects|N/A|N/A|1|members|
|114|AcuityAds|N/A|N/A|1|members|
|120|Integral Ad Science|N/A|N/A|1|members|
|122|Dealer.com|N/A|N/A|1|members|
|123|Vizury Interactive Solutions Pvt. Ltd.|N/A|N/A|1|members|
|125|FOutClient01Bidder|1|members|N/A|N/A|
|137|Semcasting|1|members|N/A|N/A|
|139|adtheorent_bidder|1|members|N/A|N/A|
|145|AdPilot|1|members|N/A|N/A|
|158|Adobe - Display|1|members|N/A|N/A|
|160|AppNexus Testing Data Provider Bidder|1|members|N/A|N/A|
|164|LiquidM Technology GmbH|1|members|N/A|N/A|
|172| Nextroll (Adroll) 3 | members_and_seats | Bidding with seats on 100% of traffic|Eligible for Seat ID Deals|
|177|Adloox (Data Provider)|1|members|N/A|N/A|
|179|El Toro (Data Provider)|1|members|N/A|N/A|
|180|Crimson Tangerine Ltd.|1|members|N/A|N/A|
|183 | Verizon Media Group| Bidding with seats on 100% of traffic|Eligible for Seat ID Deals|N/A|N/A|
|194|Mediarithmics|1|members|N/A|N/A|
|197|mbr targeting GmbH|1|members|N/A|N/A|
|216|Mobile Listening Bidder|1|members|N/A|N/A|
|218|The Weather Channel, LLC (Data Provider)|1|members|N/A|N/A|
|222|Rockerbox, Inc|1|members|N/A|N/A|
|225|MaxPoint Interactive|1|members|N/A|N/A|
|226|4Info, Inc. (Cadent)|1|members|N/A|N/A|
|228|BlueCava, Inc.|1|members|N/A|N/A|
|230|TradeLab (Data Provider)|1|members|N/A|N/A|
|236|Opt Out Advertising B.V.|1|members|N/A|N/A|
|240|Ubimo|1|members|N/A|N/A|
|245|Media IQ Digital Ltd|1|members|N/A|N/A|
|247|Addictive Mobility|1|members|N/A|N/A|
|254|Active Agent| Bidding with seats on 100% of traffic | Eligible for Seat ID Deals |N/A|N/A|
|256|Platform Integrations Test RTDP (Data Provider)|1|members|N/A|N/A|
|259|dw_bidder_capacity|1|members|N/A|N/A|
|260|Triapodi LTD|1|members|N/A|N/A|
|264|Samba RDP|1|members|N/A|N/A|
|268|Civolution B.V. (Data Provider)|1|members|N/A|N/A|
|271|Accordant Media, LLC - 2|1|members|N/A|N/A|
|276|So-net Media Networks|1|members|N/A|N/A|
|283|adsquare GmbH|1|members|N/A|N/A|
|290|AppNexus Floor Optimization|1|members|N/A|N/A|
|291|Deqwas Inc.|1|members|N/A|N/A|
|297|LDMobile (netADge)|1|members|N/A|N/A|
|301|Adserver Test (Data Provider)|1|members|N/A|N/A|
|302|remerge bidder|1|members|N/A|N/A|
|304|Factual Inc (Data Provider)|1|members|N/A|N/A|
|305|Exponential Interactive, Inc.|1|members|N/A|N/A|
|306|AdDaptive Intelligence, Inc.|1|members|N/A|N/A|
|313|TradeLab2|1|members|N/A|N/A|
|315|RTB House|1|members|N/A|N/A|
|319|A.Mob|1|members|N/A|N/A|
|320|Travel Audience GmbH|1|members|N/A|N/A|
|326|Integral Ad Science (Data Provider 2)|1|members|N/A|N/A|
|327|AppNexus Programmable Data (Data Provider)|1|members|N/A|N/A|
|328|StackAdapt|Bidding with seats on 100% of traffic|Eligible for Seat ID Deals |N/A|N/A|
|329|Accordant Media, LLC|1|members|N/A|N/A|
|331|Beeswax|1|members|N/A|N/A|
|332|Mediasmart Mobile S.L.|1|members|N/A|N/A|
|333|Bidtellect|1|members|N/A|N/A|
|335|Emerse Sverige AB|1|members|N/A|N/A|
|337|Schibsted|1|members|N/A|N/A|
|341|Mindlytix SAS|1|members|N/A|N/A|
|347|Digital To Store Limited|1|members|N/A|N/A|
|349|apd_scylla 1|members|N/A|N/A|
|351|Adelphic(formerly known as Viant)|Bidding with seats on 100% of traffic|Eligible for Seat ID Deals|N/A|N/A|
|353|Jaduda GmbH|1|members|N/A|N/A|
|359|Biga Bid Media Ltd|1|members|N/A|N/A|
|360|Chalk Digital, Inc.|1|members|N/A|N/A|
|363|Kobler AS|1|members|N/A|N/A|
|368|TAPTAP Networks, S.L|1|members|N/A|N/A|
|370|Blis Media Ltd.|1|members|N/A|N/A|
|373|LinkedIn Bidder|1|members|N/A|N/A|
|375|RhythmOne LLC|1|members|N/A|N/A|
|376|Mobile Professionals B.V.|1|members|N/A|N/A|
|384|Appier Inc.|1|members|N/A|N/A|
|385|Hybrid Adtech Inc|1|members|N/A|N/A|
|386|Nanigans Bidder|1|members|N/A|N/A|
|388|Bidswitch|1|members|N/A|N/A|
|389|AdElement, Inc.|1|members|N/A|N/A|
|390|Adello Group AG|1|members|N/A|N/A|
|394|Localsensor B.V.|1|members|N/A|N/A|
|397|Adtube AS|1|members|N/A|N/A|
|399|Zemanta|Bidding with seats on 100% of traffic| Eligible for Seat ID Deals |N/A|N/A|
|402|Lerta Business Inc.|1|members|N/A|members|
|405|Hawk (TabMo SAS)|1|members|N/A| members |
|408|Smadex SL|1|members|N/A|members|
|402| Lerta Business Inc.|1| members | N/A | members |
| 405 | Hawk (TabMo SAS) | 1 | members | N/A | members |
| 408 | Smadex SL                              | 1 | members | N/A | members |
| 421 | AN Data Science Internal               | 1 |         | 1   |         |
| 423 | Smartology                             | 1 | members | N/A | members |
| 425 | Arago DSP                              | 1 | members | N/A | members |
| 430 | Yandex Europe AG                       | 1 | members | N/A | members |
| 431 | Kika Tech Inc                          | 1 | members | N/A | members |
| 435 | ReadPeak                               | 1 | members | N/A | members |
| 437 | SundaySky, Inc.                        | 1 | members | N/A | members |
| 438 | M1D (BidSwitch)                        | 1 | members | N/A | members |
| 440 | YDN                                    | 1 | members | N/A | members |
| 442 | Knorex Pte. Ltd.                       | 1 | members | N/A | members |
| 443 | Prebid Server                          | 1 | members | N/A | members |
| 446 | Dynalyst                               | 1 | members | N/A | members |
| 448 | US3                                    | 1 | members | N/A | members |
| 449 | OC GROUP TECNOLOGIA DA INFORMACAO LTDA | 1 | members | N/A | members |
| 451 | National Media Connection              | 1 | members | N/A | members |
| 453 | Pocketmath, Inc.                       | 1 | members | N/A | members |
| 454 | digiseg apn gateway                    | 1 | members | N/A | members |
| 457 | YJ Test                                | 1 | members | N/A | members |
| 461 | Beemray OY (Data Provider)             | 1 | members | N/A | members |
| 462 | appnexus-video                         | 1 | members | N/A | members |
| 463 | Deepintent | Bidding with seats on 100% of traffic | Eligible for Seat ID Deals |N/A|N/A|
| 464 | SMARTSTREAM.TV GmbH                    | 1 | members | N/A | members |
| 465 | ITN Holdings, LLC                      | 1 | members | N/A | members |
| 466 | Craid Inc.                             | 1 | members | N/A | members |
| 467 | NetSeer, Inc. (Data Provider)          | 1 | members | N/A | members |
| 468 | Eyeview Inc.                           | 1 | members | N/A | members |
| 471 | SQUARED (Data Provider Test 12)        | 1 | members | N/A | members |
| 472 | Semasio GmbH (Data Provider)           | 1 | members | N/A | members |
| 473 | Axel Springer Teaser Ad GmbH           | 1 | members | N/A | members |
| 474 | DO NOT USE - Kayla's test              | 1 | members | N/A | members |
| 475 | Amobee TV | Bidding with seats on 100% of traffic | Eligible for Seat ID Deals |N/A|N/A|
| 480 | Mnet_bidder_2.0                        | 1 | members | N/A | members |
| 481 | PLAYGROUND XYZ (Data Provider)         | 1 | members | N/A | members |
| 482 | MadHive Inc.                           | 1 | members | N/A | members |
| 483 | MSAN | Bidding with seats on 100% of traffic | Eligible for Seat ID Deals |N/A|N/A|
| 484 | AdLede (Data Provider)                 | 1 | members | N/A | members |
| 488 | Emetriq GmbH RT (Data Provider)        | 1 | members | N/A | members |
| 490 | test-1                                 | 1 | members | N/A | members |
| 492 | Test (can be deleted)                  | 1 | members | N/A | members |
| 493 | onetest2-rp-1(can be deleted)          | 1 | members | N/A | members |
| 508 |        Nano Interactive GmbH (Data Provider)       | 1 |      members      | N/A | N/A |
| 512 | Test1Bdr                                           | 1 | members           | N/A | N/A |
| 514 | Test2                                              | 1 | members           | N/A | N/A |
| 522 | Silver Bullet Media Services (Data Provider)       | 1 | members           | N/A | N/A |
| 523 | Inmar-OIQ, LLC                                     | 1 | members           | N/A | N/A |
| 524 | GCN INC                                            | 1 | members           | N/A | N/A |
| 526 | GUM GUM Inc (Data Provider)                        | 1 | members           | N/A | N/A |
| 528 | Qwarry (Data Provider)                             | 1 | members           | N/A | N/A |
| 534 | Ericson Emodo                                      | 1 | members           | N/A | N/A |
| 539 | Sirdata SAS (Data Provider)                        | 1 | members           | N/A | N/A |
| 541 | Seedtag Advertising SL (Data Provider)             | 1 | members           | N/A | N/A |
| 542 | ALLIANCE GRAVITY DATA MEDIA (Data Provider)        | 1 | members           | N/A | N/A |
| 543 | Adelaide Metrics Inc. (Data Provider)              | 1 | members           | N/A | N/A |
| 545 | Audigent (Data Provider)                           | 1 | members           | N/A | N/A |
| 546 | Cognitiv Corp, a Delaware corp (Data Provider)     | 1 | members           | N/A | N/A |
| 550 | Proxistore (Data Provider)                         | 1 | members           | N/A | N/A |
| 551 | CTV AppNexus Programmable Data (Data Provider)     | 1 | members           | N/A | N/A |
| 552 | non CTV AppNexus Programmable Data (Data Provider) | 1 | members           | N/A | N/A |
| 554 | MarketOps                                          | 1 | members           | N/A | N/A |
| 555 | Predictive Audiences RealTime APD                  | 1 | members           | N/A | N/A |
| 556 | MNTN                                               | 1 | members           | N/A | N/A |
| 557 | Ravel Technologies (Data Provider)                 | 1 | members           | N/A | N/A |
| 558 | Audigent (Test)                                    | 1 | members           | N/A | N/A |
| 559 | Choreograph RTDP (Data Provider)                   | 1 | members           | N/A | N/A |
| 560 | Decide                                             | 1 | members           | N/A | N/A |
| 561 | Goldfish Ads, LLC (Data Provider)                  | 1 | members           | N/A | N/A |
| 563 | Dable Inc                                          | 1 | members           | N/A | N/A |
| 564 | Jio Platforms Limited                              | 1 | members           | N/A | N/A |
| 565 | Jio Platforms Limited                              | 1 | members           | N/A | N/A |
| 566 | ShareThis Inc.                                     | 1 | members           | N/A | N/A |
| 567 | Mobvista International Technology Limited          | 1 | members           | N/A | N/A |
| 568 | Taboola Inc.                                       | 1 | members           | N/A | N/A |
| 571 | Adhese                                             | 1 | members           | N/A | N/A |
| 573 | ALGORIX TECHNOLOGY PTE LTD (Bidder)                | 1 | members           | N/A | N/A |
| 574 | NASMEDIA Co., LTD                                  | 1 | members           | N/A | N/A |
| 575 | Mediamath Acquisition Corporation dba Infillion    | 1 | members           | N/A | N/A |
| 576 | Eskimi UAB                                         | 1 | members           | N/A | N/A |
| 577 | Nativo Inc                                         | 1 | members           | N/A | N/A |
| 578 | RTB House S.A. (Data Provider)                     | 1 | members           | N/A | N/A |
| 579 | Taboola Inc.                                       | 1 | members           | N/A | N/A |
| 580 | HK POWER ENGINE LIMITED                            | 1 | members           | N/A | N/A |
| 581 | R&R Digital Pty Ltd                                | 1 | members           | N/A | N/A |
| 582 | Opera Software Ireland Ltd                         | 1 | members           | N/A | N/A |
| 96  | Media.Net                                          | 3 | members_and_seats | N/A | N/A |
| 129 | Platform Services Test Bidder                      | 3 | members_and_seats | N/A | N/A |
| 172 | NextRoll                                           | 3 | members_and_seats | N/A | N/A |
| 182 | PTM Internal Test Bidder 2                         | 3 | members_and_seats | N/A | N/A |
| 188 | Amazon Advertising                                 | 3 | members_and_seats | N/A | N/A |
| 427 | Adobe - Video                                      | 3 | members_and_seats | N/A | N/A |
| 483 | MSAN                                               | 3 | members_and_seats | N/A | N/A |
| 562 | Gecko Technologies DMCC                            | 3 | members_and_seats | N/A | N/A |
| 569 | Programmatic Mechanics Pontiac DSP                 | 3 | members_and_seats | N/A | N/A |
| 572 | Engageya Tracknomics                               | 3 | members_and_seats | N/A | N/A |
| 8   | MediaMath                                          | 2 | seats             | N/A | N/A |
| 20  | Amobee (Nexxen)                                    | 2 | seats             | N/A | N/A |
| 44  | Quantcast                                          | 2 | seats             | N/A | N/A |
| 82  | The Trade Desk                                     | 2 | seats             | N/A | N/A |
| 91  | AdForm                                             | 2 | seats             | N/A | N/A |
| 101 | Display & Video 360                                | 2 | seats             | N/A | N/A |
| 133 | Basis Technologies                                 | 2 | seats             | N/A | N/A |
| 183 | Yahoo DSP                                          | 2 | seats             | N/A | N/A |
| 254 | Active Agent                                       | 2 | seats             | N/A | N/A |
| 328 | StackAdapt                                         | 2 | seats             | N/A | N/A |
| 351 | Adelphic (Viant)                                   | 2 | seats             | N/A | N/A |
| 399 | Zemanta                                            | 2 | seats             | N/A | N/A |
| 463 | DeepIntent, Inc.                                   | 2 | seats             | N/A | N/A |
| 494 | PulsePoint, Inc.                                   | 2 | seats             | N/A | N/A |
| 529 | Baidu (Hong Kong) Limited                          | 2 | seats             | N/A | N/A |
| 530 | Cognitiv                                           | 2 | seats             | N/A | N/A |
| 531 | Conversant (ValueClick)                            | 2 | seats             | N/A | N/A |
| 532 | AdTheorent                                         | 2 | seats             | N/A | N/A |
| 541 | Infosys                                            | 2 | seats             | N/A | N/A |
| 542 | OpenX                                              | 2 | seats             | N/A | N/A |
| 544 | TripleLift                                         | 2 | seats             | N/A | N/A |