# wavefront-opentracing-sdk-python


![example workflow](https://github.com/wavefrontHQ/wavefront-opentracing-sdk-python/actions/workflows/main.yml/badge.svg)
[![OpenTracing Badge](https://img.shields.io/badge/OpenTracing-enabled-blue.svg)](http://opentracing.io)
[![image](https://img.shields.io/pypi/v/wavefront-opentracing-sdk-python.svg)](https://pypi.org/project/wavefront-opentracing-sdk-python/)
[![image](https://img.shields.io/pypi/l/wavefront-opentracing-sdk-python.svg)](https://pypi.org/project/wavefront-opentracing-sdk-python/)
[![image](https://img.shields.io/pypi/pyversions/wavefront-opentracing-sdk-python.svg)](https://pypi.org/project/wavefront-opentracing-sdk-python/)

## Table of Content
* [Requirements and Installation](#Requirements-and-Installation)
* [Usage](#Usage)
  * [Application Tags](#1-Set-Up-Application-Tags)
  * [WavefrontSender](#2-Set-Up-a-WavefrontSender)
  * [Reporter](#3-Set-Up-a-Reporter)
  * [WavefrontTracer](#4-Create-a-WavefrontTracer)
* [Span Logs](#Span-Logs)
* [Cross Process Context Propagation](#Cross-Process-Context-Propagation)
* [RED Metrics](#RED-Metrics)
* [License](#License)
* [How to Contribute](#How-to-Contribute)

# Welcome to Wavefront's Python SDK
This is the Wavefront by VMware OpenTracing SDK for Python that provides distributed tracing support for Wavefront.

The Wavefront OpenTracing SDK for Python automatically reports metrics, custom trace data, and derived metrics.

**Before you start implementing, let us make sure you are using the correct SDK!**


![Python Tracing SDK Decision Tree](docs/python_tracing_sdk.png)

> ***Note***:
> </br>
>   * **This is the Wavefront by VMware OpenTracing SDK for Python!**
>   If this SDK is not what you were looking for, see the [table](#wavefront-sdks) given below.
>   * See <a href="https://docs.wavefront.com/tracing_instrumenting_frameworks.html">instrument your application for tracing</a> for more information.

#### Wavefront SDKs

<table id="SDKlevels" style="width: 100%">
<tr>
  <th width="10%">SDK Type</th>
  <th width="45%">SDK Description</th>
  <th width="45%">Supported Languages</th>
</tr>

<tr>
  <td><a href="https://docs.wavefront.com/wavefront_sdks.html#sdks-for-collecting-trace-data">OpenTracing SDK</a></td>
  <td align="justify">Implements the OpenTracing specification. Lets you define, collect, and report custom trace data from any part of your application code. <br>Automatically derives Rate Errors Duration (RED) metrics from the reported spans. </td>
  <td>
    <ul>
    <li>
      <b>Java</b>: <a href ="https://github.com/wavefrontHQ/wavefront-opentracing-sdk-java">OpenTracing SDK</a> <b>|</b> <a href ="https://github.com/wavefrontHQ/wavefront-opentracing-bundle-java">Tracing Agent</a>
    </li>
    <li>
      <b>Python</b>: <a href ="https://github.com/wavefrontHQ/wavefront-opentracing-sdk-python">OpenTracing SDK</a>
    </li>
    <li>
      <b>Go</b>: <a href ="https://github.com/wavefrontHQ/wavefront-opentracing-sdk-go">OpenTracing SDK</a>
    </li>
    <li>
      <b>.Net/C#</b>: <a href ="https://github.com/wavefrontHQ/wavefront-opentracing-sdk-csharp">OpenTracing SDK</a>
    </li>
    </ul>
  </td>
</tr>

<tr>
  <td><a href="https://docs.wavefront.com/wavefront_sdks.html#sdks-for-collecting-metrics-and-histograms">Metrics SDK</a></td>
  <td align="justify">Implements a standard metrics library. Lets you define, collect, and report custom business metrics and histograms from any part of your application code.   </td>
  <td>
    <ul>
    <li>
    <b>Java</b>: <a href ="https://github.com/wavefrontHQ/wavefront-dropwizard-metrics-sdk-java">Dropwizard</a> <b>|</b> <a href ="https://github.com/wavefrontHQ/wavefront-runtime-sdk-jvm">JVM</a>
    </li>
    <li>
    <b>Python</b>: <a href ="https://github.com/wavefrontHQ/wavefront-pyformance">Pyformance SDK</a>
    </li>
    <li>
      <b>Go</b>: <a href ="https://github.com/wavefrontHQ/go-metrics-wavefront">Go Metrics SDK</a>
      </li>
    <li>
    <b>.Net/C#</b>: <a href ="https://github.com/wavefrontHQ/wavefront-appmetrics-sdk-csharp">App Metrics SDK</a>
    </li>
    </ul>
  </td>
</tr>

<tr>
  <td><a href="https://docs.wavefront.com/wavefront_sdks.html#sdks-that-instrument-frameworks">Framework SDK</a></td>
  <td align="justify">Reports predefined traces, metrics, and histograms from the APIs of a supported app framework. Lets you get started quickly with minimal code changes.</td>
  <td>
    <ul>
    <li><b>Java</b>:
    <a href="https://github.com/wavefrontHQ/wavefront-dropwizard-sdk-java">Dropwizard</a> <b>|</b> <a href="https://github.com/wavefrontHQ/wavefront-gRPC-sdk-java">gRPC</a> <b>|</b> <a href="https://github.com/wavefrontHQ/wavefront-jaxrs-sdk-java">JAX-RS</a> <b>|</b> <a href="https://github.com/wavefrontHQ/wavefront-jersey-sdk-java">Jersey</a></li>
    <li><b>.Net/C#</b>:
    <a href="https://github.com/wavefrontHQ/wavefront-aspnetcore-sdk-csharp">ASP.Net core</a> </li>
    <!--- [Python](wavefront_sdks_python.html#python-sdks-that-instrument-frameworks) --->
    </ul>
  </td>
</tr>

<tr>
  <td><a href="https://docs.wavefront.com/wavefront_sdks.html#sdks-for-sending-raw-data-to-wavefront">Sender SDK</a></td>
  <td align="justify">Lets you send raw values to Wavefront for storage as metrics, histograms, or traces, e.g., to import CSV data into Wavefront.
  </td>
  <td>
    <ul>
    <li>
    <b>Java</b>: <a href ="https://github.com/wavefrontHQ/wavefront-sdk-java">Sender SDK</a>
    </li>
    <li>
    <b>Python</b>: <a href ="https://github.com/wavefrontHQ/wavefront-sdk-python">Sender SDK</a>
    </li>
    <li>
    <b>Go</b>: <a href ="https://github.com/wavefrontHQ/wavefront-sdk-go">Sender SDK</a>
    </li>
    <li>
    <b>.Net/C#</b>: <a href ="https://github.com/wavefrontHQ/wavefront-sdk-csharp">Sender SDK</a>
    </li>
    <li>
    <b>C++</b>: <a href ="https://github.com/wavefrontHQ/wavefront-sdk-cpp">Sender SDK</a>
    </li>
    </ul>
  </td>
</tr>
</tbody>
</table>


## Requirements and Installation

This SDK supports Python 3.x.

```bash
pip install wavefront-opentracing-sdk-python
```

## Usage

[Tracer](https://github.com/opentracing/specification/blob/master/specification.md#tracer) is an OpenTracing interface for creating spans and propagating them across arbitrary transports.

This SDK provides a `WavefrontTracer` to create spans and send them to Wavefront. The `WavefrontTracer` also automatically generates and reports [RED metrics](https://github.com/wavefrontHQ/wavefront-sdk-doc-sources/blob/master/common/metrics.md#red-metrics) from your spans.

Follow these steps to create a `WavefrontTracer`:
1. [Create an `ApplicationTags` instance](#1-Set-Up-Application-Tags), to specify metadata about your application.
2. [Create a `WavefrontSender` instance](#2-Set-Up-a-WavefrontSender) to send trace data to Wavefront.
3. [Create a `WavefrontSpanReporter` instance](#3-Set-Up-a-Reporter) to report trace data to Wavefront.
4. [Create the `WavefrontTracer` instance](#4-Create-a-WavefrontTracer).


The following code sample creates a Tracer. For the details of each step, see the sections below.

```python
tracer = WavefrontTracer(reporter=reporter, application_tags=application_tags)
```

### 1. Set Up Application Tags

Application tags describe the structure of your application. They are included with every span reported to Wavefront and are associated with span tags that you can use to filter and query trace data in Wavefront.

You encapsulate application tags in an `ApplicationTags` object.
See [Instantiating ApplicationTags](https://github.com/wavefrontHQ/wavefront-sdk-doc-sources/blob/master/python/applicationtags.md).


### 2. Set Up a WavefrontSender

A `WavefrontSender` object implements the low-level interface for sending data to Wavefront. You can choose to send data using the [Wavefront proxy](https://docs.wavefront.com/proxies.html) or [direct ingestion](https://docs.wavefront.com/direct_ingestion.html).

* If you have already set up a `WavefrontSender` for another SDK that runs in the same process, use that one. (For details about sharing a Wavefront sender, see [Share a Wavefront Sender](https://github.com/wavefrontHQ/wavefront-sdk-doc-sources/blob/master/python/wavefrontsender.md#share-a-wavefront-sender).

* Otherwise, [Set Up a Wavefront Sender](https://github.com/wavefrontHQ/wavefront-sdk-doc-sources/blob/master/python/wavefrontsender.md#set-up-a-wavefront-sender).


### 3. Set Up a Reporter
You must create a `WavefrontSpanReporter` to report trace data to Wavefront. Optionally, you can create a `CompositeReporter` to send data to Wavefront and to print to the console.

#### Create a WavefrontSpanReporter
To create a `WavefrontSpanReporter`:
* Specify the Wavefront sender from [Step 2](#2-set-up-a-wavefront-sender), i.e. either `WavefrontProxyClient` or `WavefrontDirectClient`.
* (Optional) Specify a string that represents the source for the reported spans. If you omit the source, the host name is used.

Example: Create a `WavefrontSpanReporter`:

```python
import wavefront_opentracing_sdk.reporting
from wavefront_sdk import WavefrontDirectClient
  # or
  # from wavefront_sdk import WavefrontProxyClient

wavefront_sender = ...   # see Step 2

wf_span_reporter = wavefront_opentracing_sdk.reporting.WavefrontSpanReporter(
    client=wavefront_sender,
    source='wavefront-tracing-example'   # optional nondefault source name
)

# To get failures observed while reporting.
total_failures = wf_span_reporter.get_failure_count()
```

> **Note:** After you initialize the `WavefrontTracer` with the `WavefrontSpanReporter` (below), completed spans are automatically reported to Wavefront.
> You do not need to start the reporter explicitly.

#### Create a CompositeReporter (Optional)
A `CompositeReporter` enables you to chain a `WavefrontSpanReporter` to another reporter, such as a `ConsoleReporter`. A console reporter is useful for debugging.

```python
from wavefront_opentracing_sdk.reporting import CompositeReporter
from wavefront_opentracing_sdk.reporting import ConsoleReporter
from wavefront_opentracing_sdk.reporting import WavefrontSpanReporter

wf_span_reporter = ...

# Create a console reporter that reports span to stdout
console_reporter = ConsoleReporter(source='wavefront-tracing-example')

# Instantiate a composite reporter composed of console and WavefrontSpanReporter.
composite_reporter = CompositeReporter(wf_span_reporter, console_reporter)
```

### 4. Create a WavefrontTracer

To create a `WavefrontTracer`, you pass the `ApplicationTags` and `Reporter` instances you created in the previous steps:

```python
import wavefront_opentracing_sdk

from wavefront_opentracing_sdk.reporting import WavefrontSpanReporter
from wavefront_sdk.common import ApplicationTags
from wavefront_sdk import WavefrontDirectClient
  # or
  # from wavefront_sdk import WavefrontProxyClient

application_tags = ...   # see Step 1 above
wf_span_reporter = ...   # see Step 3 above

# Construct Wavefront opentracing Tracer
tracer = wavefront_opentracing_sdk.WavefrontTracer(
    reporter=wf_span_reporter,
    application_tags=application_tags)
```

#### Add Custom Span-Level RED metrics

Optionally, you can propagate custom span-level tags to RED metrics. See [Custom Span-Level Tags for RED Metrics](https://docs.wavefront.com/trace_data_details.html#custom-span-level-tags-for-red-metrics) for details.

```python
# Construct Wavefront opentracing Tracer
tracer = wavefront_opentracing_sdk.WavefrontTracer(
    reporter=wf_span_reporter,
    application_tags=application_tags,
    red_metrics_custom_tag_keys={'env', 'location'})
```

#### Close the Tracer
Always close the tracer before exiting your application to flush all buffered spans to Wavefront.

```python
tracer.close()
```

## Span Logs

You can instrument your application to emit logs or events with spans, and examine them from the [Wavefront Tracing UI](https://docs.wavefront.com/tracing_ui_overview.html#drill-down-into-spans-and-view-metrics-and-span-logs).

Use the [OpenTracing Span object's log_kv() method](https://opentracing-python.readthedocs.io/en/latest/api.html#opentracing.Span.log_kv) in your application.


## Cross Process Context Propagation
See the [context propagation documentation](https://github.com/wavefrontHQ/wavefront-opentracing-sdk-python/tree/master/docs/contextpropagation.md) for details on propagating span contexts across process boundaries.

## RED Metrics

See the [RED metrics documentation](https://github.com/wavefrontHQ/wavefront-sdk-doc-sources/blob/master/common/metrics.md#red-metrics) for details on the out-of-the-box metrics and histograms that are provided.

## License
[Apache 2.0 License](LICENSE).

## How to Contribute

* Reach out to us on our public [Slack channel](https://www.wavefront.com/join-public-slack).
* If you run into any issues, let us know by creating a GitHub issue.
