## **Learning Outcomes**

Through this assignment, you will:

- Summarize AWS Infrastructure benefits.
- Describe AWS Regions and Availability Zones.
- Deploy Amazon EC2 instances into multiple Availability Zones.
- Configure automated and repeatable deployments with tools

<br>

---

<br>

## Game Steps (Cloud First Steps)

- Download lab files
- Set region to N Virginia (us-east-1)
- Search and go to EC2
- In EC2 Dashboard click "Launch Instance"
- Set the name to "webserver01"
- Under Application and OS Images, select Amazon Linux
- Click AMI dropdown and choose Amazon Linux 2 AMI (HVM)
- Be sure to choose Amazon Linux 2, not Amazon Linux 2023 AMI
- For instance type, choose t2.micro
- For Key pair name, choose proceed without a key pair
- Under Network settings, click "Edit"
- For VPC, choose LabVpc
- For subnet, choose the subnet in the us-east-1a zone (KEEP NOTE OF AZ FOR DIY)
- For security group: Security-Group-Lab
- For Description: HTTP Security Group
- For Type: HTTP
- Configure storage > Root volume: gp2 (confirm if needed)
- Click Advanced details
- On the console, scroll down to "User data - optional"
- Click choose file and select the user-data file
- Launch instance 
- Click View all instances
- Click the checkbox for webserver01
- Verify "Running", then under Public IPv4 DNS, click the copy button (NOT "open address")
- In new tab, paste 

<br>

---

<br>

## Game Steps (Cloud Computing Solutions - Scaling)

- Set region to N. Virginia (us-east-1)
- Search for and open EC2
- Click Instances and check the AWS Computing Solutions box
- Click details tab
- Click Instance Types (Left)
- In the filter box, search: t3.large, c5.large, r5.large and select the 3 boxes
- Click Instances (Left)
- Click the box for AWS Computing Solutions
- Under details, select (copy) the public IPv4 address and paste in a new tab (http not https)
- Click "Connect" at the top
- Click "Session Manager" and "Connect" button

```sh
sudo -i
cd ../home/ec2-user/sample_app
ls
tail -lf aws_compute_solutions.log
```

- Ctrl + C to quit then close terminal to return to Instances page
- Click Actions dropdown menu -> Instance settings -> Edit user data
- Review commands (bash script), then click Cancel
- Click Instances (left), click Instance state dropdown -> Stop instance
- In the pop-up choose "Stop"
- In Details tab, review IPv4 and DNS -> Should be empty
- Click Instance state dropdown -> Start instance
- IPv4 and DNS should be populated
- General steps: Take offline -> Change instance type