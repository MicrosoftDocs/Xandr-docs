---
title : Microsoft Invest - Asynchronous Usersync Pixels
description : User syncing happens after a publisher's page has finished loading. This allows to fire more usersync pixels per ad call without disrupting the user experience of visitors to the publisher's site. This will increase spend platform-wide as usersyncing clients will have an increased match rate, allowing them to bid higher CPMs using their proprietary data on more users.
---


# Asynchronous usersync pixels in Microsoft Invest

We've made a technical upgrade to the way we perform
[User ID Syncing with External Partners](user-id-syncing-with-external-partners.md) so that user syncing happens after
a publisher's page has completely finished loading. This allows us to
fire more usersync pixels per ad call without disrupting the user
experience of visitors to the publisher's site. This change will benefit
publishers by increasing spend platform-wide as usersyncing clients will
have an increased match rate, allowing them to bid higher CPMs using
their proprietary data on more users.

## Effects on Ghostery and related tools

Due to details of the technical implementation (described below), tools
such as [ghostery](http://www.ghostery.com) may show more pixels firing on publishers'
pages than before. Users who are fully synced should not see any
usersync pixels loading; once they're fully synced, the Ghostery calls
will stop.

To see how this works, clear your cookies and refresh the page several
times. You will see a lot of pixels fire on the first two or three page
loads (until you are fully synced). On subsequent page loads you
shouldn't see any pixels loading.

The important takeaways are:

1.  While it may appear that there are more pixels on a publisher's
    site, the usersyncing process will only begin after the entire web
    page has finished loading.
1.  The queue of available usersync pixels will run out quickly (and
    pixels will stop loading).
1.  There should be no increase in publisher page load times - in fact,
    with this change page load times should slightly improve.

## How it Works

We attach a bit of JavaScript code to the publisher's page that will
only run after the rest of the page's content has been loaded by the
browser. Once a web page (or iFrame) has finished loading, this code
calls our server asking for a usersync pixel. When that pixel returns
and is loaded, the Javascript calls back to
Xandr again, asking for another usersync pixel.
For any given tag this loop repeats a maximum of ten times, and
usersyncing will stop once there are no more usersync pixels available
or the queue of available pixels is exhausted. After the loop finishes,
the user should be fully synced across Xandr and
all of our external partners.

For those interested in more technical details, we are appending a
JavaScript callback to the browser's `window.onload` event. For more
information about how the `onload` event works, see [Mozilla's DOM Reference](https://developer.mozilla.org/en-US/docs/Web/API/GlobalEventHandlers.onload?redirectlocale=en-US&amp;redirectslug=Web%2FAPI%2Fwindow.onload) 

The steps shown below provide a simplified description of this process:

1. Parse the HTML page.
1. Build a DOM Tree (Browser's internal representation of the page).
1. `window.onload` event occurs (DOM has finished loading all page
    elements)
1. Our JavaScript code asks Xandr for usersync
    pixels to load.
1. Xandr returns the usersync pixel to the
    page.
1. The usersync pixel loads and the user ID is now synced.
1. Steps 4-6 are repeated until the user is fully synced or 10 pixels load, whatever comes sooner.

   For more detailed information about how browsers load web pages, see [How Browsers Work](http://www.html5rocks.com/en/tutorials/internals/howbrowserswork/).

## European Ad Inventory and Providing Notice, Transparency and Choice

In order for our clients to meet their transparency, notice and
choice/consent requirements under the GDPR and the existing ePrivacy
Directive, Xandr
supports [the IAB Europe Transparency &amp; Consent Framework](http://advertisingconsent.eu/) (the "Framework").
This is a reference for publishers using the macros to surface notice,
transparency and choice to end users located in the EEA and signal
approved vendors and, where necessary, pass consent, to
Xandr and demand sources and their vendors
through the Xandr platform. This resource should
not be construed as legal advice and Xandr makes
no guarantees about compliance with any law or regulation. Please note
that because every company and its collection, use, and storage of
personal data is different, you should also seek independent legal
advice relating to obligations under European regulations, including the
GDPR and the existing ePrivacy Directive. Only a lawyer can provide you
with legal advice specifically tailored to your situation. Nothing in
this guide is intended to provide you with, or should be used as a
substitute for, legal advice tailored to your business. **Note our**
 [Service Policies](https://wiki.xandr.com/display/policies/Home) (login required) **(for Buying,
Selling, and Data Providers) include privacy-specific obligations of
which you should be aware.**

*`${GDPR_APPLIES}`*

Designates whether GDPR regulations are applied. Specifically, it
indicates whether the user is located in a GDPR impacted country, or if
we have a GDPR-required signal passed with the request. 1 if yes and 0
if no.

A "0" may be received from an EEA country. It is the publisher's choice
to signal in this manner.

*`${GDPR_CONSENT_STRING}`*

This is the IAB GDPR consent string. If the GDPR applies, then this will
have a list of user approved vendors based on the [IAB GDPR Transparency and Consent
Framework](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework).

## Related topics

- [User ID Syncing with External Partners](user-id-syncing-with-external-partners.md)
- [User ID Mapping with getUID and mapUID](user-id-mapping-with-getuid-and-mapuid.md)
