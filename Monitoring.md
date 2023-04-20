# Monitoring 

Good monitoring should provide:

- The state of the world, from the top (the business) down
- Assistance in fault diagnostics
- A source of information for infrastructure, application development, and business 

And it should be:

- Built into design and the life cycle of application development and deployment.
- Automated and provided as self-service, where possible.

Consists of: 

- performance analysis
- capacity planning
- incident response 
- failure detection

## Types of monitoring data

That data primarily takes two forms:

- Metrics — Most modern monitoring tools rely most heavily on metrics to help us understand what’s going on in our environments. Metrics are stored as time series data that record the state of measures of your applications. We’ll see more about this shortly.
- Logs — Logs are (usually textual) events emitted from an application. While they’re helpful for letting you know what’s happening, they’re often most useful for fault diagnosis and investigation. 


## Types of metrics

- Gauges are numbers that are expected to go up or down. A gauge is essentially a snapshot of a specific measurement.
- Counters are numbers that increase over time and never decrease. Although they never decrease, counters can sometimes reset to zero and start incrementing again.
- Histogram is a metric that samples observations. This is a frequency distribution of a dataset. You group data together, a process called “binning”, and present the groups in a such a way that their relative sizes are visualized. Each observation is counted and placed into buckets. This results in multiple metrics: one for each bucket, plus metrics for the sum and count of all values.


## USE Method

For every resource, check utilization, saturation, and errors. The method is most effective for the monitoring of resources that suffer performance issues under high utilization or saturation.

- A resource - A component of a system. In Traditionally a physical server component like CPUs, disks, etc., but many folks also include software resources in the definition.
- Utilization - The average time the resource is busy doing work. It’s usually expressed as a percentage over time.
- Saturation - The measure of queued work for a resource, work it can’t process yet. This is usually expressed as queue length.
- Errors - The scalar count of error events for a resource.

## Four Golden Signals

The Google Four Golden Signals come out of the Google SRE book. They take a similar approach to the USE Method, specifying a series of general metric types to monitor. Rather than being system-level-focused time series, the metric types in this methodology are more application or user-facing:

- Latency - The time taken to service a request, distinguishing between the latency of successful and failed requests. A failed request, for example, might return with very low latency skewing your results.
- Traffic - The demand on your system—for example, HTTP requests per second or transactions for a database system.
- Errors - The rate that requests fail, whether explicit failures like HTTP 500 errors, implicit failures like wrong or invalid content being returned, or policy-based failures—for instance if you’ve mandated that failures over 30ms should be considered errors.
- Saturation - The “fullness” of your application or the resources that are constraining it—for example, memory or IO. This also includes impending saturation, such as a rapidly filling disk.

## RED method

With the RED method, three key metrics are instrumented that monitor
every microservice in your architecture:
(Request) Rate – the number of requests, per second, your
services are serving.
(Request) Errors – the number of failed requests per second.
(Request) Duration – The amount of time each request takes
expressed as a time interval.

## Alerts and notifications

Alerts and notifications are the primary output from monitoring tools. An alert is raised when something happens—for example, when a threshold is reached. This, however, doesn’t mean anyone’s been told about the event. That’s where notifications come in. A notification takes the alert and tells someone or something about it: an email is sent, an SMS is triggered, a ticket is opened, or the like.

To build a good notification system you need to consider the basics of:

- What problems to notify on.
- Who to tell about a problem.
- How to tell them.
- How often to tell them.
- When to stop telling them, do something else, or escalate to someone else.

Monitoring framework should focus on:

- Making notifications actionable, clear, and articulate. Just the use of notifications written by humans rather than by computers can make a significant difference in the clarity and utility of those notifications.
- Adding context to notifications. Send notifications that contain additional information about the component we’re notifying on.
- Only sending those notifications that make sense.

