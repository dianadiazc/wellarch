+++ 
title = "Task 4: Creating an Application Load Balancer and a Target Group"
chapter = false 
weight = 4 
+++

End of task architecture

<img src="../images/lab2-task4.png" alt="drawing" width="800"/>

1. Create ALB security group

```sh
aws ec2 create-security-group --description "ALB Security group" --group-name "wa-alb-sg" --vpc-id $VPC
export albSg=`aws ec2 describe-security-groups --filters Name=group-name,Values=wa-alb-sg --query 'SecurityGroups[*].GroupId' --output text --region us-west-2`

aws ec2 authorize-security-group-ingress --group-id $albSg --protocol "tcp" --port "80" --cidr "0.0.0.0/0"
```

2. Create ALB for ASG

```sh
export albSubnet1Id=`aws ec2 describe-subnets --filters Name=tag:Name,Values=wa-public-subnet-1 --query 'Subnets[*].SubnetId' --output text --region us-west-2`

export albSubnet2Id=`aws ec2 describe-subnets --filters Name=tag:Name,Values=wa-public-subnet-2 --query 'Subnets[*].SubnetId' --output text --region us-west-2`

aws elbv2 create-load-balancer --name "waAlb" --subnets $albSubnet1Id $albSubnet2Id --security-groups $albSg --type "application"
```

3. Create Target Group

```sh
aws elbv2 create-target-group --name "waAutoscale-tg" --protocol "HTTP" --port 80 --vpc-id $VPC --target-type "instance"
export waTg=`aws elbv2 describe-target-groups --names waAutoscale-tg --query 'TargetGroups[*].TargetGroupArn' --output text --region us-west-2`
```

4. Create listener for ALB

```sh
export albArn=`aws elbv2 describe-load-balancers --names waAlb --query 'LoadBalancers[*].LoadBalancerArn' --output text --region us-west-2`

## Download template listener.json file
curl -o listener-source.json https://ee-assets-prod-us-east-1.s3.us-east-1.amazonaws.com/modules/6cfbb89d4a74400082ad348b4ec61df1/v1/listener-source.json

envsubst < "listener-source.json" > "listener.json"

aws elbv2 create-listener --load-balancer-arn $albArn --protocol "HTTP" --port 80 --default-actions file://listener.json 
```