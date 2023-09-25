---
Title : User Mapping Visual and Walk-Through
Description : <a href="user-id-mapping-with-getuid-and-mapuid.md" class="xref">User
---


# User Mapping Visual and Walk-Through



<a href="user-id-mapping-with-getuid-and-mapuid.md" class="xref">User
ID Mapping</a> describes how to map your internal user IDs and
Xandr user IDs so that you can pass
Xandr your internal userdata that you will use
to buy impressions. Here we describe visually what's happening and walk
through the synching process.

In this example the advertiser Prostarr Sportswear stores the ID map on
their end. They use the getuid call to obtain the
Xandr ID via querystring parameter.

Example

Let's say Prostarr Sportswear has internal IDs on everyone who has
visited their retail site, and some of those IDs are tied to past
purchases. They want to sync user IDs with
Xandr, so that they can add this data to our
server-side cookie store and use it to target users. They put an
Xandr getUID pixel on their homepage. Let's
assume that Xandr has "seen" this user before
somewhere in their system and so has marked the user's browser cookie
with an Xandr user ID.

![User Map](media/usermap.png)


**Step 1.** When the page loads, the browser makes this call/request to
Xandr:
`https://ib.``adnxs``.com/getuid?https://prostarradserver.com/pixel?``adnxs``_uid=$UID`.
The request includes the `ib.``adnxs``.com`
browser cookie (which is passed in the header of the HTTP request). The
cookie includes the Xandr user ID.

**Step 2.** The Xandr Impression Bus passes back
the URL of Prostarr's ad server that was contained in the above
querystring. In addition, it appends the Xandr
user ID (from the user's Xandr browser cookie)
in place of $UID.
`https://prostarradserver.com/pixel?``adnxs``_uid=12345678.`

**Step 3.** The call in step 2 includes the
Xandr ID. In addition, Prostarr's browser cookie
data is passed with the call. Prostarr's ad server can now link the two
in their database.




