# How to Contribute

Development of function conversion suites for different programming languages. Refer to the proposal first: [Add Function Framework](https://github.com/OpenFunction/OpenFunction/blob/main/docs/proposals/202105_add_function_framework.md) .

- Main function template

  During the build process of OpenFunction, the builder renders the user code using the main function template, based on which the mian function in the app image is generated.

  Refer to [main-function-template](https://github.com/OpenFunction/OpenFunction/blob/main/docs/proposals/202105_add_function_framework.md#main-function-template) to learn how it works.

- Function handler library

  Used to register different types of functions to the HTTP server to provide terminal access.

  Refer to [function-handler-library](https://github.com/OpenFunction/OpenFunction/blob/main/docs/proposals/202105_add_function_framework.md#function-handler-library) to learn how it works.

- Function Context

  A standard context structure to pass function semantics.

  Refer to [function-context](https://github.com/OpenFunction/OpenFunction/blob/main/docs/proposals/202105_add_function_framework.md#function-context) to learn how it works.
  
  For detailed Function Context specs visit [OpenFunction Context Specs](docs/OpenFunction-context-specs.md).

## Development Guide

Please refer to the [OpenFuntion Development Guide](https://github.com/OpenFunction/OpenFunction/tree/main/docs/development) before start contributing.