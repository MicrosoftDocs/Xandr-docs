---
title: Export and Import Object Details in Bulk
description: In this article, learn how to export and import details for multiple line items, creatives, segment groups, splits, and split segment groups simultaneously.
ms.date: 10/28/2023
---

# Export and import object details in bulk

Instead of creating or updating one object at a time, you can export and import details for multiple line items, creatives, segment groups, splits, and split segment groups simultaneously into the **Insertion Orders** and **Line Items** grids using one Excel file.

With the ability to export and import object details using one Excel file, you can quickly do the following, which only reduces repetition
and improves efficiency:

- Edit details for multiple objects.
- Duplicate existing object configurations so that you only have to update minor details such as dates and identifiers.
- Audit object configurations to identify areas that need to be set up more strategically to improve bottom lines.

## Export object details

You can export object details from the **Insertion Orders** and **Line Items** grids by selecting the appropriate checkboxes for the corresponding objects and clicking **Export**. A **Bulk Uploader Tool Results** dialog displays stating whether the export was successful or unsuccessful. If the export was successful, an XLSX file is generated with all the related object details and downloadable from your browser. If the export was unsuccessful due to connection or configuration issues, please contact your account manager.

> [!NOTE]
> Insertion order details can only be exported using the **Insertion Orders** grid. When exporting object details from the **Insertion Orders** grid, you can include child line items and all associated creative, segment group, split, and split segment group details by selecting the **Include child Line Items in export file** checkbox from the **Bulk Exporter Tool** dialog.

## Import object details

To make the import process seamless, we've created a [bulk importer template](https://download.microsoft.com/download/6/f/7/6f755603-e9af-4148-9e52-02e1fb7262b0/Xandr/Bulk-Importer-Template.xlsx) for you to use when gathering the necessary details. You can also use the exported XLSX file by simply updating the object details within it as needed. We've created [Bulk Importer Template Guidelines](bulk-importer-template-guidelines.md) to help you format each parameter correctly within the bulk importer template. To reference the correct identifiers and codes that you want to include in the bulk importer template, use our [bulk importer lists](https://download.microsoft.com/download/6/f/7/6f755603-e9af-4148-9e52-02e1fb7262b0/Xandr/Bulk-Importer-Lists.xlsx).

> [!NOTE]
> Only XLS and XLSX file formats are supported. The Excel file won't be imported if it's over 100 KB. To prevent any bulk upload processing issues, try not to include too many object details in your Excel file.

Once you've made the necessary updates to the bulk importer template or exported XLSX file, save it and click **Import** from either the
**Insertion Orders** grid or **Line Items** grid depending upon the details that you're importing. A **Bulk Uploader Tool Results** dialog displays with a list of all the objects that were imported successfully, as well as any objects that couldn't be imported due to formatting issues, errorenous data, and/or incompatible data combinations.

> [!NOTE]
> Insertion order details can only be imported using the **Insertion Orders** grid.

## Related topics

- [Working with Insertion Orders](working-with-insertion-orders.md)
- [Working with Line Items](working-with-line-items.md)
- [Bulk Importer Template Guidelines](bulk-importer-template-guidelines.md)
