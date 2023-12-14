---
Title : Ad Server Settings
Description : You can set your Ad Quality settings to limit creatives served on your
ms.date: 10/28/2023
property based on the ad servers associated with the creative. In this
---


# Ad Server Settings



You can set your Ad Quality settings to limit creatives served on your
property based on the ad servers associated with the creative. In this
context an ad server is determined to be any technology vendor that is
in a creative's call chain. We associate a vendor to a creative when we
see a matching hostname between a vendor and calls in the creative's
call chain.

You can create a collection that either bans or allows one or more ad
servers.



<b>Warning:</b> Creating a collection of
trusted ad servers will significantly limit the number of advertisers
who can bid on your impressions. If you don't receive the amount of
impressions you expect, check these settings to ensure you're allowing
the appropriate ad servers to serve creatives on your property.



To create a collection of eligible or banned ad servers, first navigate
to the **Ad Quality** page for
either your publisher or your network. (See
<a href="explore-publisher-ad-quality.md" class="xref">Explore
Publisher Ad Quality</a> or
<a href="network-ad-quality-screen.md" class="xref">Network Ad Quality
Screen</a> for more on setting ad quality.) Modifying the ad server
settings at the network level will apply the settings to all publishers
on the network. If your network is owned and operated, you'll always
want to create these settings at the network level.

By default, all ad servers are eligible to serve creatives on your
property. You can change the default under Ad
Servers by clicking the button next to
Default ad server eligibility and
changing the default to Banned.



<b>Warning:</b> If you change the default
under Ad Servers to
Banned, no creatives will serve until
you've edited the Ad Servers and created a collection of eligible ad
servers.



To create a collection of ad servers that are either Eligible or Banned,
follow these steps:

Step 1. Go to the Ad Servers page.

From the **Network Ad Quality**
page or the **Publisher Ad
Quality** page, under Ad
Servers, click Edit next to
**Ad Servers**. This will open the **Ad
Servers** page.

Step 2. Set the default eligibility.

At the top of the page are two options,
Eligible and
Banned.
Eligible is selected by default. (If
you changed the default to Banned on
the Ad Quality screen,
Banned will be selected here.) Making
all ad servers eligible by default allows you to create of set of
specific ad servers that will be banned. Click the
Banned option if you want to ban all
ad servers by default, then create a set of ad servers that are
eligible.

Step 3. Create a list of banned or trusted ad servers.

On the left side of the screen is a list of ad servers with a button
next to each one.

- If Eligible is selected as the
  default eligibility, each button will show the **Banned** symbol.
  Click the button next to each ad server that you want to ban from
  serving creatives to your network or publisher. This will move the ad
  server to the set of **Banned Ad Servers** on the right.
- If **Banned** is selected as the default eligibility, each button will
  show the **Eligible** symbol. Click the button next to each ad server
  that you want to trust to serve creatives to your network or
  publisher. This will move the ad server to the set of **Eligible Ad
  Servers** on the right.

It is possible to create two collections of ad servers, a collection of
trusted ad servers and a collection of banned ad servers. However, this
isn't necessary because the default will still apply to all ad servers
that have not been added to a collection.

Step 4. Save your ad server settings.

Click Save to save your changes.




