---
title: Performance Metrics with Copilot in Microsoft Monetize 
description: Copilot in Microsoft Monetize helps you quickly access key performance metrics for your campaigns, line items, and deal line items—without navigating complex reports.
ms.date: 12/03/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Performance metrics with Copilot in Microsoft Monetize 

Copilot in Microsoft Monetize helps you quickly access key performance metrics for your campaigns, line items, and deal line items—without navigating complex reports. It provides a fast, intuitive way to view the data you need to make actionable and informed decisions. The responses are generated using data from the Historical Report API, which includes metrics from October 2024 through the present and insights are presented in a concise, conversational format, with direct links to the relevant objects for deeper analysis. 

> [!NOTE]
> Copilot in Microsoft Curate currently does not support performance metrics.

Copilot can summarize performance data such as delivery metrics (impressions, clicks, etc.) and revenue, reducing the number of steps needed to find important insights and simplifying campaign management. The specific report Copilot calls to answer each query is available in the response under the Learn more collapsible section. Users can select the report link to open the corresponding results directly in the Report app. 
 
> [!NOTE]
> Copilot responds to prompts that request simple reporting data. For complex report results, use the Report app.

## Key features

Copilot supports the following performance insights: 
- Lifetime metrics summaries: You can view lifetime performance metrics for line items orders, advertisers, publishers, placements, placement groups, from launch to the most recent available data. 
> [!NOTE]
> Metrics default to lifetime unless you specify a timeframe.
- Timeframe specific metrics: You can drill down into performance for a specific time range. 
    - You can specify the timeframe in your prompt. For Example: “How many impressions did line item XYZ serve from January 12, 2025, to February 12, 2025?”.
    - If Copilot can’t identify the object in the request, an object search box appears in the chat window to help you search for a specific object. 
- **Line item summaries:** View delivery, and budget status for a line item or order by providing the Order name/ID or line item name/ID. 
- **Object metadata insights:** You can access key object settings and configuration details. For all supported objects, you can ask questions about their metadata. For example: 
    - “What is the priority of line item XYZ?” 
    - “Who is the advertiser for order ABC?” 
- **Advertiser summaries:** You can get performance insights for placements and creatives by specifying the Advertiser, Creative name, or ID. 
- **Placement insights:** You can identify standard metrics associated to revenue and impressions for placements using the placement ID or name. 
> [!NOTE]
> If no specific object ID is provided, Copilot verifies the object and may ask for a date.

## Access performance metrics with Copilot in Microsoft Monetize 

Copilot icon is available on every screen within the Microsoft Monetize, providing real-time assistance and contextual guidance. You can access Copilot at any time to ask questions, explore prepopulated prompts, and retrieve relevant performance data. 

- In the top-right corner, select the Copilot icon. 
- A Copilot chat window opens within the current screen. 
- In the bottom-right corner of the chat window, select View Prompts to explore prepopulated prompts.  
- For a more tailored response, you can refine your prompts as such: 
    - For summaries:
        - Summarize my line item performance. 
        - What’s the CTR for order XXX? 
    - For structured answers:
        - Provide a bullet list of impressions served by line item XYZ last week. 
    - For navigations:
        - Take me to Line items XYZ. 
        - Take me to Order ABC. 
    - For performance insights 
        - How did line item Z perform? 
        - How many impressions has line item X received in the last week? 
        - What is the viewability rate of line item Y? 
        - How much revenue has order XYZ generated this month? 
    - For order performance metrics 
        - How many impressions does line item XYZ have? 
        - How many impressions has placement XYZ received in the last X days? 
        - What is the CTR for line XYZ? 
        - How much revenue has order XYZ generated this month? 
- Choose a relevant prompt or enter a custom prompt, ensuring it is specific and concise with relevant context. 
- Select **Enter** to submit the question and review Copilot’s response. 
- Copilot guides you through object selection and timeframe refinement. 
- Each response includes a link to the object for deeper analysis. Select **Learn more** under a response to view related help content, or **Take me there** to navigate to the relevant page. 
- You can also provide feedback on Copilot's responses by selecting the thumbs up or thumbs down symbol, which helps improve the LLM models. 
- Copilot retains chat history when the window is closed and reopened within the same session. 
- To clear the chat history and start anew, select **Start over** in the top-right corner of Copilot’s preview window. 


## Related topics

- [Copilot in Microsoft Monetize](copilot-in-microsoft-monetize.md)