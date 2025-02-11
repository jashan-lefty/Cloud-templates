In this project, we deploy a highly available WordPress application on AWS using various services like EC2, RDS, ELB, S3, and CloudFormation. We begin by setting up a custom VPC with public and private subnets, including appropriate routing via NAT and IGW. Within this VPC, we configure an RDS instance with MySQL 8.0.35, ensuring it's in a private subnet with no public access and allowing necessary traffic only from the web server.
Next, we set up an Application Load Balancer (ALB) in the public subnets to distribute traffic to backend web servers. The ALB is configured with HTTP listeners and an associated security group to allow internet traffic. Additionally, we create an S3 bucket for storing media files, integrating it with WordPress using the "Offload Media" plugin.
For the EC2 instances hosting WordPress, we launch them in public subnets, configuring them with Amazon Linux 2 AMI, t2.micro instance type, and appropriate security groups. We use user data scripts to install necessary packages and set up WordPress on these instances. A similar EC2 instance is launched in a different public subnet to serve as a template for the Auto Scaling Group (ASG).
Furthermore, we create a Launch Template for the ASG, specifying the AMI, instance type, key pair, and security group. The ASG is configured with scaling policies to maintain a minimum of 1 and a maximum of 3 instances, scaling out when CPU utilization exceeds 70% and scaling in when it falls below 25%. Instances launched by the ASG are deployed into private subnets.
Finally, we orchestrate the infrastructure deployment using CloudFormation, splitting it into two templates: one for networking-related services and another for application infrastructure. Testing involves accessing the WordPress site via the ALB, checking ASG behavior, verifying S3 integration, and ensuring RDS Multi-AZ functionality.
This project showcases a robust and scalable architecture for hosting WordPress applications on AWS, leveraging various AWS services and best practices in infrastructure management.

![image](https://github.com/user-attachments/assets/5e17b006-3d13-45b6-9ad7-fd26294e4cbe)



