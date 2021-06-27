  # VPC Cloud Formation
CloudFormation Templates to create VPC with two public and two private subnets and creating EC2 instances installed apache WebServer inside all subnets.


![Alt text](./vpc.png?raw=true "Title")

## VPC Template
* CloudFormation Trmplate **0-vpc_cfn.yml**.
* You have to run this template first to impelemt vpc and all it's components.
* 
### Parameters
   Name | Description | Type | Default | 
   |------|-------------|:----:|:-----:|
   | VpcCIDR | CIDR notation for this VPC | String | 10.40.0.0/16 |
   | PublicSubnet1CIDR | CIDR notation for the public subnet in the first Availability Zone | String | 10.40.1.0/24 |
   | PublicSubnet2CIDR | CIDR notation for the public subnet in the second Availability Zone | String | 10.40.2.0/24 |
   | PrivateSubnet1CIDR | CIDR notation for the private subnet in the first Availability Zone | String |10.40.10.0/24 |
   | PrivateSubnet2CIDR | CIDR notation for the private subnet in the second Availability Zone | String | 10.40.20.0/24 |

### OUTPUTS
| Name | Description |
|------|-------------|
| VPC | A reference to the created VPC |
| PublicSubnets | A list of the public subnets |
| PrivateSubnets | A list of the private subnets |
| PublicSubnet1 |  A reference to the public subnet in the 1st Availability Zone |
| PublicSubnet2 |  A reference to the public subnet in the 2nd Availability Zone |
| PrivateSubnet1 | A reference to the private subnet in the 1st Availability Zone |
| PrivateSubnet2 | A reference to the private subnet in the 2nd Availability Zone |
| VpcCiderBlock |A reference to VpcCIDR |


## WebServers Template
* CloudFormation Template **1-servers_cfn.yml**
  
### Prequests 
* HTML page uploaded in S3 bucket.
* Upload **1.0-apache-ec2.yml** to S3 bucket, it is used as a nested template to create the ec2 instances with main WebServer configuration.
* SSH key generated from AWS console.

### INPUTS

 Name | Description | Type | Default | 
|------|-------------|:----:|:-----:|
| BastionInstanceType | WebServer instance type. | string | t2.micro |
| BastionImageId | Latest Amazon Linux AMI SSM . | string | Latest Amazon Linux AMI |
| SSHLocation | The IP address range that can be used to SSH Bastion instance |
| KeyName | Name of EC2 KeyPair to enable SSH access to the instances | string | n/a |
| S3BucketName | Name of S3 bucket to download HTML file from | string | n/a |
| IndexPrefix | Prefix of HTML file uploaded to S3 | string | n/a |
| InstanceType | WebServer instance type. | string | t2.micro |
| WebImageId | Latest Amazon Linux AMI SSM . | string | Latest Amazon Linux AMI |

### OUTPUTS
| Name | Description |
|------|-------------|
| BastionPublicIP | Public IP address of the web server |

