---
title: "Blog 1"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

## Automating Oracle Database@AWS Deployment with Terraform

Deploying Oracle Database systems on cloud platforms is always a challenge that requires balancing performance, scalability, and consistency in infrastructure management. With Oracle Database@AWS (ODB@AWS), Oracle has brought the Exadata platform – hardware system optimized specifically for Oracle Database – directly into AWS data centers, allowing businesses to leverage Oracle's high performance while taking advantage of AWS's rich service ecosystem.

However, to fully build an Oracle Database@AWS environment, administrators must perform multiple configuration steps such as setting up ODB Network, deploying Exadata Infrastructure, creating VM Clusters, and connecting to Amazon VPC. If done entirely on AWS Console, this process is quite complex, time-consuming, and prone to errors when the number of deployment environments increases.

In this article, we will explore how to use Terraform to automate the entire Oracle Database@AWS deployment process. Through the Infrastructure as Code (IaC) model, businesses can standardize infrastructure, minimize configuration errors, and deploy systems quickly and consistently.

---

## Architecture Guidance

Oracle Database@AWS is designed to combine Oracle Exadata's performance with AWS's scalability and flexibility. Instead of running Oracle Database on separate infrastructure, businesses can deploy directly on AWS infrastructure while still using Exadata's optimized features.

In this model, Terraform serves as the orchestration tool for the entire resource creation process. Infrastructure components are described in HCL source code and automatically deployed by Terraform in the correct dependency order, helping ensure consistency across environments.

The solution includes four main components:

* ODB Network: Dedicated network connecting AWS and Oracle Cloud Infrastructure (OCI), providing low-latency private connectivity.
* Oracle Exadata Infrastructure: Exadata hardware infrastructure deployed directly in AWS Availability Zone to provide high-performance data processing capabilities.
* Exadata VM Cluster: Virtual machine cluster running Oracle Grid Infrastructure and Oracle Database.
* ODB Peering Connection: Private network connection between Amazon VPC and ODB Network, allowing applications on AWS to securely access Oracle Database.

> _Figure 1. Overall architecture; colored boxes represent distinct services._

After the above components are successfully created, businesses can deploy Oracle Database with full scalability, high availability, and integration capabilities with AWS services.

---

## Why Use Terraform?

Terraform is one of the most popular Infrastructure as Code tools today. Instead of operating directly on the AWS management console, the entire infrastructure is described in HCL (HashiCorp Configuration Language) code. Terraform reads these configuration files and automatically creates resources in the correct dependency order.

Implementing Terraform provides many benefits:

* Fully automate the infrastructure deployment process.
* Eliminate manual configuration operations on AWS Console.
* Ensure consistent configuration across Development, Testing, and Production environments.
* Easily manage changes through Git.
* Reusable configuration for multiple different projects.
* Support infrastructure scaling and updates without affecting existing resources.

For organizations deploying multiple Oracle Database systems or implementing DevOps, Terraform helps significantly reduce deployment time and increase infrastructure control capabilities.

---

## Prerequisites for Deployment

Before running Terraform, ensure the following preparation steps are completed:

### 1. Register for Oracle Database@AWS

Businesses need to register for Oracle Database@AWS service through AWS Marketplace and complete the Onboarding process with Oracle.

### 2. Link Accounts

AWS Account must be linked with Oracle Cloud Infrastructure (OCI Tenancy) so Terraform has permission to manage resources on both platforms.

Terraform Provider Configuration

Terraform needs to configure two Providers simultaneously:

* AWS Provider
* OCI Provider

These two Providers allow Terraform to communicate with AWS and Oracle Cloud APIs.

### 3. Set Up IAM Permissions

The account used by Terraform needs full permissions to create, update, and delete resources on both AWS and Oracle Cloud.

After completing the above conditions, administrators can start deploying Oracle Database@AWS infrastructure using Terraform.

---

## Terraform Deployment Process

Terraform will create Oracle Database@AWS components in the correct dependency order. Each component is defined as a Resource in Terraform.

### Step 1. Initialize ODB Network

The first step is to create Oracle Database Network, which establishes a private network connection between AWS and Oracle Cloud Infrastructure.

Example Terraform configuration:

```hcl
resource "aws_odb_network" "example" {
  display_name         = "odb-my-net"
  availability_zone_id = "use1-az6"
  client_subnet_cidr   = "10.2.0.0/24"
  backup_subnet_cidr   = "10.2.1.0/24"
  s3_access            = "DISABLED"
  zero_etgl_access     = "DISABLED"
  tags = {
    "env" = "dev"
  }
}
```

#### In the above configuration:

* display_name defines the ODB Network name.
* availability_zone_id specifies the Availability Zone for deployment.
* client_subnet_cidr and backup_subnet_cidr define two network ranges for application traffic and backup.
* s3_access allows Oracle Database to access Amazon S3.
* zero_etl_access enables Zero-ETL integration capability.

After completing this step, all Oracle Database resources will be deployed on the newly created ODB Network.

### Step 2. Deploy Oracle Exadata Infrastructure

Next, Terraform initializes Exadata hardware infrastructure.

```hcl
resource "aws_odb_cloud_exadata_infrastructure" "example" {
  display_name         = "my-exa-infra"
  availability_zone    = "use1-az6"
  shape                = "exadata.oci.x11m"
  database_server_type = "X11M"
  storage_server_type  = "X11M-HC"
  maintenance_window {
    custom_action_timeout_in_mins = 16
    days_of_week = [{ name = "MONDAY" }, { name = "TUESDAY" }]
    hours_of_day = [11, 16]
    is_custom_action_timeout_enabled = true
    lead_time_in_weeks = 3
    months = [{ name = "FEBRUARY" }, { name = "MAY" }, { name = "AUGUST" }, { name = "NOVEMBER" }]
    patching_mode = "ROLLING"
    preference = "CUSTOM_PREFERENCE"
    weeks_of_month = [2, 4]
  }
  tags = {
    "env" = "dev"
  }
}
```

Oracle Exadata Infrastructure provides dedicated hardware platform to run Oracle Database with high performance.

At this step, administrators can choose configurations suitable for their needs such as:

* Compute Node
* Storage Server
* Storage capacity
* Availability Zone

Terraform will automatically link Exadata Infrastructure with the ODB Network created in the previous step.

### Step 3. Initialize Exadata VM Cluster

After Exadata Infrastructure is ready, Terraform continues to deploy VM Cluster.

```hcl
resource "aws_odb_cloud_vm_cluster" "example" {
  display_name                    = "my-vm-cluster"
  cloud_exadata_infrastructure_id = "<exadata-infra-id>"
  odb_network_id                  = "<odb-network-id>"
  cpu_core_count                  = 6
  gi_version                      = "23.0.0.0"
  hostname_prefix                 = "apollo12"
  ssh_public_keys                 = ["your-ssh-public-key"]
  license_model                   = "LICENSE_INCLUDED"
  data_storage_size_in_tbs        = 20.0
  db_servers                      = ["db-server-1", "db-server-2"]
  db_node_storage_size_in_gbs     = 120.0
  memory_size_in_gbs              = 60
  tags = {
    "env" = "dev"
  }
}
```

VM Cluster is the environment that directly runs Oracle Database.

Here, administrators can configure:

* CPU Core count.
* Memory.
* Oracle Grid Infrastructure.
* Oracle Home.
* Oracle Database version.

With Terraform, all these parameters are stored as source code, making it easy to scale or reuse for different environments.

### Step 4. Set Up ODB Peering Connection

After Oracle Database Infrastructure is created, the final step is to establish network connection between Amazon VPC and ODB Network.

```hcl
resource "aws_odb_network_peering_connection" "example" {
  display_name   = "example-peering"
  odb_network_id = "<odb-network-id>"
  peer_network_id = "<vpc-id>"
  tags = {
    "env" = "dev"
  }
}
```

Peering Connection allows applications deployed on Amazon EC2, Amazon ECS, or Amazon EKS to access Oracle Database through a private network connection, reducing latency and enhancing security.

After Terraform completes this step, the entire Oracle Database@AWS infrastructure is ready to deploy and operate the database.

---

## Post-Deployment Architecture

After Terraform completes the provisioning process, the entire Oracle Database@AWS infrastructure will be created in the correct dependency order. Terraform automatically manages resource relationships, freeing administrators from manual operations on AWS Console.

The post-deployment architecture includes the following components:

| Component                     | Role                                                                           |
| ----------------------------- | ------------------------------------------------------------------------------ |
| ODB Network                   | Establish private network connecting AWS with Oracle Cloud Infrastructure (OCI). |
| Oracle Exadata Infrastructure  | Provides Exadata hardware infrastructure serving Oracle Database.                |
| Oracle Exadata VM Cluster     | Environment running Oracle Grid Infrastructure and Oracle Database.             |
| ODB Peering Connection        | Connects Amazon VPC with ODB Network for application Database access.          |
| AWS Provider                  | Manages and deploys resources on AWS.                                          |
| OCI Provider                  | Manages Oracle Cloud Infrastructure resources.                                  |

All resources are managed by Terraform in **Terraform State**, making it easy to track infrastructure status, update, or expand the system in the future.

---

## Deploying the Project with Terraform

AWS has provided a sample project on GitHub to help users quickly deploy Oracle Database@AWS using Terraform.

First, download the source code:

```bash
git clone https://github.com/aws-samples/sample-odb-launch-using-terraform.git

cd sample-odb-launch-using-terraform
```

After downloading the source code, initialize Terraform:

```bash
terraform init
```

The above command will download necessary Providers such as AWS Provider and OCI Provider.

Next, check the deployment plan:

```bash
terraform plan
```

Terraform will analyze all source code and display the list of resources to be created, updated, or deleted.

If all configurations are correct, proceed with deployment:

```bash
terraform apply
```

Terraform will sequentially execute:

1. Create ODB Network.
2. Initialize Oracle Exadata Infrastructure.
3. Create Oracle Exadata VM Cluster.
4. Set up ODB Peering Connection.
5. Update Terraform State.

After completion, the Oracle Database@AWS environment is ready to deploy Database and connect with applications on AWS.

---

## Best Practices When Using Terraform

For Oracle Database systems in enterprise environments, AWS recommends applying several best practices to increase stability and manageability.

### 1. Always Run `terraform plan` Before `terraform apply`

Checking the deployment plan helps detect unexpected changes early before impacting the Production environment.

### 2. Manage Terraform State Remotely

Do not store `terraform.tfstate` file on personal computers.

Instead, use:

* Amazon S3 to store State.
* Amazon DynamoDB for State Locking.

This allows multiple team members to work simultaneously without conflicts.

### 3. Manage Source Code with Git

All Terraform code should be stored on GitHub or GitLab for:

* Tracking change history.
* Performing Code Review.
* Restoring configuration when needed.
* Integrating CI/CD.

### 4. Separate Environments

Use variables or Terraform Workspace to separate environments:

* Development
* Testing
* Staging
* Production

This helps limit impacts between environments and simplifies the deployment process.

### 5. Avoid Direct Changes on AWS Console

After implementing Infrastructure as Code, all changes should be made through Terraform instead of directly editing on AWS Console. This helps avoid **Configuration Drift**, ensuring actual infrastructure always matches the source code.

---

## Target Audience

Oracle Database@AWS combined with Terraform is suitable for various technical teams.

* **Database Administrator (DBA):** Automate Oracle Database deployment and administration.
* **Cloud Engineer:** Standardize Oracle infrastructure on AWS using Infrastructure as Code model.
* **DevOps Engineer:** Integrate database deployment into CI/CD pipeline.
* **Enterprise Architect:** Design scalable and maintainable Oracle Database infrastructure.
* **Enterprise Business:** Organizations migrating Oracle Database systems from On-premises to AWS while still requiring Oracle Exadata's high performance.

---

## Conclusion

Oracle Database@AWS provides a new approach to deploying Oracle Database on cloud platforms by combining Oracle Exadata's performance with the AWS service ecosystem. However, this comes with configuring multiple infrastructure components and requiring consistency during deployment.

Terraform helps solve this problem through **Infrastructure as Code** model, allowing the entire infrastructure to be defined in source code instead of manual operations on the management interface. Through automation, version management, and configuration reuse capabilities, Terraform not only shortens deployment time but also minimizes configuration error risks and improves system operational efficiency.

For businesses building or modernizing Oracle Database infrastructure on AWS, combining Oracle Database@AWS with Terraform is an appropriate solution to standardize deployment processes, increase scalability, and simplify long-term administration.

Source: AWS Database Blog - Provision Oracle Database@AWS resources using Terraform.
