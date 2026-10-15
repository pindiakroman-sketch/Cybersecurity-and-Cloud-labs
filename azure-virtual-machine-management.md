# Azure Virtual Machine Management

## Lab Overview

- **Platform:** Microsoft Azure Portal
- **Category:** Cloud Infrastructure / Azure Administration
- **Difficulty:** Beginner
- **Tools:** Microsoft Azure Portal, Azure Virtual Machines
- **Focus:** Virtual machine lifecycle management, VM provisioning, compute sizing

## 1. Executive Summary

This lab focused on fundamental virtual machine management tasks in Microsoft Azure. I started an existing virtual machine that was in a stopped state and provisioned a new virtual machine intended for the marketing department, configuring its compute resources as part of the deployment process.

## 2. Technical Investigation

### Step 1: Reviewing Existing Virtual Machines

I accessed the **Virtual Machines** service in the Azure Portal and reviewed the available virtual machines in the environment.

During the review, I identified an existing virtual machine that was stopped.

In Azure, the distinction between a stopped VM and a deallocated VM is important:

- **Stopped:** The virtual machine is not running, but compute resources may still be allocated and billed.
- **Stopped (deallocated):** The virtual machine's compute resources have been released, generally stopping compute charges while other billable resources may continue to incur costs.

### Step 2: Starting the Existing Virtual Machine

I selected the stopped virtual machine and initiated the start operation through the Azure Portal.

Starting an existing VM restores its compute operation, provided the deployment and underlying resources are healthy.

A complete operational check should verify the VM's power state and, where applicable, confirm that the operating system and required services are accessible.

### Step 3: Provisioning a New Virtual Machine

I created a new virtual machine intended for the marketing department.

During provisioning, I configured compute-related settings. Azure VM deployments typically involve the following configuration areas:

| Configuration | Purpose |
|---|---|
| Virtual machine name | Identifies the resource |
| Region | Defines the Azure deployment location |
| Operating system image | Specifies the operating system |
| VM size | Determines available CPU and memory resources |
| Networking | Defines virtual network connectivity and network access |
| Authentication | Controls administrative access to the operating system |

The exact VM size, CPU and memory allocation, operating system, region, and network settings were not retained in my notes.

### Step 4: Deployment Verification

After provisioning, the recommended validation process is to confirm that the deployment completed successfully and that the new VM reached the expected operational state.

In a production environment, additional checks should include network connectivity, access permissions, monitoring, and compliance with organizational configuration standards.

## 3. Findings

- Identified an existing stopped virtual machine.
- Initiated the start operation for the existing VM.
- Provisioned a new virtual machine intended for the marketing department.
- Configured compute resources during the provisioning process.
- Exact resource names, VM sizes, CPU and memory specifications, operating system details, and deployment results were not retained in the available notes.
- The environment was described as production-like; the precise environment type and deployment validation results were not recorded.

## 4. Security Recommendations

1. **Apply Least-Privilege Access:** Use Azure Role-Based Access Control (RBAC) to ensure that administrators and users receive only the permissions required for their responsibilities.
2. **Secure Network Connectivity:** Restrict inbound access using Network Security Groups (NSGs). Avoid exposing administrative ports such as SSH or RDP directly to the public internet unless there is a justified and appropriately secured requirement.
3. **Monitor and Control Costs:** Use Azure Monitor to track VM availability and relevant performance metrics. Review VM sizing and deallocate resources when they are no longer required, in accordance with operational policies.

## 5. Key Takeaways

This exercise provided practical experience with Azure virtual machine lifecycle management, including starting an existing VM and provisioning a new VM for a business department. It also reinforced the importance of selecting appropriate compute resources, verifying deployments, applying access controls, and monitoring cloud infrastructure.

---

**Portfolio Note:** This write-up is based on my available lab notes. Exact VM configuration values and deployment verification evidence were not retained.
