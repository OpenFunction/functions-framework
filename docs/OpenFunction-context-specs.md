# OpenFunction Context Specs

## Overview

### Statement

`Scope` indicates which functions-framework has already support this item.

#### functions-framework abbreviation

OpenFunction/functions-framework-go -> ff-go

## Context

| Key        | Type            | Description                                               | Scope                                                        | example                                |
| ---------- | --------------- | --------------------------------------------------------- | ------------------------------------------------------------ | -------------------------------------- |
| name       | string, require | Function name                                             | [ff-go](https://github.com/OpenFunction/functions-framework-go) | "myfunction", "hello-func"             |
| version    | string, require | Function version                                          | [ff-go](https://github.com/OpenFunction/functions-framework-go) | "v1", "v2"                             |
| request_id | string          | Request ID, uuid format                                   | [ff-go](https://github.com/OpenFunction/functions-framework-go) | "a0f2ad8d-5062-4812-91e9-95416489fb01" |
| protocol   | enum, require   | Function serving kind, see [Protocol](#protocol)          | [ff-go](https://github.com/OpenFunction/functions-framework-go) | "gRPC", "HTTP"                         |
| port       | string, require | Function serving port                                     | [ff-go](https://github.com/OpenFunction/functions-framework-go) | "8080", "50001"                        |
| input      | object          | Function input from bindings data, see [Input](#input)    | [ff-go](https://github.com/OpenFunction/functions-framework-go) |                                        |
| outputs    | object          | Function output to bindings data, see [Outputs](#outputs) | [ff-go](https://github.com/OpenFunction/functions-framework-go) |                                        |
| runtime    | enum, require   | Function serving runtime, see [Runtime](#runtime)         | [ff-go](https://github.com/OpenFunction/functions-framework-go) | "Knative", "Dapr"                      |
| state      | string          | Used to store the states of the function in operation     |                                                              |                                        |

### Protocol 

We currently support `HTTP` and `gRPC` protocol modes.

| Value | Description                         | Scope                                                        |
| ----- | ----------------------------------- | ------------------------------------------------------------ |
| HTTP  | Serving function with HTTP protocol | [ff-go](https://github.com/OpenFunction/functions-framework-go) |
| gRPC  | Serving function with gRPC protocol | [ff-go](https://github.com/OpenFunction/functions-framework-go) |

<div align="right">
    <b><a href="#context">↥ back to Context</a></b>
</div>

### Input

| Key        | Type   | Description                                                  | Scope                                           | example                                |
| ---------- | ------ | ------------------------------------------------------------ | -------------------------------------- | -------------------------------------- |
| name       | string | Input name. When using Dapr as runtime, this name needs to be consistent with the corresponding Dapr component resource name. Refer to [this docs](https://docs.dapr.io/concepts/components-concept/) to learn about Dapr components. | [ff-go](https://github.com/OpenFunction/functions-framework-go) | "demo-kafka", "cron-job" |
| enable | bool, require | Switch of input                              | [ff-go](https://github.com/OpenFunction/functions-framework-go) | true, false                |
| pattern | string | Input serving listening path. For HTTP functions, it can be set to "/somepath" while "somepath" for gRPC functions. This indicates the destination of the input data. | [ff-go](https://github.com/OpenFunction/functions-framework-go) | "echo", "/echo" |
| in_type | enum   | Input type. Effective only when using Dapr as runtime. See [InType](#intype) | [ff-go](https://github.com/OpenFunction/functions-framework-go) |                          |

#### InType

Effective only when using Dapr as runtime. 

| Value    | Description                                                  | Scope                                                        |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| bindings | Indicates that the input is the Dapr bindings component. Refer to [Bindings API reference](https://docs.dapr.io/reference/api/bindings_api/) to learn more about Dapr bindings components. | [ff-go](https://github.com/OpenFunction/functions-framework-go) |
| pubsub   | Indicates that the input is the Dapr pubsub component. Refer to [Pub/sub API reference](https://docs.dapr.io/reference/api/pubsub_api/) to learn more about Dapr bindings components. <br />:heavy_exclamation_mark:Note that when using pubsub as input, the name of pubsub's topic should be assigned to the input's pattern. | [ff-go](https://github.com/OpenFunction/functions-framework-go) |
| invoke   | Indicates that the input is the Dapr service invocation component. Refer to [Service invocation API reference](https://docs.dapr.io/reference/api/service_invocation_api/) to learn more about Dapr bindings components.<br />:heavy_exclamation_mark:Note that when using invoke as input, the name of invoke method should be assigned to the input's pattern. | [ff-go](https://github.com/OpenFunction/functions-framework-go) |

<div align="right">
    <b><a href="#context">↥ back to Context</a></b>
</div>

### Outputs

| Key            | Type          | Description                                                  | Scope                                                        | example     |
| -------------- | ------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ----------- |
| enable         | bool, require | Switch of outputs                                            | [ff-go](https://github.com/OpenFunction/functions-framework-go) | true, false |
| output_objects | map           | A map of Output objects. <br />The key is the name of output. When using Dapr as runtime, this name needs to be consistent with the corresponding Dapr component resource name. Refer to [this docs](https://docs.dapr.io/concepts/components-concept/) to learn about Dapr components. <br />The value is output object, see [Output](#output) | [ff-go](https://github.com/OpenFunction/functions-framework-go) |             |

#### Output

| Key      | Type   | Description                                                  | Scope                                                        | example                                     |
| -------- | ------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------- |
| pattern  | string | Output serving listening path. For HTTP functions, it can be set to "/somepath" while "somepath" for gRPC functions. This indicates the destination of the out data. | [ff-go](https://github.com/OpenFunction/functions-framework-go) | true, false                                 |
| out_type | enum   | Output type. Effective only when using Dapr as runtime. See [OutType](#outtype) | [ff-go](https://github.com/OpenFunction/functions-framework-go) |                                             |
| params   | map    | Used to store parameters when using output.                  | [ff-go](https://github.com/OpenFunction/functions-framework-go) | {"method": "post"}, {"operation": "create"} |

##### OutType

Effective only when using Dapr as runtime. 

| Value    | Description                                                  | Scope                                                        |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| bindings | Indicates that the output is the Dapr bindings component. Refer to [Bindings API reference](https://docs.dapr.io/reference/api/bindings_api/) to learn more about Dapr bindings components. | [ff-go](https://github.com/OpenFunction/functions-framework-go) |
| pubsub   | Indicates that the output is the Dapr pubsub component. Refer to [Pub/sub API reference](https://docs.dapr.io/reference/api/pubsub_api/) to learn more about Dapr bindings components. <br />:heavy_exclamation_mark:Note that when using pubsub as output, the name of pubsub's topic should be assigned to the output's pattern. | [ff-go](https://github.com/OpenFunction/functions-framework-go) |
| invoke   | Indicates that the output is the Dapr service invocation component. Refer to [Service invocation API reference](https://docs.dapr.io/reference/api/service_invocation_api/) to learn more about Dapr bindings components.<br />:heavy_exclamation_mark:Note that when using invoke as output, the name of invoke method should be assigned to the output's pattern. | [ff-go](https://github.com/OpenFunction/functions-framework-go) |

<div align="right">
    <b><a href="#context">↥ back to Context</a></b>
</div>

### Runtime

We currently support `Knative` and `Dapr` serving runtime.

| Value   | Description                           | Scope                                                        |
| ------- | ------------------------------------- | ------------------------------------------------------------ |
| Knative | Serving function with Knative runtime | [ff-go](https://github.com/OpenFunction/functions-framework-go) |
| Dapr    | Serving function with Dapr runtime    | [ff-go](https://github.com/OpenFunction/functions-framework-go) |

<div align="right">
    <b><a href="#context">↥ back to Context</a></b>
</div>
