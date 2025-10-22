---
title: Sherlock - Creative Quality Control
description: Learn how we use Sherlock to detect malicious content and assist our human auditors with ad quality. 
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Sherlock - Creative quality control

Xandr takes malware extremely seriously, and we actively work to be at the forefront of prevention in order to protect our customers.

We utilize our own automated creative scanning system system, Sherlock, to detect malicious content and assist our human auditors with ad quality. Sherlock simulates real traffic as accurately as possible. Because we do not wish to describe our methods to any potential bad actors, we currently don't disclose details of the process in our documentation.

## Anti-Malvertising policy for buyers

We have developed an [Part of Service Policies](../policies-regulations/index.yml) whose goal is to ensure that our clients are making all necessary efforts to keep our platform safe. Select the above link and read this policy carefully to understand your responsibilities.

## Malware issues or questions

If you have any malware related issues or questions, complete our [Customer Support form](https://help.xandr.com/s/login/) and select **Anti-Malvertising** as the Request Type. If you feel that your creative was deactivated erroneously for loading a non-malicious domain, open a ticket and provide your reasoning as well as contacts for the domain owner so that we are able to further investigate.

## Violation reports and automated emails

Upon detecting a violation, our system sends an email to the client contact that we have for creative audit notifications. This email includes the reason for violation (for example loading a blocklist SLD), as well as a link to a report showing a detailed call chain of the violation.

This report is similar to the output one would see while running a program such as TamperData or HTTPScoop and shows both the order of the calls as well as a column titled **cache** which has a cached copy of content loaded at each step. **Be aware that these cached copies could contain malicious components if, for example, a virus was loaded.** These cached copies can be used for additional debugging on your end. For example, checking javascript that was loaded to determine a creative ID in another system.

## Remove a domain from our blocklist

We build our blocklists from a variety of sources both internal and external. Our team investigates each of these domains, which remain blocked if we are unable to contact the owner and determine the validity. If you feel a domain was incorrectly blocked, use our [Customer Support form](https://help.xandr.com/s/login/) to open a ticket (select "Anti-Malvertising" as the Request Type) and provide as many details as possible. For example, here are details that we need to investigate your ticket:

- What company owns this domain? What is their main business website, business address, and any other details?
- Direct contact for the owner of the domain (email is fine)

Once we have this information, we reach out to the owner to determine if the domain can be removed from our blocklist. As a matter of policy, we blocklist as soon as we see a potential problem and then complete the investigation. This is to ensure that both your publisher relationships and your reputation are protected.
