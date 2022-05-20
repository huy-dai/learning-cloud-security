# Wiz

Link to [Wiz Datasheet](https://www.threatscape.com/wp-content/uploads/2021/06/Wiz-Datasheet-April-2021.pdf)

## Key Use Cases

Wiz can help to:
 - Provide an inventory of cloud resources, including PaaS, VMs, containers, etc.
 - Correlate issues across the cloud stack to identify high-risk infiltration vectors
 - Raise warnings and notification high-risk issues to the right team
 - Create a cloud governance practice that manages risks with a given risk budget

Wiz combines functionality of a **Cloud Security Posture Management (CSPM)**, a vulnerability scanner, container security, and SIEM into a single graph. it is able to analyze the full cloud stack across many different platforms (AWS, Azure, GCP, Kubernetes, etc.) It also strives to look at threats in full context of cloud rather than just focusing at single vulnerabilities or misconfigurations in isolation. 

## Threats

Some threat / practices it looks for include:
- Key management
- Identity and access:
  - Wiz map the identity structure of every resource to the role it can take on, taking into account mitigating controls such as **Service Control Policies (SCP)** and permission boundaries
- External exposure: 
  - See what part of the cloud is exposed to public Internet
- Later movement
- Vulnerability and patch management
- Secure configuration

## Key Features

Key features that Wiz offers include:
- Snapshot scanning: Snapshotting each VM system volume and analyze the various layer of the stack with no performance impact
- Scanning for secrets
- Remediation workflow: Automate process of creating tickets in service tracking products for raising alerts
- Inventory and asset management
- Project-based cloud governance