## **Learning Outcomes**

Through this assignment, you will:

- Describe how pricing estimates are obtained.
- Use the AWS Pricing Calculator to estimate the price of an AWS architecture.
- Configure automated and repeatable deployments with tools.
- Identify container services that are available for serverless computing

<br>

---

<br>

## Cloud Quest Steps

- Open a new tab and go to https://calculator.aws and click "Create Estimate"
- At the top click "My Estimate" and click "Create Group"
- Group name: Web Servers, click "Create Group"
- Click "Add Service" and Find Service: ec2 and click "Configure"
- Description: Web Server Estimate
- Choose a Region: US East (N. Virginia)
- Under EC2 Specifications:
	- Operating system: Linux
	- Workloads: Daily spike traffic
	- Workload Days: all days
	- Baseline: 2
	- Peak: 4
	- Hours: 8
	- Minutes: 0
	- vCPUs: 2
	- Memory(GiB): 4GiB
	- Network Performance: Any Network Performance
	- Instance Type: t2.medium
	- On-Demand Payment Option
- Click expand Show Calculations and click estimated workload hours
- Scroll down to workload hours per month (REVIEW INFO) and close
- Expand Amazon Elastic Block Store (EBS)
- Storage for each EC2 Instance: General Purpose SSD (gp3)
- General Purpose SSD
- IPOS: 30
- Snapshot frequency: Weekly
- Amount changed per snapshot: 1 GB
- Expand Data transfer
- Inbound Data Transfer: Internet (free)
- Enter Amount: 1
- Data amount: TB per month
- Outbound Data Transfer: Internet
- Enter Amount: 100
- Data amount: GB per month
- Expand show calculations
- Click "Save and add service"
- Click "View Summary"
- Click "Share" at the top
- Agree and continue
- Copy public link
- 