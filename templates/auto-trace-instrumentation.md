<!-- This piece of documentation should exist only for ADOT SDKs that support some form of auto-instrumentation. It outlines how to use automatic instrumentation for tracing. The documentation that ends up on aws-otel.github.io should match this structure -->

# Tracing with the AWS Distro for OpenTelemetry {Language} Auto-Instrumentation and X-Ray

## Introduction

1-2 paragraphs. Scope of this guide, and explanation of how ADOT Auto-Instrumentation and X-Ray interact.

Optional diagram of ADOT and X-Ray components.

## Requirements

{Minimum supported language version} or later is required to run an application using OpenTelemetry

Note: You’ll also need to have the [ADOT Collector](https://aws-otel.github.io/docs/getting-started/collector) running to export traces to X-Ray.

## Installation

Commands or links to download and install the auto-instrumentation solution.

If necessary (depending on language/build system), include how to add these dependencies to their build files.

## Running an Application with Auto-Instrumentation

All instructions here should be completely zero-touch to the customer's code.

How to enable the auto-instrumentation for an application.

How to configure it to use the X-Ray ID generator and propagator.

How to enable resource detectors (if currently possible).

### Configuring Auto-Instrumentation

Describe any configurations via environment variable, command line option, or some other non-invasive method that might be relevant. Also include a link to the upstream documentation on how to configure auto-instrumentation.

## Using Manual Instrumentation

Describe any caveats for using manual instrumentation alongside auto-instrumentation. Link to the manual instrumentation docs.

## Sample Application

This should just link to the auto-instrumented sample app for this language in GitHub. There should be a README describing how to run it there.
