# Capital One Hack - 2019

Link to [article](https://krebsonsecurity.com/2019/08/what-we-can-learn-from-the-capital-one-hack/)

## Context

Capital One  has a misconfigured **open-source Web Application Firewall (WAF)** that it used as part of its cloud service in an **EC2 instance** on Amazon Web Services (AWS). Originally the WAF was deployed in tangent with Apache Web Server to mitigate common attacks towards Web Application. 

As a result, personal and financial data from more than 100 million customers were exposed.

## The misconfiguration

The misconfiguration allowed an intruder to trick the firewall into replaying requests to a backend resource on the AWS platform called the **metadata service**. The metadata service is normally responsible for handing out temporary information to a cloud server, including issuing current credentials that allow the server to access any resource in the cloud to which it has access.

Normally, in AWS what the credentials can be used for depends on the permissions assigned to the requesting service. In Capital One's case, the misconfigured WAF assigned too many permissions (e.g. listing all files in any buckets + read contents of each of those files). This vulnerability is called a **Server Side Request Forgery (SSRF)**, in which a server is tricked into running commands that it should never have been permitted to run, including those that allow it to talk to the metadata service.

It should be noted that SSRF attacks are not among the dozen or so attack methods which the WAF has detection rules for. This is a problem, because SSRF has been growing as a serious threat for organizations that use **public clouds**. AWS, for example, could provide better protection by including extra identifying information in requests sent to the metadata service (like Google does), but it choses not to for backwards compatibility.

## Challenges

One major challenges for companies moving their operations from physical data centers to the cloud is that very often the employees responsible for the transition are application and software developers who may not be very knowledgeable in security. Implementing cloud security often requires specialized knowledge, from understanding how EC2 works to understanding Amazon's **Identity and Access Management (IAM)** system, along with best practices to authenticate with AWS services.