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
  "clientPort": "44538",
  "inputs": {},
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
| port       | string | Function serving port.                                    | [ff-go](https://github.com/OpenFunction/functions-framework-go) | "50001"                        |
| clientPort | string | Dapr client port. | [ff-go](https://github.com/OpenFunction/functions-framework-go) | "44544" |
| inputs     | map       | Function input from bindings data.<br />A map of Input objects. The key is the name of input and the value is input object, see [Input](#input). <br />Empty means no input. | [ff-go](https://github.com/OpenFunction/functions-framework-go) |                                        |
| outputs    | map        | Function output to bindings data. <br />A map of Output objects. The key is the name of output and the value is output object, see [Output](#output). <br />Empty means no output. | [ff-go](https://github.com/OpenFunction/functions-framework-go) |                                        |
| runtime    | enum, require   | Function serving runtime, see [Runtime](#runtime).       | [ff-go](https://github.com/OpenFunction/functions-framework-go) | "Knative", "OpenFuncAsync"       |
| state      | string          | Used to store the states of the function in operation.    |                                                              |                                        |

### Input

Example:

```json
{
  "my-input": {
    "uri": "my-uri",
    "Component": "my-component",
    "type": "bindings",
    "metadata": {
      "Content-Type": "application/json; charset=utf-8"
    }
  }
}
```

Specification:

| Key        | Type   | Description                                                  | Scope                                           | example                                |
| ---------- | ------ | ------------------------------------------------------------ | -------------------------------------- | -------------------------------------- |
| name(key) | string | Input name. | [ff-go](https://github.com/OpenFunction/functions-framework-go) | "demo-kafka", "cron-job" |
| uri | string | Input serving listening path. This indicates the destination of the input data.<br />Bindings: same as the component's name, can be omitted.<br />Pubsub: represent the topic's name, cannot be omitted. | [ff-go](https://github.com/OpenFunction/functions-framework-go) | "echo" |
| type | string | Input type. When using OpenFuncAsync as runtime, you need to set the `type` (refer to [Input Type](#input-type)) parameter. | [ff-go](https://github.com/OpenFunction/functions-framework-go) | "bindings" |
| component | string | The component's name. | [ff-go](https://github.com/OpenFunction/functions-framework-go) | "componentA" |
| metadata | map | The metadata to be passed to dapr for use. Usage can be found in dapr's documentation. | [ff-go](https://github.com/OpenFunction/functions-framework-go) |  |

#### Input Type

Effective only when using OpenFuncAsync as runtime. 

| Value    | Description                                                  | Scope                                                        |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| bindings | Indicates that the input is the Dapr bindings component. Refer to [Bindings API reference](https://docs.dapr.io/reference/api/bindings_api/) to learn more about Dapr bindings components. | [ff-go](https://github.com/OpenFunction/functions-framework-go) |
| pubsub   | Indicates that the input is the Dapr pubsub component. Refer to [Pub/sub API reference](https://docs.dapr.io/reference/api/pubsub_api/) to learn more about Dapr bindings components. <br />:heavy_exclamation_mark:Note that when using pubsub as input, the name of pubsub's topic should be assigned to the input's uri. | [ff-go](https://github.com/OpenFunction/functions-framework-go) |

<div align="right">
    <b><a href="#context">↥ back to Context</a></b>
</div>

### Outputs

Examples:

```json
{
  "my-output": {
    "uri": "my-uri",
    "Component": "my-component",
    "type": "bindings",
    "operation": "post"
  }
}
```

Specification:

#### Output

| Key       | Type   | Description                                                  | Scope                                                        | example                  |
| --------- | ------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------ |
| name(key) | string | Output name.                                                 | [ff-go](https://github.com/OpenFunction/functions-framework-go) | "demo-kafka", "cron-job" |
| uri       | string | Output serving listening path. This indicates the destination of the output data.<br />Bindings: same as the component's name, can be omitted.<br />Pubsub: represent the topic's name, cannot be omitted. | [ff-go](https://github.com/OpenFunction/functions-framework-go) | "echo"                   |
| type      | string | Output type. When using OpenFuncAsync as runtime, you need to set the `type` (refer to [Output Type](#output-type)) parameter. | [ff-go](https://github.com/OpenFunction/functions-framework-go) | "bindings"               |
| component | string | The component's name.                                        | [ff-go](https://github.com/OpenFunction/functions-framework-go) | "componentA"             |
| metadata  | map    | The metadata to be passed to dapr for use. Usage can be found in dapr's documentation. | [ff-go](https://github.com/OpenFunction/functions-framework-go) |                          |
| operation | string | The operation's name. Usage can be found in dapr's documentation. | [ff-go](https://github.com/OpenFunction/functions-framework-go) | "post", "create"         |

##### Output Type

Effective only when using OpenFuncAsync as runtime. 

| Value    | Description                                                  | Scope                                                        |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| bindings | Indicates that the output is the Dapr bindings component. Refer to [Bindings API reference](https://docs.dapr.io/reference/api/bindings_api/) to learn more about Dapr bindings components. | [ff-go](https://github.com/OpenFunction/functions-framework-go) |
| pubsub   | Indicates that the output is the Dapr pubsub component. Refer to [Pub/sub API reference](https://docs.dapr.io/reference/api/pubsub_api/) to learn more about Dapr bindings components. <br />:heavy_exclamation_mark:Note that when using pubsub as output, the name of pubsub's topic should be assigned to the output's uri. | [ff-go](https://github.com/OpenFunction/functions-framework-go) |

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
