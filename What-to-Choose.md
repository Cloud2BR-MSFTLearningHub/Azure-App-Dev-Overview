# What to Choose - Azure App Dev Services Overview


Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/) [Cloud2BR OSS - Learning Hub](https://github.com/Cloud2BR-MSFTLearningHub)

Last updated: 2025-08-04

----------------------


> Click here to read more about [Technology choices for Azure solutions](https://learn.microsoft.com/en-us/azure/architecture/guide/technology-choices/technology-choices-overview)

<img width="450" alt="image" src="https://github.com/user-attachments/assets/0713d101-94ef-40a9-9e55-0a780036ce7a" />

## Choose a compute service

> This diagram is a **decision-making guide for selecting the right Azure compute service**. It helps you determine the best option based on whether you are **migrating an existing workload** or **building a new application**. The flow considers factors like cloud optimization, containerization, orchestration needs, and control requirements.

<img width="900" height="916" alt="image" src="https://github.com/user-attachments/assets/fb6daaa9-50c2-4e9b-8195-e5f144ac63d2" />

From [Choose an Azure compute service](https://learn.microsoft.com/en-us/azure/architecture/guide/technology-choices/compute-decision-tree)

<details>
<summary>Migration Path Explained</summary>

> When migrating workloads, the first question is whether the application is **already optimized for the cloud**:

*   **If optimized:**
    *   Use **Azure App Service** for web applications.
    *   Use **Azure VMware Solution** for VMware-based workloads.

*   **If not optimized:**
    *   Check if the workload can be **containerized**:
        *   **Yes:** Choose orchestration solutions like:
            *   **VMware Tanzu on Azure VMs**
            *   **Kubernetes on Azure VMs**
            *   **OpenShift on Azure VMs**
        *   **No:** Use **Virtual Machines** for a lift-and-shift approach.

*   For VMware-specific workloads, **Azure VMware Solution** provides a seamless migration path.

</details>

<details>
<summary> Building New Applications Explained </summary>

> For new builds, start by asking if you need **full control**:

*   **Yes:**
    *   Use **Virtual Machines** for complete control.
    *   Use **Azure Batch** for HPC workloads.

*   **No:**
    *   Is the workload **event-driven** with short-lived processes?
        *   **Yes:** Use **Azure Functions** for serverless execution.
    *   Do you need **managed web hosting**?
        *   **Yes:** Use **Azure App Service**.
    *   Do you need **full orchestration**?
        *   **Yes:** Options include:
            *   **Azure Kubernetes Service (AKS)**
            *   **Azure Container Apps**
            *   **Azure Service Fabric**
            *   **Red Hat OpenShift**
        *   **No:** Use **Azure Container Instances** or **Azure Container Apps** for lightweight container hosting.

</details>

<details>
<summary>Service Categories</summary>

- **Container-exclusive services**: These services are designed specifically for containerized workloads and provide orchestration, scaling, and management capabilities tailored for containers:
    *   **Azure Container Instances (ACI):** A lightweight option for running containers without orchestration. Ideal for simple, isolated container tasks.
    *   **Azure Kubernetes Service (AKS):** A fully managed Kubernetes environment for complex container orchestration, scaling, and advanced workloads.
    *   **Azure Container Apps:** A serverless container platform for microservices and event-driven applications, with built-in autoscaling and Dapr integration.
    *   **VMware Tanzu on Azure VMs:** Enables Kubernetes-based container orchestration on Azure Virtual Machines using VMware Tanzu for hybrid and enterprise scenarios.
    *   **OpenShift on Azure VMs:** Provides Red Hat OpenShift capabilities on Azure infrastructure for organizations that prefer OpenShift for container orchestration.
- **Container-compatible services**: These services can run containerized workloads but are not exclusively designed for containers. They offer flexibility for mixed environments:
    *   **Azure Batch:** A compute service for large-scale parallel and HPC workloads. Supports containerized jobs for batch processing.
    *   **Azure Functions:** A serverless compute option for event-driven workloads. Can run containerized functions for portability and custom dependencies.
    *   **Azure App Service:** A managed platform for hosting web apps and APIs. Supports containerized deployments alongside traditional code-based apps.
    *   **Azure Service Fabric:** A distributed systems platform for microservices and containers, offering orchestration and lifecycle management for complex applications.

</details>

Choose an Azure compute option for microservices: 

> In summary, this flowchart helps developers choose between **AKS**, **Azure Container Apps**, and **Azure Functions** by evaluating factors like compute requirements, containerization, Kubernetes control, and workload type. It simplifies decision-making for modern cloud-native architectures.

<img width="983" height="500" alt="image" src="https://github.com/user-attachments/assets/dff4caed-52d9-429a-88cf-2af7de349906" />

From [Choose an Azure compute option for microservices](https://learn.microsoft.com/en-us/azure/architecture/microservices/design/compute-options)

> - This diagram is a **decision-making guide for selecting the right Azure compute service** based on application requirements. It starts with the question of whether your workload needs **dedicated compute resources** or can run in a **serverless environment**.
> - If **dedicated compute is required**, the next consideration is whether **GPU access** is needed. GPU requirements often indicate workloads like AI/ML or high-performance computing.
> - From there, the diagram asks if **Kubernetes API access** is necessary. If yes, the best choice is **Azure Kubernetes Service (AKS)**, which provides full Kubernetes orchestration and control. If Kubernetes API access is not needed, then **Azure Container Apps** is recommended for running containerized microservices without managing Kubernetes directly.
> - If **dedicated compute is not required**, the diagram moves toward **serverless options**. It checks if the workload is a **containerized microservice**. If yes, **Azure Container Apps** is suitable because it supports serverless containers with autoscaling. If not containerized, the next question is whether the workload is **code-based and non-containerized**. If yes, **Azure Functions** is the ideal choice for event-driven, serverless execution of small pieces of code.

## Choose a hybrid option

> These options enable hybrid and edge computing scenarios, allowing organizations to run Azure services in disconnected, on-premises, or multicloud environments.

<img width="1280" height="720" alt="image" src="https://github.com/user-attachments/assets/cd933ab9-4085-4bc9-9896-c3b1c59c33c7" />

From [Hybrid solution decision tree](https://learn.microsoft.com/en-us/azure/architecture/guide/technology-choices/hybrid-considerations#hybrid-solution-decision-tree)

<details>
<summary><b>Diagram explanation</b> (Click to expand)</summary>

> *   This diagram is a **decision-making guide for selecting the right Azure edge or hybrid compute service** based on hosting, deployment, and workload requirements. It starts by asking whether the solution is **existing/custom**, **multicloud**, or **Azure-specified**.
> *   If the solution is **existing or custom**, the next consideration is whether it is **restricted** or **datacenter-based**.
>     *   For **restricted environments**, the diagram distinguishes between **mass deployment** (ideal for IoT workloads) and **low-scale deployment** (traditional IT and cloud-native workloads).
>         *   **Mass deployment** leads to **Azure IoT Edge**, which enables running cloud intelligence locally on IoT devices.
>     *   For **datacenter-based workloads**, the decision focuses on whether the workload uses **containers**, **VMs**, or **SQL**.
>         *   **Containers** → Use **Azure Arc-enabled Kubernetes** for hybrid container orchestration.
>         *   **VMware workloads** → Use **Azure Arc-enabled VMware, SCVMM, or individual servers** for management.
>         *   **SQL workloads** → Use **Azure Arc-enabled data services** for hybrid database capabilities.
> *   If the solution is **multicloud**, similar options apply for containers, VMs, and SQL, leveraging **Azure Arc** for unified management across clouds.
> *   If the solution is **Azure-specified**, the decision moves to **hardware type** and **workload type**:
>     *   **Hardware as a service** or **Azure-like datacenter** leads to **Azure Local** or **Azure Stack Hub** for full Azure capabilities on-premises.
>     *   For **data transfer and compute**, the diagram offers **Azure Stack Edge** devices in different models:
>         *   **Datacenter** → Azure Stack Edge Pro GPU
>         *   **Portable** → Azure Stack Edge Pro 2
>         *   **Ruggedized** → Azure Stack Edge Mini R or Pro R

</details>

## Choose a networking service

> This diagram is a **decision-making guide for selecting the right Azure networking and application delivery service** based on whether you are hosting a web application, APIs, or need global distribution and performance optimization.

<img width="1238" height="1594" alt="image" src="https://github.com/user-attachments/assets/661872a6-3d85-4542-a226-f27dc496e913" />

From [Choose a load balancing solution for your scenario](https://learn.microsoft.com/en-us/azure/architecture/guide/technology-choices/load-balancing-overview#choose-a-load-balancing-solution-for-your-scenario)

<details>
<summary><b>Diagram explanation</b> (Click to expand)</summary>

> *   It starts by asking if the workload is a **web application (HTTP/HTTPS)**.
>     *   If **No**, and the application is not internet-facing, the recommendation is **Azure Load Balancer** for internal traffic distribution.
>     *   If **Yes**, and the application is internet-facing, the next question is whether it is **global or deployed in multiple regions**.
>         *   If **Yes**, the solution combines **Traffic Manager + Azure Load Balancer** for global DNS-based routing and regional load balancing.
> *   For **API-only hosting**, the diagram suggests **API Management** for secure API publishing and lifecycle management.
> *   If the application is internet-facing and not limited to APIs, the next consideration is whether you need **SSL offload or application-layer processing per request**.
>     *   If **Yes**, use **Azure Front Door + Application Gateway** for global load balancing with advanced Layer 7 features.
>     *   If hosting only APIs with SSL offload, use **Azure Front Door + API Management**.
> *   For hosting scenarios like **PaaS (App Service, Functions)**, **IaaS (VMs)**, or **AKS**, the diagram recommends:
>     *   **Azure Front Door** for global routing and acceleration.
>     *   Combine with **Application Gateway ingress controller** for AKS or **Azure Load Balancer** for VMs.
> *   If **performance acceleration** is required, **Azure Front Door** is the primary choice because it provides global edge caching and routing.
> *   For workloads that do not require global distribution but need Layer 7 routing, **Application Gateway** is recommended.
>     *   For API-only workloads in this scenario, combine **Application Gateway + API Management**.

</details>

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1532-limegreen" alt="Total views">
  <p>Refresh Date: 2025-10-23</p>
</div>
<!-- END BADGE -->
