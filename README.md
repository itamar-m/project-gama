# project-gama
## AWS CloudFormation for Disaster Recovery scenario

A Disaster Recovery situation is very common as it is well known that hardware and software can break, so to reduce time during a recovery event, AWS CloudFormation can help on that.

This project will demonstrate the use of the AWS CloudFormation service to efficiently deploy infrastructure into AWS.

In order to do that, a couple of AWS CloudFormation Templates are requires to deploy the Network & Computing components, plus assumes that there is an Amazon Machine Images (AMI) replicated to a desired AWS Region already(as part of the Disaster Recovery plan). This AMI contains a simple node.js application (working on port 8080) for demonstration purposes.

- The file <i>01-vpc-subnets.yml</i> creates the VPC and Subnets, along with use of the Intrinsic Function <i>!Cidr</i> to generate the CIDR blocks for each subnet.
- The file <i>02-public-layer.yml</i> creates the Internet Gateway, and sets it to the VPC. Then creates a public route table, and associates it to the 2 public subnets. Finally, creates a public route to the internet. Some information at this state is imported from the previous AWS CloudFormation Template above.
- The file <i>03-nat-gw.yml</i> has the code to create a NAT Gateway for the 2 private subnets access the internet for updates/patching. The NAT Gateway requires and Elastic IP address.
- The file <i>04-ecs-sg.yml</i> has the code to create the required Security Group to protect the EC2 instance, the EC2 instance itself based on the AMI and assigns an Elastic IP address for internet access.

### Commands
- Deploy the VPC and Subnets.
  - <i>aws cloudformation deploy --stack-name [STACK_NAME] --template-file ./01-vpc-subnets.yml --parameter-overrides VpcSubnetCidrs=[CIDR_BLOCK_RANGE]</i>
- Deploy the Internet Gateway and Public Route Tables.
  - <i>aws cloudformation  deploy  --stack-name [STACK_NAME] --template-file ./02-public-layer.yml --parameter-overrides NetworkStack=[NETWORK_STACK]</i>
- Deploy the NAT Gateway for the private subnets access internet.
  - <i>aws cloudformation  deploy  --stack-name [STACK_NAME] --template-file ./03-nat-gw.yml --parameter-overrides NetworkStack=[NETWORK_STACK]</i>
- Deploy the Security Group and EC2 Instance with AIM ID previously created.
  - <i>aws cloudformation deploy --stack-name [STACK_NAME] --template-file ./04-ec2-sg.yml --parameter-overrides NetworkStack=[NETWORK_STACK] ImageAIM=[AMI_ID] EC2KeyPair=[EC2_KEY_PAIR]</i>

### References
  - [AWS CloudFormation user guide] (https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/Welcome.html)
