---
title: Synchronize Your User IDs
description: This page covers steps for Storing the mapping with Xandr.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Synchronize your user IDs

This page provides an introduction to user ID synchronization and details about mapping between Xandr user IDs and the user IDs understood by your bidder.

The integration between your bidder and Xandr is a server-side integration. This means that:

- Communication occurs strictly between Xandr's impression bus and your bidder instances
- During the bidding process, you will not have direct access to your cookies in the user's browser

If we receive the impression through a server-side integration from  supply partner, we will not have access to our cookie on the user's browser. For this reason we perform user synchronization with our supply partners. This results in a mapping between the Xandr user ID and the supply partner ID. The mapping can be stored either by Xandr, in our server-side cookie store, or by the supply partner.

A similar solution is available to bidders and data providers. In order to perform the syncing, we must first identify where the mapping is to be stored.

> [!WARNING]
> Your bidder must be set to active Your bidder, or data provider must be set to **active** in order for this synchronization to occur.

## Storing the mapping with Xandr

> [!NOTE]
> From April 22, 2019, Xandr no longer supports the `userdata_javascript` and `setuid_function` fields. Bidders can make the setuid call directly.

To store the mapping with Xandr,

1. Add the following function to your bidder's "userdata_javascript" field on the [Bidder Service](bidder-service.md):

   ``` 
      function setuid(code){ ud.uid = code; }
   ```

1. Next, set the "setuid_function" field on the [Bidder Service](bidder-service.md) as follows:

    ``` 
    setuid
    ```

1. Now, you can use the following URL within a pixel call to push your user ID into the user's cookie and the Xandr server-side cookie store:

    ``` 
    https://ib.adnxs.com/setuid?entity=[BIDDER_ID]&code=[USER_ID]
    
    ```

1. Replace \[BIDDER_ID\] with your bidder's ID (available from the Bidder Service) and \[USER_ID\] with the user ID you have stored for that user.

   In case TCF signals are available on the page, "gdpr" and `"gdpr_consent"`, `GET` parameters must be included at the end of the /setuid url:  

    ``` 
    https://ib.adnxs.com/setuid?entity=[BIDDER_ID]&code=[UID]&gdpr=[GDPR_APPLIES]&gdpr_consent=[GDPR_CONSENT_STRING]
    
    ```

   > [!WARNING]
   > As of April 22, 2019, Xandr no longer supports the `"userdata_json"` field in the bid request. You can receive your unique user id through the "`buyeruid"` field.

   You will receive your user ID as part of the bid request's `"userdata_json"` field, as in the example below:

  ``` 
{
    "bid_request": {
        ...
        "bid_info": {
            ...,
            "userdata_json": "{\"global_freq\":3,\"last_seen\":1237220391,\"uid\":\"HeVQkH6inotalk0Livh8Vw\"}",
            ...
        },
        ...
    }
}
```

You will receive your user ID as part of the bid request's "buyeruid" field, as in the example below:

``` 
{
    "request": {
        ...
        "user": {
            ...,
            "buyeruid": "HeVQkH6inotalk0Livh8Vw",
            ...
        },
        ...
    }
}
```

**setUID example**

```
https://ib.adnxs.com/setuid?entity=123&code=HeVQkH6inotalk0Livh8Vw&gdpr=1&gdpr_consent=CPaPwEAPaPwEAACAKAFRBWCgAP_AAH_AAAqIHttf_X__b3_j-_59__t0eY1f9_7_v-0zjhfdt

```

## Bidder/Data provider stored mapping

To extract the Xandr user ID for any given user, you will direct the user to our getUID service through a pixel call. The impression bus will redirect the user to the URL specified in the getUID call, replacing a user ID macro with the ID we have stored for that user. This process gives us access to our cookie in that user's browser and allows us to read the ID.

The format of the getUID service is:

``` 
https://ib.adnxs.com/getuid?[REDIRECT_URL]

```

The redirect must contain the user ID macro, in the format $UID, with the ID we have for that user. The example call below will result in the following:

1. Direct the user to [https://ib.adnxs.com/getuid?https://ad.adserver.com/pixel?adnxs_uid=$UID](https://www.epsilon.com/us?redirect=cnvr-home)
1. Replace the $UID macro with a9f4072b-ec2d-42cb-8930-e3388a7d47c2
1. Redirect the user to [https://ad.adserver.com/pixel?adnxs_uid=a9f4072b-ec2d-42cb-8930-e3388a7d47c2](https://www.epsilon.com/us?redirect=cnvr-home)

In case TCF signals are available on the page, "gdpr" and "gdpr_consent", GET parameters must be included at the end of the /getuid url:

``` 
https://ib.adnxs.com/getuid?https://ad.adserver.com/pixel?adnxs_uid=$UID&gdpr=[GDPR_APPLIES]&gdpr_consent=[GDPR_CONSENT_STRING]

```

**getUID example**

``` 
https://ib.adnxs.com/getuid?https://ad.adserver.com/pixel?adnxs_uid=$UID&gdpr=1&gdpr_consent=CPaPwEAPaPwEAACAKAFRBWCgAP_AAH_AAAqIHttf_X__b3_j-_59__t0eY1f9_7_v-0zjhfdt

```

Next step: [Receiving a Notify Request](receive-a-notify-request.md)

## Privacy consideration  

> [!NOTE]
> For both endpoints, if TCF parameters are passed in the redirect URL, Xandr will utilize these parameters to determine if a cookie sync can be performed. If the signals received are interpreted as having insufficient legal basis, Xandr will be unable to process the cookie sync request, and it will return the following error message: "Request failed due to privacy signals."
Additionally, if TCF signals cannot be provided when calling our URLs, partners must append the **consent** parameter to the URL. The **consent** parameter accepts binary values: **1** if the user has given consent, and **0** if consent has been denied. This parameter must be included to perform user syncs in certain geographical areas.

### Examples of consent parameter usage

Please see the examples below for how to use the **consent** parameter in URLs:

#### Example of a `getuid` call with user consent

```
https://ib.adnxs.com/getuid?https://ad.adserver.com/pixel?adnxs_uid=$UID&consent=1

```

#### Example of a `getuid` call without user consent

```
https://ib.adnxs.com/getuid?https://ad.adserver.com/pixel?adnxs_uid=$UID&consent=0

```

#### Example of a `setuid` call with user consent

```
https://ib.adnxs.com/setuid?entity=[BIDDER_ID]&code=[UID]&consent=1

```

#### Example of a `setuid` call  without user consent

```
https://ib.adnxs.com/setuid?entity=[BIDDER_ID]&code=[UID]&consent=0

```
