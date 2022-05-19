# OpenFunction Context Specs

## Overview

### Statement

`Scope` indicates which functions-framework has already support this item.

#### functions-framework abbreviation

OpenFunction/functions-framework-go -> ff-go

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
  "runtime": "Async",
  "state": "",
  "prePlugins": [],
  "postPlugins": [],
  "pluginsTracing": {
    "enable": true,
    "provider": {
      "name": "skywalking",
      "oapServer": "localhost:xxx"
    },
    "tags": {
      "key": "value"
    },
    "baggage": {
      "key": "value"
    }
  },
  "out": {
    "code": 200,
    "data": "",
    "error": "",
    "metadata": {}
  }
}
```

Specification:

| Key        | Type            | Description                                               | Scope                                                        | example                                |
| ---------- | --------------- | --------------------------------------------------------- | ------------------------------------------------------------ | -------------------------------------- |
| name       | string, require | Function name.                                            | [ff-go](https://github.com/OpenFunction/functions-framework-go) | "myfunction", "hello-func"             |
| version    | string, require | Function version.                                         | [ff-go](https://github.com/OpenFunction/functions-framework-go) | "v1", "v2"                             |
| requestID | string          | Request ID, uuid format.                                  | [ff-go](https://github.com/OpenFunction/functions-framework-go) | "a0f2ad8d-5062-4812-91e9-95416489fb01" |
| port       | string | Function serving port.                                    | [ff-go](https://github.com/OpenFunction/functions-framework-go) | "50003"                       |
| clientPort | string | Dapr client port. (default is "50001" in Kubernetes mode) | [ff-go](https://github.com/OpenFunction/functions-framework-go) | "50001" |
| inputs     | map       | Function input from bindings data.<br />A map of Input objects. The key is the name of input and the value is input object, see [Input](#input). <br />Empty means no input. | [ff-go](https://github.com/OpenFunction/functions-framework-go) |                                        |
| outputs    | map        | Function output to bindings data. <br />A map of Output objects. The key is the name of output and the value is output object, see [Output](#output). <br />Empty means no output. | [ff-go](https://github.com/OpenFunction/functions-framework-go) |                                        |
| runtime    | enum, require   | Function serving runtime, see [Runtime](#runtime).       | [ff-go](https://github.com/OpenFunction/functions-framework-go) | "Knative", "Async"   |
| state      | string          | Used to store the states of the function in operation.    |                                                              |                                        |
| out | map | Outputs after the function is run, see [Out](#out). | [ff-go](https://github.com/OpenFunction/functions-framework-go) | |
| prePlugins | array | List of names of plugins executed before the user function. | [ff-go](https://github.com/OpenFunction/functions-framework-go) | ["plg1", "plg2"] |
| postPlugins | array | List of names of plugins executed after the user function. | [ff-go](https://github.com/OpenFunction/functions-framework-go) | ["plg1", "plg2"] |
| pluginsTracing | map | Configuration of the tracing plugins, see [PluginsTracing](#pluginstracing). | [ff-go](https://github.com/OpenFunction/functions-framework-go) |  |

### Input

Example:

```json
{
  "my-input": {
    "uri": "my-uri",
    "componentName": "my-component",
    "componentType": "bindings.kafka",
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
| componentType | string | Input type. When using Async as runtime, you need to set the `type` (refer to [Input Type](#input-type)) parameter. | [ff-go](https://github.com/OpenFunction/functions-framework-go) | "bindings.kafka" |
| componentName | string | The component's name. | [ff-go](https://github.com/OpenFunction/functions-framework-go) | "componentA" |
| metadata | map | The metadata to be passed to dapr for use. Usage can be found in dapr's documentation. | [ff-go](https://github.com/OpenFunction/functions-framework-go) |  |

#### Input Type

Effective only when using Async as runtime. 

| Value      | Description                                                  | Scope                                                        |
| ---------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| bindings.* | Indicates that the input is the Dapr bindings component. Refer to [Bindings API reference](https://docs.dapr.io/reference/api/bindings_api/) to learn more about Dapr bindings components. | [ff-go](https://github.com/OpenFunction/functions-framework-go) |
| pubsub.*   | Indicates that the input is the Dapr pubsub component. Refer to [Pub/sub API reference](https://docs.dapr.io/reference/api/pubsub_api/) to learn more about Dapr bindings components. <br />:heavy_exclamation_mark:Note that when using pubsub as input, the name of pubsub's topic should be assigned to the input's uri. | [ff-go](https://github.com/OpenFunction/functions-framework-go) |

<div align="right">
    <b><a href="#context">↥ back to Context</a></b>
</div>

### Outputs

Examples:

```json
{
  "my-output": {
    "uri": "my-uri",
    "componentName": "my-component",
    "componentType": "bindings.kafka",
    "operation": "post"
  }
}
```

Specification:

#### Output

| Key           | Type   | Description                                                  | Scope                                                        | example                  |
| ------------- | ------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------ |
| name(key)     | string | Output name.                                                 | [ff-go](https://github.com/OpenFunction/functions-framework-go) | "demo-kafka", "cron-job" |
| uri           | string | Output serving listening path. This indicates the destination of the output data.<br />Bindings: same as the component's name, can be omitted.<br />Pubsub: represent the topic's name, cannot be omitted. | [ff-go](https://github.com/OpenFunction/functions-framework-go) | "echo"                   |
| componentType | string | Output type. When using Async as runtime, you need to set the `type` (refer to [Output Type](#output-type)) parameter. | [ff-go](https://github.com/OpenFunction/functions-framework-go) | "bindings.kafka"         |
| componentName | string | The component's name.                                        | [ff-go](https://github.com/OpenFunction/functions-framework-go) | "componentA"             |
| metadata      | map    | The metadata to be passed to dapr for use. Usage can be found in dapr's documentation. | [ff-go](https://github.com/OpenFunction/functions-framework-go) |                          |
| operation     | string | The operation's name. Usage can be found in dapr's documentation. | [ff-go](https://github.com/OpenFunction/functions-framework-go) | "post", "create"         |

##### Output Type

| Value      | Description                                                  | Scope                                                        |
| ---------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| bindings.* | Indicates that the output is the Dapr bindings component. Refer to [Bindings API reference](https://docs.dapr.io/reference/api/bindings_api/) to learn more about Dapr bindings components. | [ff-go](https://github.com/OpenFunction/functions-framework-go) |
| pubsub.*   | Indicates that the output is the Dapr pubsub component. Refer to [Pub/sub API reference](https://docs.dapr.io/reference/api/pubsub_api/) to learn more about Dapr bindings components. <br />:heavy_exclamation_mark:Note that when using pubsub as output, the name of pubsub's topic should be assigned to the output's uri. | [ff-go](https://github.com/OpenFunction/functions-framework-go) |

<div align="right">
    <b><a href="#context">↥ back to Context</a></b>
</div>

### Runtime

We currently support `Knative` and `Async` serving runtime.

| Value   | Description                                               | Scope                                                        |
| ------- | --------------------------------------------------------- | ------------------------------------------------------------ |
| Knative | Serving function with Knative runtime (based on Knative). | [ff-go](https://github.com/OpenFunction/functions-framework-go) |
| Async   | Serving function with Async runtime (based on KEDA+Dapr). | [ff-go](https://github.com/OpenFunction/functions-framework-go) |

<div align="right">
    <b><a href="#context">↥ back to Context</a></b>
</div>

### Out

| Key      | Type   | Description                                     | Scope                                                        | example          |
| -------- | ------ | ----------------------------------------------- | ------------------------------------------------------------ | ---------------- |
| code     | int    | Return code of the function.                    | [ff-go](https://github.com/OpenFunction/functions-framework-go) | 200, 500         |
| data     | string | The data returned by the function.              | [ff-go](https://github.com/OpenFunction/functions-framework-go) | "some data"      |
| error    | string | The error information returned by the function. | [ff-go](https://github.com/OpenFunction/functions-framework-go) | "some error"     |
| metadata | map    | The metadata returned by the function.          | [ff-go](https://github.com/OpenFunction/functions-framework-go) | {"key": "value"} |

<div align="right">
    <b><a href="#context">↥ back to Context</a></b>
</div>

### PluginsTracing

| Key      | Type | Description                                                  | Scope                                                        | example                           |
| -------- | ---- | ------------------------------------------------------------ | ------------------------------------------------------------ | --------------------------------- |
| enable   | bool | Whether to enable tracing capability.                        | [ff-go](https://github.com/OpenFunction/functions-framework-go) | true, false                       |
| provider | map  | Configuration of tracing capability provider, see [TracingProvider](#tracingprovider) | [ff-go](https://github.com/OpenFunction/functions-framework-go) |                                   |
| tags     | map  | Tags for tracing.                                            | [ff-go](https://github.com/OpenFunction/functions-framework-go) | {"func": "function-with-tracing"} |
| baggage  | map  | Baggage for tracing.                                         | [ff-go](https://github.com/OpenFunction/functions-framework-go) | {"key": "sw8-correlation"}        |

<div align="right">
    <b><a href="#context">↥ back to Context</a></b>
</div>

### TracingProvider

| Key       | Type   | Description                                                  | Scope                                                        | example         |
| --------- | ------ | ------------------------------------------------------------ | ------------------------------------------------------------ | --------------- |
| name      | string | The name of the provider (if the tracing capability is enabled, this name will be automatically inserted into the list of plugin names) | [ff-go](https://github.com/OpenFunction/functions-framework-go) | "skywalking"    |
| oapServer | string | The oap server address.                                      | [ff-go](https://github.com/OpenFunction/functions-framework-go) | "localhost:xxx" |

<div align="right">
    <b><a href="#context">↥ back to Context</a></b>
</div>

