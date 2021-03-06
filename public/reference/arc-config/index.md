# Lambda function configuration

> ## `config.arc`, `config.json`, `config.yaml`, `config.toml`


## Overview

Configure individual Lambda function properties within a given function's config file (e.g. `src/http/get-index/config.arc`), or globally for all functions within your project manifest.

- `runtime` - Officially supported: one of `nodejs12.x` (default), `nodejs10.x`, `deno`, `python3.7`, `python3.6`, or `ruby2.5`, etc.
  - Also configurable, but not officially supported by Architect: `java8`, `go1.x`, `dotnetcore2.1`
- `memory` - number, between `128`MB and `3008`MB in 64 MB increments
  - Memory size also directly correlates with CPU speed; higher memory levels are available in more capable Lambda clusters
- `timeout` - number, in seconds (max `900`)
- `concurrency` - number, `0` to AWS account maximum (if not present, concurrency is unthrottled)
- `layers` - Up to 5 Lambda layer ARNs; **must be in the same region as deployed**
- `policies` - Additional Lambda role policy ARNs

> Note: any function configurations made globally in your project manifest will be overridden by individual functions. For example, if your `app.arc` includes `memory 128`, and `src/http/get-index/config.arc` includes `memory 3008`, all functions except `get /` will be configured with 128MB of memory, while `get /` will override that global with 3008MB.

Example:

```arc
@aws
runtime python3.7
memory 256
timeout 3
concurrency 1
layers {ARN}
policies {ARN}
```

To use multiple layers or policies:

```arc
@aws
runtime python3.7
memory 256
timeout 3
concurrency 1
layers
  {ARN1}
  {ARN2}
  {ARN3}
policies
  {ARN4}
  {ARN5}
  {ARN6}
```

Read more about the [Lambda limits](https://docs.aws.amazon.com/lambda/latest/dg/limits.html) and [resource model](https://docs.aws.amazon.com/lambda/latest/dg/resource-model.html).

---

## Next: [Setup AWS region & profile with `@aws`](/reference/arc/aws)
