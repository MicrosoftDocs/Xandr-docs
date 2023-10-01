---
Title : Troubleshooting Invalid Users
Description : To minimize the incidence of invalid users, drop the user sync pixel
more frequently and expire old users out of your database after a period
of inactivity.
---


# Troubleshooting Invalid Users





To minimize the incidence of invalid users, drop the user sync pixel
more frequently and expire old users out of your database after a period
of inactivity.

<div id="buy-side-service-template__note_ygm_jqd_vwb"


Note: This recommendation only applies
to display. For mobile, since user syncing is not a possibility, device
IDs will be valid if we have previously seen them coming in through
mobile supply requests.)





There are several reasons a user ID can be invalid:

1.  If there is a typo in the UID, the user is invalid.
2.  Xandr expires UIDs on a rolling basis such that the users who
    haven't been seen for the longest period of time are removed from
    our database to make room for new users. If you upload UIDs that are
    very old, chances are you will have a high percentage of invalid
    users in your file. It's a best practice to keep your cookie mapping
    fresh and match rate high by collecting UIDs as frequently as
    possible.
3.  If a client syncs a user Xandr has never seen before, Xandr (via
    getUID) performs a bounce to the page, sets a UID, and returns that
    UID back to the client. However, Xandr does not yet store the user
    ID server side until we see the user a *second time*. Thus, for all
    the users we've seen only once from a getUID call, when their UIDs
    are pushed to us server side via the Batch Segment upload, you will
    see invalid user ID errors. These IDs exist in the user's cookie,
    but not in our server-side data store.




