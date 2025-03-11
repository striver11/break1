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
        F[API Gateway] -->|Routes Requests| B[Customers Service]
        F[API Gateway] -->|Routes Requests| C[Vets Service]
        F[API Gateway] -->|Routes Requests| D[Visits Service]
        F[API Gateway] -->|Routes Requests| E[GenAI Service]
    end

    subgraph Monitoring
        I[Grafana] -->|Collects Metrics| J[Prometheus]
        J[Prometheus] -->|Monitors| B[Customers Service]
        J[Prometheus] -->|Monitors| C[Vets Service]
        J[Prometheus] -->|Monitors| D[Visits Service]
        J[Prometheus] -->|Monitors| E[GenAI Service]
        J[Prometheus] -->|Monitors| F[API Gateway]
    end

    subgraph Frontend
        K[AngularJS Frontend] -->|Interacts with| F[API Gateway]
    end

    subgraph Admin
        H[Admin Server] -->|Monitors| B[Customers Service]
        H[Admin Server] -->|Monitors| C[Vets Service]
        H[Admin Server] -->|Monitors| D[Visits Service]
        H[Admin Server] -->|Monitors| E[GenAI Service]
        H[Admin Server] -->|Monitors| F[API Gateway]
    end

    subgraph Docker
        L[Docker Compose] -->|Orchestrates| A[Config Server]
        L --> B[Customers Service]
        L --> C[Vets Service]
        L --> D[Visits Service]
        L --> E[GenAI Service]
        L --> F[API Gateway]
        L --> G[Discovery Server]
        L --> H[Admin Server]
        L --> I[Grafana]
        L --> J[Prometheus]
    end

    click B "javascript:showFiles('customers-service')"
    click C "javascript:showFiles('vets-service')"
    click D "javascript:showFiles('visits-service')"
    click E "javascript:showFiles('genai-service')"

    subgraph CustomersServiceFiles
        B1[config]
        B1 --> B1a[MetricConfig.java]
        B2[model]
        B2 --> B2a[Owner.java]
        B2 --> B2b[OwnerRepository.java]
        B2 --> B2c[Pet.java]
        B2 --> B2d[PetRepository.java]
        B2 --> B2e[PetType.java]
        B3[web]
        B3 --> B3a[OwnerController.java]
        B3 --> B3b[PetController.java]
        B3 --> B3c[PetTypeController.java]
    end

    subgraph VetsServiceFiles
        C1[config]
        C1 --> C1a[MetricConfig.java]
        C2[model]
        C2 --> C2a[Vet.java]
        C2 --> C2b[VetRepository.java]
        C3[web]
        C3 --> C3a[VetController.java]
    end

    subgraph VisitsServiceFiles
        D1[config]
        D1 --> D1a[MetricConfig.java]
        D2[model]
        D2 --> D2a[Visit.java]
        D2 --> D2b[VisitRepository.java]
        D3[web]
        D3 --> D3a[VisitController.java]
    end

    subgraph GenAIServiceFiles
        E1[config]
        E1 --> E1a[MetricConfig.java]
        E2[model]
        E2 --> E2a[GenAIModel.java]
        E2 --> E2b[GenAIRepository.java]
        E3[web]
        E3 --> E3a[GenAIController.java]
    end

    subgraph APIGatewayFiles
        F1[config]
        F1 --> F1a[GatewayConfig.java]
        F2[model]
        F3[web]
        F3 --> F3a[APIGatewayController.java]
    end

    subgraph DiscoveryServerFiles
        G1[config]
        G1 --> G1a[DiscoveryConfig.java]
        G2[model]
        G3[web]
        G3 --> G3a[DiscoveryController.java]
    end

    subgraph AdminServerFiles
        H1[config]
        H1 --> H1a[AdminConfig.java]
        H2[model]
        H3[web]
        H3 --> H3a[AdminController.java]
    end

    subgraph GrafanaFiles
        I1[config]
        I1 --> I1a[GrafanaConfig.java]
        I2[model]
        I3[web]
        I3 --> I3a[GrafanaController.java]
    end

    subgraph PrometheusFiles
        J1[config]
        J1 --> J1a[PrometheusConfig.java]
        J2[model]
        J3[web]
        J3 --> J3a[PrometheusController.java]
    end
