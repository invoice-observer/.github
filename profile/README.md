# invoice-observer (bounded context) and its Invoice Observer applications

The "invoice-observer" bounded context (in terms of DDD) corresponds to the invoice management monitoring subdomain,
usually a part of reporting or audit system.

The Invoice Observer consists of two applications, residing in separate repositories:
[Invoice Core App](https://github.com/invoice-observer/invoice-core-app.git) and [Invoice Monitoring CLI](https://github.com/invoice-observer/invoice-monitoring-cli.git),
designed as independent microservices.

## Overview

### [Invoice Core](https://github.com/invoice-observer/invoice-core-app/blob/main/README.md)

It's an ASP.NET Core API implementing primitive invoice management with JWT-based authentication,
a simple Razor Pages UI, SQLite persistence via Entity Framework, and publishing invoice events to RabbitMQ for monitoring.

### [Invoice Monitoring](https://github.com/invoice-observer/invoice-monitoring-cli/blob/main/README.md)

A .NET console application that subscribes to invoice events from RabbitMQ (e.g., `invoice.added`, `invoice.updated`,
`invoice.deleted`), consumes messages from CloudAMQP or local RabbitMQ, and pretty-prints JSON payloads
for monitoring and auditing.

## License

This bounded context is licensed under the terms of the [MIT License](../LICENSE).

## Contact

Eduard Danziger

[eduard.danziger@gmx.de](mailto:eduard.danziger@gmx.de)
