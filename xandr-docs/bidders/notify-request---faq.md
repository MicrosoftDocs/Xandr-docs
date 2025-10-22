---
title: Notify Request - FAQ
description: In this article, explore answers to frequently asked questions about notify request, their data center, and errors.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Notify request - FAQ

## Data center

### Sometimes, the notify request comes from a different data center than the original bid request. Why does that happen?

This behavior is expected. The reason this would happen is that impressions are load balanced to a particular data center based on the location of the user. There are certain geographical areas which have dual coverage with our data centers. Depending on the type of auction/ad call that the impression comes through, the notify is actually a separate process that is disconnected from the auction itself. This happens in situations where the user is served a special "accept" URL that tells their browser to fetch the ad content from us separately from the ad call with initiated the impression. This final "accept" URL can potentially be routed to a different data center than the original impression, resulting in the behavior you are seeing and describing.

## Missing notifies

### I am seeing creatives delivered with macros populated but I have not received a corresponding "won" notify request. What could cause this?

There are several reasons that a notify request would not be sent or delivered. Internally, we maintain a metric for "failed" notifies, i.e., those notifies which could not be sent due to bandwidth issues. In this case, you will likely also be experiencing throttling/aborting on bid request. In this case, you should see some amount of notify requests which contain the error message "Request throttled or aborted". Another potential cause for the non-delivery of "won" notify requests is that the notify is delivered once we have received some kind of confirmation that the impression was actually won. For impressions where Xandr is the final decision-maker, we send the notify at the end of the auction once we have determined the winner. For auctions where Xandr is not the final decision-maker (e.g., server-side impressions from supply partners like Google Ad Manager, Rubicon, Pubmatic and AdMeld), we send the notification of a "won" impression when the deciding party has informed us that we have won. In some cases, it may take an extraordinarily long time for us to receive the callback (we refer to it as an "accept bid callback"). When the accept bid callback is received, we check how long it has been since the auction. For several reasons (discussed below), if the elapsed time is more than 60 seconds, we consider the callback to have timed out. When we receive a timed out callback, we do not treat it the same as a normal callback. Most notably, we do not log the win and we do not send out a notify request for that auction. However, we **do** deliver the creative the same way. That means you may see a creative delivered without any corresponding notify request. Our reasons for treating "timed out" accept bid callbacks differently are:

- It is very common for supply partners to emit send Xandr duplicate callbacks for the same impression. This results in multiple duplicate notifications being sent out to bidders, requiring deduplication in the data pipeline. The more we can minimize duplicates, the more efficiently the platform can operate.
- Setting the timeout threshold at 60 seconds allows us to minimize the look-back period when aggregating our log data for reporting on delivered impressions. For any impressions where Xandr is not the final decision-maker, we maintain two logs: one for our auction of the
impression and one for the accept bid callback. This requires us to join those two logs to determine which impressions were delivered. By minimizing the look-back period, we can ensure that hourly reporting experiences minimal delays. The number of timed out callbacks should be minimal, so this does not contribute significantly to any discrepancies.
- Very often, a timed out callback is a result of a very slow internet connection between the user and the ad server. If this is the case, there is a good chance that the user is in the process of navigating away from the page and may not see the ad.

## Errors

### Metrics allows me to see my error rate, but I want to know what kinds of errors we are generating. Is this possible?

If you are getting `notify_requests`, by default you will be sent errors for timeouts and throttled or aborted requests. All other types of errors are included in the `"error"` field of lost notifications. So to have the best understanding of all errors, it's recommended that you have the `"notify_lost"` field of your bidder object set to true. If this is something you want to enable, ask your technical support representative.

## Related topics

- [Notify Request](notify-request.md)
- [Integrate a Bidder](integrate-a-bidder.md)
