---
title: Bulk Importer Guidelines for Split Segment Groups
description: In this article, understand the bulk importer guidelines and the setup for split segment groups when adding data to the bulk importer template.
---

# Bulk importer guidelines for split segment groups

Please do not rename the Split Segment Groups sheet within the bulk importer template.

## Temporary ID information

| Column Name | Description | Potential Values | Mandatory | Example |
|---|---|---|---|---|
| Split Temporary Id | Specifies the identifier used to link segment groups to a parent split within the spreadsheet. This is a placeholder value and will not be the actual identifier of the newly-created object. | Alphanumeric value | No | example123 |

## Split segment group setup

| Column Name | Description | Potential Values | Mandatory | Example |
|---|---|---|---|---|
| Split Id | Specifies the identifier of the existing split that will target the segment. | Numeric value | No | 1234 |
| Split Name | Specifies the name of the split. | Characters | No | My split |
| Segment Id | Specifies the identifier assigned to the segment. | Numeric value | Yes | 1234 |
| Group | Specifies the segment group that is associated with the segment target. | Numeric value | Yes | 1 |
| Include or Exclude | Specifies whether to include or exclude this target. | - include <br> - exclude | Yes | include |
| Fired Greater Than | Specifies the maximum minute threshold indicating when a user was added to the segment. | Numeric value | No | 10 |
| Fired Less Than | Specifies the minimum minute threshold indicating when a user was added to the segment. | Numeric value | No | 1 |
| Value Greater Than | Targets segment values that are greater than the specified value. For example, if the specified value is 10, then you would be targeting any segment value that is greater than 10. | Numeric value | No | 80 |
| Value Less Than | Targets segment values that are less than the specified value. For example, if the specified value is 10, then you would be targeting any segment value that is less than 10. | Numeric value | No | 100 |
| Value Equal To | Targets exact segment values. | Numeric value | No | 5 |

## Related topics

- [Bulk Importer Template Guidelines](bulk-importer-template-guidelines.md)
- [Exporting and Importing Object Details in Bulk](exporting-and-importing-object-details-in-bulk.md)
