---
title: Reporting in Microsoft Monetize
description: Reporting in Microsoft Monetize offers a comprehensive and unified access to a broad set of dimensions and metrics, streamlining the reporting experience to enable users to efficiently analyze, troubleshoot, and make data-driven decision. 
ms.date: 04/29/2023
ms.author: shsrinivasan
---


# Reporting in Microsoft Monetize

Reporting in Microsoft Monetize offers a comprehensive and unified access to a broad set of dimensions and metrics, streamlining the reporting experience to enable users to efficiently analyze, troubleshoot, and make data-driven decision.  

> [!NOTE] 
> Certain reports, including the new Historical Reports, are accessed through separate workflows and are not consolidated within the new reporting builder. For more information, see [Historical Reporting in Microsoft Monetize](monetize-historical-reporting.md).

## Navigate Reporting in Microsoft Monetize  

To access the reporting screen, navigate to Reporting from the left pane and select from the following submenu options: 
- **Report Center:** Use the Report Center to view your Saved and Recent reports in one place. 
- **Create New:** Select Create New to start building a new report. Begin by choosing a report type that fits your analysis needs. 
- **Historical Report:** Historical Report is the new primary analytics report in Microsoft Monetize. It consolidates data covering more than 10 legacy report types, including Network Analytics, Seller Brand Review, and Seller Fill and Delivery. For more information, see [Historical Reporting in Microsoft Monetize](monetize-historical-reporting.md).
- **Legacy Reporting:** Use Legacy Reporting to access the legacy version of the reporting interface, where legacy reports are still available. 
> [!NOTE] 
> The legacy reporting interface will remain accessible for 60 days after the GA date to support workflow continuity and allow time for any necessary adjustments. 

### Report Center 

The Report Center serves as a central location for accessing all your Saved, Scheduled, and Recent reports. It is organized into two main tabs: 

- **Saved Reports:** The **Saved** tab displays all the reports you have saved within the platform.   
    - Select the report name, to view the results of a report. This will run the report and display its output. 
    - Select schedule using the drop-down menu next to each saved report to add or modify scheduling settings. 
    - Select the **Edit** button to edit a report. This opens the report in the report builder, where you can make any necessary changes. 
    - Select the **Delete** button and confirm the action in the confirmation dialog, to delete a report 
> [!NOTE] 
> Saved and Recent reports from the legacy UI are also available in the new interface. These are shown together in a unified view, with scheduling details displayed as metadata alongside the saved report. 
- **Recent Reports:** The **Recent** tab displays a list of all previously run reports. This allows you to quickly revisit previous results or use them as a baseline to create a new report. 
    - Select the report name, to view the results of a previously run report. This will re-run the report and display the latest data. 
    - The **Status** column indicates whether a report is Ready or Processing. You can only view or download the results once the report status is **Ready**. 
    - Select the **Download** button, to download a report. You will be prompted to choose a file format—XLSX, CSV, Excel/TSV, or JSON. Once selected, the file will download directly in your browser. 


### Creating New 
- To create a new report, select **Create New** from the Reporting sub-menu or click the **Create New** button at the top right corner of the **Report Center** screen. This will take you to the **Create New Report** screen, that displays a selection of report types, organized into two main sections:
    - Monetize Reports: Microsoft Monetize offers a range of report types that provide metrics across various dimensions under the Monetize Reports. These reports are grouped into the following categories: 
        - **Analytics:** Analytical category contains reports that enable you to analyze platform requests and transactions. 
        - **Billing and Usage:** Billing and Usage category contains reports that provide data for billing, creative audits, and the usage of data and vendors on the platform. 
        - **Reach:** Reach category contains reports that enable you to understand unique user counts, user frequency, and segments. 
        - **Troubleshooting:** Troubleshooting category contains reports that are designed to assist with investigating bid rejections, consent management, deals, and viewability. 
        - **Other:** Other category contains reports such as Forecast reporting that can be used to view both buy and sell-side data for a network member. 
    > [!NOTE]
    > Each report type card includes a brief description of its purpose, helping you quickly identify which report suits your needs. 
    - **Legacy Reports:** To ensure continuity, all legacy report types remain accessible and are organized under the Legacy tab in the Report Selection screen. These reports are categorized as follows: 
        - **Analytics:** Analytical category contains reports that enable you to analyze platform requests and transactions. 
        - **Troubleshooting:** Troubleshooting category contains reports that are designed to assist with investigating bid rejections, consent management, deals, and viewability.
- Select the **Create New Report** from the category of report you want to pull data from. 
- Select the desired time period for the report, from the **Date** drop-down menu. The drop-down offers several standard lookback windows, as well as a Custom option for selecting specific start and end dates.  
- Select the **Filter** button to open a side pane on the right to apply Filters. Here, you can apply restrictions to the data by selecting the **Include** or **Exclude** radio button for each filter object. Available filters are searchable, and you can view possible values for each. The **Show Selected** toggle lets you easily see all current selections. You can also copy and paste a comma-separated list of IDs by toggling the option from Manual Selection to Bulk Add IDs. You can match the IDs against all non-deleted objects or choose to skip validation, which will allow you to filter on objects that were deleted previously but are no longer deleted. 
- Select the appropriate interval from the drop-down menu. The *8Interval Selection** option to specify how the data should be grouped by date or time. The available options for grouping data are: 
    - **Hourly:** Data is grouped by the hour. 
    - **Daily:** Data is grouped by the day. 
    - **Monthly:** Data is grouped by the month. 
    - **Cumulative:** Data is displayed for an entire selected period. 
- Select the Metrics to measure the performance of the dimensions you’ve selected. To select a metric, simply check the corresponding checkbox. 
- Select the Show Selections button to display all selected dimensions and metrics. 
- For advanced settings, click the gear icon in the top-right corner to open the Advanced Settings menu. Here, you can adjust the currency, timezone, and enable the option to include IDs as a separate column. 
> [!NOTE]
> Currency selection is available only for specific report types and defaults to the member’s currency when applicable. 
- Select the **Run Report** button, to generate the report, select. If the report contains over 1,000 rows, a preview will be shown in the UI. For larger reports that may take longer to process, you can select **Run in Background & Email Results** or **Run in Background & Download Results** from the drop-down menu in the **Run Report** button. 
- Select the **Download** button, after the report is generated. The available download formats are XLSX, CSV, Excel/TSV, and JSON. 
- To save the report, click the drop-down menu next to the Run Report button and select Run & Save Report. 

#### View and interact with report results 

After you select **Run Report**, the interface displays a preview of up to 1,000 rows of data. 
- By default, the results are sorted by the **Date** column (if selected). If no date is selected, results are sorted in descending order by one of the metrics. To sort by a different column, select the column header. To toggle between ascending and descending order. 
- To resize a column: 
    - Hover over the right edge of the column header until the resize cursor appears. 
    - Click and drag to adjust the column width as needed. 
- You can update your report by adjusting the **Time Period**, **Interval**, **Filters**, or *8Advanced Settings**, and then select **Run Report** again to refresh the results with the new settings. 
- To modify the dimensions, metrics, or reorder columns: 
    - Select the **Edit** button located at the far right of the screen. This opens the selections panel where you can adjust the report fields and column order. 

### Historical report 

Historical Report is the primary analytics report in Microsoft Monetize, offering comprehensive data across a wide range of dimensions and metrics. It consolidates more than ten legacy report types, including Network Analytics, Seller Brand Review, and Seller Fill and Delivery. The Historical report reduces the number of report types a user needs to interact with, providing features to improve usability such as categorization of Dimensions and Metrics and comprehensive search capability. For more information, see [Historical Reporting in Microsoft Monetize](monetize-historical-reporting.md).


### Legacy reporting 

Legacy Reporting enables you to access the legacy version of the reporting interface, where legacy reports are still available. Legacy reports will no longer be populated with new Microsoft Monetize data starting in mid-2025. Historical data will remain available up to each report’s standard retention period or `730` days, whichever is shorter. This applies to reports such as Network Analytics and Advertiser Video Analytics. 
> [!NOTE]
> Users are strongly encouraged to transition to the new reporting experience for accessing data generated after `10th October 2024`. 


## In this guide

- [Historical Reporting in Microsoft Monetize](monetize-historical-reporting.md)