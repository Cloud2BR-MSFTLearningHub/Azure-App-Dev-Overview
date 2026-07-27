# Azure App Dev Services Overview

Last updated: 2026-07-27

<details markdown>
<summary>List of references</summary>

- [Types of cloud computing](https://azure.microsoft.com/en-us/resources/cloud-computing-dictionary/types-of-cloud-computing/)
- [What is Azure Service Bus?](https://learn.microsoft.com/en-us/azure/service-bus-messaging/service-bus-messaging-overview)
- [Technology choices for Azure solutions](https://learn.microsoft.com/en-us/azure/architecture/guide/technology-choices/technology-choices-overview)
- [Choose between Azure messaging services](https://learn.microsoft.com/en-us/azure/service-bus-messaging/compare-messaging-services)

</details>

> A landing zone is a general cloud framework that sets up the core structure for
> all workloads. Each use case (like an app, data pipeline, or API) then builds on
> top of this framework, using the same environments (Dev, Test, UAT, Prod) and
> CI/CD pipelines to move code safely into production. It is general by design, but
> applied per use case.

## Types of cloud computing

![Types of cloud computing](https://github.com/user-attachments/assets/4088401d-c4ec-4e6d-9236-01a0658a767f){ .diagram-standard }

| Category | Models and details |
| --- | --- |
| Deployment models | **Private:** Dedicated infrastructure for one organization; high security and control. **Public:** Services delivered over the internet; shared resources; cost-effective and scalable. **Hybrid:** Combines private and public clouds; enables workload flexibility and optimization. |
| Service models | **IaaS (Infrastructure as a Service):** Virtualized servers, storage, and networking; you manage the operating system and apps. **PaaS (Platform as a Service):** Complete platform for app development and deployment; no infrastructure management. **SaaS (Software as a Service):** Fully managed applications delivered over the internet. |

!!! tip "Deployment models"
    - **Private cloud:** dedicated environment for one organization, hosted
      on-premises or by a partner, offering maximum control and compliance.
    - **Public cloud:** shared infrastructure managed by a provider such as Azure,
      delivering scalability and cost efficiency for most workloads.
    - **Hybrid cloud:** combines on-premises (private) and public cloud, enabling
      flexibility for regulated data, disaster recovery, and gradual adoption.

<details markdown>
<summary>Private cloud (Azure Stack)</summary>

- **What:** dedicated cloud environment for one organization, hosted on-premises or by a partner.
- **Why:** maximum control, security, and compliance for sensitive workloads.
- **When to use:** regulatory compliance (finance, healthcare); mission-critical apps requiring isolation.
- **Azure services:** Azure Stack Hub (run Azure services in your datacenter); Azure Arc (manage hybrid resources with Azure governance).
- **Integration services:** API Management (secure APIs for internal apps); Logic Apps (automate workflows across on-premises and cloud).

</details>

<details markdown>
<summary>Public cloud (Azure Global)</summary>

- **What:** services delivered over the internet, shared across customers.
- **Why:** cost-effective, scalable, and fast to deploy.
- **When to use:** dynamic workloads, SaaS adoption, global reach.
- **Azure services:** Azure App Service (host web apps without managing infrastructure); Azure Virtual Machines (compute on demand); Azure Blob Storage (scalable object storage).
- **Integration services:** Event Grid (event-driven architecture); Service Bus (reliable messaging); Event Hubs (massive data ingestion).

</details>

<details markdown>
<summary>Hybrid cloud (Azure hybrid solutions)</summary>

- **What:** combines private and public clouds for flexibility.
- **Why:** balance security with scalability; gradual cloud adoption.
- **When to use:** legacy modernization, burst capacity needs.
- **Azure services:** Azure Arc (unified management across on-premises and cloud); Azure ExpressRoute (private connectivity to Azure); Azure Site Recovery (disaster recovery).
- **Integration services:** Logic Apps (connect on-premises ERP with cloud CRM); Data Factory (extract, transform, and load for hybrid data flows).

</details>

## Service responsibility model

![Cloud service responsibility model from on-premises to IaaS, PaaS, and SaaS](https://github.com/user-attachments/assets/24cff45a-6f9c-4cce-91d4-5dab402a83ef){ .diagram-wide }

Key foundational components in the traditional cloud service responsibility model
move from On-premises to IaaS to PaaS to SaaS.

![The nine layers of the cloud service responsibility model](https://github.com/user-attachments/assets/b4a4134b-c2e1-4d7f-ae19-e38a9448021e){ .diagram-standard }

!!! note
    These nine layers are conceptual, not exhaustive. They represent the major
    areas of control and management. In reality there can be additional sub-layers
    or specialized services (security, identity, monitoring, compliance) that span
    across these layers.

1. **Applications** - end-user software and business apps running on the platform.
2. **Data** - information stored, processed, and managed within the system.
3. **Runtime** - execution environment for applications (for example .NET, Java).
4. **Middleware** - software that connects apps and services (messaging, APIs).
5. **Operating system** - core system software managing hardware and apps.
6. **Virtualization** - abstraction layer enabling multiple operating systems on hardware.
7. **Servers** - physical or virtual machines hosting workloads.
8. **Storage** - persistent data storage systems (disks, blobs, databases).
9. **Networking** - connectivity infrastructure for communication and data transfer.

<details markdown>
<summary>IaaS (Infrastructure as a Service)</summary>

- **What:** virtualized compute, storage, and networking.
- **Azure services:** Azure Virtual Machines, Azure Virtual Network, Azure Load Balancer, and Microsoft Dev Box for cloud dev environments.
- **Integration services:** Service Bus (messaging between virtual machines and apps); Event Hubs (streaming telemetry); API Management (expose APIs from virtual-machine-hosted apps).
- **Use cases:** lift-and-shift migrations, disaster recovery, custom environments, hosting legacy apps with API exposure.

</details>

<details markdown>
<summary>PaaS (Platform as a Service)</summary>

- **What:** managed platform for app development and deployment.
- **Azure services:** Azure App Service (web apps and APIs); Azure Functions (serverless compute); Azure Container Apps (microservices and containers); Azure Kubernetes Service (orchestration); Azure Spring Apps (managed Spring Boot for Java); Azure SQL Database and Azure SQL Managed Instance.
- **Integration services:** Logic Apps (workflow automation); API Management (secure and publish APIs); Event Grid (event-driven architecture); SignalR Service (real-time communication).
- **Use cases:** modern app development, microservices, rapid prototyping, event-driven apps, enterprise integration.

</details>

<details markdown>
<summary>SaaS (Software as a Service)</summary>

- **What:** fully managed apps delivered over the internet.
- **Azure examples:** Microsoft 365 (productivity); Dynamics 365 (CRM and ERP); Microsoft Fabric and Power BI (analytics and visualization); Power Platform (low-code app development).
- **Integration services:** Logic Apps (connect SaaS with ERP or CRM); Event Grid (trigger workflows from SaaS events); API Management (extend SaaS capabilities via APIs).
- **Use cases:** productivity tools, CRM, analytics, low-code or no-code app development.

</details>

!!! note
    Control decreases as you move from on-premises to IaaS to PaaS to SaaS. The
    trade-off is that more convenience means less control. Choose IaaS when you need
    operating-system-level control, PaaS when you want to focus on app development,
    and SaaS when you want zero infrastructure management.

## Event, message, stream

![Comparison of event, message, and stream on Azure](https://github.com/user-attachments/assets/c9005aac-1014-41d2-85bc-ae7327b87bf2){ .diagram-standard }

!!! tip
    - **Event (Event Grid):** best for lightweight notifications and reactive architectures.
    - **Message (Service Bus):** use when you need guaranteed delivery, ordering, or transactional integrity.
    - **Stream (Event Hubs):** ideal for high-throughput streaming such as IoT telemetry or real-time analytics.

| Aspect | Event | Message | Stream |
| --- | --- | --- | --- |
| Definition | Lightweight notification that something happened; does not carry full business data. | Data packet intended for processing; often contains business-critical info with guaranteed delivery. | Continuous flow of data for real-time processing and analytics. |
| Characteristics | Fire-and-forget with basic retries; reactive; small metadata payload. | Durable until processed; supports sessions, transactions, and dead-letter queues; larger payloads. | High-throughput ingestion; partitioned for scalability; built for streaming. |
| Azure service | **Event Grid** routes events from sources (Blob Storage, IoT Hub) to subscribers (Functions, Logic Apps). | **Service Bus** provides enterprise messaging with first-in-first-out ordering, sessions, and reliability. | **Event Hubs** ingests millions of events per second for telemetry and analytics. |
| Use cases | Trigger workflows on upload; notify downstream systems; fan-out notifications. | Order processing; payment workflows requiring guaranteed delivery; transactional microservice communication. | IoT telemetry ingestion; real-time analytics; streaming to Synapse or Databricks. |

Reference: [Choose between Azure messaging services - Event Grid, Event Hubs, and Service Bus](https://learn.microsoft.com/en-us/azure/service-bus-messaging/compare-messaging-services).

![Data ingestion and processing workflow using Azure services](https://github.com/user-attachments/assets/516b1579-25e8-4d1c-b78e-c4aee6b05f60){ .diagram-standard }

## Azure App Dev services

![Azure App Dev and integration services](https://github.com/user-attachments/assets/afac1692-a25a-448e-9607-c9b452793ea9){ .diagram-standard }

See the [What to choose](what-to-choose.md) guide for compute, hybrid, and
networking decision trees.

- **Logic Apps:** orchestration of workflows and business processes.
- **Functions:** serverless compute execution.
- **Data Factory:** bulk data movement and transformation.
- **Event Hubs:** massive data ingestion.
- **Service Bus:** enterprise messaging.
- **Event Grid:** event routing and delivery.
- **API Management:** API creation, access control, and management.

<details markdown>
<summary>Logic Apps (orchestration)</summary>

Automates workflows and integrates apps, data, and services across organizations.

- **Key features:** visual designer for workflows; connectors for SaaS, on-premises, and APIs; B2B integration with EDI standards.
- **Use case:** automating order processing, approvals, or integrating CRM with ERP.

</details>

<details markdown>
<summary>Azure Functions (processing)</summary>

Provides serverless compute for executing code in response to events.

- **Key features:** pay-per-execution; multiple languages (C#, Python, JavaScript); integrates with Event Grid, Service Bus, and Event Hubs.
- **Use case:** real-time data processing, image resizing, or IoT telemetry handling.

</details>

<details markdown>
<summary>Data Factory (data movement)</summary>

Extract, transform, and load service for moving and transforming data at scale.

- **Key features:** hybrid data integration; built-in connectors for databases, SaaS, and big-data stores; pipeline orchestration.
- **Use case:** migrating data from SQL Server to Azure Synapse Analytics.

</details>

<details markdown>
<summary>Event Hubs (data ingestion)</summary>

Handles massive data ingestion for real-time analytics.

- **Key features:** high-throughput event streaming; integrates with Stream Analytics and Synapse; millions of events per second.
- **Use case:** collecting telemetry from IoT devices or application logs.

</details>

<details markdown>
<summary>Service Bus (messaging)</summary>

Enterprise-grade messaging for reliable communication between services.

- **Key features:** queues and topics for decoupled communication; transactions and dead-letter queues; asynchronous messaging patterns.
- **Use case:** order processing systems where components communicate asynchronously.

</details>

<details markdown>
<summary>Event Grid (event routing)</summary>

Event-driven architecture for routing events between sources and handlers.

- **Key features:** low-latency delivery; custom topics and system events; integrates with Functions, Logic Apps, and Storage.
- **Use case:** triggering workflows when a file is uploaded to Blob Storage.

</details>

<details markdown>
<summary>API Management (exposure)</summary>

Securely expose APIs to internal and external consumers.

- **Key features:** API gateway with throttling, caching, and transformation; developer portal for documentation; analytics and monitoring.
- **Use case:** publishing REST APIs for mobile apps or partner integrations.

</details>
