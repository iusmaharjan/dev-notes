---
title: Resources for Google Associate Cloud Engineer Certification Preparartion
description: Compilation of documentation, notes, and hands on exercises I used for the preparation for Google Associate Cloud Engineer Certification
date: 2025-07-04
tags:
  - google-cloud
  - certification
---

The [Associate Cloud Engineer](https://cloud.google.com/learn/certification/cloud-engineer) provides the basic overview of the certification and steps to get prepared for the certification. This guide consists of the resources that I utilized for my preparation.

The main resources that I used is the official Cloud Engineer Learning path. I have compiled the documentation, notes, and hands on based on the official exam guide.

I scheduled my exam for June 30, 2025 with revised version of the exam being just launched, and my resources reflects the same exam guide.

# Cloud Engineer Learning Path

[Cloud Engineer Learning Path](https://www.cloudskillsboost.google/paths/11) provides a comprehensive introduction to google cloud and the services that are important for Google Associate Cloud Engineer Certification. My recommended approach to do the learning path is as follows:

- Get an overview of the foundations and core services
  - Google Cloud Fundamentals: Core Infrastructure
  - Essential Google Cloud Infrastructure: Foundation
  - Essential Google Cloud Infrastructure: Core Services
  - Elastic Google Cloud Infrastructure: Scaling and Automation
- If time permits, dive into more details for specific sections
  - Getting Started with Google Kubernetes Engine
  - Logging and Monitoring in Google Cloud
  - Observability in Google Cloud
  - Getting Started with Terraform for Google Cloud
- Practice Hands On (do it in your own Google account if you do not have enough credits)
  - Implement Load Balancing on Compute Engine
  - Set Up an App Dev Environment on Google Cloud
  - Develop your Google Cloud Network
  - Build Infrastructure with Terraform on Google Cloud
- For review, follow "Preparing for Your Associate Cloud Engineer Journey"

The Learning path also recommends the following Skill Badges

- [Develop your Google Cloud Network](https://www.cloudskillsboost.google/course_templates/625)
- [Set Up an App Dev Environment on Google Cloud](https://www.cloudskillsboost.google/course_templates/637)
- [Build Infrastructure with Terraform on Google Cloud](https://www.cloudskillsboost.google/course_templates/636)

# Section 1: Setting up a cloud solution environment (~23% of the exam)

Follow: <https://console.cloud.google.com/cloud-setup/overview>

## 1.1 Setting up cloud projects and accounts

### Creating a resource hierarchy

**Documentation:**

- <https://cloud.google.com/resource-manager/docs/cloud-platform-resource-hierarchy#resource-hierarchy-detail>
- <https://cloud.google.com/resource-manager/docs/creating-managing-organization#setting-up>

**Hands On:**

- <https://cloud.google.com/docs/enterprise/cloud-setup#checklist-heading-1>

**Notes:**

- Best Practices
  - Use a separate staging organization to test policy changes before you apply them in your main organization.
  - Don't use your staging organization for managing testing environments. Testing environments are critical to the productivity of development and DevOps teams.
  - Use a separate organization other than staging or main organization for experimenting.

**Notes:**

- Google Cloud Resource Hierarchy
- Services and APIs are enabled on a per-project basis
- Project Attributes:
  - Project ID (unique, immutable and customizable at creation only)
  - Project Number (unique, immutable, auto-assigned)
  - Project Name (mutable)

### Applying organizational policies to the resource hierarchy

**Documentation:**

- <https://cloud.google.com/resource-manager/docs/organization-policy/overview>
- <https://cloud.google.com/resource-manager/docs/organization-policy/creating-managing-policies>

**Notes:**

- Managed Policies (Example: `iam.managed.disableServiceAccountCreation`)
- Custom Policies
  - Organization policy administrator (r`oles/orgpolicy.policyAdmin`) IAM role on the organization is required
    - `orgpolicy.constraints.list`
    - `orgpolicy.policies.create`
    - `orgpolicy.policies.delete`
    - `orgpolicy.policies.list`
    - `orgpolicy.policies.update`
    - `orgpolicy.policy.get`
    - `orgpolicy.policy.set`
  - Parameters include
    - resource type
    - method types
    - condition
    - action type (ALLOW/DENY)
    - display name
    - description

**Hands On:**

- <https://cloud.google.com/docs/enterprise/cloud-setup#checklist-section-6>

### Granting members Identity and Access Management (IAM) roles within a project

**Documentation:**

- <https://cloud.google.com/iam/docs/overview#policy-inheritance>
- <https://cloud.google.com/iam/docs/granting-changing-revoking-access>
- <https://cloud.google.com/iam/docs/managing-conditional-role-bindings>

**Notes:**

- Custom IAM Role
  - You will need to manage the permissions that define the custom role you create
  - Custom role can only be applied to project or organization level
- The effective allow or deny policy for a resource is the union of the allow or deny policy set on the resource and the allow or deny policy inherited from its ancestors.
- In IAM, permissions are typically represented in the form `service.resource.verb`
- Legacy Basic Roles
  - Unlike with other basic roles, you can't add conditions to role bindings for legacy basic roles.
- Format for Roles:
  - Basic roles
    - Reader: `roles/reader`
    - Writer: `roles/writer`
    - Admin: `roles/admin`
  - Basic roles (legacy):
    - Viewer: `roles/viewer`
    - Editor: `roles/editor`
    - Owner: `roles/owner`
  - Predefined roles: `roles/SERVICE.IDENTIFIER`
  - Project-level custom roles: `projects/PROJECT_ID/roles/IDENTIFIER`
  - Organization-level custom roles: `organizations/ORG_ID/roles/IDENTIFIER`
- Best Practices:
  - Principle of least privilege: Give users the minimum permissions required to perform their role, and remove access as soon as it is no longer needed.
  - Role-based access control (RBAC): Assign permissions to groups of users according to their job role. Do not add permissions to individual user accounts.
- Conditional Binding Use Cases:
  - Grant temporary access (`request.time`)
  - Resource-based access (`resource.type` and `resource.name`)
  - Tag-based access (`resource.matchTag`, `resource.hasTagKey`, `resource.matchTagId`, `resource.hasTagKeyId`)

**Hands On:**

- <https://cloud.google.com/docs/enterprise/cloud-setup#checklist-heading-3>
- <https://cloud.google.com/docs/enterprise/cloud-setup#checklist-heading-5>

### Managing users and groups in Cloud Identity (manually and automated)

**Documentation:**

- <https://cloud.google.com/iam/docs/groups-in-cloud-console>
- <https://cloud.google.com/architecture/identity/overview-google-authentication#managed_user_account>

**Notes:**

- Options for creating users:
  - Create managed user accounts using Cloud Identity or Google Workspace
  - Federate external identity using Cloud Identity or Google Workspace
    - Requires same email in both external and Google Cloud Identities
    - You can sync identities from external source using Google Cloud Directory Sync (GCDS) or provision accounts using an external authoritative source
  - Workforce Identity Federation
    - use an external identity provider (IdP) to authenticate and authorize a workforce without synchronizing user identities from your existing IdP to Google Cloud identities

**Hands On:**

- <https://cloud.google.com/docs/enterprise/cloud-setup#checklist-heading-2>

### Enabling APIs within projects

**Documentation:**

- <https://cloud.google.com/endpoints/docs/openapi/enable-api>

**Notes:**

- `roles/servicemanagement.serviceConsumer` is used to grant access to enable API for a project

### Provisioning and setting up products in Google Cloud Observability

**Documentation:**

- <https://cloud.google.com/stackdriver/docs>
- <https://cloud.google.com/logging/docs/region-support#buckets-locations>
- <https://cloud.google.com/logging/docs/default-settings>
- <https://cloud.google.com/logging/docs/routing/managed-encryption>
- <https://cloud.google.com/logging/docs/custom-constraints>
- <https://cloud.google.com/architecture/stream-logs-from-google-cloud-to-splunk>

**Notes:**

- Set up a central monitoring by creating a scoping project
  - Cloud Monitoring officially supports up to 375 Google Cloud projects per metrics scope
    - You can add up to 3,500 Google Cloud projects per metrics scope , but you might experience performance issues, especially when querying custom metrics or historical data.
    - Cloud Monitoring guarantees performant queries and charts only for 375 Google Cloud projects per metrics scope.
- Use Cloud Logging to consolidate your organization's logs into a single log bucket, stored in the central logging project

**Hands On:**

- <https://cloud.google.com/docs/enterprise/cloud-setup#checklist-heading-7>

### Assessing quotas and requesting increases

**Documentation:**

- <https://cloud.google.com/docs/quotas/view-manage>
- <https://cloud.google.com/resource-manager/docs/creating-managing-projects#managing_project_quotas>

### Setting up standalone organizations

**Documentation:**

- <https://cloud.google.com/resource-manager/docs/standalone-organization-overview>

### Setting up cloud networking

**Documentation:**

- <https://cloud.google.com/vpc/docs/overview>
- <https://cloud.google.com/vpc/docs/shared-vpc>

**Hands On:**

- <https://cloud.google.com/docs/enterprise/cloud-setup#checklist-heading-8>
- <https://cloud.google.com/docs/enterprise/cloud-setup#checklist-heading-9>

### Confirming availability of products in geographical locations (e.g., regional, global)

**Documentation:**

- <https://cloud.google.com/about/locations#products-available-by-location>
- <https://cloud.google.com/compute/docs/regions-zones/global-regional-zonal-resources>

**Note:**

- Check in <https://status.cloud.google.com/>

### Configuring Cloud Asset Inventory and using Gemini Cloud Assist to analyze resources

**Documentation:**

- <https://cloud.google.com/asset-inventory/docs/asset-inventory-overview>
- <https://cloud.google.com/gemini/docs/cloud-assist/iam-requirements>
- <https://cloud.google.com/gemini/docs/cloud-assist-panel#inspect_your_cloud_resources_applications_and_data>

**Notes:**

- Gemini Cloud Assist requires Cloud Asset Viewer (`roles/cloudasset.viewer`) to analyze the resources

## 1.2 Managing billing configuration

### Creating one or more billing accounts

**Documentation:**

- <https://cloud.google.com/billing/docs/concepts#billing_account>
- <https://cloud.google.com/billing/docs/how-to/create-billing-account>

**Notes:**

- Cloud Billing accounts pay for usage costs in Google Cloud projects and Google Maps Platform projects.
  - Cloud Billing accounts do not pay for Google Workspace accounts.
  - Google Workspace customers need a separate Google Workspace billing account.
- A Cloud Billing account operates in a single currency and is linked to a Google payments profile.

**Hands On:**

- <https://cloud.google.com/docs/enterprise/cloud-setup#checklist-heading-4>

### Linking projects to a billing account

**Documentation:**

- <https://cloud.google.com/billing/docs/how-to/view-linked>
- <https://cloud.google.com/billing/docs/how-to/modify-project>
- <https://cloud.google.com/billing/docs/how-to/secure-project-billing-account-link>

**Notes:**

- A Cloud Billing account can be linked to one or more projects.
- Usage costs are tracked by Project and are charged to the linked Cloud Billing account.
- Important: Projects that are not linked to an active Cloud Billing account cannot use Google Cloud or Google Maps Platform services. This is true even if you only use services that are free.
- To prevent unintentionally changing the billing account that pays for a project, or disabling billing on a project, secure the billing relationship of your project by locking the link between a project and its Cloud Billing account.

### Establishing billing budgets and alerts

**Documentation:**

- <https://cloud.google.com/billing/docs/how-to/budgets>
- <https://cloud.google.com/billing/docs/how-to/budgets-notification-recipients>

**Notes:**

- Budge Properties
  - Name
  - Scope
  - Amount
  - Threshold Rules and Actions
- Budget Alerts
  - Role-based
    - Scoped to Billing Account: Billing Account Users and Administrators
    - Scoped to Project: Billing Account Users and Administrators, Project Owners
  - Using Cloud Monitoring
    - You can specify other people in your organization (for example, project managers) to receive budget alert emails.
    - You can set up to 5 Cloud Monitoring channels to define email recipients that will receive budget alerts.

### Setting up billing exports

**Documentation:**

- <https://cloud.google.com/billing/docs/how-to/export-data-bigquery>

**Notes:**

- Types of Exports
  - Standard Usage Cost Data:  Contains standard Cloud Billing account cost usage information, such as account ID, invoice date, services, SKUs, projects, labels, locations, cost, usage, credits, adjustments, and currency.
  - Detailed Usage Cost Data: Includes everything in the *standard usage cost data* plus resource-level cost data, like a virtual machine or SSD that generates service usage.
  - Pricing Data: Contains Cloud Billing account pricing information, such as account ID, services, SKUs, products, geographic metadata, pricing units, currency, aggregation, and tiers. (alternatives are to use pricing page or pricing API).
- Exported data can be queries using BigQuery and visualized using Looker Studio.

**Hands On:**

- [Examining Billing Data with Big Query](https://www.cloudskillsboost.google/paths/11/course_templates/49/labs/548427)

# Section 2: Planning and implementing a cloud solution (~30% of the exam)

## 2.1 Planning and implementing compute resources

### Selecting appropriate compute choices for a given workload (e.g., Compute Engine,Google Kubernetes Engine [GKE], Cloud Run, Cloud Run functions, Knative serving)

**Documentation:**

- <https://cloud.google.com/blog/products/compute/choosing-the-right-compute-option-in-gcp-a-decision-tree>
- <https://cloud.google.com/hosting-options>
- <https://cloud.google.com/compute/docs/overview>

### Launching a compute instance (e.g., availability policy, SSH keys)

**Documentation:**

- <https://cloud.google.com/compute/docs/instances/setting-vm-host-options>
- <https://cloud.google.com/compute/docs/instances/create-start-instance>
- <https://cloud.google.com/compute/docs/machine-resource>

**Notes:**

- Availability Policy
  - Host Events: Maintenance Event and Host Error
  - Maintenance Policy
    - Behavior: Migrate / Terminate
    - Automatic Restart Policy
    - Host Error Detection Time
    - Local SSD Recovery Time
  - Preemptible and Spot Instance
- Pricing Model
- Images: Public vs Custom Images
- Metadata and scripts for startup and shutdown

**Machine Families and Series:**

| Purpose                      | Family                                                                 | Series                          |
| ---------------------------- | ---------------------------------------------------------------------- | ------------------------------- |
| General purpose              | **N** (Balanced), **E** (Cost Optimized), **Tau**(Scale-out Optimized) | N1, N2, N2D, E2, TauT2D, TauT2A |
| Compute optimized            | **C**, **H**                                                           | C2, C2D, H3                     |
| Memory optimized             | **M**                                                                  | M1, M2, M3                      |
| Accelerator optimized (GPUs) | **A**, **G**                                                           | A2, G2                          |

**Size Categories:**

| Size         | Description         | Memory Ratio           |
| ------------ | ------------------- | ---------------------- |
| **standard** | Balanced CPU:memory | 1:4 (1 vCPU : 4GB RAM) |
| **highmem**  | More memory         | 1:8                    |
| **highcpu**  | More CPU            | 1:1                    |
| **megamem**  | Very high memory    | 1:14+                  |
|              |                     |                        |

**Hands On:**

- [Creating Virtual Machines](https://www.cloudskillsboost.google/paths/11/course_templates/50/labs/530377)
- [Working with Virtual Machines](https://www.cloudskillsboost.google/paths/11/course_templates/50/labs/530386)

### Choosing the appropriate storage for Compute Engine (e.g., zonal Persistent Disk, regional Persistent Disk, Google Cloud Hyperdisk)

**Documentation:**

- <https://cloud.google.com/compute/docs/disks>

**Notes:**

- Zonal persistent disk: Efficient, reliable block storage
- Regional persistent disk: Regional block storage replicated in two zones
- Local SSD: High performance, transient, local block storage
  - 375 GB in size
  - up to 24 can be attached for 9TB per instance
- Cloud Storage buckets: Affordable object storage
- Filestore: High performance file storage for Google Cloud users
- RAM Disk (tempfs)
- Max number of persistent disks is 16 for shared-core and 128 for others
- Persistent Disk Types
  - pd-standard
  - pd-ssd
  - pd-balanced
  - pd-extreme (zonal only)

### Creating an autoscaled managed instance group by using an instance template

**Documentation:**

- <https://cloud.google.com/compute/docs/instance-groups/creating-groups-of-managed-instances>
- <https://cloud.google.com/compute/docs/instance-groups/updating-migs>

**Notes:**

- Methods to apply new configuration:
  - Automatic (proactive)
  - Selective (opportunistic)
  - Recreation of VMs
- Instance group can be resized and autoscaled
- Autoscaling Policies
  - CPU Utilization
  - Load Balancing capacity
  - Monitoring Metrics
  - Queue-based Workload
  - Schedule-based

**Hands On:**

- [Configure an Application Load Balancer with Autoscaling](https://www.cloudskillsboost.google/paths/11/course_templates/178/labs/470301)

### Configuring OS Login

**Documentation:**

- <https://cloud.google.com/compute/docs/oslogin>
- <https://cloud.google.com/compute/docs/oslogin/set-up-oslogin>
- <https://cloud.google.com/compute/docs/oslogin/manage-oslogin-in-an-org>

**Note:**

- lets you use Compute Engine IAM roles to manage SSH access to Linux instances
- Set `enable-oslogin` and `enable-oslogin-2fa` to TRUE in project or VM metadata

### Configuring VM Manager

**Documentation:**

- <https://cloud.google.com/compute/docs/vm-manager>
- <https://cloud.google.com/compute/vm-manager/docs/setup>
- <https://cloud.google.com/compute/vm-manager/docs/patch/create-patch-job>
- <https://cloud.google.com/compute/vm-manager/docs/os-policies/working-with-os-policies>

**Notes:**

- VM Manager is a suite of tools that you can use to manage operating systems for large virtual machine (VM) fleets running Windows and Linux on Compute Engine and provides following services:
  - Patch
  - OS Inventory Management
  - OS Policies

### Using Spot VM instances and custom machine types

**Documentation:**

- <https://cloud.google.com/compute/docs/instances/preemptible>
- <https://cloud.google.com/compute/docs/instances/spot>
- <https://cloud.google.com/compute/docs/instances/create-use-spot>
- <https://cloud.google.com/compute/docs/instances/creating-instance-with-custom-machine-type>

### Installing and configuring the command-line interface (CLI) for Kubernetes (kubectl)

**Documentation:**

- <https://cloud.google.com/kubernetes-engine/docs/how-to/cluster-access-for-kubectl>

**Notes:**

```
gcloud components install gke-gcloud-auth-plugin
gcloud container clusters get-credentials bootcamp --zone=us-west1-b
```

### Deploying a GKE cluster with different configurations (e.g., GKE Autopilot, regional clusters, private clusters)

**Documentation:**

- <https://cloud.google.com/kubernetes-engine/docs/concepts/kubernetes-engine-overview>
- <https://cloud.google.com/kubernetes-engine/docs/concepts/configuration-overview>
- <https://cloud.google.com/kubernetes-engine/docs/how-to/creating-an-autopilot-cluster>
- <https://cloud.google.com/kubernetes-engine/docs/how-to/creating-a-zonal-cluster>
- <https://cloud.google.com/kubernetes-engine/docs/how-to/creating-a-regional-cluster>

**Notes:**

- Mode: Autopilot vs Standard
- Availability: Zonal (Standard only) vs Regional
- Network Routing: VPC-native vs Routes-based
- Network Isolation: Public vs Private

### Deploying a containerized application to GKE

**Documentation:**

- Cloud Build to build containers:
  - <https://cloud.google.com/artifact-registry/docs/docker/store-docker-container-images>
  - <https://cloud.google.com/build/docs/building/build-containers>
  - <https://cloud.google.com/build/docs/configuring-builds/create-basic-configuration>
- <https://cloud.google.com/kubernetes-engine/docs/concepts/network-overview>
- <https://cloud.google.com/kubernetes-engine/docs/get-started/deploy-workloads>
- <https://cloud.google.com/kubernetes-engine/docs/concepts/service>

**Hands On:**

- <https://www.cloudskillsboost.google/paths/11/course_templates/2/labs/541354>
- <https://www.cloudskillsboost.google/course_templates/663>

### Deploying an application to serverless compute platforms, including for the processing of Google Cloud events (e.g., Pub/Sub events, Cloud Storage object change notification events, Eventarc)

**Documentation:**

- App Engine
  - <https://cloud.google.com/appengine/docs/an-overview-of-app-engine>
  - <https://cloud.google.com/appengine/docs/the-appengine-environments>
- Cloud Run
  - <https://cloud.google.com/run/docs/overview/what-is-cloud-run>
  - <https://cloud.google.com/blog/topics/developers-practitioners/cloud-run-story-serverless-containers>
  - <https://cloud.google.com/blog/topics/developers-practitioners/learn-cloud-functions-snap>
  - <https://cloud.google.com/run/docs/triggering/trigger-with-events>

**Common Events:**

| **Trigger Type**         | **Event Sources** | **Common Use Cases**                             | **Example Events**                                |
| ------------------------ | ----------------- | ------------------------------------------------ | ------------------------------------------------- |
| **HTTP**                 | Direct requests   | REST APIs, webhooks, web apps, microservices     | `GET`, `POST`, `PUT`, `DELETE` requests           |
| **Cloud Storage**        | Object lifecycle  | File processing, image resizing, data pipelines  | `finalize`, `delete`, `archive`, `metadataUpdate` |
| **Pub/Sub**              | Message queues    | Async processing, event streaming, notifications | Message published to topic                        |
| **Cloud Firestore**      | Database changes  | Real-time data sync, user activity tracking      | Document `write`, `delete`                        |
| **Firebase Auth**        | User management   | User onboarding, profile setup, access control   | User `create`, `delete`                           |
| **Firebase Realtime DB** | Database events   | Live data updates, chat applications             | `create`, `write`, `update`, `delete`             |
| **Cloud Scheduler**      | Time-based        | Cron jobs, scheduled tasks, maintenance          | Scheduled execution (cron format)                 |
| **Eventarc**             | Advanced events   | Audit logs, custom events, 3rd party integration | Cloud Audit Logs, custom events                   |

## 2.2 Planning and implementing storage and data solutions

### Choosing and deploying data products (e.g., Cloud SQL, BigQuery, Firestore, Spanner, Bigtable, AlloyDB, Dataflow, Pub/Sub, Google Cloud Managed Service for Apache Kafka, Memorystore)

**Documentation:**

- <https://cloud.google.com/storage-options/>

**Hands On:**

- [Implementing Cloud SQL](https://www.cloudskillsboost.google/paths/11/course_templates/49/labs/548411)

### Choosing and deploying storage products (e.g., Cloud Storage, Filestore, Google Cloud NetApp Volumes) and Cloud Storage options (e.g., Standard, Nearline, Coldline, Archive)

**Documentation:**

- <https://cloud.google.com/storage/docs/introduction>
- <https://cloud.google.com/filestore/docs/overview>
- <https://cloud.google.com/netapp/volumes/docs/discover/overview>
- <https://cloud.google.com/parallelstore/docs/overview>

### Loading data (e.g., command-line upload, load data from Cloud Storage, Storage Transfer Service)

**Documentation:**

- <https://cloud.google.com/blog/topics/developers-practitioners/bigquery-explained-data-ingestion>
- <https://cloud.google.com/bigquery/docs/loading-data>

**Notes:**

- BigQuery Data Transfer Service is the simplest process to set up transfers between Cloud Storage and BigQuery. It is encompassed by one command. It is also free.ansfer Options

**Data Transfer Methods:**

| Method                       | Use Case                                                    | Speed                | Cost                  |
| ---------------------------- | ----------------------------------------------------------- | -------------------- | --------------------- |
| **gsutil**                   | Command-line uploads/downloads                              | Depends on bandwidth | Free (except network) |
| **Console Upload**           | Small files via web interface                               | Slow                 | Free                  |
| **JSON/XML API**             | Programmatic access                                         | Moderate             | Free (except network) |
| **Transfer Appliance**       | Petabyte-scale offline transfer                             | N/A (shipped)        | Hardware rental fees  |
| **Storage Transfer Service** | Scheduled/recurring transfers for Cloud-to-Cloud Migrations | Fast                 | Free                  |
| **Offline Media Import**     | Third-party provider uploads data from physical media       | N/A                  | Third party fees      |

**Specialized Transfer Options:**

| Service                        | Best For           | Capacity |
| ------------------------------ | ------------------ | -------- |
| **Transfer Appliance (TA40)**  | 40TB of data       | 40TB     |
| **Transfer Appliance (TA300)** | 300TB of data      | 300TB    |
| **BigQuery Data Transfer**     | Analytics data     | Varies   |
| **Database Migration Service** | Database transfers | Varies   |

### Maintaining multi-region redundancy across data solutions

**Documentation:**

- Cloud SQL
  - <https://cloud.google.com/sql/docs/mysql/configure-ha>
  - <https://cloud.google.com/sql/docs/mysql/replication>
  - <https://cloud.google.com/spanner/docs/instance-configurations>
  - <https://cloud.google.com/spanner/docs/replication>
  - <https://cloud.google.com/storage/docs/availability-durability>
  - <https://cloud.google.com/storage/docs/using-cross-bucket-replication>
  - <https://cloud.google.com/bigtable/docs/replication-overview>

**Notes:**

- Cloud SQL
  - Regional Failover
  - Supports cross-regional and external replicas
- Spanner supports regional, dual-regional, and multi-regional configurations
  - Regions can be read-write, read-only or witness regions
  - Strongly consistent replication
- Cloud Storage supports Region, Dual-Region, and Multi-Region location configurations
  - Objects stored in a dual-region or multi-region bucket are stored redundantly in at least two separate geographic places.
- Cloud Storage also support Cross-Bucket Replication
- Big Table support eventually consistent replication across clusters in single region, multi-region and global configurations

## 2.3 Planning and implementing networking resources

### Creating a VPC with subnets (e.g., custom mode VPC, Shared VPC)

**Documentation:**

- <https://cloud.google.com/vpc/docs/vpc>
- <https://cloud.google.com/vpc/docs/shared-vpc>

**Notes:**

- VPC Types: default, auto-mode, custom-mode
- Auto mode subnets size is /20 (expandable up to /16)

**Hands On:**

- [VPC Networking](https://www.cloudskillsboost.google/paths/11/course_templates/50/labs/530364)

### Creating and applying Cloud Next Generation Firewall (Cloud NGFW) policies with ingress and egress rules and attributes (e.g., action, source, destination, targets, protocols, ports)

**Documentation:**

- <https://cloud.google.com/firewall/docs/about-firewalls>
- <https://cloud.google.com/firewall/docs/firewalls>
- <https://cloud.google.com/firewall/docs/firewall-policies-rule-details>

### Using Tags (e.g., secure Tags) and service accounts in Cloud NGFW policy rules

**Documentation:**

- <https://cloud.google.com/firewall/docs/tags-firewalls-overview>

**Notes:**

- Identity and Access Management (IAM)-governed tags, also referred to as secure tags, are created and managed in Resource Manager as tag keys and tag values.
  - Secure tag values can be used to specify sources for ingress rules and targets for ingress or egress rules in a hierarchical firewall policy, global network firewall policy, or regional network firewall policy.
  - To use a secure tag key with Cloud NGFW, you must set the `purpose` attribute of the tag key to `GCE_FIREWALL`, and you must specify the `purpose-data` attribute
    - Uou can set the `purpose-data` attribute of the tag key to `network`, followed by a single VPC network specification. The specified VPC network must be located in the parent organization.
    - You can set the `purpose-data` attribute of the tag key to `organization=auto`.
- Network tags are character strings without access controls that can be added to virtual machine (VM) instances or instance templates.
  - Network tags can be used to specify sources for ingress Virtual Private Cloud (VPC) firewall rules and targets for ingress or egress VPC firewall rules.

### Establishing network connectivity (e.g., Cloud VPN, VPC Network Peering, Cloud Interconnect)

**Documentation:**

- <https://cloud.google.com/network-connectivity/docs/vpn/concepts/topologies>
- <https://cloud.google.com/network-connectivity/docs/vpn/how-to/moving-to-ha-vpn>

**Hands On:**

- <https://www.cloudskillsboost.google/paths/11/course_templates/178/labs/470286>

**Network Connectivity Options**

| Connection Method        | Description                                                                                                                                                                                                                     | SLA                                                                                   | Capacity                                | Access Type           | Requirements                                                                          |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- | --------------------------------------- | --------------------- | ------------------------------------------------------------------------------------- |
| Cloud VPN                | IPSec Tunnel that uses cloud router to make connection dynamic and exchanges route information over VPN using BGP                                                                                                               | HA 99.99% and Classic 99.9%<br>Max MTU:  1460 bytes                                   | 1.5-3 Gbps per tunnel                   | Internal IP Addresses | Remote VPN Gateway                                                                    |
| Direct Peering           | Puts router in the same public datacenter as a Google Point of Presence (PoP)                                                                                                                                                   | Not covered by a Google SLA                                                           | 10 Gbps per link                        | Public IP Address     | Connection in Google Cloud PoP                                                        |
| Carrier Peering          | Gives direct access from an on-premise network through a service provider's network                                                                                                                                             | Not covered by a Google SLA                                                           | Varies based on partner offering        | Internal IP Addresses | Service Provider                                                                      |
| Dedicated Interconnect   | Allows for one or more direct, private connections to Google using a colocation facility                                                                                                                                        | Covered by SLA up to 99.99% SLA, Can be backed up by VPN for even greater reliability | 10 Gbps or 100 Gbps per connection link | Internal IP Addresses | Connection to a Colocation Facility                                                   |
| Partner Interconnect     | Connectivity through a supported Service Provider (Useful if a data center is in a physical location that cannot reach dedicated interconnect colocation facility or if the data does not warrant an entire 10 GBps connection) | Can be covered up to a 99.99% SLA                                                     | 50 Mbps -50 Gbps per connection link    | Internal IP Addresses | Service Provider                                                                      |
| Cross-Cloud Interconnect | Establish high-bandwidth dedicated connectivity between Google Cloud and another cloud service provider to support adoption of multi-cloud strategy                                                                             | 99.99% SLA                                                                            | 10 Gbps or 100 Gbps per connection link | Internal IP Addresses | Primary and redundant<br>ports (Google Cloud<br>and remote cloud<br>service provider) |

### Choosing and deploying load balancers

**Documentation:**

- <https://cloud.google.com/load-balancing/docs/load-balancing-overview>
- <https://cloud.google.com/load-balancing/docs/choosing-load-balancer>
- GKE
  - <https://cloud.google.com/kubernetes-engine/docs/concepts/ingress>
  - <https://cloud.google.com/kubernetes-engine/docs/concepts/ingress-ilb>
  - <https://cloud.google.com/kubernetes-engine/docs/concepts/ingress-xlb>
  - <https://cloud.google.com/kubernetes-engine/docs/how-to/load-balance-ingress>
  - <https://cloud.google.com/kubernetes-engine/docs/how-to/internal-load-balance-ingress>

**Notes:**

- Choose an Application Load Balancer when you need a flexible feature set for your applications with HTTP(S) traffic.
- Application Load balancer Health Check Sources: `35.191.0.0/16` and `130.211.0.0/22`
- Choose a proxy Network Load Balancer to implement TCP proxy load balancing to backends in one or more regions. (TCP/SSL connections)
- Choose a passthrough Network Load Balancer to preserve client source IP addresses, avoid the overhead of proxies, and to support additional protocols like UDP, ESP, and ICMP.
- GKE
  - Internal Application Load Balancer can only use Network Endpoint Groups(NEGs).
  - To implement network load balancing you create a service object with these settings:
    - type: LoadBalancer
    - External Traffic Policy
      - Cluster - traffic will be load balanced to any healthy GKE node and then kube-proxy will send it to a node with the pod.
      - Local - nodes without the pod will be reported as unhealthy. Traffic will only be sent to nodes with the pod. Traffic will be sent directly to pod with source ip header info included.
  - To implement an external Application Load Balancer, create an ingress object with the following settings:
    - Routing depends on URL path, session affinity, and the balancing mode of backend Network endpoint groups (NEGS)
    - The object type is ingress.
    - Using ingress.class: “gce” annotation in the metadata deploys an external load balancer
    - External load balancer is deployed at Google Points of presence
    - Static IP for ingress lasts as long as the object.
  - To implement an internal Application Load Balancer, create an ingress object with the following settings:
    - Routing depends on URL path, session affinity, and balancing mode of the backend NEGS
    - The object kind is ingress
    - Metadata requires an Ingress.class: “gce-internal” to spawn an internal load balancer.
    - Proxies are deployed in a proxy only subnet in a specific region in your VPC.
    - Only NEGs are supported. Use the following annotation in your service metadata:
      - `cloud.google.com/neg: '{"ingress": true}'`
    - Forwarding rule is assigned from the GKE node address range.

**Hands On:**

- [Configure an Application Load Balancer with Autoscaling](https://www.cloudskillsboost.google/paths/11/course_templates/178/labs/470301)
- <https://www.cloudskillsboost.google/paths/11/course_templates/178/labs/470309>

### Differentiating Network Service Tiers

**Documentation:**

- <https://cloud.google.com/network-tiers/docs/overview>

## 2.4 Planning and implementing resources through infrastructure as code

### Infrastructure as code tooling (e.g., Fabric FAST, Config Connector, Terraform, Helm)

**Documentation:**

- <https://developer.hashicorp.com/terraform/intro>
- <https://cloud.google.com/docs/terraform>
- <https://cloud.google.com/infrastructure-manager/docs/overview>
- <https://github.com/GoogleCloudPlatform/cloud-foundation-fabric>
- <https://github.com/GoogleCloudPlatform/cloud-foundation-fabric/tree/master/fast>
- <https://cloud.google.com/config-connector/docs/overview>

**Hands On:**

- <https://www.cloudskillsboost.google/paths/11/course_templates/178/labs/470317>

**Notes:**

- Fabric FAST provides provides terraform modules to quickly set up production-ready GCP organization.

### Planning and executing infrastructure as code deployments, including versioning, state management, and updates

**Documentation:**

- <https://cloud.google.com/docs/terraform/resource-management/store-state>
- <https://cloud.google.com/docs/terraform/resource-management/export>

# Section 3: Ensuring successful operation of a cloud solution (~27% of the exam)

## 3.1 Managing compute resources

### Remotely connecting to a Compute Engine instance

**Documentation:**

- <https://cloud.google.com/compute/docs/connect/standard-ssh#openssh-client>
- <https://cloud.google.com/solutions/connecting-securely>
- <https://cloud.google.com/compute/docs/instances/connecting-to-windows>

**Notes:**

- Connection through internal IP addresses
  - using IAP
  - using Bastion Host
  - using Cloud VPN

### Viewing current running Compute Engine instances

**Documentation:**

- <https://cloud.google.com/compute/docs/instances/get-list>

### Working with snapshots and images (e.g., create, view, and delete images or snapshots; schedule a snapshot)

**Documentation:**

- <https://cloud.google.com/compute/docs/disks/snapshots>
- <https://cloud.google.com/compute/docs/disks/manage-snapshots>

**Notes:**

- You can’t delete a snapshot schedule that is still attached to a persistent disk
- Snapshots are incremental
- A Snapshot schedule and its source persistent disk have to be in the same region
- Snapshot Types:
  - Standard
  - Archive
  - Instant
- You can restore them to a new persistent disk. The new disk can be in a different zone or region, so you can use snapshots to move VMs
- Use Cases
  - Back up using snapshot
  - Migrate data using snapshot
  - Transfer from HDD to SSD

### Viewing current running GKE cluster inventory (e.g., nodes, Pods, Services)

**Documentation:**

- <https://cloud.google.com/kubernetes-engine/docs/quickstarts/tour-cluster>

### Configuring GKE to access Artifact Registry

**Documentation:**

- <https://cloud.google.com/artifact-registry/docs/integrate-gke>

### Working with GKE node pools (e.g., add, edit, or remove a node pool; autoscaling node pool)

**Documentation:**

- <https://cloud.google.com/kubernetes-engine/docs/concepts/node-pools>
- <https://cloud.google.com/kubernetes-engine/docs/how-to/create-arm-clusters-nodes>

### Working with Kubernetes resources (e.g., Pods, Services, StatefulSets)

**Documentation:**

- <https://cloud.google.com/kubernetes-engine/docs/concepts/service>
- <https://cloud.google.com/kubernetes-engine/docs/learn/get-started-with-kubernetes>

### Managing horizontal and vertical Pod autoscaling configurations

**Documentation:**

- <https://cloud.google.com/kubernetes-engine/docs/concepts/cluster-autoscaler>
- <https://cloud.google.com/kubernetes-engine/docs/how-to/scaling-apps>
- <https://cloud.google.com/kubernetes-engine/docs/concepts/horizontalpodautoscaler>
- <https://cloud.google.com/kubernetes-engine/docs/concepts/verticalpodautoscaler>

### Managing GKE Autopilot Pod resource requests

**Documentation:**

- <https://cloud.google.com/kubernetes-engine/docs/how-to/autopilot-compute-classes>

### Deploying new versions of a Cloud Run application

**Documentation:**

- <https://cloud.google.com/run/docs/deploying#revision>

**Notes:**

- Changing any configuration settings results in the creation of a new revision, even if there is no change to the container image.
- Each revision created is immutable.

### Adjusting application traffic splitting parameters (e.g., Cloud Run, Cloud Run functions, GKE)

**Documentation:**

- <https://cloud.google.com/kubernetes-engine/docs/concepts/traffic-management#splitting>
- <https://cloud.google.com/run/docs/rollouts-rollbacks-traffic-migration#split-traffic>

### Configuring autoscaling for a Cloud Run application

**Documentation:**

- <https://cloud.google.com/run/docs/about-instance-autoscaling>

**Notes:**

- Configure Maximum Instances, Minimum Instances, and Concurrency

## 3.2 Managing storage and data solutions

### Managing and securing objects in Cloud Storage buckets

**Documentation:**

- <https://cloud.google.com/storage/docs/creating-buckets>
- Security and Encryption

  **Notes:**

- If you do not specify a location, the bucket will be created by default in the US.

**Hands On:**

- [Cloud Storage](https://www.cloudskillsboost.google/paths/11/course_templates/49/labs/548407)

### Setting object lifecycle management policies for Cloud Storage buckets

**Documentation:**

- <https://cloud.google.com/storage/docs/storage-classes>
- <https://cloud.google.com/storage/docs/lifecycle>

**Hands On:**

- [Cloud Storage](https://www.cloudskillsboost.google/paths/11/course_templates/49/labs/548407)

### Executing queries to retrieve data from data instances (e.g., Cloud SQL, BigQuery, Bigtable, Spanner, Firestore, AlloyDB)

**Documentation:**

- <https://cloud.google.com/spanner/docs/create-query-database-console#run-query>
- <https://cloud.google.com/bigtable/docs/bigquery-analysis>
- <https://cloud.google.com/datastore/docs/concepts/queries>

**Notes:**

- Cloud SQL does not support user-defined functions so you may need to deploy MySQL in a VM if you require to support user-defined function

### Estimating costs of data storage resources

**Documentation:**

- <https://cloud.google.com/products/calculator?hl=en>

### Backing up and restoring database instances (e.g., Cloud SQL, Firestore, Spanner, AlloyDB, Bigtable)

**Documentation:**

- See for each service

### Reviewing job status (e.g., Dataflow, BigQuery)

**Documentation:**

- <https://cloud.google.com/dataflow/docs/guides/jobs-list>
- <https://cloud.google.com/bigquery/docs/managing-jobs#about-jobs>

### Using Database Center to manage the Google Cloud database fleet

**Documentation:**

- <https://cloud.google.com/database-center/docs/overview>

## 3.3 Managing networking resources

### Adding a subnet to an existing VPC

**Documentation:**

- <https://cloud.google.com/vpc/docs/create-modify-vpc-networks#subnet-rules>

### Expanding a subnet to have more IP addresses

**Documentation:**

- <https://cloud.google.com/sdk/gcloud/reference/compute/networks/subnets/expand-ip-range>
- <https://cloud.google.com/vpc/docs/create-modify-vpc-networks#expand-subnet>

**Notes:**

- `gcloud compute networks subnets expand-ip-range SUBNET --prefix-length = PREFIX_LENGTH`
- Subnet size
  - 21 - 2046 hosts
  - 20 - 4091 hosts

### Reserving static external or internal IP addresses

**Documentation:**

- <https://cloud.google.com/vpc/docs/reserve-static-internal-ip-address>
- <https://cloud.google.com/vpc/docs/reserve-static-external-ip-address>

### Adding custom static routes in a VPC

**Documentation:**

- <https://cloud.google.com/vpc/docs/static-routes>

### Working with Cloud DNS and Cloud NAT

**Documentation:**

- <https://cloud.google.com/nat/docs/overview>
- <https://cloud.google.com/nat/docs/gce-example>
- <https://cloud.google.com/dns/docs/overview/>

**Hands On:**

- [Implement Private Access and Cloud NAT](https://www.cloudskillsboost.google/paths/11/course_templates/50/labs/530368)
- [Tutorial: Set up a domain](https://cloud.google.com/dns/docs/tutorials/create-domain-tutorial)

## 3.4 Monitoring and logging

### Creating Cloud Monitoring alerts based on resource metrics

**Documentation:**

- <https://cloud.google.com/monitoring/alerts>

**Hands On:**

- <https://www.cloudskillsboost.google/paths/11/course_templates/49/labs/548435>

### Creating and ingesting Cloud Monitoring custom metrics (e.g., from applications or logs)

**Documentation:**

- <https://cloud.google.com/monitoring/agent/ops-agent>
- <https://cloud.google.com/monitoring/bindplane/collecting-on-prem-hybrid>

### Exporting logs to external systems (e.g., on-premises, BigQuery)

**Documentation:**

- <https://cloud.google.com/logging/docs/export/configure_export_v2>
- <https://cloud.google.com/logging/docs/export/pubsub#integrate-thru-pubsub>

### Configuring log buckets, log analytics, and log routers

**Documentation:**

- <https://cloud.google.com/logging/docs/buckets>
- <https://cloud.google.com/logging/docs/analyze/query-and-view>
- <https://cloud.google.com/logging/docs/routing/overview>

### Viewing and filtering logs in Cloud Logging

**Documentation:**

- <https://cloud.google.com/logging/docs/log-analytics>
- <https://cloud.google.com/logging/docs/view/building-queries>
- <https://cloud.google.com/logging/docs/analyze/query-and-view>

### Viewing specific log message details in Cloud Logging

**Documentation:**

- <https://cloud.google.com/logging/docs/view/logs-explorer-interface>
- <https://cloud.google.com/logging/docs/export/using_exported_logs>

### Using cloud diagnostics to research an application issue (e.g., Cloud Trace, Cloud Profiler, Query Insights, index advisor)

**Documentation:**

- <https://cloud.google.com/trace/docs/overview>
- <https://cloud.google.com/trace/docs/setup>
- <https://cloud.google.com/error-reporting/docs/grouping-errors>
- <https://cloud.google.com/profiler/docs/about-profiler>

### Viewing the Personalized Service Health dashboard

**Documentation:**

- <https://cloud.google.com/service-health/docs/overview>

### Configuring and deploying Ops Agent

**Documentation:**

- <https://cloud.google.com/monitoring/agent/ops-agent/install-index>

### Deploying Google Cloud Managed Service for Prometheus

**Documentation:**

- <https://cloud.google.com/stackdriver/docs/managed-prometheus>
- <https://cloud.google.com/stackdriver/docs/managed-prometheus/setup-managed>
- <https://cloud.google.com/stackdriver/docs/managed-prometheus/query-cm>

### Configuring audit logs

**Documentation:**

- <https://cloud.google.com/logging/docs/audit>

### Using Gemini Cloud Assist for Cloud Monitoring

**Documentation:**

- <https://cloud.google.com/gemini/docs/bigquery/set-up-gemini>
- <https://cloud.google.com/gemini/docs/cloud-assist/overview>

### Using Active Assist to optimize resource utilization

**Documentation:**

- <https://cloud.google.com/recommender/docs/whatis-activeassist>
- <https://cloud.google.com/blog/topics/developers-practitioners/automated-cleanup-unused-google-cloud-projects/>

# Section 4: Configuring access and security (~20% of the exam)

## 4.1 Managing Identity and Access Management (IAM)

### Viewing and creating IAM policies

**Documentation:**

- <https://cloud.google.com/iam/docs/overview>

### Managing the various role types and defining custom IAM roles (e.g., basic, predefined, custom)

**Documentation:**

- <https://cloud.google.com/iam/docs/creating-custom-roles>

## 4.2 Managing service accounts

### Creating service accounts

**Documentation:**

- <https://cloud.google.com/docs/authentication#service-accounts>
- <https://cloud.google.com/iam/docs/service-accounts-create#creating_a_service_account>
- <https://cloud.google.com/iam/docs/service-account-permissions>

**Hands On:**

- <https://www.cloudskillsboost.google/paths/11/course_templates/49/labs/548397>

### Using service accounts in IAM policies with minimum permissions

**Documentation:**

- <https://cloud.google.com/docs/authentication/>

### Assigning service accounts to resources

**Documentation:**

- <https://cloud.google.com/compute/docs/access/create-enable-service-accounts-for-instances#using>
- <https://developers.google.com/identity/protocols/oauth2/service-account#python>

**Notes:**

- Resources in Google Cloud can be assigned a service account that acts as the resource’s default identity. This process is known as attaching a service account to a resource. The resource, or apps running on the resource, impersonate the attached service account to access Google Cloud APIs

### Managing IAM permissions of a service account

**Documentation:**

- <https://cloud.google.com/iam/docs/manage-access-service-accounts>

**Notes:**

- To add a policy to a service account run the `gcloud projects add-iam-policy-binding` command.
  - The `--member` argument should be a string starting with `serviceAccount:` and containing your service account id with an email address suffix of `@project_id.iam.gserviceaccount.com` and `--role` argument contains the role you want to assign to the service account

### Managing service account impersonation

**Documentation:**

- <https://cloud.google.com/docs/authentication/use-service-account-impersonation>

**Notes:**

- Requires Service Account Token Creator (roles/iam.serviceAccountTokenCreator) IAM role with iam.serviceAccounts.getAccessToken
- CLI
  - One Time: `gcloud storage buckets list --impersonate-service-account=SERVICE_ACCT_EMAIL`
  - Default: `gcloud config set auth/impersonate_service_account SERVICE_ACCT_EMAIL`
  - Application Default Credentials: `gcloud auth application-default login --impersonate-service-account SERVICE_ACCT_EMAIL`

### Creating and managing short-lived service account credentials

**Documentation:**

- <https://cloud.google.com/iam/docs/create-short-lived-credentials-direct>

### Using a Google Cloud service account with a GKE application

**Documentation:**

- <https://cloud.google.com/kubernetes-engine/docs/how-to/service-accounts>
- <https://cloud.google.com/iam/docs/create-managed-workload-identities-gke>
