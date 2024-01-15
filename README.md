# Web Tier using AWS EC2 Linux (Single AZ and mulit attach EBS)

Deploying Linux Server EC2 Instances in AWS using Terraform single AZ with multi-attach EBS

![Alt text](/images/diagram.png)


1. vpc module - to create vpc, public subnets, internet gateway, security groups and route tables
2. web module - to create Linux Web EC2 instances with userdata script to display instance metadata using latest Amazon Linux ami in multiple subnets created in vpc module
3. main module - Above modules get called in main config. Also create and multi-attach EBS to EC2 instances

## Side Notes:
Multi Attach EBS is supported by io2 type only and can be attached to only specific instances

https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-volumes-multi.html


Terraform Plan Output:
```
Plan: 15 to add, 0 to change, 0 to destroy.
```

Terraform Apply Output:
```
Apply complete! Resources: 15 added, 0 changed, 0 destroyed.

Outputs:

aws_ebs_volume_id = "vol-0c435b4ee98bf0a88"
ec2_instance_ids = [
  "i-0fc8e0a22098fc4e3",
  "i-00c3d9e854fe98a83",
  "i-05ad62000bb15d168",
  "i-00de4618581eea346",
]
public_subnets = "subnet-036c7553c4937f19a"
security_groups_ec2 = [
  "sg-0339f89ad20bcba28",
]
```
EBS Volumes:

![Alt text](/images/volumes.png)


Running Website:

![Alt text](/images/vm1.png)

![Alt text](/images/vm2.png)

![Alt text](/images/vm3.png)

![Alt text](/images/vm4.png)

Terraform Destroy Output:
```
Plan: 0 to add, 0 to change, 15 to destroy.

Destroy complete! Resources: 15 destroyed.
```