---
title: Intro to HTTP
description: Learn the basics of HTTP and how it is important for online advertising. This page covers different concepts related to HTTP like URL, Scheme, Hostname, Port and DNS.   
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: industry-reference
ms.author: shsrinivasan
---


# Intro to HTTP

Understanding the basics of how HTTP works is integral to understanding online advertising technology. For example, we deal with "cookie data"---but how does that cookie data get passed into an ad server or used in an ad request? What's actually contained in a cookie? Where do cookies live and how do we access cookie data on an ad call?

And you may have asked yourself at some point, Why isn't my click tracking working? What's a segment pixel? Why do I need user ID mapping? To answer, you need to understand what's really happening when your browser contacts a web server, and very few people DO understand this---including most people in the online ad industry.

There are a lot of information on the internet about HTTPs, below is a quick summary to get you started. Please [let us know](mailto:wiki@appnexus.com) what's helpful for you and what suggestions you have, and let us know if you've found any good intro guides.

## HTTP definition

HTTP stands for Hypertext Transfer Protocol, and it's how different parts of the Internet communicate with each other. HTTP is what's known as a "request-response" language because your web browser (Firefox, Safari, etc.) sends an HTTP request to a server that is hosting the web content you want to work with. The server then sends an HTTP response back to your web browser.

This is why you will hear your browser referred to as a "client," and the browser-server relationship as a "client-server" relationship. A browser only makes requests, and the server serves the client's requests with responses.

:::image type="content" source="./media/http.png" alt-text="Screenshot of HTTP.":::

## Uniform resource locator (URL)

Most everyone is familiar with URLs. They are the web addresses you type into the address bar on your browser. A URL, which is written in standard HTTP, provides the means to identify and **locate** a **resource.** A resource can be graphics, text, or an application, etc.

Below is the standard syntax of a URL:

``` 
scheme://hostname:port/path?query_string
```
Let's review the following URL and find the article "Choice Tables - Delicious Ways to Love Downtown Los Angeles" on the New York Times website:

[https://www.nytimes.com/2010/09/12/travel/12choice.html?_r=1&src=me&ref=travel](https://www.nytimes.com/2010/09/12/travel/12choice.html?_r=1&src=me&ref=travel)

### Scheme

This defines the type of resource. We are dealing with HTTP, so the example above is of an HTTP resource. The scheme tells the server what type of resource the client (your browser) is looking for and what format the rest of the locator will be in. There are other types of Schemes, such as FTP, that we will discuss later.

### Hostname

This is also called the domain name. It is a nickname for an IP address (we'll get into IP's later) that is more easily read by people. In the example above the hostname is "www.nytimes.com." So the request knows to go to the NY Times server.

### Port

The port number is optional, so it's not used in most URLs. If the port is not listed then the default port for the scheme is used. For the example above, the port is not included, but the server would know to send the URL to port 80 because this is the default port for HTTP. Another frequently used scheme is FTP which uses port 21 as a default. If you don't know much about ports don't worry about this part. We will cover more about ports later.

### Path

The path is used to define how to find the resource. The hostname sends you to the right IP address, and the path further directs how to get to a more specific location. This is similar to finding something on your computer, for example let's say you have a tax return file located at home/documents/taxes/taxreturn2009.pdf. The Path usually begins after the first single "/" and there can be multiple layers of a path, all set off by a "/".

In the example above, the path is "/2010/09/12/travel/12choice.html". Once the message reaches the nytimes.com server, it knows to continue through to each layer of the path till it reaches the final layer, "12choice". Finding a resource using a URL is a similar process to finding a file in an office. First you go to the office, then the right file cabinet, then the drawer, then the correct green hanging file, then finally the manilla folder that has the information you want.

### Query string

Query strings are always separated from the rest of the URL by a question mark. Query strings usually contain any name or "value pairs" that the client wishes to pass to the server. A value pair is the type of information and the actual information joined by an equals sign, such as food=hamburger. Value pairs are separated by ampersands, and you can have as many value pairs in a query string as you need.

In the example above, "?r=1&src=me&ref=travel" is the query string. The question mark denotes the beginning of the query string. The value pair "ref=travel", most likely refers to the fact that this article is in the travel section.

Another common example of when query strings are used is filling out an online form. This example is of the Xandr Contact Form:

:::image type="content" source="media/contact-form.png" alt-text="Screenshot of Contact Form.":::

The query string would look like this: ?Field1=George&Field2=Smith&Field3=gsmith@gsmith.com&Field4=Smith_Enterprises&Field5=Your_platform\_

## Domain name system (DNS)

A hostname or domain name actually means nothing to a server, which works in binary (all 1s and 0s). A URL is used as a "nickname" that has meaning to humans, but in order for servers to work with URLs they are translated into an IP address. We will talk more about IP Address, but IP Addresses are unique numbers assigned to every computer connected to the internet and look something like this: 1276.1345.4858.9567.

In order to have URLs consistently translated to the correct IP address all over the whole Internet, the Domain Name System was created. Domain Name Systems map domains to their IP address. When you register a URL you must attach it to an IP address and register it with DNS.

From the example above, "www.nytimes.com" would be translated into the IP address of the server that the NY Times registered with the DNS.
