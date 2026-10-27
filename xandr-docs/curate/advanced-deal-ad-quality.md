---
title: Microsoft Curate - Advanced Deal Ad Quality
description: Learn how to configure audit requirements, brand and ad server restrictions, and creative exceptions for a curated deal.
ms.date: 10/27/2026
ms.service: publisher-monetization
ms.subservice: microsoft-curate
ms.author: shsrinivasan
---

# Microsoft Curate - Advanced Deal Ad Quality

Advanced Deal Ad Quality lets you control which creatives can serve through a curated deal. From the deal creation and editing screens, you can allow or block brands and creative ad servers (sometimes called pixels), require platform-audited creatives, and create exceptions for individual creatives.

Use Advanced Deal Ad Quality to:

- Restrict delivery to specific brands or prevent certain brands from serving.
- Restrict creatives to approved ad servers or block specific ad servers.
- Allow or block specific creatives by ID.
- Require creatives to pass Microsoft's creative audit before they can serve.

Settings can apply at the member level or the deal level. Member-level settings apply by default to deals that don't have their own ad quality configuration. Deal-level settings replace the member-level configuration for a specific deal.

> [!NOTE]
> Only deal-level settings can be configured in the user interface. To configure member-level settings, use the [Curated Deal Ad Quality API Setup Guide](../digital-platform-api/curated-deal-ad-quality-api-setup-guide.md) or contact support.

## Understand how ad quality settings apply

### Member-level and deal-level settings

When a curated deal doesn't have deal-level ad quality settings, it inherits the member-level settings. An informational message in the **Advanced Deal Ad Quality** section indicates that the deal is using member-level settings.

To customize settings for that deal, you can either copy the member-level settings to the deal or create deal-level settings from scratch.

> [!IMPORTANT]
> Deal-level settings fully replace member-level settings for that deal. The two configurations aren't combined. If you create deal-level settings, include any member-level restrictions that you want to retain.

### How settings combine

A creative must meet all applicable ad quality requirements to be eligible to serve, unless you explicitly allow its creative ID. For example, a creative with an allowed brand but a blocked ad server can't serve unless you explicitly allow that creative.

Creative-level rules take precedence over the other curator ad quality settings:

- An explicitly allowed creative passes the curator's ad quality checks, even if its brand, ad server, or audit status would otherwise make it ineligible.
- An explicitly blocked creative can't serve through the curated deal, even if it meets the other curator ad quality requirements.

### Publisher ad quality settings

Curator ad quality settings can only be more restrictive than the publisher's settings. You can't override a publisher's restrictions, even by explicitly allowing a creative.

For example, if you allow a brand but the publisher blocks it, creatives associated with that brand can't serve through your curated deal on that publisher's inventory.

## Configure Advanced Deal Ad Quality

### Open the settings

1. Go to **Packages** > **Curated Deals**.
1. Create a new deal or edit an existing deal.
1. Go to the **Advanced Deal Ad Quality** section.
1. If the deal uses member-level settings and you want to customize them, choose one of the following options:
   - Copy the member-level ad quality settings to this deal so you can customize them.
   - Create deal-level ad quality settings from scratch.

   If you want to continue using member-level settings without changes, leave the deal-level settings unconfigured.

### Set the audit requirement

Under **Audit Status**, select or clear **Only allow platform-audited creatives**. This option is enabled by default.

| Setting | Behavior |
|---|---|
| Enabled | Only creatives that have successfully completed Microsoft's creative audit can serve, unless explicitly allowed by creative ID. |
| Disabled | Both audited and unaudited creatives can serve, subject to the other ad quality settings. |

An explicitly allowed creative must still pass the publisher's ad quality settings.

### Allow or block brands

1. Under **Brands**, select the **Edit** icon to open the brand selection dialog.
1. Search for brands by name or ID.
1. Choose **Allow selected brands** or **Block selected brands**, and select the brands to include.

| Selection | Behavior |
|---|---|
| Allow selected brands | When one or more brands are selected, only those brands are allowed. All other brands are blocked. |
| Block selected brands | Selected brands are blocked. All other brands remain eligible. |
| No brands selected | There are no brand restrictions. |

Creatives remain subject to the other ad quality requirements and any creative-level overrides.

### Allow or block ad servers

1. Under **Ad Servers**, select the **Edit** icon to open the ad server selection dialog.
1. Search for ad servers by name or ID.
1. Choose **Allow selected ad servers** or **Block selected ad servers**, and select the ad servers to include.

| Selection | Behavior |
|---|---|
| Allow selected ad servers | When one or more ad servers are selected, only those ad servers are eligible. All other ad servers are blocked. |
| Block selected ad servers | Selected ad servers are blocked. All other ad servers remain eligible. |
| No ad servers selected | There are no ad server restrictions. |

Creatives remain subject to the other ad quality requirements and any creative-level overrides.

### Allow or block specific creatives

1. Under **Creatives**, select the **Edit** icon to open the creative selection dialog.
1. Search using the Microsoft Advertising creative ID.
1. Explicitly allow or block each creative as needed.

| Selection | Behavior |
|---|---|
| Allow a creative | The creative passes the curator's ad quality checks, even if other curator settings would restrict it. The publisher's ad quality settings still apply. |
| Block a creative | The creative can't serve through the curated deal, even if it meets the other ad quality requirements. |

Allow a creative when it's approved for a particular buyer or campaign despite broader curator restrictions. For example, you can explicitly allow an unaudited creative even when **Only allow platform-audited creatives** is enabled.

Block a creative when you need to exclude it while keeping other creatives from the same brand or ad server eligible.

### Save the deal

After you finish configuring the ad quality settings, save the deal.

## Check ad quality eligibility

If a creative isn't eligible to serve, review the following:

1. **Active configuration**: Determine whether the deal uses member-level or deal-level settings. If deal-level settings exist, only that configuration applies.
1. **Creative overrides**: Check whether the creative ID is explicitly blocked or allowed.
1. **Audit status**: If the creative isn't explicitly allowed and **Only allow platform-audited creatives** is enabled, confirm that it has passed Microsoft's creative audit.
1. **Brands and ad servers**: If the creative isn't explicitly allowed, confirm that both its brand and ad servers meet the configured restrictions. An allowlist with at least one selection blocks everything not selected.
1. **Publisher settings**: Confirm that the publisher permits the creative. Curator settings can't override publisher restrictions.

Passing these checks makes a creative eligible under the ad quality settings; it doesn't guarantee delivery.

## Best practices

- Configure member-level settings when the same rules apply across most deals.
- Use deal-level settings when a specific buyer or brand requires different controls.
- Copy member-level settings before customizing a deal if you want to retain the existing restrictions.
- Regularly review restricted brands and ad servers to ensure they reflect current business requirements.
- Keep **Only allow platform-audited creatives** enabled when working with buyers that require additional creative quality safeguards.

## Related topics

- [Curated Deal Ad Quality API Setup Guide](../digital-platform-api/curated-deal-ad-quality-api-setup-guide.md)
- [Create a Simplified Deal Line Item](create-a-simplified-deal-line-item.md)
- [Curated Deals](curated-deals.md)
