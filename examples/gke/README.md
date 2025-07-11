# Understanding Dynamic Workload Scheduler (DWS) Consumption Models for Google Cloud AI Accelerators

Dynamic Workload Scheduler (DWS) is a resource management and capacity scheduling platform for Google Cloud AI Accelerators (GPUs & TPUs).

There are four primary [consumption models](https://cloud.google.com/ai-hypercomputer/docs/consumption-models) to consider:

* **DWS Flex Mode (Flex-start)**
* **DWS Calendar Mode (Reservation)**
* **On-Demand**
* **Spot**

To learn about the pricing model of different DWS modes, visit [Dynamic Workload Scheduler pricing
](https://cloud.google.com/products/dws/pricing?e=48754805&hl=en).

## Key Consumption Models

### DWS Flex Mode

Flex Mode is designed for workloads that can run for up to seven days and can start whenever capacity becomes available. It intelligently queues your request and automatically provisions your virtual machines (VMs) once resources are ready.

* **Ideal Workloads**: Best suited for batch jobs, model fine-tuning, experimentation, shorter training jobs, and offline inference. This includes tasks like small model pre-training, simulations, and batch inference.
* **Key Features**:
    * No minimum duration is required for capacity requests.
    * You only pay for the resources your workload actually consumes; if a job finishes early, you can terminate the VMs and stop paying.
    * You can request any GPU machine type.
    * It offers discounted pricing of up to 53% for vCPUs and GPUs.
    * DWS can be used with orchestrators like Kueue for GKE node pools, supporting popular ML frameworks such as Ray, Kubeflow, and PyTorch.

### DWS Calendar Mode (Future Reservations)

Calendar Mode is for workloads that require a precise start time and have a defined duration. It allows you to reserve GPU capacity in advance for fixed blocks of time.

* **Ideal Workloads**: Suitable for time-bound workloads or for reserving capacity for periods shorter than a one-year Committed Use Discount (CUD). This includes pre-training and multi-host inference for foundation models.
* **Key Features**:
    * Initially supports reservations for 7 or 14-day durations, which can be purchased up to 8 weeks ahead of time.
    * Your reservation is confirmed based on availability, and capacity is delivered to your project on the requested start date.
    * At the end of the specified duration, the VMs are terminated and the reservations are deleted.
    * You can reserve A4X, A4, or A3 Ultra machine types.

### Spot

Spot VMs provide access to compute resources at a lower price but can be preempted by Compute Engine at any time if those resources are needed elsewhere.

* **Ideal Workloads**: Best for fault-tolerant workloads where interruptions are acceptable, such as batch processing, high-performance computing (HPC), and continuous integration/continuous deployment (CI/CD).
* **Key Features**:
    * Offers significant discounts ranging from 60% to 91% for vCPUs, GPUs, and Local SSD disks.
    * You can request any GPU machine type.
    * VMs run until they are stopped, deleted, or preempted by Compute Engine.

## Choosing the Right Model

The best consumption model depends on your workload's specific requirements for duration, cost sensitivity, and predictability.

| **Model** | **Best For** | **Duration** | **Availability** | **Pricing** |
| :--- | :--- | :--- | :--- | :--- |
| **DWS Flex Mode** | Batch jobs, fine-tuning, experiments | Up to 7 days | Queued until capacity is available | Discounted (up to 53%) |
| **DWS Calendar Mode**| Time-bound workloads, advance capacity reservation | Fixed durations (e.g., 7 or 14 days) | Reserved for a future start time | Discounted (up to 53%) |
| **Spot** | Fault-tolerant, non-urgent tasks | Can be preempted at any time | Immediate, based on availability | Deeply discounted (60-91%) |

## Deployment recipes per consumption model
The links below point to recipes to launch several kinds of accelerators on different consumption models, including `spot`, `on demand`, `dws flex`, `dws calendar` and `reservations`.

* [a3-highgpu-8g](./gke-a3-highgpu/README.md)
* [a3-megagpu-8g](./gke-a3-megagpu/README.md)
* [a3-ultragpu-8g](./gke-a3-ultragpu/README.md)
* [a4-highgpu-8g](./gke-a4-highgpu/README.md)
* [a4x-highgpu-4g](./gke-a4x-highgpu/README.md)