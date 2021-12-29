# OpenFunction Functions Framework
The OpenFunction function framework is designed to provide users with the ability to convert function code into application that support multiple runtimes.

## OpenFunction Context

You can learn more about the design of the OpenFunction Context by visiting [function-context](https://github.com/OpenFunction/OpenFunction/blob/main/docs/proposals/202105_add_function_framework.md#function-context).

You can learn more about the different versions of the OpenFunction Context specification by visiting the links below:

- [Context Specs v0.2.0](docs/v0.2.0/OpenFunction-context-specs.md)

- [Context Specs v0.1.0](docs/v0.1.0/OpenFunction-context-specs.md)

The direct user of Context is the OpenFunction Builder (Go) and the following is a compatible relationship between Context, Builder and OpenFunction.

> You can get the corresponding version compatibility information in the specific builder repository. Here we use the OpenFunction Go (v1.15) builder as an example.

| OpenFunction | Context | Builder (Go)                                |
| ------------ | ------- | ------------------------------------------- |
| v0.3.*       | v0.1.0  | v0.2.2 (openfunction/builder-go:v0.2.2-1.15) |
| v0.4.*       | v0.2.0  | v0.3.0 (openfunction/builder-go:v0.3.0-1.15) |
| v0.5.*       | v0.2.0  | v0.4.0 (openfunction/builder-go:v0.4.0-1.15) |

## Functions Framework Samples

You can visit [OpenFunction/samples: Functions-framework samples](https://github.com/OpenFunction/samples#functions-framework-samples) for examples of functions-framework.

## Support

### Language

- Go: [functions-framework-go](https://github.com/OpenFunction/functions-framework-go)
- Nodejs: [functions-framework-nodejs](https://github.com/openFunction/functions-framework-nodejs)

### Runtime

- Knative
- OpenFuncAsync

### Function Type

- HTTP

  The framework creates a route that associates the "/" url path and the user function. After that, it starts the HTTP service according to the PORT parameter.

- CloudEvent

  The CloudEvent provides a handler for handling HTTP requests while binding user function. The framework creates a route that associates the "/" url path and the CloudEvent HTTP handler. After that, it starts the HTTP service according to the PORT parameter.

- OpenFunction

  > This function type is an implementation of [Data Bindings](https://github.com/cncf/wg-serverless/tree/master/whitepapers/serverless-overview#data-bindings)

  The framework creates a route that associates the specified HTTP url path with the user function.

  The framework also provides the SDK for getting data and sending data. Users can use [OpenFunction Context](#openfunction-context) to handle function resource contexts, including performing "get data" and "send data".
  

## Contributing

You can get help on developing OpenFunction Functions Framework by visiting [CONTRIBUTING](CONTRIBUTING.md) .
