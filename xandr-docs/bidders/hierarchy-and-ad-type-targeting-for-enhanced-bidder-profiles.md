---
title: Enhanced Bidder Profiles Ad Type Targeting
description: This article explains the hierarchy and ad type targeting for enhanced bidder profiles.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Enhanced Bidder profiles ad type targeting

## Hierarchy

In the past, bidder profiles had a parent/child hierarchy. This added additional complexity to the bidder profiles. Now bidder profiles have only a single level. For traffic to get through, it only needs to meet the requirement of one active profile. This results in a very simple, manageable system that is an ally in troubleshooting endeavors.

In summary:

- Bidder profiles only have a single level. Parent/child hierarchy is not there anymore.
- The impression must meet all the requirements of any of the profile objects to be sent to the bidder (see the chart below for more information).
  - OR relationship across profile objects
  - AND relationship within the profile

### Hierarchy for bidder profiles

The impression must meet **all** the requirements **of at least one** profile object to be sent to the bidder.

| Description of Behavior | Example | Formula |
|:---|:---|:---|
| Profiles will have an OR relationship across profile objects | There are 3 profiles associated with the bidder:<br> - P1: include country, Canada<br> - P2: exclude ad type, Banner<br> - P3: include Exchange 1<br><br>An impression must meet the requirement of either P1, P2, or P3. It does not need to meet the requirements of all 3 profiles. | P1 OR P2 OR P3 |
| Profiles will have an AND relationship within the profile object. | There is a single profile object associated with a bidder:<br> - P1 includes ad type, banner (V1) and includes Exchange 1, Direct (V2)<br><br>The incoming impression must come from a member in Exchange 1, Direct **and** be a banner ad type. | V1 AND V2 |
| Profiles will have an OR relationship within fields | There is a single profile object associated with a bidder:<br> - P1 includes ad type, banner (F1) and ad type, video (F2)<br><br>The incoming impression can be either a banner or video in order to pass profile check. | F1 OR F2 |
| Combined behavior within and across profiles | There are 2 profiles associated with the bidder:<br> - P1: include country, Canada (V1) and Exchange 2, Connect (V2)<br> - P2: excludes ad type, Banner (V3) and includes country, Belgium (V4)<br><br>The incoming impression must either be from Canada and a member in the Connect Exchange or a banner impression from Belgium. | (V1 and V2) OR (V3 and V4) |

## Media type targeting - Sizes and ad types

In the past, profiles did not support filtering or targeting by a specific ad type (banner, native, audio, video). A bidder could exclude both native and video by including all other sizes besides 1x1 in the sizes target array. Similarly, you could target native and video by including only 1x1.

In Enhanced Bidder Profiles, we wanted to give users the ability to target/filter on ad types. This will give maximum flexibility to our partners. In addition, video and banner ad types will have a "sizes" action to allow filtering/targeting by sizes for those specific ad types.

The following rules apply:

- An ad type must be explicitly excluded in a `PUT`/`POST` in order to be excluded. Otherwise, it is implied to be included.
- If no size is listed, then all sizes are assumed to be excluded or included (depending on ad type action).
- If a size is listed, then it is included or excluded depending on the action for that ad type.
- Sizes only apply to video and banner ad types.
- 1x1 and 0x0 sizes are not allowed in the sizes object.

### Use cases

#### Exclude native ad type

##### `PUT`/`POST` Call

```
{
        "bidder_profile": {
                "code": "test_1",
                "description": "Test Profile",
                "targeting": {
                        "ad_types": {
                                "native": {
                                        "action": "exclude"
                                }
                        }
                }
        }
}
```

##### `GET` response

```
{
        "bidder_profile": {
                "id": 2,
                "bidder_id": 129,
                "code": "test_1",
                "description": "Test Profile",
                "targeting": {
                        "ad_types": {
                                "native": {
                                        "action": "exclude"
                                },
                                "banner": {
                                        "action": "include"
                                },
                                "video": {
                                        "action": "include"
                                },
                                "audio": {
                                        "action": "include"
                                }
                        }
                },
                "last_activity": "2018-04-19 21:06:36",
                "created_on": "2018-04-19 21:06:36"
        }
}
```

> [!NOTE]
> The `GET` call will output the remaining ad types as included.

#### Include only the banner ad type

##### `PUT`/`POST` call

```
{
        "bidder_profile": {
                "code": "test_1",
                "description": "Test Profile",
                "targeting": {
                        "ad_types": {
                                "native": {
                                        "action": "exclude"
                                },
                                "banner": {
                                        "action": "include"
                                },
                                "audio": {
                                        "action": "exclude"
                                },
                                "video": {
                                        "action": "exclude"
                                }
                        }
                }
        }
}
```

##### `GET` response

```
{
        "bidder_profile": {
                "id": 2,
                "bidder_id": 129,
                "code": "test_1",
                "description": "Test Profile",
                "targeting": {
                        "ad_types": {
                                "native": {
                                        "action": "exclude"
                                },
                                "banner": {
                                        "action": "include"
                                },
                                "video": {
                                        "action": "exclude"
                                },
                                "audio": {
                                        "action": "exclude"
                                }
                        }
                }
        }
}
```

> [!NOTE]
> All the other ad types must be explicitly excluded in order to include only a single ad type.

#### Include only banner ad type with size 200x100

##### `PUT`/`POST` call

```
{
        "bidder_profile": {
                "id": 2,
                "code": "test_1",
                "description": "Test Profile",
                "targeting": {
                        "ad_types": {
                                "native": {
                                        "action": "exclude"
                                },
                                "banner": {
                                        "action": "include",
                                        "sizes": [{
                                                "width": 200,
                                                "height": 100
                                        }]
                                },
                                "audio": {
                                        "action": "exclude"
                                },
                                "video": {
                                        "action": "exclude"
                                }
                        }
                }
        }
}
```

##### `GET` response

```
{
        "bidder_profile": {
                "id": 2,
                "bidder_id": 129,
                "code": "test_1",
                "description": "Test Profile",
                "targeting": {
                        "ad_types": {
                                "native": {
                                        "action": "exclude"
                                },
                                "banner": {
                                        "action": "include",
                                        "sizes": [{
                                                "width": 200,
                                                "height": 100
                                        }]
                                },
                                "video": {
                                        "action": "exclude"
                                },
                                "audio": {
                                        "action": "exclude"
                                }
                        }
                }
        }
}
```

> [!NOTE]
> The sizes object must be included within the banner ad type. No other banner sizes will pass through this profile.

#### Include a video ad type with size 1x1

##### `PUT`/`POST` call

```
{
        "bidder_profile": {
                "id": 2,
                "code": "test_1",
                "description": "Test Profile",
                "targeting": {
                        "ad_types": {
                                "native": {
                                        "action": "exclude"
                                },
                                "banner": {
                                        "action": "include"
                                },
                                "audio": {
                                        "action": "exclude"
                                },
                                "video": {
                                        "action": "exclude",
                                        "sizes": [{
                                                "width": 1,
                                                "height": 1
                                        }]
                                }
                        }
                }
        }
}
```

##### `GET` response

N/A - Error

> [!NOTE]
> We do not support targeting 1x1 or 0x0 sizes for ad types.

#### Target the native ad type with size

##### `PUT`/`POST` call

```
{
        "bidder_profile": {
                "id": 2,
                "code": "test_1",
                "description": "Test Profile",
                "targeting": {
                        "ad_types": {
                                "native": {
                                        "action": "exclude",
                                        "sizes": [{
                                                "width": 100,
                                                "height": 100
                                        }]
                                },
                                "banner": {
                                        "action": "include"
                                },
                                "audio": {
                                        "action": "exclude"
                                },
                                "video": {
                                        "action": "exclude"
                                }
                        }
                }
        }
}
```

##### `GET` response

N/A - Error

> [!NOTE]
> Size targeting is not supported for audio and native at this time.

## Related topics

- [Exchange Service](./exchange-service.md)
- [Enhanced Bidder Profiles](./enhanced-bidder-profiles.md)
- [API Use Cases for Enhanced Bidder Profiles](./api-use-cases-for-enhanced-bidder-profiles.md)
- [Frequently Asked Questions (FAQ) for Enhanced Bidder Profiles](./frequently-asked-questions-faq-for-enhanced-bidder-profiles.md)
- [Changelog for Enhanced Bidder Profiles](./changelog-for-enhanced-bidder-profiles.md)
- [Bidder Profile Migration Guide](./bidder-profile-migration-guide.md)
