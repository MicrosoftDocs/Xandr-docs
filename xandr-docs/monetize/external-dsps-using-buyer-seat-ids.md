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

|Bidder ID|Bidder Name|Seat ID Bidding Status|Seat ID Deal Status|supports_deal_buyer_entity_id|category|
|--|--|--|--|--|--|
| 8   |MediaMath | Bidding with seats on 100% of traffic | Eligible for Seat ID Deals |1|N/A|
| 13  |OwnerIQ |N/A|N/A |1|members|
| 17  |Roku OneView|N/A|N/A|1|members|
| 18  |Zeta | Bidding with seats on 100% of traffic|Eligible for Seat ID Deals|3|members_and_seats|
| 20  |Amobee(formerly known as Turn)|Bidding with seats on 100% of traffic|Eligible for Seat ID Deals|N/A|N/A|
| 33  |Peer39 |N/A |N/A |1 |members|
| 34  |Epsilon/Conversant |Bidding with seats on 100% of traffic|Eligible for Seat ID Deals|3|members_and_seats|
| 44  |Quantcast | Bidding with seats on 100% of traffic | Eligible for Seat ID Deals |N/A|N/A|
| 48  |Proximic|N/A|N/A|1|members|
| 52  |Criteo|N/A|N/A|1|members|
| 54  |iPromote | Bidding with seats on 100% of traffic | Eligible for Seat ID Deals|3 | members_and_seats|
| 65  |eyeReturn|N/A|N/A|1|members|
| 66  |Simpli.fi|N/A|N/A|1|members|
| 74  |ClickDistrict (Platform 161 / Verve DSP)|N/A|N/A|1|members|
| 78  |Accordant Media, LLC|N/A|N/A|1|members|
| 82  | The Trade Desk | Bidding with seats on 100% of traffic | Eligible for Seat ID Deals |N/A|N/A|
| 87  |Buzzlogic|N/A|N/A|1|members|
| 89  |Grapeshot|N/A|N/A|1|members|
| 91  | Adform | Bidding with seats on 100% of traffic | Eligible for Seat ID Deals |N/A|N/A|
| 94  |AdGear|N/A|N/A|1|members|
| 96  | Media.net | Bidding with seats on 100% of traffic | Eligible for Seat ID Deals |3| members_and_seats|
| 98  |DoubleVerify|N/A|N/A|1|members|
|100  |sociomantic|labs GmbH|N/A|N/A|1|members|
|101  |DV360 (formerly known as DBM)|Bidding with seats on 100% of traffic|Eligible for Seat ID Deals|N/A|N/A|
|107  |Bidtheatre|N/A|N/A|1|members|
|112  |Delta Projects|N/A|N/A|1|members|
|114|AcuityAds|N/A|N/A|1|members|
|120|Integral Ad Science|N/A|N/A|1|members|
|122|Dealer.com|N/A|N/A|1|members|
|123|Vizury Interactive Solutions Pvt. Ltd.|N/A|N/A|1|members|
|125|FOutClient01Bidder|N/A|N/A|1|members|
|137|Semcasting|N/A|N/A|1|member|
|139|adtheorent_bidder|N/A|N/A|1|members|
|145|AdPilot|N/A|N/A|1|members|
|158|Adobe - Display|N/A|N/A|1|members|
|160|AppNexus Testing Data Provider Bidder|N/A|N/A|1|members|
|164|LiquidM Technology GmbH|N/A|N/A|1|members|
|172| Nextroll (Adroll) | Bidding with seats on 100% of traffic|Eligible for Seat ID Deals|3 | members_and_seats|
|177|Adloox (Data Provider)|N/A|N/A|1|members|
|179|El Toro (Data Provider)|N/A|N/A|1|members|
|180|Crimson Tangerine Ltd.|N/A|N/A|1|members|
|183 | Verizon Media Group| Bidding with seats on 100% of traffic|Eligible for Seat ID Deals|N/A|N/A|
|194|Mediarithmics|N/A|N/A|1|members|
|197|mbr targeting GmbH|N/A|N/A|1|members|
|216|Mobile Listening Bidder|N/A|N/A|1|members|
|218|The Weather Channel, LLC (Data Provider)|N/A|N/A|1|members|
|222|Rockerbox, Inc|N/A|N/A|1|members|
|225|MaxPoint Interactive|N/A|N/A|1|members|
|226|4Info, Inc. (Cadent)|N/A|N/A|1|members|
|228|BlueCava, Inc.|N/A|N/A|1|members|
|230|TradeLab (Data Provider)|N/A|N/A|1|members|
|236|Opt Out Advertising B.V.|N/A|N/A|1|members|
|240|Ubimo|N/A|N/A|1|members|
|245|Media IQ Digital Ltd|N/A|N/A|1|members|
|247|Addictive Mobility|N/A|N/A|1|members|
|254|Active Agent| Bidding with seats on 100% of traffic | Eligible for Seat ID Deals |N/A|N/A|
|256|Platform Integrations Test RTDP (Data Provider)|N/A|N/A|1|members|
|259|dw_bidder_capacity|N/A|N/A|1|members|
|260|Triapodi LTD|N/A|N/A|1|members|
|264|Samba RDP|N/A|N/A|1|members|
|268|Civolution B.V. (Data Provider)|N/A|N/A|1|members|
|271|Accordant Media, LLC - 2|N/A|N/A|1|members|
|276|So-net Media Networks|N/A|N/A|1|members|
|283|adsquare GmbH|N/A|N/A|1|members|
|290|AppNexus Floor Optimization1|members|N/A|N/A|
|291|Deqwas Inc.|N/A|N/A|1|members|
|297|LDMobile (netADge)|N/A|N/A|1|members|
|301|Adserver Test (Data Provider)|N/A|N/A|1|members|
|302|remerge bidder|N/A|N/A|1|members|
|304|Factual Inc (Data Provider)|N/A|N/A|1|members|
|305|Exponential Interactive, Inc.|N/A|N/A|1|members|
|306|AdDaptive Intelligence, Inc.|N/A|N/A|1|members|
|313|TradeLab2|N/A|N/A|1|members|
|315|RTB House|N/A|N/A|1|members|
|319|A.Mob|N/A|N/A|1|members|
|320|Travel Audience GmbH|N/A|N/A|1|members|
|326|Integral Ad Science (Data Provider 2)|N/A|N/A|1|members|
|327|AppNexus Programmable Data (Data Provider)|N/A|N/A|1|members|
|328|StackAdapt|Bidding with seats on 100% of traffic|Eligible for Seat ID Deals |N/A|N/A|
|329|Accordant Media, LLC|N/A|N/A|1|members|
|331|Beeswax|N/A|N/A|1|members|
|332|Mediasmart Mobile S.L.|N/A|N/A|1|members|
|333|Bidtellect|N/A|N/A|1|members|
|335|Emerse Sverige AB|N/A|N/A|1|members|
|337|Schibsted|N/A|N/A|1|members|
|341|Mindlytix SAS|N/A|N/A|1|members|
|347|Digital To Store Limited|N/A|N/A|1|members|
|349|apd_scylla N/A|N/A|1|members|
|351|Adelphic(formerly known as Viant)|Bidding with seats on 100% of traffic|Eligible for Seat ID Deals|N/A|N/A|
|353|Jaduda GmbH|N/A|N/A|1|members|
|359|Biga Bid Media Ltd|N/A|N/A|1|members|
|360|Chalk Digital, Inc.|N/A|N/A|1|members|
|363|Kobler AS|N/A|N/A|1|members|
|368|TAPTAP Networks, S.L|N/A|N/A|1|members|
|370|Blis Media Ltd.|N/A|N/A|1|members|
|373|LinkedIn Bidder|N/A|N/A|1|members|
|375|RhythmOne LLC|N/A|N/A|1|members|
|376|Mobile Professionals B.V.|N/A|N/A|1|members|
|384|Appier Inc.|N/A|N/A|1|members|
|385|Hybrid Adtech Inc|N/A|N/A|1|members|
|386|Nanigans Bidder|N/A|N/A|1|members|
|388|Bidswitch|N/A|N/A|1|members|
|389|AdElement, Inc.|N/A|N/A|1|members|
|390|Adello Group AG|N/A|N/A|1|members|
|394|Localsensor B.V.|N/A|N/A|1|members|
|397|Adtube AS|N/A|N/A|1|members|
|399|Zemanta|Bidding with seats on 100% of traffic| Eligible for Seat ID Deals |N/A|N/A|
|402|Lerta Business Inc.|N/A|members|1|members|
|405|Hawk (TabMo SAS)|N/A| members |1|members|
| 408 | Smadex SL                                          | N/A | N/A | 1 | members           |
| 421 | AN Data Science Internal 1                         | N/A | N/A | 1 | members           |
| 423 | Smartology                                         | N/A | N/A | 1 | members           |
| 425 | Arago DSP                                          | N/A | N/A | 1 | members           |
| 430 | Yandex Europe AG                                   | N/A | N/A | 1 | members           |
| 431 | Kika Tech Inc                                      | N/A | N/A | 1 | members           |
| 435 | ReadPeak                                           | N/A | N/A | 1 | members           |
| 437 | SundaySky, Inc.                                    | N/A | N/A | 1 | members           |
| 438 | M1D (BidSwitch)                                    | N/A | N/A | 1 | members           |
| 440 | YDN                                                | N/A | N/A | 1 | members           |
| 442 | Knorex Pte. Ltd.                                   | N/A | N/A | 1 | members           |
| 443 | Prebid Server                                      | N/A | N/A | 1 | members           |
| 446 | Dynalyst                                           | N/A | N/A | 1 | members           |
| 448 | US3                                                | N/A | N/A | 1 | members           |
| 449 | OC GROUP TECNOLOGIA DA INFORMACAO LTDA             | N/A | N/A | 1 | members           |
| 451 | National Media Connection                          | N/A | N/A | 1 | members           |
| 453 | Pocketmath, Inc.                                   | N/A | N/A | 1 | members           |
| 454 | digiseg apn gateway                                | N/A | N/A | 1 | members           |
| 457 | YJ Test                                            | N/A | N/A | 1 | members           |
| 461 | Beemray OY (Data Provider)                         | N/A | N/A | 1 | members           |
| 462 | appnexus-video                                     | N/A | N/A | 1 | members           |
| 463 | Deepintent|Bidding with seats on 100% of traffic | Eligible for Seat ID Deals|N/A| N/A |
| 464 | SMARTSTREAM.TV GmbH                                | N/A | N/A | 1 | members           |
| 465 | ITN Holdings, LLC                                  | N/A | N/A | 1 | members           |
| 466 | Craid Inc.                                         | N/A | N/A | 1 | members           |
| 467 | NetSeer, Inc. (Data Provider)                      | N/A | N/A | 1 | members           |
| 468 | Eyeview Inc.                                       | N/A | N/A | 1 | members           |
| 471 | SQUARED (Data Provider Test 12)                    | N/A | N/A | 1 | members           |
| 472 | Semasio GmbH (Data Provider)                       | N/A | N/A | 1 | members           |
| 473 | Axel Springer Teaser Ad GmbH                       | N/A | N/A | 1 | members           |
| 474 | DO NOT USE - Kayla's test                          | N/A | N/A | 1 | members           |
| 475 | Amobee TV| Bidding with seats on 100% of traffic| Eligible for Seat ID Deals| N/A| N/A |
| 480 | Mnet_bidder_2.0                                    | N/A | N/A | 1 | members           |
| 481 | PLAYGROUND XYZ (Data Provider)                     | N/A | N/A | 1 | members           |
| 482 | MadHive Inc.                                       | N/A | N/A | 1 | members           |
| 483 | MSAN  | Bidding with seats on 100% of traffic | Eligible for Seat ID Deals| N/A | N/A  |
| 484 | AdLede (Data Provider)                             | N/A | N/A | 1 | members           |
| 488 | Emetriq GmbH RT (Data Provider)                    | N/A | N/A | 1 | members           |
| 490 | test-1                                             | N/A | N/A | 1 | members           |
| 492 | Test (can be deleted)                              | N/A | N/A | 1 | members           |
| 493 | onetest2-rp-1(can be deleted)                      | N/A | N/A | 1 | members           |
| 508 | Nano Interactive GmbH (Data Provider)              | N/A | N/A | 1 | members           |
| 512 | Test1Bdr                                           | N/A | N/A | 1 | members           |
| 514 | Test2                                              | N/A | N/A | 1 | members           |
| 522 | Silver Bullet Media Services (Data Provider)       | N/A | N/A | 1 | members           |
| 523 | Inmar-OIQ, LLC                                     | N/A | N/A | 1 | members           |
| 524 | GCN INC                                            | N/A | N/A | 1 | members           |
| 526 | GUM GUM Inc (Data Provider)                        | N/A | N/A | 1 | members           |
| 528 | Qwarry (Data Provider)                             | N/A | N/A | 1 | members           |
| 534 | Ericson Emodo                                      | N/A | N/A | 1 | members           |
| 539 | Sirdata SAS (Data Provider)                        | N/A | N/A | 1 | members           |
| 541 | Seedtag Advertising SL (Data Provider)             | N/A | N/A | 1 | members           |
| 542 | ALLIANCE GRAVITY DATA MEDIA (Data Provider)        | N/A | N/A | 1 | members           |
| 543 | Adelaide Metrics Inc. (Data Provider)              | N/A | N/A | 1 | members           |
| 545 | Audigent (Data Provider)                           | N/A | N/A | 1 | members           |
| 546 | Cognitiv Corp, a Delaware corp (Data Provider)     | N/A | N/A | 1 | members           |
| 550 | Proxistore (Data Provider)                         | N/A | N/A | 1 | members           |
| 551 | CTV AppNexus Programmable Data (Data Provider)     | N/A | N/A | 1 | members           |
| 552 | non CTV AppNexus Programmable Data (Data Provider) | N/A | N/A | 1 | members           |
| 554 | MarketOps                                          | N/A | N/A | 1 | members           |
| 555 | Predictive Audiences RealTime APD                  | N/A | N/A | 1 | members           |
| 556 | MNTN                                               | N/A | N/A | 1 | members           |
| 557 | Ravel Technologies (Data Provider)                 | N/A | N/A | 1 | members           |
| 558 | Audigent (Test)                                    | N/A | N/A | 1 | members           |
| 559 | Choreograph RTDP (Data Provider)                   | N/A | N/A | 1 | members           |
| 560 | Decide                                             | N/A | N/A | 1 | members           |
| 561 | Goldfish Ads, LLC (Data Provider)                  | N/A | N/A | 1 | members           |
| 563 | Dable Inc                                          | N/A | N/A | 1 | members           |
| 564 | Jio Platforms Limited                              | N/A | N/A | 1 | members           |
| 565 | Jio Platforms Limited                              | N/A | N/A | 1 | members           |
| 566 | ShareThis Inc.                                     | N/A | N/A | 1 | members           |
| 567 | Mobvista International Technology Limited          | N/A | N/A | 1 | members           |
| 568 | Taboola Inc.                                       | N/A | N/A | 1 | members           |
| 571 | Adhese                                             | N/A | N/A | 1 | members           |
| 573 | ALGORIX TECHNOLOGY PTE LTD (Bidder)                | N/A | N/A | 1 | members           |
| 574 | NASMEDIA Co., LTD                                  | N/A | N/A | 1 | members           |
| 575 | Mediamath Acquisition Corporation dba Infillion    | N/A | N/A | 1 | members           |
| 576 | Eskimi UAB                                         | N/A | N/A | 1 | members           |
| 577 | Nativo Inc                                         | N/A | N/A | 1 | members           |
| 578 | RTB House S.A. (Data Provider)                     | N/A | N/A | 1 | members           |
| 579 | Taboola Inc.                                       | N/A | N/A | 1 | members           |
| 580 | HK POWER ENGINE LIMITED                            | N/A | N/A | 1 | members           |
| 581 | R&R Digital Pty Ltd                                | N/A | N/A | 1 | members           |
| 582 | Opera Software Ireland Ltd                         | N/A | N/A | 1 | members           |
| 18  | Zeta DSP                                           | N/A | N/A | 3 | members_and_seats |
| 34  | Epsilon                                            | N/A | N/A | 3 | members_and_seats |
| 54  | iPromote                                           | N/A | N/A | 3 | members_and_seats |
| 96  | Media.Net                                          | N/A | N/A | 3 | members_and_seats |
| 129 | Platform Services Test Bidder                      | N/A | N/A | 3 | members_and_seats |
| 172 | NextRoll                                           | N/A | N/A | 3 | members_and_seats |
| 182 | PTM Internal Test Bidder 2                         | N/A | N/A | 3 | members_and_seats |
| 188 | Amazon Advertising                                 | N/A | N/A | 3 | members_and_seats |
| 427 | Adobe - Video                                      | N/A | N/A | 3 | members_and_seats |
| 483 | MSAN                                               | N/A | N/A | 3 | members_and_seats |
| 562 | Gecko Technologies DMCC                            | N/A | N/A | 3 | members_and_seats |
| 569 | Programmatic Mechanics Pontiac DSP                 | N/A | N/A | 3 | members_and_seats |
| 572 | Engageya Tracknomics                               | N/A | N/A | 3 | members_and_seats |
| 8   | MediaMath                                          | N/A | N/A | 2 | seats             |
| 20  | Amobee (Nexxen)                                    | N/A | N/A | 2 | seats             |
| 44  | Quantcast                                          | N/A | N/A | 2 | seats             |
| 82  | The Trade Desk                                     | N/A | N/A | 2 | seats             |
| 91  | AdForm                                             | N/A | N/A | 2 | seats             |
| 101 | Display & Video 360                                | N/A | N/A | 2 | seats             |
| 133 | Basis Technologies                                 | N/A | N/A | 2 | seats             |
| 183 | Yahoo DSP                                          | N/A | N/A | 2 | seats             |
| 254 | Active Agent                                       | N/A | N/A | 2 | seats             |
| 328 | StackAdapt                                         | N/A | N/A | 2 | seats             |
| 351 | Adelphic (Viant)                                   | N/A | N/A | 2 | seats             |
| 399 | Zemanta                                            | N/A | N/A | 2 | seats             |
| 463 | DeepIntent, Inc.                                   | N/A | N/A | 2 | seats             |
| 494 | PulsePoint, Inc.                                   | N/A | N/A | 2 | seats             |
| 529 | Baidu (Hong Kong) Limited                          | N/A | N/A | 2 | seats             |
| 530 | Cognitiv                                           | N/A | N/A | 2 | seats             |
| 535 | Stirista_Bidder                                    | N/A | N/A | 2 | seats             |
| 537 | OctillionMediaLLC                                  | N/A | N/A | 2 | seats             |
| 544 | MGID Inc                                           | N/A | N/A | 2 | seats             |
| 548 | MSAN Test                                          | N/A | N/A | 2 | seats             |
| 553 | GDMServices, Inc. d/b/a Bidmind                    | N/A | N/A | 2 | seats             |