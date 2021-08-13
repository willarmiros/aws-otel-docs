<!--This piece of documentation should exist for all supported languages in ADOT. It outlines how to perform manual instrumentation for tracing. The documentation that ends up on aws-otel.github.io should match this structure.-->

# Tracing with the AWS Distro for OpenTelemetry {Lanuage} SDK

## Introduction

1-2 paragraphs. Scope of this guide, and explanation of how ADOT SDK and X-Ray interact.

Optional diagram of ADOT and X-Ray components.

## Requirements

{Minimum supported language version} or later is required to run an application using OpenTelemetry

Note: You’ll also need to have the [ADOT Collector](https://aws-otel.github.io/docs/getting-started/collector) running to export traces to X-Ray.

## Installation

Commands or links to download and install the following packages and their dependencies:

* X-Ray ID Generator
* X-Ray propagator
* OTel SDK for tracing
* OTel API for tracing
* OTLP GRPC exporter

If necessary (depending on language/build system), include how to add these dependencies to their build files.

## Setting up the Global Tracer

### Sending Traces to AWS X-Ray

Explain how to instantiate a new tracer provider and provide it with the X-Ray ID generator, X-Ray propagator, and OTLP exporter pointing to the collector's address.

```
code sample of setting up the tracer provider with above components
```

### Using the AWS resource Detectors

How to install the AWS Resource detectors dependency (if it's already included with ID generator/propagator, you can explain that).

The ADOT {language} SDK supports automatically recording metadata in EC2, Elastic Beanstalk, ECS, and EKS environments.

```
code snippet for adding EC2 detector
```

To see what attributes are captured and how to add other resource detectors, see the OpenTelemetry documentation (should link to upstream docs for resource detectors).

### Logging

Document how to provide your own logger & change log level.

```
sample code for substituting in a custom logger and changing log level
```

## Instrumenting an Application

**Warning: Some instrumentations are not yet stable and the attributes they collect are subject to change until the instrumentation reaches 1.0 stability. It is recommended to pin a specific version of an instrumentation**

OpenTelemetry provides a wide range of instrumentations for popular {language} libraries. Instrumenting a library means that every time the library is used to make or handle a request is automatically wrapped with a populated span.

### Instrumenting Incoming Requests

How to install the instrumentation library at a pinned version (if not yet stable). This would be for the popular server frameworks that OTel supports.

Explain and include a code sample for at least 1 of the most popular ways of instrumenting incoming requests to a server. *This can be a link to the upstream's instrumentation documentation*.

Ideally, we should include several libaries if we're just linking to upstream.

### Instrumenting the AWS SDK

How to install the instrumentation library at a pinned version (if not yet stable).

Explain how to instrument the AWS SDK (both versions if applicable). Include a link to the upstream documentation. This section should *not* just be a link because it's the AWS SDK, which should have 1st-class support.

```
Code snippet for adding AWS SDK instrumentation
```

### Instrumenting HTTP Libraries

Link to the upstream's instrumentation documentation for the language's native HTTP client and/or popular HTTP clients, depending on common practices for the language.

### Instrumenting SQL Libraries

Link to the upstream's instrumentation documentation for MySQL, Postgres, and other popular ORMs or SQL libraries.

## Custom Instrumentation

### Creating Custom Spans

You can use custom spans to monitor the performance of internal activities that are not captured by instrumentation libraries. Note that only spans of kind `Server` are converted into X-Ray segments, all other spans are converted into X-Ray subsegments. For more on segments and subsegments, see the [AWS X-Ray developer guide](https://docs.aws.amazon.com/xray/latest/devguide/xray-concepts.html#xray-concepts-segments).

```
code snippet for starting a Server span, with comment saying it will become an X-Ray segment.

code snippet for starting an Internal (default) span, with comment saying it will become an X-Ray subsegment.
```

### Adding custom attributes

You can also add custom key-value pairs as attributes onto your spans. If you add special prefixes to these attributes, they will be automatically converted to metadata or annotations in the X-Ray backend. To read more about X-Ray annotations and metadata see the [AWS X-Ray Developer Guide](https://docs.aws.amazon.com/xray/latest/devguide/xray-concepts.html#xray-concepts-annotations).

```
code snippet for adding metadata & annotation attributes
```

### Multi-Threaded Applications

This section is optional but can describe any considerations that developers should take into account if they are instrumenting a multi-threaded or asynchronous application.

## Sample Application

This section can be formatted in whatever way makes sense to the sample app developer. You can even just link to the sample app's repository with a README for instructions on deploying it. The instructions should walk through the end-to-end setup of an application which at a minimum is a server that accepts HTTP requests and makes downstream HTTP and AWS SDK requests.
