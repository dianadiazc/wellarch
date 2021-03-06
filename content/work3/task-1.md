+++ 
title = "Task 1: Adding subnets to a second AZ" 
chapter = false 
weight = 1 
+++

Remember the starting point architecture:

<img src="../images/starting.png" alt="drawing" width="500"/>

In this task, you will create **two additional subnets in a second Availability Zone** to improve application reliability. We can improve availability for applications by using two Availability Zones for our deployment and by decoupling the applications and dividing the tiers. We will use services that work across multiple Availability Zones, such as Elastic Load Balancing, Auto Scaling and Amazon RDS Multi-AZ. This will ensure tolerance to failures on the resource level and on the Availability Zone level. 

At the end of this task this will be the lab architecture:

<img src="../images/lab2-task1.png" alt="drawing" width="600"/>

{{% notice note %}}
Even though you can create subnets, load balancers, auto scaling groups and other application components using the AWS Console, in this Lab we are going to take advantage of the benefits of automation using commands in the **AWS CLI** using **AWS CloudShell**.
{{% /notice %}}

1. Make sure that your AWS console session is using Oregon region. This lab uses Oregon (us-west-2) as the default region.

<img src="../images/region.png" alt="drawing" width="600"/>

2. Open AWS CloudShell.

<img src="../images/cs1.png" alt="drawing" width="800"/>

3. Close the "Welcome window" and you will see the AWS CLI ready to start executing commands.

<img src="../images/cs2.png" alt="drawing" width="500"/>

4. Install module dependency `envsubst` (Substitutes shell format strings with environment variables in text)

```sh
sudo yum install gettext -y
```


{{% notice warning %}}
If you **close or leave AWS CloudShell**, please ensure to execute **sudo yum install gettext -y** command again, because this installation  is not persistent and you will use it every time that you find **envsubst** in the subsequent commands. 
{{% /notice %}}


5. In the dialog box, uncheck "Ask before pasting multiline code" option and click on **Paste**.

<img src="../images/cs3.png" alt="drawing" width="500"/>

You will see the following output:

<img src="../images/cs4.png" alt="drawing" width="900"/>

6. Add AWS account number

```sh
export awsAccount=`aws sts get-caller-identity --query "Account" --output text` && echo awsAccount=$awsAccount >> ~/.bashrc
```

7. Add VPC id as environment variable

```sh
export VPC=`aws ec2 describe-vpcs --filters Name=tag:Name,Values=wa-lab-vpc --query 'Vpcs[*].VpcId' --output text --region us-west-2` && echo VPC=$VPC >> ~/.bashrc
```

8. Create a public and a private subnet in the second AZ (us-west-2b).

```sh
aws ec2 create-subnet --vpc-id $VPC --cidr-block "10.100.2.0/24" --availability-zone "us-west-2b" --tag-specifications 'ResourceType=subnet, Tags=[{Key=Name,Value=wa-public-subnet-2}]'

aws ec2 create-subnet --vpc-id $VPC --cidr-block "10.100.3.0/24" --availability-zone "us-west-2b" --tag-specifications 'ResourceType=subnet, Tags=[{Key=Name,Value=wa-private-subnet-2}]'
```

9. Add private a route table as environment variable.

```sh
export publicRt=`aws ec2 describe-route-tables --filters Name=tag:Name,Values=wa-public-rt --query 'RouteTables[*].RouteTableId' --output text --region us-west-2` && echo publicRt=$publicRt >> ~/.bashrc

export privateRt=`aws ec2 describe-route-tables --filters Name=tag:Name,Values=wa-private-rt --query 'RouteTables[*].RouteTableId' --output text --region us-west-2` && echo privateRt=$privateRt >> ~/.bashrc
```

10. Add a new private subnet and a public subnet as environment variables.

```sh
export publicSubnetId=`aws ec2 describe-subnets --filters Name=tag:Name,Values=wa-public-subnet-2 --query 'Subnets[*].SubnetId' --output text --region us-west-2` && echo publicSubnetId=$publicSubnetId >> ~/.bashrc

export privateSubnetId=`aws ec2 describe-subnets --filters Name=tag:Name,Values=wa-private-subnet-2 --query 'Subnets[*].SubnetId' --output text --region us-west-2` && echo privateSubnetId=$privateSubnetId >> ~/.bashrc
```

11. Associate private and public route tables.

```sh
aws ec2 associate-route-table --subnet-id $publicSubnetId --route-table-id $publicRt

aws ec2 associate-route-table --subnet-id $privateSubnetId --route-table-id $privateRt
```
