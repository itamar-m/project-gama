# project-gama
## AWS CloudFormation Templates for OnDemand Deployments

This project will demonstrate the use of the AWS CloudFormation service to efficiently deploy infrastructure into AWS. In order to do that couple AWS CloudFormation Templates are requires to deploy AWS Network and Compute components.

- The file <i>vpc-subnets.yml</i> contains the VPC and Subnets, along with use of the Intrinsic Function <i>!Cidr</i> to generate the CIDR blocks for each subnet.


### References:
  - [AWS CloudFormation user guide] (https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/Welcome.html)
