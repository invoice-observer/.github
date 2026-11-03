<h1><img src="https://raw.githubusercontent.com/invoice-observer/.github/main/pictures/invoice-observer-v3.png" alt="Invoice Observer logo" width="28" height="28" align="center"> &nbsp;invoice-observer and its applications</h1>

A simple invoice management and monitoring system. An ASP.NET Core application manages invoices
and publishes events to RabbitMQ; a separate .NET console application consumes and displays them.
The two applications are developed as independent microservices.

It can serve as a monitoring component within a larger reporting or audit system.

## Key Components

| Repository | Tech | Description |
|-----------|------|-------------|
| [invoice-core-app](https://github.com/invoice-observer/invoice-core-app) | C# / ASP.NET Core / Razor Pages / EF Core | Invoice management API with JWT authentication, a Razor Pages UI with cookie authentication, SQLite persistence and RabbitMQ event publishing |
| [invoice-monitoring-cli](https://github.com/invoice-observer/invoice-monitoring-cli) | C# / .NET / RabbitMQ | Console application consuming invoice events from CloudAMQP or local RabbitMQ and pretty-printing JSON payloads for monitoring and auditing |

## Architecture Overview

```mermaid
flowchart TD

classDef dottedBox fill:transparent,fill-opacity:0.55,stroke-dasharray:20 5,stroke-width:2px;

apiClient["API Client"]
browser["Web Browser"]

subgraph invoiceCoreApp["invoice-core-app"]
    api["REST API"]
    razorUi["Razor Pages UI"]
    invoiceCore["Invoice Service"]
    api --> invoiceCore
    razorUi --> invoiceCore
end
class invoiceCoreApp dottedBox

sqlite[("SQLite")]
rabbitMq[("RabbitMQ")]
monitoring["invoice-monitoring-cli<br>(.NET Console)"]

apiClient -->|HTTP / JWT| api
browser -->|HTTP / Cookie Auth| razorUi
invoiceCore -->|Persistence via EF Core| sqlite
invoiceCore -->|Publish invoice events| rabbitMq
rabbitMq -->|Consume and display JSON| monitoring
```

## License

The invoice-observer is licensed under the terms of the [MIT License](https://github.com/invoice-observer/.github/blob/main/LICENSE).

## Contact

Eduard Danziger

[https://github.com/eduarddanziger](https://github.com/eduarddanziger)

[eduard.danziger@gmx.de](mailto:eduard.danziger@gmx.de)
