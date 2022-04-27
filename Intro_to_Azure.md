# Intro to Azure Fundamentals Guide

Link to [short course](https://docs.microsoft.com/en-us/learn/modules/intro-to-azure-fundamentals/)

## Why use cloud computing?

Cloud computing can help enterprises:
 - Lower operating costs: Only pay for the services / resources that they use
 - Run infrastructure more efficiently: Less need to due internal maintenance and instead focus more time on developing the applications to run the computing platform
 - Allow for scaling: Cloud computing offers high flexibility in terms of scaling and downscaling resources as needed.

## What is Azure?

Azure offers IAAS, PAAS, and SAAS. It provides more than 100 services powered by virtualization and virtual machines. Each Azure server runs a special software called **Fabric Controller**, which is responsible for creating VMs on the server and connecting the server to the **Orchestrator**. The Orchestrator is responsible for managing all client requests and forwarding it to corresponding servers. Users interact with the Orchestrator through the Orchestrator Web APIs, which includes the Azure portal.

### Azure Marketplace

Azure Marketplace connect user with Microsoft partners and independent software vendors which offer solutions that are optimized to run on Azure (spanning open-source container platforms, VM images, databases, developer tools, threat detection, etc.)

## Azure Services

![Diagram of Azure services](Pictures/azure_services.png)

Azure services can be divided into ten main categories:
1. Compute: Allowing running virtual machines, **Kubernetes** (cluster management for VMs that run containerized services)
2. Networking: Providing VPN services, load balancing network traffic, DNS, CDN, DDoS protection
3. Storage: Store various ffiles (**Azure File Storage** is most prominent)
4. Mobile: Build and deploy native apps across many different device platforms. 
5. Databases: Support various proprietary and open-source database solutions from SQL to CosmoDB to PostgreSQL.
6. Web: Build, deploy, and scale web applications
7. IoT: Connect, monitor, and launch IoT devices. Analyze data from sensors and use it to take actions
8. Big Data: Support running data analytics on large amounts of data
9. AI: Use ML to build, train, and deploy models on the cloud
10. DevOps: Create, build, and release pipelines that provide continuous integration and delivery for company applications

# Intro to Azure Security

Link to [Microsoft article](https://docs.microsoft.com/en-us/azure/security/fundamentals/overview)s

Azure is a public cloud service platform supporting a broad selection of OS, programming languages, frameworks, tools, database, and services. It can run Linux containers with Docker integration; build apps with JavaScript, Python, .NET, PHP, Java, and Node.js; build back-ends for iOS, Android, and Windows devices.

The built-in security capabilities of Azure can be divided into six areas:

1. Operations
   1. **Microsoft Sentinel** is a SIEM and SOAR solution. It delivers intelligent security analytics and threat intelligence across the enterprise
      1. Aside: What is SIEM and SOAR?
      2. Ref: <https://www.ibm.com/topics/siem>, <https://www.rapid7.com/solutions/security-orchestration-and-automation/>
      3. SIEM, short for **Security Information and Event Management**, is a security solution that helps companies detect potential security threats and vulnerabilities before they can disrupt business operations. In the past SIEMS were mainly treated as a log management system for regulatory compliance and reporting, though nowadays it has become powerful in threat detection through integration with AI and machine learning.
      4. SOAR, short for **Security Orchestration, Automation, and Response**, is a collection of software solutions that allow companies to streamline security operations in three areas:
         1. Threat and vuln management
         2. Incident response
         3. Security operation automation: Automatic handling of SecOps related task (such as scanning for vulnerabilities, analyzing log)
   2. **Azure Monitor**: Visualize, query, alert, and automate handling of data both the Azure subscription **Activity Log** and individual **Resource Logs**.
2. Applications
   1. Web app vulnerability scanning
   2. **Web app firewall (WAF)**: Help protect web applications from common web-based attacks like SQL injection, XSS, and session hijacking. 
   3. App service authentication and authorization
3. Storage
   1. Azure **role-base access control (RBAC)**: Allows restricting access to resources based on roles. Access rights are granted by assigning the appropriate Azure role to groups and application at a certain scope. 
   2. Encryption in transit: Use of transport-level encryption, client-side encryption
   3. Data-at-rest encryption: Include disk encryption
   4. Enabling/controlling browser-based clients using **CORS**
4. Networking 
   1. Network layer controls
   2. **Azure Firewall:** A cloud-native and intelligent network firewall that provides threat protection for cloud workload. It is a fully stateful firewall (meaning it monitors the full of active network connections along with their complete context) as a service with built-in high availability 
   3. **Azure Virtual Network (VNet)**: Allows representation of our own network in the cloud
   4. **Application Gateway**: Provides various load balancing capabilities for the applications
5. Compute
   1. Antimalware and antivirus: Use antimalware software from security vendors
   2. **Azure Key Vault**: Allows for simplifying management and security of critical secrets and keys by storing them in the Azure Key Vault, which stores them in *Hardware Security Modules (HSMs)*. Permission and access to keys are then managed through **Azure Active Directory**
   3. VM backups
   4. VM disk encryption: APplies Bitlocker or DM-crypt (if Linux) to provide volume encryption for OS and data disk. Integrated with Azure Key Vault to manage and control keys
6. Identity
   1.  Support for MFA, password policy enforcement, token-based authentication, Azure RBAC (assigning permissions based on roles)
