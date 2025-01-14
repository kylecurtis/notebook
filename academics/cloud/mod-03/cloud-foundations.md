# AWS Global Infrastructure

## **Section 1: AWS Global Infrastructure**

#### **AWS Global Infrastructure**

The diagram provides a look at the 22 current AWS Regions, as well as a few Regions that will become available soon, including Milan, Cape Town, and Indonesia (as of October 2019).

#### **AWS Regions**

An AWS Region is a physical geographical location with one or more Availability Zones. Availability Zones in turn consist of one or more data centers.

To achieve fault tolerance and stability, AWS Regions are isolated from one another. Resources in one Region are not automatically replicated to other Regions, therefore, when you store data in a specific Region, it is not replicated outside that Region.

It is your responsibility to replicate data across Regions, if your business or project needs require it.

AWS Regions introduced before March 20, 2019 are enabled by default. Any Regions that were introduced after March 20, 2019-such as Asia Pacific (Hong Kong) and Middle East (Bahrain)-are disabled by default. You must enable these Regions before you can use them. You can use the AWS Management Console to enable or disable a Region.

Additionally, some Regions have restricted access. For example, an Amazon AWS (China) account provides access to the Beijing and Ningxia (Ning-Sha) Regions only. Visit the AWS website and search for ‘China Region’ for more details.

Whereas the isolated AWS GovCloud (US) Region is designed to allow US government agencies and customers to move sensitive workloads into the cloud by addressing their specific regulatory and compliance requirements.

#### **Selecting a Region**

There are a few factors that you should consider when selecting the optimal Region, or Regions where you will tore data and use AWS services.

It is imperative to consider data governance and legal requirements when selecting an AWS Region. Local laws might require that certain information be kept within geographical boundaries. Such laws might restrict the Regions where you can offer content or services. For example, consider the European Union (EU) Data Protection Directive.

All else being equal, it is generally desirable to run your applications and store your data in a Region that is as close as possible to the user and systems that will access them. This will help to reduce latency for users and systems accessing your AWS resources. To test latency between your location and all AWS Regions you can use a website like CloudPing.

As an additional consideration, it is important to note that not all AWS services are available in all Regions.

Finally, there is some variation in the cost of running services, which can depend on which Region you choose. For example, as of this recording, running an On-Demand t3.medium size Amazon Elastic Compute Cloud (Amazon EC2) Linux instance in the US East (Ohio) Region costs $0.0416 per hour, but running the same instance in the Asia Pacific (Tokyo) Region costs $0.0544 per hour.

#### **Availability Zones**

Each AWS Region has multiple, isolated locations that are known as Availability Zones.

Each Availability Zone provides the ability to operate applications and databases that are more highly available, fault-tolerant, and scalable than would be possible with a single data center.

Every Availability Zone can include multiple data centers (typically three), and at full-scale, they can include hundreds of thousands of servers. They are fully isolated partitions of the AWS Global Infrastructure. Availability Zones have their own power infrastructure, and they are physically separated from other Availability Zones by several kilometers -though all Availability Zones are within 100 km of each other.

All Availability Zones are interconnected with high-bandwidth, low-latency networking over fully redundant, dedicated fiber which provides high-throughput between Availability Zones. This network allows for synchronous replication between Availability Zones.

Availability Zones help build highly available applications. When an application is partitioned across Availability Zones, applications are better isolated and protected from issues such as lightning, tornadoes, earthquakes, and more.

You are responsible for selecting the Availability Zones where your systems will reside. Systems can span multiple Availability Zones and AWS recommends replicating across Availability Zones for resiliency. You should design your systems to survive the temporary or prolonged failure of a single Availability Zone if a disaster occurs.

#### **AWS data centers**

The foundation for the AWS infrastructure is the data centers. Customers do not specify a data center for the deployment of resources. Instead, an Availability Zone is the most granular level of specification that a customer can make. However, a data center is the location where the actual data resides. Amazon operates state-of-the-art, highly available data centers. Although rare, failures can occur that affect the availability of instances in the same location. If you host all your instances in a single location that is affected by such a failure, none of your instances will be available.

AWS Data centers are securely designed with several factors in mind:

Each location is carefully evaluated to mitigate environmental risk.

Next, Data centers have a redundant design that anticipates and tolerates failure while maintaining service levels.

To ensure availability, critical system components are backed up across multiple Availability Zones.

To ensure capacity, AWS continuously monitors service usage to deploy infrastructure to support availability commitments and requirements.

Additionally, Data center locations are not disclosed and all access to them is restricted.

And in the event of a failure, automated processes move data traffic away from the affected area.

AWS uses custom network equipment sourced from multiple original device manufacturers (ODMs). ODMs design and manufacture products based on specifications from a second company. The second company then rebrands the products for sale.

#### **Points of Presence**

Amazon CloudFront is a content delivery network (CDN) used to distribute content to end users in order to reduce latency. Amazon Route 53 is a Domain Name System (DNS) service. Requests going to either one of these services will be routed to the nearest edge location automatically in order to lower latency.

AWS Points of Presence are located in most of the major cities across 30 countries around the world. To deliver an improved near real-time user experience Points of Presence continuously measure internet connectivity performance, and computing to find the best possible way to route the traffic requests. They are used by many AWS services, including Amazon CloudFront, Amazon Route 53, AWS Shield, and AWS Web Application Firewall (AWS WAF) services.

Regional edge caches are used by default with Amazon CloudFront. Regional edge caches are used when you have content that is not accessed frequently enough to remain in an edge location. Regional edge caches absorb this content and provide an alternative to fetching content directly from the origin server.

#### **AWS infrastructure features**

Now that you have a good understanding of the major components that describe the AWS Global Infrastructure, let's consider the benefits provided by this infrastructure.

The AWS Global Infrastructure has several valuable features:

First, it is elastic and scalable. This means resources can dynamically adjust to increases or decreases in capacity requirements. It can also rapidly adjust to accommodate growth.

Second, this infrastructure is fault tolerant, which means it has built-in component redundancy which enables it to continue operations despite a failed component.

Finally, it requires minimal to no human intervention, while providing high availability with minimal down time.

Thanks for watching, we’ll see you in the next video.

<br>

---

<br>

## **Section 2: AWS services and service categories**

AWS offers a broad set of global cloud-based products that can be used as building blocks for common cloud architectures. Here is a look at how these cloud based products are organized.

#### **AWS foundational services**

The AWS Global Infrastructure can be broken down into three elements: Regions, Availability Zones, and Points of Presence, which include edge locations. This infrastructure provides the platform for a broad set of services, such as networking, storage, compute services, and databases-and these services are delivered as an on-demand utility that is available in seconds, with pay-as-you-go pricing.

#### **AWS categories of services**

AWS offers a broad set of cloud-based services. There are 23 different product or service categories, and each category consists of one or more services. This course will not attempt to introduce you to each service. Rather, the focus of this course is on the services that are most widely used and offer the best introduction to the AWS Cloud. This course also focuses on services that are more likely to be covered in the AWS Certified Cloud Practitioner exam.

Take a moment and review the highlighted services categories discussed in this course.

Let’s take a look at the most widely used services.

#### **Storage service category**

The AWS Storage services category is represented by:

Amazon Simple Storage Service (Amazon S3), which is an object storage service that offers scalability, data availability, security, and performance.

Amazon Elastic Block Store (Amazon EBS) which is a high-performance block storage designed for use with Amazon EC2 for both throughput and transaction intensive workloads.

Next we have Amazon Elastic File System (Amazon EFS). This storage service provides a scalable, fully managed elastic Network File System (NFS) file system for use with AWS Cloud services and on-premises resources.

Finally, we have Amazon Simple Storage Service Glacier which is a secure, durable, and extremely low-cost Amazon S3 cloud storage class for data archiving and long-term backup.

#### **Compute service category**

AWS compute services include:

Amazon Elastic Compute Cloud (Amazon EC2) that provides resizable compute capacity as virtual machines in the cloud.

The Amazon EC2 Auto Scaling service enables you to automatically add, or remove EC2 instances according to conditions that you define.

Next we have Amazon Elastic Container Service (Amazon ECS), a highly scalable, high-performance container orchestration service that supports Docker containers.

The Amazon Elastic Container Registry (Amazon ECR) service is a fully-managed Docker container registry that makes it easy for developers to store, manage, and deploy Docker container images.

AWS Elastic Beanstalk is a service for deploying and scaling web applications and services on familiar servers such as Apache and Microsoft Internet Information Services (IIS).

There is also AWS Lambda which enables you to run code without provisioning or managing servers. You pay only for the compute time that you consume. There is no charge when your code is not running.

Amazon Elastic Kubernetes Service (Amazon EKS) makes it easy to deploy, manage, and scale containerized applications that use Kubernetes on AWS.

Finally we have AWS Fargate , a compute engine for Amazon ECS that allows you to run containers without having to manage servers or clusters.

#### **Database service category**

The AWS database services category includes:

Amazon Relational Database Service (Amazon RDS) an easy to set up, operate, and scalable relational database in the cloud. It provides resizable capacity while automating time-consuming administration tasks, such as hardware provisioning, database setup, patching, and backups.

Next we have Amazon Aurora which is a MySQL and PostgreSQL-compatible relational database. It is up to five times faster than standard MySQL databases and three times faster than standard PostgreSQL databases.

Amazon Redshift enables you to run analytic queries against petabytes of data that is stored locally in Amazon Redshift, and directly against exabytes of data stored in Amazon S3. It delivers fast performance at any scale.

Finally we have Amazon DynamoDB, a fully managed key-value and document No-SQL database that delivers single-digit millisecond performance at any scale, with built-in security, backup and restore, and in-memory caching.

#### **Networking and content delivery service category**

Next we have the AWS networking and content delivery services category. Services in this category include:

Amazon Virtual Private Cloud (Amazon VPC) which enables you to provision logically isolated sections of the AWS Cloud to launch AWS resources in a virtual network that you define.

Additionally we have Elastic Load Balancing that automatically distributes incoming application traffic across multiple targets, such as Amazon EC2 instances, containers, IP addresses, and Lambda functions.

Amazon CloudFront is a fast content delivery network (CDN) service that securely delivers data, videos, applications, and application programming interfaces (APIs) to customers globally, with low latency and high transfer speeds.

The AWS Transit Gateway service enables customers to connect their Amazon Virtual Private Clouds (VPCs) and their on-premises networks to a single, centrally managed gateway.

Next we have Amazon Route 53, a scalable cloud Domain Name System (DNS) web service designed to give you a reliable way to route end users to internet applications. It translates names (like www.example.com) into the numeric IP addresses (like 192.0.2.1) that computers use to connect to each other.

AWS Direct Connect provides a way to establish a dedicated private network connection from your data center or office to AWS, which can reduce network costs and increase bandwidth throughput.

To wrap up the networking service category we have AWS VPN that provides a secure private tunnel from your network or device to the AWS global network.

#### **Security, identity, and compliance service category**

AWS security, identity, and compliance services include

AWS Identity and Access Management (IAM) which enables you to manage access to AWS services and resources securely.

AWS Organizations allows you to restrict what services and actions are allowed in your accounts.

Next we have Amazon Cognito which lets you add user sign-up, sign-in, and access control to your web and mobile apps.

The AWS Artifact service provides on-demand access to AWS security and compliance reports, as well as select online agreements.

Additionally the AWS Key Management Service (AWS KMS) enables you to create and manage encryption keys. You can use AWS KMS to control the use of encryption across a wide range of AWS services and in your applications.

Lastly we have AWS Shield which is a managed Distributed Denial of Service (DDoS) protection service that safeguards applications running on AWS.

#### **AWS cost management service category**

Onto the AWS cost management services which includes:

The AWS Cost and Usage Report which contains the most comprehensive set of AWS cost and usage data available, including additional metadata about AWS services, pricing, and reservations.

Next we have AWS Budgets where you can set custom budgets that alert you when your AWS costs or usage exceed (or are forecasted to exceed) your budgeted amount.

Lastly, the AWS Cost Explorer has an easy-to-use interface that enables you to visualize, understand, and manage your AWS costs and usage over time.

#### **Management and governance service category**

Wrapping up the AWS Service category overview we have AWS management and governance services which include:

The AWS Management Console which provides a web-based user interface for accessing your AWS account.

Next we have AWS Config which provides a service that helps you track resource inventory and changes.

The Amazon CloudWatch service allows you to monitor resources and applications.

AWS Auto Scaling provides features that allow you to scale multiple resources to meet demand.

Next we have the AWS Command Line Interface providing a unified tool to manage AWS services.

AWS Trusted Advisor is an online tool helps you optimize performance and security using AWS Best Practices.

Additionally we have the AWS Well-Architected Tool which provides help in reviewing and improving your workloads.

Lastly, AWS CloudTrail tracks user activity and API usage across AWS Accounts.

Thanks for watching, we’ll see you in the next video.