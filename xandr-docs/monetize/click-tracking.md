---
title: Microsoft Monetize - Click Tracking
description: Explore click tracking's key role in optimizing Microsoft Advertising for CPC and CPA goals, bidding, and gauging campaign success.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Click tracking

Click tracking serves many useful purposes within the ad serving industry as a whole. For Microsoft Advertising, click tracking is necessary for optimizing to CPC and CPA goals, for bidding CPC and CPA, and for measuring a campaign's success.

In order for Microsoft Advertising to track a click to the corresponding impression, a click tracker needs to load when a user clicks on a creative. When the Microsoft Advertising click tracker is loaded:

1. A click is recorded on the Microsoft Advertising server.
1. There is a redirect to the webpage that follows the click tracker.

    For example:

    ```
    https://nym1-ib.adnxs.com/click2?
    ```

    In this example, the Microsoft Advertising click tracker is followed by the Microsoft Advertising homepage. When the link is loaded, a click is recorded on Microsoft Advertising, and then there is a redirect to the Microsoft Advertising homepage.

## Tracking clicks on hosted creatives

Microsoft Advertising will configure the click tracking for hosted creatives such as JPGs, GIFs, and PNGs since they are wrapped in our creative templates. Our templates are set up in such a way that a dynamically-generated click tracker is correctly populated in the creative content. For more information, see [Creative Templates](creative-templates.md).

All you have to do is enter the landing page URL in the **Landing Page** field and select the **Enable Click Tracking** checkbox if you're using Console, and a click URL with encoded information about the creative will be automatically appended to the creative. When a user clicks the URL, the user's browser will first request the URL from adnxs.com. The encoded information in the URL will be recorded by the server. The user's browser will be redirected to the landing page configured for the creative.

## Tracking third-party clicks on URLs for hosted creatives

Most third-party click tracking URLs will automatically redirect to the landing page, so all you have to do is enter the click tracking URL directly in the **Landing Page** field. After clicking the creative, the tracker will load and redirect to the landing page.

## Tracking clicks on third-party tags

A simple third-party tag is made up of two parts:

- An `<a>` tag, or anchor tag, which wraps around the image.
- An `<image>` tag, which loads an image.

For example:

```
<a href="https://www.cnn.com" target="_blank"><img src="media/Ad-MediumRectangle-300x250.png" width="300" height="250"></a>
```

The anchor tag contains a "href" or hyperlink reference, which in this case is cnn.com. When the creative is clicked, the browser will redirect to cnn.com. The landing page will load as specified by the `target` parameter, which in this case is "\_blank", to indicate that the page should load in a new window or tab. In order for a third-party tag to track clicks, the `${CLICK_URL_ENC}` macro must be implemented. When an impression is delivered, the macro will be replaced with a dynamically-generated click tracker. The click tracker loads only when the creative is clicked. To achieve this, the macro should be placed right before the creative's landing page as shown here:

```
<a href="${CLICK_URL_ENC}https://www.cnn.com" target="_blank"><img src="media/Ad-MediumRectangle-300x250.png" width="300" height="250"></a>
```

When an image is clicked, the "href" page loads. A click is tracked on Microsoft Advertising and followed by a redirect to https://www.cnn.com. For example:

```
<a href="https://nym1-ib.adnxs.com/click2?AAAAAAAAAAAAAAAAAAAA./clickenc=https://www.cnn.com" target="_blank"><img src="https://upload.wikimedia.org/wikipedia/commons/2/24/Ad-MediumRectangle-300x250.jpg" width="300" height="250"></a>
```

After the user is redirected to the href, such as https://www.cnn.com, the following takes place:

1. The Microsoft Advertising impression bus generates a click tracker by populating the `${CLICK_URL_ENC}` macro.
1. The click tracker is passed to the third-party ad server in the tag.
1. The third-party ad server will take the click tracker and insert it correctly into the creative so that it will load when the creative is clicked.

For a URL-HTML, URL-JS, raw-HTML, or raw-JS creative, you will need to include one of the following Microsoft Advertising macros in the appropriate place in your URL/tag:

| Macro | Description |
|--|--|
| `${CLICK_URL}` | The click tracking url. |
| `${CLICK_URL_ENC}` | The encoded click tracking url (only necessary for some third-party ad servers) |

Although an encoded version is available for certain ad servers, you'll most likely want to include the `${CLICK_URL}` macro. For example:

```
https://ad.doubleclick.net/adi/N5364.Ivillage.com/B2965815.5;sz=728x90;click=${CLICK_URL};ord=${CACHEBUSTER}?
```

Here "click" is the DoubleClick variable for accepting external click URLs. When the full URL string above is passed from Microsoft Advertising to the user's browser, the impression bus 
will replace `${CLICK_URL}` with the actual click Microsoft Advertising URL, which is easily identified by the large number of uppercase A's present in the string. The Microsoft Advertising click URL will look something like this:

```
https://nym1-ib.adnxs.com/click2?AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA__________-No5xOAAAAAAEAAAAAAAAAAAAAAAAAAABd8gsAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAQAAAAAAAAEAcAsHNwAAAAA./clickenc=
```

Therefore, the expanded DoubleClick content will look as follows:

```
https://ad.doubleclick.net/adi/N5364.Ivillage.com/B2965815.5;sz=728x90;click=https://nym1-ib.adnxs.com/click2?AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA__________-No5xOAAAAAAEAAAAAAAAAAAAAAAAAAABd8gsAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAQAAAAAAAAEAcAsHNwAAAAA./clickenc=;ord=1330398521?
```

The creative will first direct the browser to the impression bus where the click will be recorded, and then to the landing page (the landing page is specified after our `clickenc=` variable). In this example, DoubleClick will use our click URL and `${CACHEBUSTER}` macro when delivering the final creative content to the user's page. The `${CACHEBUSTER}` macro ensures that a fresh call is made to the ad server every time the tag is called, so you are accurately counting impressions. If you don't add the `${CACHEBUSTER}` macro to the tag, you may see inaccurate impression totals. For more information, see [Table 2](supported-creative-macros.md).

## Examples of failures

| Failure | Description |
|--|--|
| Failed to click on creative that appears blank | Creative failed to render during the test due to geo fencing or third party protection. |
| Failed to click on a creative | Creative did not respond to clicking. For example, clicking only a specific button. |
| Creative loads landing page in the same browser window | Creative interfers with the browser navigation. |
| Click tracker did not fire | Creative responded to clicking normally but did not load the clicktracking URL. |

In order to properly track clicks, all hosted HTML5 creatives must refer the click tag parameter in the URL of the creative when it is served. Also when the creative is clicked, it should open specific the landing page defined in your setup.

Creative designers can either use their own code to ensure that the reference is present, or use helper code provided in the Microsoft Advertising HTML5 library.

## Related topics

- [Click Track Test](click-track-test.md)
- [Test Click Tracking Manually](test-click-tracking-manually.md)
