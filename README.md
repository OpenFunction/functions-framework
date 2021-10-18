# OpenFunction Functions Framework
OpenFunction Functions Framework is designed to provide users of FaaS with a suite of tools to convert user code into application code that supports multiple runtimes.

## OpenFunction Context Specs

For detailed Function Context specs visit:

- [OpenFunction Context Specs v0.3.1](docs/v0.3.1/OpenFunction-context-specs.md).
- [OpenFunction Context Specs latest](docs/latest/OpenFunction-context-specs.md).

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

  The framework also provides the SDK for getting data and sending data. Users can use [OpenFunctionContext](#openfunction-context-specs) to handle function resource contexts, including performing "get data" and "send data".
  

## Contributing

You can get help on developing OpenFunction Functions Framework by visiting [CONTRIBUTING](CONTRIBUTING.md) .
