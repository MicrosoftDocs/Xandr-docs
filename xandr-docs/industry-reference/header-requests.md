---
title: Header Requests
description: In this article, find information on header requests and each element of a request.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: industry-reference
ms.author: shsrinivasan
---

# Header requests

## Browser and header requests

So we now understand the syntax of how web browsers locate resources, but what good does just locating resources do? (And, BTW, the way that the request gets physically routed, say from your apartment in Dallas to a New York Times server in Tampa, is another story.) We also want to be able to do things with these resources. The description of what you want to do with the resource is in your Browser's "header request."

Browser Headers have the following format:

```
Request
Headers
Body of the Message
```

## Actual browser request

I wanted to see an actual browser request so I downloaded the Firefox add-on [Live HTTP Headers](https://addons.mozilla.org/firefox/addon/http-header-live/versions/) to view the HTTP headers I was sending. This is an example of a header when I typed in `www.google.com`. The request is a GET Request because I want the page retrieved. And the header lists information and requirements such as return the content in English, I'm using Mozilla Firefox Version 3.6.6, and others you can read below. As you can see, this Request contains no Body of the Message.

:::image type="content" source="media/actual-browser-request.png" alt-text="A screenshot that shows the elements of an actual browser request.":::

## Description of each element in a request

1. **Request:** This is the action that the client wants the server to perform on the resource, such as "download content from nytimes.com". The most common possible actions are below.

    | METHOD | Description | New York Times L.A. Article Example |
    |---|---|---|
    | GET | Retrieve the resource | If you just wanted to see the article, the GET command would retrieve the content. |
    | POST | Allow whatever is the body of the message to be posted as a subordinate to the resource | If you want to comment on the article, the post command would take what you wrote in the Body of the Message and Post it to the existing content. |
    | PUT | Stores the body of the message under the URL as an updated version | If you wanted to edit the comment you just made, you could use the PUT command. |
    | DELETE | Requests that the hosting server delete the resource | If you wanted to delete your comment |
    | TRACE | Repeats the request that the server is reading, allows you to see what the server is seeing | Would allow you to see what the NY Times server is reading |
    | OPTIONS | Returns the possible actions that a particular server accepts for a particular resource | If you wanted to see what capabilities the NY Times was giving you. For example, the NY Times might only allow you to add comments and not delete them, so DELETE would not be returned as an action you could perform |
    | CONNECT | Used to create a secure connection (https) | If you were signing up for the NY Times online and needed to input your credit card information, this is the request your browser would make to get a secure connection |

1. **Headers:** These contain the operating parameters of the HTTP Request. Examples of headers are what kind of language your browser accepts, content types, character fields, etc. Wikipedia has a pretty comprehensive list of possible headers that you can explore.

1. **An Empty Line**

1. **Body of the Message:** This contains information that is used during a POST or PUT command.
