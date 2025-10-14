---
title: Using Postman with the Yield Analytics API
description: In this article, learn how to use Postman with Yield Analytics APIs and working with templates for API calls.
ms.service: publisher-monetization
ms.subservice: yield-analytics-api
ms.date: 10/28/2023
---

# Using Postman with the Yield Analytics API

## Overview

The goal of this tutorial is to take a new Postman install and walk away with a template for every API call available in the public Yield Analytics API. This will prove a basis by API calls can be tailored to specific clients data without the need to repeatedly build out the boilerplate parameter of an API call. By the end of the tutorial you should have a solid base for interacting with the API via:

- A Template for every API Call in the Yield Analytics Public API
- Environment variables to allow for abstracting template calls to fit any clients needs
- A working environment for a specific customer
- How to export and share a specific call you’re working on
- Basic understanding of converting http calls into other formats such as cURL

## Swagger templates for Yield Analytics API services

- [Product and Inventory Service Template](https://download.microsoft.com/download/4/0/0/40099106-6f9f-4b38-8aac-0dc7567404db/yield-analytics-api/productresource-swagger.json)
- [Insertion Order Service Template](https://download.microsoft.com/download/4/0/0/40099106-6f9f-4b38-8aac-0dc7567404db/yield-analytics-api/insertionorderresource-swagger.json)
- [Order Line Service Template](https://download.microsoft.com/download/4/0/0/40099106-6f9f-4b38-8aac-0dc7567404db/yield-analytics-api/orderlineresource-swagger.json)
- [Query Engine Service Template](https://download.microsoft.com/download/4/0/0/40099106-6f9f-4b38-8aac-0dc7567404db/yield-analytics-api/queryengineresource-swagger.json)

## Importing a Swagger template into Postman

- Copy the Swagger Template URL by copying the address or clicking through and copying the url from the desired template listed above.
- In Postman select: file → import.

  :::image type="content" source="media/postman-file-import.png" alt-text="A screenshot that shows how to navigate to the Import option in Postman.":::

- Select Import From Link and paste in the Template URL.

  :::image type="content" source="media/postman-import-swagger.png" alt-text="A screenshot that shows how to import from link in Postman.":::

- Note that the headers have a standard key and a value wrapped in {{}}. Leave these in place and continue to the next section.

  :::image type="content" source="media/postman-header-variables.png" alt-text="A screenshot of the Headers tab with standard keys and values.":::
  
## Setting Up a Postman environment with variables

- In Postman, text wrapped in {{}} will be treated as a variable. Variables are symbols that can take different values. You might be familiar with variables from other languages from your prior programming experience. Variables in Postman work the same way.

- Postman also supports the concept of an environment. This is essentially a collection of variables that translate to a working group for the desired client you want to interact with.

- The following image shows several variables: {{client_url}}, {{accepts}}, {{username}}, {{password}} and {{source}}

  :::image type="content" source="media/postman-header-variables.png" alt-text="A screenshot of the Headers tab with different variables.":::

- In order to setup an environment click the gear icon located above the current active API call and select Manage Environments.

  :::image type="content" source="media/postman-env-gear-icon.png" alt-text="A screenshot that shows how to navigate to Manage Environments option.":::

- Next click on the add button, name your environment and add in the variable names with values as shown in the following image

  :::image type="content" source="media/postman-env-example.png" alt-text="A screenshot that shows the Manage Environments dialog box with some variable names and values added.":::

- Finally select your new environment from the environment dropdown

  :::image type="content" source="media/postman-env-dropdown.png" alt-text="A screenshot that shows the Environments dropdown.":::

- When your API call is invoked the variables in {{}} will be replaced by the value you’ve assigned to the variable at runtime.

> [!NOTE]
> The templates are meant to speed up the development of API calls and very likely will not work until the url and body parameters have been tweaked using data applicable to the client.

## Exporting an API call from Postman

- Postman provides multiple mechanisms for sharing work. Exporting provides a quick and easy way to share an API call that you’re working on. The process will download a .json file that includes all the parameters you’ve added to the call. This .json file can then be imported by another user using the import process described before. The only difference being you would import from a file rather than a link.

  > [!NOTE]
  > You’ll need to clear out your password before exporting.

- The main goals here are knowledge sharing and providing engineering with a runnable example that we can use to quickly determine if the call is incorrect or if the server action is incorrect.

  :::image type="content" source="media/postman-export-call.png" alt-text="A screenshot that shows how to export a call on Postman.":::

## Converting an https call to a cURL command

Postman provides a quick and easy way to convert these HTTPS API calls into other formats. Simply click on the "Code" link on the right hand side of your active API call and then select the conversion you want as depicted in the following image:

:::image type="content" source="media/postman-convert-to-curl.png" alt-text="A screenshot that shows how to convert a http call to a cURL command on Postman.":::
