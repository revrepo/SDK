**RevAPM's Acceleration SDK**

Quick Start Guide Can be found here: https://revapm.zendesk.com/hc/en-us/categories/201142933-RevSDK

Self Service for SDK key can be found here: https://portal.revapm.net/#/signup/plans

RevAPM's Website: https://www.revapm.com/

**Introduction**

<span style="font-weight: 400;">The Rev Mobile  SDK is a simple way to connect a mobile application to Rev's global content acceleration and analytics platform.</span>

<span style="font-weight: 400;">The Rev Mobile SDK (Software Development Kit) is a set of libraries that provide the means necessary to report and accelerate the delivery of content to applications running on mobile devices. The Rev SDK utilizes a specially designed set of networking protocols to provide acceleration to a given mobile application.  Network traffic that is normally directed to and from the mobile App is sent through the Rev SDK, which utilizes Rev’s global network to accelerate the App’s traffic.</span>**

<span style="font-weight: 400;">The SDK can function utilizing  either of two Rev-optimized protocols – an UDP-based protocol RMP (Rev Mobile Protocol) or TCP-based protocol DOTS (Dynamically Optimized Transport System) to transfer the content over the wireless network. The SDK determines, which protocol provides better performance for that particular App, device, and wireless network at that moment in time. Once the appropriate protocol is selected, the protocol then senses network, device and App conditions, and adapts its own behavior in real time to provide the fastest possible transfer of data overall.</span>

<span style="font-weight: 400;">The Rev SDK communicates with the Rev server in the Rev network, maintaining the flow of content, and monitoring and reporting on the operation of the SDK while sending performance data reflecting data transfer rates, bandwidth, latencies, etc. This raw data  is then forwarded to Rev log servers, and processed for reporting purposes. Processed data is then forwarded to the Rev analytics backend  service, where the performance information is made available to Rev customers via the API or portal.  </span>

**Why is the SDK needed? **

**Performance**

<span style="font-weight: 400;">While cellular network operators claim that user bandwidth has been increased in 4G-LTE, there are some indications that in many cases the latency experienced by users has actually increased. Many analysts have concluded that these cellular networks are congested, resulting in high latencies and less bandwidth utilization than potentially available.</span>

<span style="font-weight: 400;">In any event, here is available and unused bandwidth in most cellular networks, even while congested, and much of this is due to inefficiencies of conventional TCP and peculiarities of the cellular network as described in part in the following sections. What is needed is a properly designed networking protocol that can adaptively and intelligently navigate through these networks and utilize the unused bandwidth, and thereby decrease total round-trip delays.</span>

**<span style="font-weight: 400;">The Rev SDK helps mitigate the impact of congestion by using and optimizing UDP and TCP for the acceleration of content.   </span>**

The SDK provides the following transport enhancements:

1.  <span style="font-weight: 400;">Optimized data transport -- for faster speeds in both downlink and uplink directions</span>
2.  <span style="font-weight: 400;">Reliable transport – detects and handles packet loss efficiently, orders packets properly</span>
3.  <span style="font-weight: 400;">Minimal protocol overhead -- for session establishment,both in connection start-up and in continuous operation</span>
4.  <span style="font-weight: 400;">No teardown of connection due to cellular radio state transitions (without ongoing power requirements) or transfers to neighboring cell sites</span>
5.  <span style="font-weight: 400;">TLS/SSL support using X.509v3 certificates</span>
6.  <span style="font-weight: 400;">Transparent penetration of cellular network middle-boxes -- operates without interference from middle boxes in the cellular network.</span>
7.  <span style="font-weight: 400;">Encryption/decryption of headers and payload as with SSL</span>

*   <span style="font-weight: 400;">Port “spoofing”</span>
*   <span style="font-weight: 400;">Session performance data can be recorded and utilized to optimize subsequent transport sessions to the same client</span>
*   <span style="font-weight: 400;">Header/payload compression</span>

9.  <span style="font-weight: 400;">Environment-agnostic performance improvements -- Operates equally well in wired environments, accelerating data transport over that provided by conventional TCP</span>

 **Visibility**

<span style="font-weight: 400;">Another problem the Rev SDK solves is the lack of end-to-end visibility of an App’s performance. Rev provides this visibility by combining network, transactions and device metric and analytics into a single interface.   </span>

<span style="font-weight: 400;">The Rev mobile analytics interface offer reporting dashboards for daily active users (DAU), monthly active users (MAU) and average request time (processing). There are multiple pie charts which will display user count, request count and gigabytes transferred.  The pie charts can be available for geographies, mobile devices, operating systems and per carrier.   Also available is the ratio between Wi-Fi and cellular networks.</span>

<span class="c1">Top-object reports for the following aggregations:</span>

*   Top requests
*   Top objects with slowest response time
*   Top objects with slowest TTFB
*   Top objects with 404 responses
*   Top objects with 5xx responses
*   Top objects with cache misses
*   <span class="c1">Top objects with completion failures</span> 

**How it works**

Once the SDK is compiled into the App, the Rev SDK has three operating modes: Report, Transfer, and Transfer Plus Report.

When the mode is set to Transfer, the SDK works by intercepting NSURL calls. AFNetworking, NSCache, RestKit as well as anything built on NSurl will all be intercepted. The SDK allows configuration for what domains and/or sites are intercepted. By default, all requests are intercepted and sent to the Rev edge using DOTS or RMP.

The SDK reporting function will report numerous App, wireless and handset details. The amount of reporting is configurable via the Rev Portal or API. The controls at a high level are for handset reporting interval, log level and number of requests per report. Reporting interval is the period of time between when the analytics are sent to the device. The log level is the levels of detail with debug level being the most detailed. The number of requests per report is the number of user data requests is performed before sending the analytics to Rev.

There are three separate data streams between the Rev edge and the handset. This is shown in Figure 1\. The data path for the App data is the first. This uses Rev’s RMP or DOTS for acceleration of the content delivery. The second data stream is the SDK control telemetry. Using the Rev portal or APIs, different configuration parameters can be sent to the Rev SDK over this stream. The controls are for reporting, data interception and other SDK features. Last data stream is for analytics. The analytics are sent from the handset to the Rev edge, collected and combined with the proxy HTTP log data, thus providing end-to-end visibility.

 ![](https://revapm.zendesk.com/hc/en-us/article_attachments/202442846/image00.png)

Detailed last mile diagram - Figure 1

The control and analytics streams are sent to the Rev backend.While App data stream is set to the Rev edge, depending on the request, the requested object may be a cache hit, dynamic which is requested from origin or pulled from a 3<span class="c2">rd</span> party provider.

For non-dynamic content, Rev does offer edge caching and the ability for custom VCL rules for complex applications. Rev supports instant purging of objects via the Rev portal and APIs. 3<span class="c2">rd</span> party content can also be pulled depending on the configuration of the SDK.  By default, all requests, including 3<span class="c2">rd</span> party requests sent to the Rev edge where the objects are requested from their origin(s). Rev will cache 3<span class="c2">rd</span> party objects based on the cache headers of the specific object. The end to end data flow can be seen in Figure 2.

![](https://revapm.zendesk.com/hc/en-us/article_attachments/202442856/image01.png)

  End-to-End diagram - Figure 2
