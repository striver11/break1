# Project Architecture

```mermaid
graph TD
    subgraph Infrastructure
        A[Config Server] -->|Provides Configuration| B[Customers Service]
        A --> C[Vets Service]
        A --> D[Visits Service]
        A --> E[GenAI Service]
        A --> F[API Gateway]
        A --> G[Discovery Server]
        A --> H[Admin Server]
        A --> I[Grafana]
        A --> J[Prometheus]
    end

    subgraph Services
        B[Customers Service] -->|Registers with| G[Discovery Server]
        C[Vets Service] -->|Registers with| G[Discovery Server]
        D[Visits Service] -->|Registers with| G[Discovery Server]
        E[GenAI Service] -->|Registers with| G[Discovery Server]
        F[API Gateway] -->|Routes Requests| B
        F -->|Routes Requests| C
        F -->|Routes Requests| D
        F -->|Routes Requests| E
    end

    subgraph Monitoring
        I[Grafana] -->|Collects Metrics| J[Prometheus]
        J -->|Monitors| B
        J -->|Monitors| C
        J -->|Monitors| D
        J -->|Monitors| E
        J -->|Monitors| F
    end

    subgraph Frontend
        K[AngularJS Frontend] -->|Interacts with| F
    end

    subgraph Admin
        H[Admin Server] -->|Monitors| B
        H -->|Monitors| C
        H -->|Monitors| D
        H -->|Monitors| E
        H -->|Monitors| F
    end

    subgraph Docker
        L[Docker Compose] -->|Orchestrates| A
        L --> B
        L --> C
        L --> D
        L --> E
        L --> F
        L --> G
        L --> H
        L --> I
        L --> J
    end
