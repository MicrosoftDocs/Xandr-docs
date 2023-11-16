---
title: Microsoft Curate - Create Event Code Manually
description: The article describes how you can manually create event code based on a template and deploy it on your website.
---
# Create event code manually

You can manually create event code based on a template and deploy it on your website.

Use the following template to create the code for your standard event,
where:

- *EventName* is the name for your event
- *UUID* is the unique ID for your pixel as shown in the Xandr UI

See [Standard Events and Parameters](standard-events-and-parameters.md)

```
<script> 
     pixie('event', 'EventName'); 
</script> 

<noscript>
     <img width="1" height="1" style="display:none;" 
     src="//ib.adnxs.com/pixie?pi=UUID&e=EventName&script=0" />
</noscript>
```

## Related topics

- [Universal Pixel Code Structure](universal-pixel-code-structure.md)
- [Standard Events and Parameters](standard-events-and-parameters.md)
- [Create Custom Events and Parameters](create-custom-events-and-parameters.md)