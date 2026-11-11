# AWS Cloud Labs

AWS hands-on labs documented as real troubleshooting cases: symptom, diagnosis, root cause and fix.
EC2, networking, security groups and AWS CLI.

Each lab folder has its own README with the architecture, the issues I hit and how I solved them.

| # | Lab | AWS services | What was built / fixed |
|---|-----|--------------|------------------------|
| 01 | [Introduction to Amazon EC2](01-introduction-to-amazon-ec2/) | EC2, EBS, VPC, Security Groups | Apache web server from user data; unreachable until the security group allowed HTTP |
| 02 | [Build your VPC and Launch a Web Server](02-build-your-vpc-and-launch-a-web-server/) | VPC, Subnets, Internet Gateway, NAT Gateway, Route Tables, EC2 | Custom multi-AZ VPC with a PHP web server; caught subnets that were silently all in one AZ |
