# A3 High Consumption Model Examples

Below are examples and links to configurations for different consumption models for `a3-highgpu` VMs.

### Spot
TBC

### Dynamic Workload Scheduler (DWS) Flex Start
To deploy a GKE cluster for a3-highgpu-8g nodes using DWS, you can go through this process:

Clone the Cluster Toolkit from the git repository:
```
cd ~
git clone https://github.com/GoogleCloudPlatform/cluster-toolkit.git
```
Install the Cluster Toolkit:
```
cd cluster-toolkit && git checkout main && make
```
Create a Cloud Storage bucket to store the state of the Terraform deployment:
```
gcloud storage buckets create gs://BUCKET_NAME \
    --default-storage-class=STANDARD \
    --project=PROJECT_ID \
    --location=COMPUTE_REGION_TERRAFORM_STATE \
    --uniform-bucket-level-access
gcloud storage buckets update gs://BUCKET_NAME --versioning
```
Deploy the cluster using environment variables to specify DWS parameters:
```
gcluster deploy examples/gke-a3-highgpu.yaml \
    --vars static_node_count=0 \
    --vars enable_flex_start=true \
    --vars enable_queued_provisionning=true \
    --vars maax_run_duration=3600 \
    --vars project_id=PROJECT_UD \
    --vars deployment_name=gke-a3high-deployment \
    --vars authorized_cidr= <your-ip-address>/32
```
### Reservation or Dynamic Workload Scheduler (DWS) Calendar Mode
TBC
### On Demand
TBC
