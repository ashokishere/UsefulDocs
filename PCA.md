Service Level Object(SLO) – target value or range for an SLI

SLI - Latency
SLO – Latency < 100ms
SLI – availability
SLO – 99.9% uptime

SLOs should be directly related to the customer experience. The main purpose of the SLO is to quantify reliability of a product to a customer

For SLOs it maybe tempting to set them to aggressive values like 100% uptime however this will come at a higher cost
The goal is not to achieve perfection but instead to make customers happy with the right level of reliability
If a customer is happy with 99% reliability increasing it any further doesn’t add any other value

Service Level Agreement(SLA) – contract between a vendor and a user that
guarantees a certain SLO The consequences for not meeting any SLO can be financial based but can also
be variety of other things as well


Prometheus is an open-source monitoring tool that collects metrics data,
and provide tools to visualize the collected data
In addition, Prometheus allows you to generate alerts when metrics reach
a user specified threshold
Prometheus collects metrics by scraping targets who expose metrics
through an HTTP endpoint
Scraped metrics are then stored in a time series database which can be
queried using Prometheus’ built-in query language PromQl

Prometheus is designed to monitor time-series data that is numeric
Prometheus is primarily written GoLang
SounCloud to Open Source

Prometheus Monitor?

• CPU/Memory Utilization
• Disk space
• Service Uptime
• Application specific data
• Number of exceptions
• Latency
• Pending Requests




What type of data should Prometheus not monitor
• Events
• System logs
• Traces


<img width="1185" alt="image" src="https://github.com/ashokishere/UsefulDocs/assets/46769524/ca915f41-5ab9-484e-b37f-4a3d715589de">


Prometheus collects metrics bysending http requests to /metrics endpoint of each target
Prometheus can be configured to use a different path other then /metrics

Exporters collect metrics and expose them in a format Prometheus expects

Prometheus has several native exporters
• Node exporters(Linux servers)
• Windows
• MySQL
• Apache
• HAProxy


Prometheus comes with client librariesthat allow you to expose anyapplication metrics you need Prometheus to track 

Language support:
• Go
• Java
• Python
• Ruby
• Rust

pull based model like (Zabix ,nagios)

In a pushed based model, the targets are configured to push the metric data to the metrics server
 
Pushed based systems include:
• Logstash
• Graphite
• OpenTSDB


Some of the benefits of using a pull based system:
• Easier to tell if a target is down
• In a pushed based system we don’t know if its down or has
been decommissioned
• Push based systems could potentially overload metrics server if too
many incoming connections get flooded at same time
• Pull based systems have a definitive list of targets to monitor,
creating a central source of truth


Push based monitoring excels in the following areas:
• event-based systems, pulling data wouldn’t be a viable option
• However, Prometheus is for collecting metrics and not monitoring
events
• Short lived jobs, as they may end before a pull can occur
• Prometheus has feature called Pushgateway to handle this
situation

Promtools is a utility tool shipped with Prometheus that can be used to:
• Check and validate configuration
• Validate Prometheus.yml
• Validate rules files
• Validate metrics passed to it are correctly formatted
• Can perform queries on a Prometheus server
• Debugging & Profiling a Prometheus server
• Perform unit tests against Recording/Alerting rules


Counter

✓ How many times did X happen
✓ Number can only increase
    Total #requests
    Total #Exceptions
    Total # ofjobexecutions


Gauge
✓ What is the current value of X
✓ Can go up or down

Current CPU Utilization
Available System Memory
Number of concurrent requests

Histogram
✓ How long or how big something is
✓ Groups observations into configurable bucket sizes
  Response time
  Request size

Docker Engine metrics 

  How much cpu does docker use
  
✓ Total number of failed image builds
✓ Time to process container actions
✓ No metrics specific to a container

cAdvisor metrics

How much cpu/mem does each

container use
✓ Number of processes running inside a container
✓ Container uptime
✓ Metrics on a per container basis

What is PromQL
✓ Short for Prometheus Query Language
✓ Main way to query metrics within Prometheus
✓ Data returned can be visualized in dashboards
✓ Used to build alerting rules to notify administrators


Expression Data Structure

• Selectors & modifiers
• Operators & Functions
• Vector Matching
• Aggregators
• Subqueries
• Histogram/Summary


String – a simple string value (currently unused)
✓ Scalar – a simple numeric floating point value
✓ Instant Vector – set of time series containing a singlesample for each time series, all sharing the same timestamp
     
✓ Range Vector – set of time series containing a range of data points over time for each time series


To get historic data use an offset modifier after the label matching

$ node_memory_Active_bytes{instance=“node1”} offset 5m


Suffix Meaning

ms Milliseconds
s Seconds
m Minutes
h Hours
d Days
w Weeks
y Years, which have 365 days


PromQL has 3 logical operators

OR
AND
UNLESS
Unless operator results in a vector consisting of elements on the left side for which there are no elements on the right side


One-To-One vector matching – Every element in the vector onthe left of the operator tries to find a single matching element on the right

Many-To-One vector matching – each vector elements on the one side can match with multiple elements on the many side

Many-To-One is when each vector element on the one side can match with multiple elements on the many side


Aggregation operators, allow you to take an instant vector and aggregate its elements, resulting in a new instant vector, with fewer elements

Aggregator Description

Sum Calculate sum over dimensions
Min Select minimum over dimensions
Max Select maximum over dimensions
Avg Average over dimensions
Group All values in the resulting vector are 1
Stddev Calculate population standard deviations over dimensions
Stdvar Calculate population standard variance over dimensions
Count Count number of elements in the vector
Count_values Count number fo elements with same value
Bottomk Smallest k elements by sample value
Topk Largest k elements by sample value
Quantile calculate φ-quantile (0 ≤ φ ≤ 1) over dimensions


The without keyword does the opposite of by and
tells the query which labels not to include in the
aggregation


Instead we are more interested in the rate at which
a counter metric increases.
The rate() and irate() function provides the per
second average rate of change

rate

Looks at the first and last data points within a range
• Effectively an average rate over the range
• Best used for slow moving counters and alerting rules

irate

Looks at the last two data points within a ranged
• Instant rate
• Should be used for graphing volatile,
fast-moving counters


Make sure there is atleast 4 samples within a given time range, ideally
more.
• 15s scrape interval 60s window gives 4 samples
• When combining rate with an aggregation operator, always take rate()
first, then aggregate
• This is so rate() function can detect counter resets
• $ sum without(code,handler)(rate(http_requests_total[24h]))


Quantiles - determine how many values in a distribution are above or below a certain
limit
Quantiles represent percentiles.
90% quantile would mean at what value is 90 percent of the data less than


Alertmanager is responsible for receiving
© Copyright KodeKloud
alerts generated from Prometheus and
converting them into notifications.
These notifications can include, pages,
webhooks, email messages, and chat
messages
