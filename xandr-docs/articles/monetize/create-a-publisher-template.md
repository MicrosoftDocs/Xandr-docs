---
Title : Create a Publisher Template
Description : A Publisher Template is a collection of ad quality settings created by a
network administrator. Publisher Templates ease publisher creation and
---


# Create a Publisher Template



A Publisher Template is a collection of ad quality settings created by a
network administrator. Publisher Templates ease publisher creation and
set-up by allowing a network administrator to define common ad quality
settings for a number of publishers at once. When a template is edited,
all publishers using that template will be updated with those settings.
Use a Publisher Template if you want to maintain a group of publishers'
ad quality settings together. Note that associating a publisher with a
Publisher Template is optional.

For more information on the relationship between Publisher Templates and
Network Profiles, see
<a href="working-with-publisher-ad-quality.html" class="xref">Working
with Ad Quality</a>.



## Step 1. Create a new Publisher Template

To create a new Publisher Template, navigate to the
Network tab's
Ad Quality section and click the
Create New Template button.



Important: You can edit an existing
Publisher Template by clicking on its name, then clicking the
Full Edit button.



The Create New Template dialog will
appear. This is where you'll enter the template's name and add any notes
you'd like to include. After saving, you'll return to the
Network Ad Quality screen, where
you'll edit each of the available options as described in Step 2.





## Step 2. Determine which creatives are eligible to serve on your inventory



Note: The Ad
Servers option below is in beta and not widely available to all
customers. We plan to release this feature to all users at a future
date.



You can determine which creatives will be eligible to serve on your
inventory based on one or more of the following attributes:

- Bidders
- Buyers
- Categories
- Technical Attributes
- Brands
- Languages
- Ad Servers

**Bidders**

You can manage bidders and individual bidder seats that serve on your
inventory by defining trust level settings here. Choose from

<table id="ID-00000208__table-be54650f-1ada-4f0a-8898-69fb53e85ea3"
class="table">
<thead class="thead">
<tr class="header row">
<th
id="ID-00000208__table-be54650f-1ada-4f0a-8898-69fb53e85ea3__entry__1"
class="entry">Trust Level</th>
<th
id="ID-00000208__table-be54650f-1ada-4f0a-8898-69fb53e85ea3__entry__2"
class="entry">Description</th>
</tr>
</thead>
<tbody class="tbody">
<tr class="odd row">
<td class="entry"
headers="ID-00000208__table-be54650f-1ada-4f0a-8898-69fb53e85ea3__entry__1">Standard</td>
<td class="entry"
headers="ID-00000208__table-be54650f-1ada-4f0a-8898-69fb53e85ea3__entry__2">Apply
ad quality standards, require platform audit.</td>
</tr>
<tr class="even row">
<td class="entry"
headers="ID-00000208__table-be54650f-1ada-4f0a-8898-69fb53e85ea3__entry__1">Medium</td>
<td class="entry"
headers="ID-00000208__table-be54650f-1ada-4f0a-8898-69fb53e85ea3__entry__2">Apply
ad quality standards, trust buyer self-classification.</td>
</tr>
<tr class="odd row">
<td class="entry"
headers="ID-00000208__table-be54650f-1ada-4f0a-8898-69fb53e85ea3__entry__1">High</td>
<td class="entry"
headers="ID-00000208__table-be54650f-1ada-4f0a-8898-69fb53e85ea3__entry__2">Bypass
ad quality standards, require platform audit.</td>
</tr>
<tr class="even row">
<td class="entry"
headers="ID-00000208__table-be54650f-1ada-4f0a-8898-69fb53e85ea3__entry__1">Maximum</td>
<td class="entry"
headers="ID-00000208__table-be54650f-1ada-4f0a-8898-69fb53e85ea3__entry__2">Bypass
ad quality standards, do not require platform audit.</td>
</tr>
<tr class="odd row">
<td class="entry"
headers="ID-00000208__table-be54650f-1ada-4f0a-8898-69fb53e85ea3__entry__1">Banned</td>
<td class="entry"
headers="ID-00000208__table-be54650f-1ada-4f0a-8898-69fb53e85ea3__entry__2">Ban
all creatives from this buyer.</td>
</tr>
</tbody>
</table>

<div id="ID-00000208__p-bcdcaad3-9e18-427b-9fd6-6f995c6f01a5" >

The bidders and their seats are mapped to the existing buyer IDs, and
all trust settings are inherited by both. Updating trust settings to
either one of the sections (Buyers or Bidders) will update trust
settings for the same bidder or seat in both sections.

<div id="ID-00000208__note-a37c50d0-9ebf-4569-a828-65e3cc8a11fa"


Note: Updating the trust level for
Bidders will apply the same trust level to all Seats. However, Bidder
trust can be overridden by updating Seat-level trust settings from
Use Bidder to another trust level.





The default trust setting for Bidders is inherited from the Buyers
section and any adjustments to the trust settings should be made in the
Buyer’s section. To know more about Buyer Seat IDs, see: <a
href="https://docs.xandr.com/bundle/monetize_monetize-standard/page/topics/understanding-buyer-seat-ids.html"
class="xref" target="_blank">Understanding Buyer Seat IDs</a>

**Buyers**

In the Buyers section, click the
Edit button. You'll be presented with
a dialog where you can edit the trust level associated with individual
buying members. The buyer trust levels and their descriptions are as
follows:

<table class="table">
<thead class="thead">
<tr class="header row">
<th id="ID-00000208__entry__13" class="entry">Trust Level</th>
<th id="ID-00000208__entry__14" class="entry">Description</th>
</tr>
</thead>
<tbody class="tbody">
<tr class="odd row">
<td class="entry" headers="ID-00000208__entry__13">Standard</td>
<td class="entry" headers="ID-00000208__entry__14">Apply ad quality
standards, require platform audit.</td>
</tr>
<tr class="even row">
<td class="entry" headers="ID-00000208__entry__13">Medium</td>
<td class="entry" headers="ID-00000208__entry__14">Apply ad quality
standards, trust buyer self-classification.</td>
</tr>
<tr class="odd row">
<td class="entry" headers="ID-00000208__entry__13">High</td>
<td class="entry" headers="ID-00000208__entry__14">Bypass ad quality
standards, require platform audit.</td>
</tr>
<tr class="even row">
<td class="entry" headers="ID-00000208__entry__13">Maximum</td>
<td class="entry" headers="ID-00000208__entry__14">Bypass ad quality
standards, do not require platform audit.</td>
</tr>
<tr class="odd row">
<td class="entry" headers="ID-00000208__entry__13">Banned</td>
<td class="entry" headers="ID-00000208__entry__14">Ban all creatives
from this buyer.</td>
</tr>
</tbody>
</table>

**Categories**

Depending upon the category the creative falls into, you may choose to
mark it as:

- Eligible: The creative will serve.
- Banned: The creative will not serve.
- Default: Reuse the default settings
  (i.e., mark as **Eligible**).

**Technical Attributes**

You may allow or disallow certain creatives based upon technical
attributes such as whether the creative is an expandable, or whether it
plays audio. Choose from:

- Eligible: The creative will serve.
- Banned: The creative will not serve.
- Default: Reuse the default settings
  (i.e., mark as **Eligible**).

**Brands**

There may be creatives associated with certain brands that you would
prefer don't serve on your inventory. You can define those settings
here. Choose from:

- Eligible: The creative will serve.
- Banned: The creative will not serve.
- Default: Reuse the default settings
  (i.e., mark as **Eligible**).

You can enter a list of brands with the Bulk
Search option.

You can also filter and show only those brands that are new in the last
7 days:

**Languages**

Your inventory may interest users who speak certain languages; you can
choose to allow creatives using those languages here. You may also
exclude creatives using certain languages. Choose from:

- Eligible: The creative will serve.
- Banned: The creative will not serve.
- Default: Reuse the default settings
  (i.e., mark as **Eligible**).

**Ad Servers**



Note: This option is not available to
all customers at this time.



You can choose to serve only those creatives that are hosted on a
specific set of ad server domains. All ad servers are eligible by
default. If you want to allow or ban creatives based on the ad server
called by that creative, click Edit
under Ad Servers . This will take you
to the Ad Server screen. See
<a href="ad-server-settings.html" class="xref">Ad Server Settings</a>
for information on using the Ad
Server screen to create collections of eligible or banned ad
servers.





## Step 3. Apply frequency caps to attributes

You can apply per-user frequency caps to particular creatives based on
one or both of the following attributes:

- **Sensitive Categories**: The creative may belong to a sensitive
  category such as "Dating" or "Politics".
- **Technical Attributes**: The creative may have undesirable technical
  attributes, such as whether it plays audio.

By default frequency caps are turned off, in which case you'll see
No limit per user in the upper right
corner of the section. To change this, click
No limit per user. (If frequency caps
have already been set, this area will show the frequency, such as **2
imps per day**, rather than **No limit per user**.) This will expand an
area where you can set the frequency caps for the attributes and
categories to which they're applied.

For more information on frequency caps, see
<a href="frequency-and-recency-caps.html" class="xref"
title="From the Audience &amp; Location Targeting section, you can apply frequency and recency caps to your line item to prevent overexposure by limiting how many (frequency) and how often (recency) creatives are shown to a user. You can use the Creative Frequency and Recency Report to view how often and how frequently users are viewing a specific advertiser&#39;s creatives.">Frequency
and Recency Caps</a>.






