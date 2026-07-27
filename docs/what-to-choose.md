# What to Choose - Azure App Dev Services

Last updated: 2026-07-27

Reference: [Technology choices for Azure solutions](https://learn.microsoft.com/en-us/azure/architecture/guide/technology-choices/technology-choices-overview).

## Choose a compute service

This is a decision-making guide for selecting the right Azure compute service. It
helps you determine the best option based on whether you are migrating an existing
workload or building a new application, considering cloud optimization,
containerization, orchestration needs, and control requirements.

Reference: [Choose an Azure compute service](https://learn.microsoft.com/en-us/azure/architecture/guide/technology-choices/compute-decision-tree).

<details markdown>
<summary>Migration path explained</summary>

When migrating workloads, the first question is whether the application is already
optimized for the cloud.

- **If optimized:** use **Azure App Service** for web applications, or **Azure VMware Solution** for VMware-based workloads.
- **If not optimized:** check whether the workload can be containerized.
    - **Yes:** choose orchestration such as VMware Tanzu, Kubernetes, or OpenShift on Azure Virtual Machines.
    - **No:** use **Virtual Machines** for a lift-and-shift approach.
- For VMware-specific workloads, **Azure VMware Solution** provides a seamless migration path.

</details>

<details markdown>
<summary>Building new applications explained</summary>

For new builds, start by asking whether you need full control.

- **Yes:** use **Virtual Machines** for complete control, or **Azure Batch** for high-performance computing (HPC).
- **No:**
    - Event-driven with short-lived processes? Use **Azure Functions** for serverless execution.
    - Need managed web hosting? Use **Azure App Service**.
    - Need full orchestration? Consider **Azure Kubernetes Service (AKS)**, **Azure Container Apps**, **Azure Service Fabric**, or **Red Hat OpenShift**.
    - Otherwise, use **Azure Container Instances** or **Azure Container Apps** for lightweight container hosting.

</details>

<details markdown>
<summary>Service categories</summary>

- **Container-exclusive services** are designed specifically for containerized workloads:
    - **Azure Container Instances (ACI):** lightweight containers without orchestration.
    - **Azure Kubernetes Service (AKS):** fully managed Kubernetes for complex orchestration.
    - **Azure Container Apps:** serverless containers for microservices and event-driven apps.
    - **VMware Tanzu on Azure VMs** and **OpenShift on Azure VMs** for hybrid and enterprise scenarios.
- **Container-compatible services** can run containers but are not exclusive to them:
    - **Azure Batch:** large-scale parallel and HPC workloads, including containerized jobs.
    - **Azure Functions:** serverless, event-driven workloads, including containerized functions.
    - **Azure App Service:** managed web apps and APIs, including containerized deployments.
    - **Azure Service Fabric:** distributed systems platform for microservices and containers.

</details>

### Choose a compute option for microservices

This flowchart helps you choose between **AKS**, **Azure Container Apps**, and
**Azure Functions** by evaluating compute requirements, containerization,
Kubernetes control, and workload type.

Reference: [Choose an Azure compute option for microservices](https://learn.microsoft.com/en-us/azure/architecture/microservices/design/compute-options).

- If **dedicated compute** is required, check whether **GPU access** is needed (AI/ML or HPC), then whether **Kubernetes API access** is necessary.
    - Kubernetes API needed: choose **Azure Kubernetes Service (AKS)**.
    - Not needed: choose **Azure Container Apps** for containerized microservices.
- If **dedicated compute is not required**, move toward serverless.
    - Containerized microservice: **Azure Container Apps** (serverless containers with autoscaling).
    - Code-based and non-containerized: **Azure Functions** for event-driven execution.

## Choose a hybrid option

These options enable hybrid and edge computing, allowing organizations to run
Azure services in disconnected, on-premises, or multicloud environments.

Reference: [Hybrid solution decision tree](https://learn.microsoft.com/en-us/azure/architecture/guide/technology-choices/hybrid-considerations#hybrid-solution-decision-tree).

<details markdown>
<summary>Decision explained</summary>

Start by asking whether the solution is existing/custom, multicloud, or
Azure-specified.

- **Existing or custom**, then restricted or datacenter-based:
    - **Restricted environments:** mass deployment (IoT) leads to **Azure IoT Edge**; low-scale deployment suits traditional and cloud-native workloads.
    - **Datacenter-based:** containers use **Azure Arc-enabled Kubernetes**; VMware uses **Azure Arc-enabled VMware, SCVMM, or servers**; SQL uses **Azure Arc-enabled data services**.
- **Multicloud:** similar options for containers, virtual machines, and SQL, using **Azure Arc** for unified management.
- **Azure-specified:** decide by hardware and workload type.
    - Hardware as a service or Azure-like datacenter leads to **Azure Local** or **Azure Stack Hub**.
    - For data transfer and compute at the edge, use **Azure Stack Edge** (Pro GPU for datacenter, Pro 2 for portable, Mini R or Pro R for ruggedized).

</details>

## Choose a networking service

This is a decision-making guide for selecting the right Azure networking and
application-delivery service based on whether you host a web application, APIs, or
need global distribution and performance optimization.

Reference: [Choose a load balancing solution for your scenario](https://learn.microsoft.com/en-us/azure/architecture/guide/technology-choices/load-balancing-overview#choose-a-load-balancing-solution-for-your-scenario).

<details markdown>
<summary>Decision explained</summary>

- Is the workload a **web application (HTTP/HTTPS)**?
    - **No** and internal: use **Azure Load Balancer** for internal traffic.
    - **Yes** and internet-facing: is it global or multi-region?
        - **Yes:** combine **Traffic Manager + Azure Load Balancer** for global DNS-based routing and regional load balancing.
- For **API-only hosting**, use **API Management** for secure API publishing and lifecycle management.
- If internet-facing and not API-only, do you need **SSL offload or per-request Layer 7 processing**?
    - **Yes:** use **Azure Front Door + Application Gateway** for global load balancing with Layer 7 features.
    - APIs with SSL offload: use **Azure Front Door + API Management**.
- For **PaaS**, **IaaS**, or **AKS** hosting: use **Azure Front Door** for global routing, combined with an **Application Gateway ingress controller** for AKS or **Azure Load Balancer** for virtual machines.
- If **performance acceleration** is required, **Azure Front Door** provides global edge caching and routing.
- For non-global Layer 7 routing, use **Application Gateway**, and combine with **API Management** for API-only workloads.

</details>
