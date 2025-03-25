---
title: RTSS Limitations
description: Explore the Real-Time Signals Service (RTSS) limitations and use cases that don't work well with RTSS.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Real-Time Signals Service (RTSS) limitations

This section describes situations and use cases that don't work well with RTSS.

## Target retrievals via segment ID

Currently, there's no way to retrieve all targets associated with a segment. Keep track of all targets uploaded to a segment. Alternatively, you can use the RTSS API service to make `GET` calls and check whether a single target belongs to a particular segment.

## Anti-targeting

Because of the way RTSS works, exclusion targeting is not a good fit. If there is a cache miss for a specific target that has not come through on an impression yet, RTSS looks in the database to see if this target exists, and then loads it into the cache for the next time it sees that impression. For that initial impression, RTSS will skip adding the anti-target segments, and the anti-target will not work. We do not currently recommend using RTSS in this scenario.
