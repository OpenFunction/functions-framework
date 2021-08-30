# OpenFunction Context Specs

## Overview

### Statement

`Scope` indicates which functions-framework has already support this item.

#### functions-framework abbreviation

OpenFunction/functions-framework-go -> ff-go

OpenFunction/functions-framework-nodejs -> ff-js

## Context

Example:

```json
{
  "name": "function",
  "version": "v1",
  "requestID": "a0f2ad8d-5062-4812-91e9-95416489fb01",
  "port": "50002",
  "input": {},
  "outputs": {},
  "runtime": "OpenFuncAsync",
  "state": ""
}
```

Specification:

| Key        | Type            | Description                                               | Scope                                                        | example                                |
| ---------- | --------------- | --------------------------------------------------------- | ------------------------------------------------------------ | -------------------------------------- |
| name       | string, require | Function name.                                            | [ff-go](https://github.com/OpenFunction/functions-framework-go) | "myfunction", "hello-func"             |
| version    | string, require | Function version.                                         | [ff-go](https://github.com/OpenFunction/functions-framework-go) | "v1", "v2"                             |
| requestID | string          | Request ID, uuid format.                                  | [ff-go](https://github.com/OpenFunction/functions-framework-go) | "a0f2ad8d-5062-4812-91e9-95416489fb01" |
| port       | string, require | Function serving port.                                    | [ff-go](https://github.com/OpenFunction/functions-framework-go) | "50001"                        |
| input      | object          | Function input from bindings data, see [Input](#input). Empty means no input. | [ff-go](https://github.com/OpenFunction/functions-framework-go), [ff-js](https://github.com/OpenFunction/functions-framework-nodejs) |                                        |
| outputs    | map        | Function output to bindings data. <br />A map of Output objects. The key is the name of output. When using OpenFuncAsync as runtime, this name needs to be consistent with the corresponding Dapr component resource name. Refer to [this docs](https://docs.dapr.io/concepts/components-concept/) to learn about Dapr components. <br />The value is output object, see [Output](#output). Empty means no output. | [ff-go](https://github.com/OpenFunction/functions-framework-go), [ff-js](https://github.com/OpenFunction/functions-framework-nodejs) |                                        |
| runtime    | enum, require   | Function serving runtime, see [Runtime](#runtime).       | [ff-go](https://github.com/OpenFunction/functions-framework-go) | "Knative", "OpenFuncAsync"       |
| state      | string          | Used to store the states of the function in operation.    |                                                              |                                        |

### Input

Example:

```json
{
  "name": "my_input",
  "uri": "my_topic",
  "params": {
    "type": "pubsub"
  }
}
```

Specification:

| Key        | Type   | Description                                                  | Scope                                           | example                                |
| ---------- | ------ | ------------------------------------------------------------ | -------------------------------------- | -------------------------------------- |
| name       | string | Input name. When using OpenFuncAsync as runtime, this name needs to be consistent with the corresponding Dapr component resource name. Refer to [this docs](https://docs.dapr.io/concepts/components-concept/) to learn about Dapr components. | [ff-go](https://github.com/OpenFunction/functions-framework-go), [ff-js](https://github.com/OpenFunction/functions-framework-nodejs) | "demo-kafka", "cron-job" |
| uri | string | Input serving listening path. This indicates the destination of the input data. | [ff-go](https://github.com/OpenFunction/functions-framework-go), [ff-js](https://github.com/OpenFunction/functions-framework-nodejs) | "echo" |
| params | map | Input params. When using OpenFuncAsync as runtime, you need to set the `type` (refer to [Input Type](#input-type)) parameter. | [ff-go](https://github.com/OpenFunction/functions-framework-go), [ff-js](https://github.com/OpenFunction/functions-framework-nodejs) | {"type": "pubsub"} |

#### Input Type

Effective only when using OpenFuncAsync as runtime. 

| Value    | Description                                                  | Scope                                                        |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| bindings | Indicates that the input is the Dapr bindings component. Refer to [Bindings API reference](https://docs.dapr.io/reference/api/bindings_api/) to learn more about Dapr bindings components. | [ff-go](https://github.com/OpenFunction/functions-framework-go) |
| pubsub   | Indicates that the input is the Dapr pubsub component. Refer to [Pub/sub API reference](https://docs.dapr.io/reference/api/pubsub_api/) to learn more about Dapr bindings components. <br />:heavy_exclamation_mark:Note that when using pubsub as input, the name of pubsub's topic should be assigned to the input's uri. | [ff-go](https://github.com/OpenFunction/functions-framework-go), [ff-js](https://github.com/OpenFunction/functions-framework-nodejs) |
| invoke   | Indicates that the input is the Dapr service invocation component. Refer to [Service invocation API reference](https://docs.dapr.io/reference/api/service_invocation_api/) to learn more about Dapr bindings components.<br />:heavy_exclamation_mark:Note that when using invoke as input, the name of invoke method should be assigned to the input's uri. | [ff-go](https://github.com/OpenFunction/functions-framework-go), [ff-js](https://github.com/OpenFunction/functions-framework-nodejs) |

<div align="right">
    <b><a href="#context">↥ back to Context</a></b>
</div>

### Outputs

Examples:

```json
{
  "my_output": {
    "uri": "print",
    "params": {
      "method": "post",
      "type": "invoke"
    }
  }
}
```

Specification:

#### Output

| Key    | Type   | Description                                                  | Scope                                                        | example                                     |
| ------ | ------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------- |
| uri    | string | Output serving listening path. This indicates the destination of the out data. | [ff-go](https://github.com/OpenFunction/functions-framework-go), [ff-js](https://github.com/OpenFunction/functions-framework-nodejs) | "echo"                                      |
| params | map    | When using OpenFuncAsync as runtime, you need to set the `type` (refer to [Output Type](#output-type)) parameter. <br />You also need to set other relevant parameters according to [Dapr's docs](https://docs.dapr.io/reference/api/). | [ff-go](https://github.com/OpenFunction/functions-framework-go), [ff-js](https://github.com/OpenFunction/functions-framework-nodejs) | {"method": "post"}, {"operation": "create"} |

##### Output Type

Effective only when using OpenFuncAsync as runtime. 

| Value    | Description                                                  | Scope                                                        |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| bindings | Indicates that the output is the Dapr bindings component. Refer to [Bindings API reference](https://docs.dapr.io/reference/api/bindings_api/) to learn more about Dapr bindings components. | [ff-go](https://github.com/OpenFunction/functions-framework-go) |
| pubsub   | Indicates that the output is the Dapr pubsub component. Refer to [Pub/sub API reference](https://docs.dapr.io/reference/api/pubsub_api/) to learn more about Dapr bindings components. <br />:heavy_exclamation_mark:Note that when using pubsub as output, the name of pubsub's topic should be assigned to the output's uri. | [ff-go](https://github.com/OpenFunction/functions-framework-go), [ff-js](https://github.com/OpenFunction/functions-framework-nodejs) |
| invoke   | Indicates that the output is the Dapr service invocation component. Refer to [Service invocation API reference](https://docs.dapr.io/reference/api/service_invocation_api/) to learn more about Dapr bindings components.<br />:heavy_exclamation_mark:Note that when using invoke as output, the name of invoke method should be assigned to the output's uri. | [ff-go](https://github.com/OpenFunction/functions-framework-go), [ff-js](https://github.com/OpenFunction/functions-framework-nodejs) |

<div align="right">
    <b><a href="#context">↥ back to Context</a></b>
</div>

### Runtime

We currently support `Knative` and `OpenFuncAsync` serving runtime.

| Value         | Description                                                  | Scope                                                        |
| ------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Knative       | Serving function with Knative runtime (based on Knative).    | [ff-go](https://github.com/OpenFunction/functions-framework-go) |
| OpenFuncAsync | Serving function with OpenFuncAsync runtime (based on KEDA+Dapr). | [ff-go](https://github.com/OpenFunction/functions-framework-go) |

<div align="right">
    <b><a href="#context">↥ back to Context</a></b>
</div>
