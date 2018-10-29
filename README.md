# project-gama
## AWS CloudFormation Templates for OnDemand Deployments

This project will demonstrate the use of the AWS CloudFormation service to efficiently deploy infrastructure into AWS. In order to do that couple AWS CloudFormation Templates are requires to deploy AWS Network and Compute components.

- The file <i>vpc-subnets.yml</i> creates the VPC and Subnets, along with use of the Intrinsic Function <i>!Cidr</i> to generate the CIDR blocks for each subnet.
- The file <i>internet-layer.yml</i> creates the Internet Gateway, and sets it to the VPC. Then creates a public route table, and associates it to the 2 public subnets. Finally, creates a public route to the internet. Some information at this state is imported from the previous AWS CloudFormation Template above.

### Commands
- Deploy the VPC and Subnets
  - <i>aws cloudformation deploy --stack-name kbulix-network --template-file ./vpc-subnets.yml --parameter-overrides VpcSubnetCidrs="10.0.0.0/16"</i>
- Deploy the Internet Gateway and Public Route Tables.
  - <i>aws cloudformation  deploy  --stack-name kbulix-internet-layer --template-file ./internet-layer.yml --parameter-overrides NetworkStack=kbulix-network</i>

### References:
  - [AWS CloudFormation user guide] (https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/Welcome.html)
