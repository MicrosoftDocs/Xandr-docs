---
title: Real Time Data Integrations Best Practices
description: Learn what are the best practices in real time data provider integrations, data provider bidder performance and Connection management. 
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: data-providers
ms.author: shsrinivasan
---

# Real time data integrations best practices

## Software stack best practices

Depending on the software stack that you decide to employ for your Data Provider, you will see a wide range of QPS performance. Having an optimal stack translates into better performing servers, which ultimately means you will need less servers to achieve the same performance.

- **Listener and application:** The listener should be used to listen to requests and the application should be processing the information in the requests; listener and application should be decoupled.
- **Recommended tech stacks:** The best performance we have seen is with LuaJIT, C, and C++ (with careful deterministic garbage collection) running on Nginx servers.Many have seen reduced timeout rates by switching to Nginx servers.
- **Non-recommended tech stacks:** We don't recommend using interpreted languages such as PHP or Python. We also don't recommend using Java (tomcat, jetty, custom) or other languages where there is non-deterministic garbage collection timing.
- **I/O:** Your solution should avoid any kind of disk I/O as it is slow and response times are random, which can easily saturate the disk, so try to have all logging done to RAM. If you must write to disk, we suggest you write to /dev/shm/filename and roll the file over every couple of minutes with a cronscript that compresses the file and moves it to disk. Run the compress at lower priority, for example,10 gzip, to help avoid CPU contention.
- **Cross CPU scheduling:** To avoid cross CPU scheduling issues, we have seen good results when using CPU affinity to keep the worker process (and it's threads) on a single CPU. We have seen this significantly increase performance when implemented while running one worker per CPU.

## Data provider bidder performance best practices

Having the appropriate targets for performance metrics (response times, timeout rates) is key to guiding your data provider to be successfully integrated on our platform.

- **Response time:** You should engineer your solution to respond to bid requests within 7 milliseconds or less as opposed to 10 milliseconds. This will ensure that your solution accounts for jitter latency.
- **Timing out:** You must aim to approach a 0% timeout rate (actually reaching no timeouts is not possible due to jitter latency). Your bidder times out when it has failed to respond to a bid request from the impression bus within 10 milliseconds of the request being sent. If you time out, the impression bus will close the connection and re-open the next time it has an impression (basically instantly). This close/open thrashing will usually cause a lot of load on the box and thus more timeouts and a cascade failure of thrashing. **Build your application so that it always responds within ~7ms with segment codes or a new line.**
- **Stress testing:** As you initiate your integration, set the pass through percentage of your bidder (through the `passthrough_percent` field of your bidder profile) to 1% and slowly increase it as you see that your bidder approaches a 100% response rate.

## Connection management best practices

Properly managing connections will be extremely important in helping your data provider effectively manage the formidable traffic levels that the impression bus sends your way.

- **Monitoring connections:** Measuring the number of ESTABLISHED vs TIME_WAIT sockets is a good way to study your server's timeouts. Use this script substituting '8080' with your port:

  `netstat -na | grep ':8080 ' | awk '{ print $NF }' | sort | uniq -c`

Good performance is indicated by mostly ESTABLISHED sockets whereas mostly TIME_WAIT sockets indicate timeouts and a cascading failure of thrashing.

- **Connection metrics:** The best metric for monitoring connections is queries/connections as opposed to connections/second.
- **Keep-Alive protocol:** You should be supporting Keep-Alive protocol and trying to keep connections open as long as possible. Typically we see 300 queries per connection, meaning that if you are closing the connection, you will see 300x more opens/closes. You should be returning "Connection: keep-alive" in your response headers.
