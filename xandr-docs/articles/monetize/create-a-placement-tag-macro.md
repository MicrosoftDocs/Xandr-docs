---
Title : Create a Placement Tag Macro
Description : If you would like even more flexibility than what our existing macros
ms.date: 10/28/2023
provide, you can create a placement tag macro, which will send custom
data on the placement ad call so that you can use it in your creative
tag. You can create a placement tag macro if you have access to both
---


# Create a Placement Tag Macro



If you would like even more flexibility than what our existing macros
provide, you can create a placement tag macro, which will send custom
data on the placement ad call so that you can use it in your creative
tag. You can create a placement tag macro if you have access to both
managed supply and demand.



Placement tag macros can be used for sending page-level data to
non-Xandr systems. For more information about
our creative macros, see <a href="creative-macros.md" class="xref"
title="You can insert creative macros into your creative third-party tags, impression trackers, landing page URLs, and third-party pixels for reporting and optimization purposes.">Creative
Macros</a>.



<b>Note:</b> Before creating placement tag
macros, you should consider the following:

- Data passed in using this method is not stored in our data pipeline.
  There is no reporting available from Xandr
  related to your use of this feature.
- Like most of our non-clicktracking creative macros, these macros are
  populated by our bidder engine. Therefore, they won't populate in
  creative previews, but only during true auctions.







1.  Create a placement using your platform or
    content management system.
    

    For more information, see
    <a href="create-a-placement.md" class="xref">Create a Placement</a>.

    
2.  Export the placement from your platform or
    content management system.
    

    For more information, see
    <a href="export-placement-tags.md" class="xref">Export Placement
    Tags</a>.

    

    

    You should now have a snippet of HTML that represents your
    placement. It should look something like this:
    ``` pre
    <!-- BEGIN JS TAG - [A Publisher You've Probably Heard of] - Default < - DO NOT MODIFY -->
    <SCRIPT SRC="https://ib.adnxs.com/ttj?id=608398&size=[WIDTHxHEIGHT]&cb=[CACHEBUSTER]" TYPE="text/javascript"></SCRIPT>
    <!-- END TAG -->
    ```

    
3.  Edit the placement tag by adding one or more of
    the query string parameters, such as
    `pt0, pt1, pt2, pt3, pt4, pt5, pt6, pt7, pt8, pt9`, to the ad call's
    URL within the HTML.
    

    This will allow the placement tag to send the custom data that you
    specified.

    

    

    

    <b>Note:</b> Please ignore the "DO NOT
    MODIFY" warning.

    

    

    

    The modified URL would look similar to this:
    `https://ib.``adnxs``.com/ttj?id=608398&size=[WIDTHxHEIGHT]&cb=[CACHEBUSTER]&pt1=product-keywords:iphone;ipad&pt2=pagescore:99.2`

    

    

    

    <b>Note:</b> Notice the differences
    between the URLs before and after adding the `pt1` and `pt2` query
    string parameters. Those parameters contain whatever data you assign
    to them, and that data will be used to populate the corresponding
    macros in your creative.

    

    
4.  Create a third-party creative.
    

    

    <b>Note:</b> You won't be able to create a
    third-party creative if you select an HTML tag that is being served
    inside an iFrame. This is because our system does not pass the
    various query string parameters when generating iFrames. Therefore,
    the macros will not populate with your custom data.

    

    

    

    For more information, see <a href="add-a-creative.md" class="xref"
    title="You can add a creative by either uploading a spreadsheet or the creative files directly from your computer. Only secure content is supported.">Add
    a Creative</a> and <a href="add-creatives-in-bulk.md" class="xref"
    title="You can add multiple third-party, hosted, and native creatives to the Creative Manager simultaneously by either uploading a spreadsheet or the creative files directly from your computer. Only secure content is supported.">Add
    Creatives in Bulk</a>.

    
5.  Inside the
    Tag text area, enter the
    JavaScript that you would like to use to generate your
    creative.
    

    The macro text "variables" available for your use include:
    - `${PT0}`
    - `${PT1}`
    - `${PT2}`
    - `${PT3}`
    - `${PT4}`
    - `${PT5}`
    - `${PT6}`
    - `${PT7}`
    - `${PT8}`
    - `${PT9}`

    The macro text variables correspond to the following query string
    parameters on the placement ad call:
    <table id="ID-000048fd__table_c43_frn_kmb" class="table">
    <thead class="thead">
    <tr class="header row">
    <th id="ID-000048fd__table_c43_frn_kmb__entry__1" class="entry">Macro
    Text</th>
    <th id="ID-000048fd__table_c43_frn_kmb__entry__2" class="entry">Query
    String Parameters</th>
    </tr>
    </thead>
    <tbody class="tbody">
    <tr class="odd row">
    <td class="entry"
    headers="ID-000048fd__table_c43_frn_kmb__entry__1"><code
    class="ph codeph">${PT0}</code></td>
    <td class="entry"
    headers="ID-000048fd__table_c43_frn_kmb__entry__2">pt0</td>
    </tr>
    <tr class="even row">
    <td class="entry"
    headers="ID-000048fd__table_c43_frn_kmb__entry__1"><code
    class="ph codeph">${PT1}</code></td>
    <td class="entry"
    headers="ID-000048fd__table_c43_frn_kmb__entry__2">pt1</td>
    </tr>
    <tr class="odd row">
    <td class="entry"
    headers="ID-000048fd__table_c43_frn_kmb__entry__1"><code
    class="ph codeph">${PT2}</code></td>
    <td class="entry"
    headers="ID-000048fd__table_c43_frn_kmb__entry__2">pt2</td>
    </tr>
    <tr class="even row">
    <td class="entry"
    headers="ID-000048fd__table_c43_frn_kmb__entry__1"><code
    class="ph codeph">${PT3}</code></td>
    <td class="entry"
    headers="ID-000048fd__table_c43_frn_kmb__entry__2">pt3</td>
    </tr>
    <tr class="odd row">
    <td class="entry"
    headers="ID-000048fd__table_c43_frn_kmb__entry__1"><code
    class="ph codeph">${PT4}</code></td>
    <td class="entry"
    headers="ID-000048fd__table_c43_frn_kmb__entry__2">pt4</td>
    </tr>
    <tr class="even row">
    <td class="entry"
    headers="ID-000048fd__table_c43_frn_kmb__entry__1"><code
    class="ph codeph">${PT5}</code></td>
    <td class="entry"
    headers="ID-000048fd__table_c43_frn_kmb__entry__2">pt5</td>
    </tr>
    <tr class="odd row">
    <td class="entry"
    headers="ID-000048fd__table_c43_frn_kmb__entry__1"><code
    class="ph codeph">${PT6}</code></td>
    <td class="entry"
    headers="ID-000048fd__table_c43_frn_kmb__entry__2">pt6</td>
    </tr>
    <tr class="even row">
    <td class="entry"
    headers="ID-000048fd__table_c43_frn_kmb__entry__1"><code
    class="ph codeph">${PT7}</code></td>
    <td class="entry"
    headers="ID-000048fd__table_c43_frn_kmb__entry__2">pt7</td>
    </tr>
    <tr class="odd row">
    <td class="entry"
    headers="ID-000048fd__table_c43_frn_kmb__entry__1"><code
    class="ph codeph">${PT8}</code></td>
    <td class="entry"
    headers="ID-000048fd__table_c43_frn_kmb__entry__2">pt8</td>
    </tr>
    <tr class="even row">
    <td class="entry"
    headers="ID-000048fd__table_c43_frn_kmb__entry__1"><code
    class="ph codeph">${PT9}</code>}</td>
    <td class="entry"
    headers="ID-000048fd__table_c43_frn_kmb__entry__2">pt9</td>
    </tr>
    </tbody>
    </table>

    

    

    Here's a simple example of how you might use the macro text inside
    your JavaScript creative's code:
    ``` pre
    var pt1 = "${PT1}";
    var pt2 = "${PT2}";
    document.write("<img src=\"https://great-ad-server.com/300x250/f0f&product_keywords=" + pt1 + "&page_score=" + pt2 + " \">");
    ```

    



>

Related Topics

- <a href="create-a-placement.md" class="xref">Create a Placement</a>
- <a href="export-placement-tags.md" class="xref">Export Placement
  Tags</a>
- <a href="click-tracking.md" class="xref"
  title="Click tracking serves many useful purposes within the ad serving industry as a whole. For Xandr, click tracking is necessary for optimizing to CPC and CPA goals, for bidding CPC and CPA, and for measuring a campaign&#39;s success.">Click
  Tracking</a>






