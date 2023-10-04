---
Title : Create a Bias Rule
Description : Note: This feature is not available by
default. If you are interested in gaining access or discussing potential
---


# Create a Bias Rule





Note: This feature is not available by
default. If you are interested in gaining access or discussing potential
use cases that may apply to your business, reach out to your
Xandr representative.



You can create bias rules to make bids appear higher or lower than they
actually are, thereby influencing the outcome of an auction.

Create a base rule to affect bids from a specific buyer or buyer group
on all of the publisher's inventory.

Create a conditional rule to affect bids from a single buyer or buyer
group on specific impressions.

You can define a per-buyer bias by impression frequency, geography,
segment, specific placement, category, or placement size. Biases affect
the way that the auction operates, but not the amount the winner pays.

For more information on biases and how they work, see
<a href="working-with-yield-management.html" class="xref">Working with
Yield Management</a>.

Create a Base Bias Rule

Create a base rule to affect specific buyer's or buyer group's bids on
all of the publisher's inventory.

Getting There

**Publisher-only clients:** Select
Partners
\>  Yield Management  \>
 Floor rules in the menu bar,
and then select a publisher if you are prompted.

**All other clients:** Select
Publishers
 \>  Floor Rules in the
menu bar, and then select a publisher if you are prompted.

Step 1. Get started

Select a publisher when you are prompted. This opens the **Bias Rule
Manager**.

Step 2. Open the Create New Base Rule dialog

Click Create New
 \>  Base Rule, or click
on the **Create a base rule** link within the
Bias section of the screen to open the
**Create New Base Rule** dialog.



Note: You can only create one base
rule. If a base rule exists, you will not be able to create a new base
rule. Instead, you can edit or delete the existing rule.



Step 3. Enter base rule details

Enter the basic details for the base rule.

- **Name** - Enter a name for your rule. It is recommended to select a
  name that aligns with your business strategy for ease of use.
- **Priority** - The base rule is automatically set to Priority 1
  (lowest). This means any existing conditional rules will take
  precedence over the base rule.
- **Description** - Enter a rule description for reference.
- **Additional Options: Code** - If you click
  Additional Options (Advanced) you
  will have the option of entering a code. Codes may be helpful for
  networks with distinct internal names/IDs, so that the names/IDs can
  be associated in Monetize and then extracted
  for reporting purposes via our API.

Step 4. Save the base bias rule

Once you have entered the rule details, click
Save. The rule will then display under
Bias Rule on the
Bias Rule Manager screen. The base
rule will be selected and the **Buyers** and
Buyer Groups tables will display in
the Bias Settings section.

Step 5. Define bias amounts

You can define bias values for specific buyers and for specific buyer
groups.

- Define bias amounts for specific buyers
- Define bias amounts for buyer groups

Define bias amounts for specific buyers

Click Edit in the
Buyers table to display the **Buyer
Bias Settings** dialog. Use the name and bias type filters to locate the
desired buyer, and then click edit
near the buyer.



Important: To streamline the process of
editing multiple buyer's bias settings, you can display the edit tools
for all buyers within the list by clicking **Mass edit**.



Select a bias type from the dropdown in the
**Bias Type** column, and then
enter a value in the field in the **Bias
Value** column. You can enter a positive (preference) or negative
(deterrent) value for either of the bias types.

- **Percentage** - The buyer's bids will be modified by a certain
  percent.
- **CPM** - The buyer's CPM bid will be modified by a specific amount.

When you have entered the desired bias amount for the buyer, click the
Save button within the row.

When you have entered all of the needed bias amounts per buyer, click
Close to finish editing the base rule.

Define bias amounts for buyer groups

Click Edit in the
Buyer Groups table to display the
**Buyer Group Bias Settings** dialog. Use the name and bias type filters
to locate the desired buyer group, and then click
edit near the buyer group. You can
create buyer groups under
Network 
\>  Partners  \>
 Demand Partners  \>
 Add New Group.



Important:

To streamline the process of editing multiple buyer group's bias
settings, you can display the edit tools for all buyer groups within the
list by clicking Mass edit.



Select a bias type from the dropdown in the
**Bias Type** column, and then
enter a value in the field in the **Bias
Value** column. You can enter a positive (preference) or negative
(deterrent) value for either of the bias types.

- **Percentage** - Bids from buyers in the group will be modified by a
  certain percent.
- **CPM** - CPM bids from buyers in the group will be modified by a
  specific amount.

When you have entered the desired bias amount for the buyer group, click
the Save button within the row.

When you have entered all of the needed bias amounts per buyer group,
click Close to finish editing the base
rule.

Create a Conditional Bias Rule

Create a conditional rule to affect buyer's or buyer group's bids on
specific impressions. You can define a per-buyer bias by impression
frequency, geography, segment, specific placement, category, or
placement size.

Getting There

**Publisher-only clients:** Select
Partners
\>  Yield Management  \>
 Floor rules in the menu bar,
and then select a publisher if you are prompted.

**All other clients:** Select
Publishers
 \>  Floor Rules in the
menu bar, and then select a publisher if you are prompted.

Step 1. Get started

Select a publisher when you are prompted. This opens the **Bias Rule
Manager**.

Step 2. Open the Create New Conditional Rule dialog

Click Create New
 \>  Conditional Rule to
open the **Create New Conditional Rule** dialog.

Step 3. Enter rule details

Enter the basic details for the conditional rule.

- **Name** - Enter a name for your rule. It is recommended to select a
  name that aligns with your business strategy for ease of use.
- **Priority** - Select the desired priority for the rule, Priority 5 is
  selected by default. It is recommended to leave lower priorities (1-4)
  for network-wide rules and use higher priorities (5-9) for your
  publisher-specific rules. It is a good idea to reserve priority 10 for
  special cases that may arise, such as emergencies or blockers.
- **Description** - Enter a rule description for reference.
- **Additional Options: Code** - If you click
  Additional Options (Advanced) you
  will have the option of entering a code. Codes may be helpful for
  networks with distinct internal names/IDs, so that the names/IDs can
  be associated in Monetize and then extracted
  for reporting purposes via our API.

Step 4. Set audience targeting (optional)

In the Audience Targeting tab, you can
select the types of users (audience) you would like the rule to apply
to.

Target frequency

Check the **Apply browser session frequency range** checkbox to create a
bias rule that applies to bids from creatives the user has viewed a
certain number of times. Enter the frequency range that you would like
the rule to apply to. Then select the **Scope**, which indicates if you
would like frequency to be calculated based on views on inventory across
the entire platform (**Platform-wide**), or only views on the
publisher's inventory (**Publisher**).

Check the **Show to users without cookies** to have the rule also apply
to bids from creatives that have been shown to cookieless users. When
this option is selected, you may violate the frequency rang you have set
since it's difficult to track views for cookieless users.

Target geography

Select Audience
Targeting  \>  Geography
to create a bias rule that applies to impressions in certain geographic
regions. You can target specific countries, regions, metro codes,
cities, or zip codes.



Warning: Be careful which geographic
targeting options you choose; you may significantly reduce the
likelihood of matching an impression. For more information, see the note
below.





Important: **A Note on the Accuracy of
Geographic Targeting by IP Address**

Users of geographic targeting should expect some degree of inaccuracy;
though targeting by country is highly accurate, the more specific the
targeting, the more imprecise the results. This is especially true when
targeting locations as granular as cities, metro codes, and zip codes.

Xandr uses the IP lookup service provided by
<a href="http://www.maxmind.com" class="xref"
target="_blank">MaxMind</a>. For more information, read about their
<a href="http://www.maxmind.com/en/geolocation_landing" class="xref"
target="_blank">GeoIP Technology</a> or
<a href="http://www.maxmind.com/app/contact" class="xref"
target="_blank">contact MaxMind directly</a>.

**Geographic Targeting and Boolean Logic**

When more than one targeting type is selected (e.g. both **Region** and
**Zip Code**), the set of matching impressions is reduced, sometimes
significantly. For example, if both the Boston MA-Manchester NH **Metro
Code** and the **City** of Manchester, NH are selected, only users who
are located in both will be targeted. Therefore, users in the **City**
of Boston will not be included at all. Another example: if both the
California **Region** and Chicago, IL **Metro Code** are selected, then
NO users will be targeted since the Chicago metro code does not overlap
with California.



**Target countries:**

Click the **Edit** link for **Country**, and then select one of the
three options: **Include all countries**, **Include United States
only**, or Include/Exclude a specific list of
countries.... If you select
Include/Exclude a specific list of
countries..., select countries in the **Available List** area and
then click Add to add them to the
**Chosen List**. The rule will apply to impressions in any of the
countries within the **Chosen List**.

**Target regions:**

Click the **Edit** link for **Region**, and then select one of the two
options: **Include all regions** or
Include/Exclude specific list of
regions.... If you select
Include/Exclude specific list of
regions..., click Add near
regions in the **Available Regions** area to add them to the **Targeted
Regions** area. The rule will apply to impressions in any of the regions
within the **Targeted Regions** area.

Region is a more granular target than Country. Generally speaking,
regions are based upon whatever method the country in question uses to
divide itself into parts. For example, regions within the United States
are states. Canada is divided into its provinces, and India is divided
into its states and union territories.

**Target metro codes:**

Click the **Edit** link for **Metro Code**, and then select one of the
two options: **Include all metro codes** or
Include/Exclude specific list of metro
codes.... If you select
Include/Exclude a specific list of metro
codes..., select metro codes in the **Available List** area and
then click Add to add them to the
**Chosen List**. The rule will apply to impressions in any of the metro
codes within the **Chosen List**.

Metro codes are smaller than regions and are only available for US
inventory. Available metro codes range from large cities such as New
York, NY and Chicago, IL, to smaller cities such as Rochester, NY,
Birmingham, AL, and Pittsburgh, PA.

**Target cities:**

Click the **Edit** link for **City**, and then select one of the two
options: **Include all cities** or
Include/Exclude specific list of
cities.... If you select
Include/Exclude a specific list of
cities..., click Add near
cities in the **Available List** area to add them to the **Chosen
List**. The rule will apply to impressions in any of the cities within
the **Targeted Cities** area.

A City is different than a Metro Code. It may be larger or smaller,
depending upon your selection. Unlike metro codes, cities are not
limited to US inventory. Cities from all around the world are
represented, ranging from Tel Aviv, Israel to Kuala Lumpur, Malaysia.

**Target zip codes:**

Click the **Edit** link for **Zip Code**, and then enter or paste the
list of comma-separated or newline-separated 5-digit zip codes that you
would like to target in the Zip Codes
field. Click Validate and the system
will verify that your zip codes are formatted correctly. The rule will
apply to impressions in any of the entered zip codes. If your list of
zip codes is formatted incorrectly, you will be presented with an error
message and given the chance to edit and resubmit your zip codes. Those
zip codes that failed the formatting validation will be listed above the
line marked See Errors Above inside
the text area. If you hover over the help bubble to the right of the
text area, you will be presented with a list of the most common errors:

- **Excel-Truncated Zeros**: Excel may truncate leading zeros from zip
  codes when copy-pasting, e.g. `06514` becomes '6514'. To prevent this
  from happening, set the cell formatting of your spreadsheet to Zip
  Code under the Numbers header of the Format Cells dialog.
- **Postal Codes, Zip+4**: Only 5-digit numeric US zip codes are
  accepted, e.g. `12804`.
- **Colons in Ranges**: Use hyphens rather than colons to denote ranges,
  e.g. `10001-10010`.
- **Descending Ranges**: Descending ranges of zip codes are not
  supported. Use ascending ranges instead, e.g. `12561-12804`.

Unlike the other settings listed here, targeting by Zip Code is
include-only. Exclude certain zip codes by entering only those you want
to target. Like metro codes, zip codes only apply to US inventory.

Target segments

Select Audience
Targeting  \>  Segment
to create a bias rule that applies to impressions seen by users in
certain segments. Check the checkboxes near the segments you would like
to target in the **Available Segments** area to add them to the
**Targeted Segments** area.

When targeting multiple segments, impressions must be associated will
**all** of the targeted segments in order for the rule to apply by
default. You can select any from the
**Target all of the following segments:** dropdown in order for the rule
to apply to impressions associated with any of the targeted segments.

In the **Require/Exclude** dropdown, select
Require to target users that belong to
the segment, or Exclude to target
users that do not belong to the segment.

Click edit in the
**Segment Age** column to define
the length of time users have to belong to the segment in order for the
rule to apply.

Check the **Show segment codes** checkbox to display an additional
**Code** column within the table.
If you entered a code when creating the segment, it will display in this
column.

Check the **Show values** checkbox to display an additional
**Value** column within the table
where you can specify portions of the segment that the rule should apply
to. Click edit in the
**Value** column, select a value
type from the **Value** dropdown, enter the value(s), and then click
Set. This feature is only relevant if
the segment you are targeting is a query string segment where parameters
have been defined. For example, let's say you have defined a travel
segment that has 2 travel_location parameters: US and Canada. If you
would like the floor rule to apply to the users within the segment
intending to travel to the US, you can select
equal to in the **Value** dropdown and
then enter US in the text field.

Rather than targeting any or all of the selected segments, you can click
on the **Boolean Logic** header to apply more complex logic.

Step 5. Set supply targeting (optional)

In the Supply Targeting tab, you can
select specific inventory you would like the rule to apply to. You can
target specific placements, content categories, or placement sizes.

Target placements

Select Include specific placements
only... to create a bias rule that applies to specific
placements. Click on a publisher in the **Available List** area to
display that publisher's exposed placements. Then click
Add near placements to add them to the
**Selected List**. You can also click
Add near a publisher in the
**Available List** area to add all of the publisher's exposed placements
at once.



Note: If you target a specific
placement, this rule will only apply to bids on that placement.



Target content categories

Select Include a specific list of content
categories... to create a bias rule that applies to inventory
within a specific category. Click on a category type in the **Available
Content Categories** area to display the list of available categories.
If you have selected **Universal Content Categories**, click on a
category name to display the list of available subcategories. Then click
Add near categories to add them to the
**Targeted Content Categories** area. You can also click
Add near a universal category in the
**Available Content Categories** area to add all of the subcategories at
once. Check the **Allow unknown content categories** checkbox for the
rule to apply to inventory that has not been categorized.



Note: Universal content categories
apply to platform-wide inventory, while custom content categories are
applied only to your managed inventory.



Target sizes

Select Specific sizes... to create a
bias rule that applies to inventory of a specific size. Click on a size
to select it for targeting. You can shift+click or command+click to
select multiple sizes within the list. You can also enter a custom size
by entering the dimensions in the Add a new
size target for this rule fields, and then clicking
Add Size. The size you have added with
then display at the bottom of the list under the **Custom Sizes**
header.

Step 6. Save the conditional bias rule

Once you have defined the rule targeting, click
Save. The rule will then display in
the conditional rules section on the Bias
Rule Manager screen.

Related Topics

- <a href="understanding-yield-management.html" class="xref">Understanding
  Yield Management</a>
- <a href="create-a-floor-rule.html" class="xref">Create a Floor Rule</a>
- <a href="update-bias-rules.html" class="xref">Update Bias Rules</a>
- <a href="update-floor-rules.html" class="xref">Update Floor Rules</a>
- <a href="segment-targeting.html" class="xref"
  title="You can target users within segments by using Boolean expressions. Users get added to segments after they&#39;ve viewed or clicked a particular creative.">Segment
  Targeting</a>
- <a href="query-string-targeting-via-placement-tags-and-segments.html"
  class="xref">Query String Targeting via Placement Tags and Segments</a>




