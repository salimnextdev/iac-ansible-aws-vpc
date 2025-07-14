# iac-ansible-aws-vpc
spinned up an Ubuntu EC2 Instance, instance_type: t2.micro region: {{region}} (region from variables file optional but you can set your region name in your variables file, I used us-east-1) 

Attached IAM Role to the Instance instead of using AWS access key and secret key as it seemed more security conscious and handong over the RBAC to te AWS account in its entirety.

Created the playbooks which access the variables, and I have specified the list of modules.

It used Python boto3.

In the beginning, I installed the boto library using - sudo apt install python3-boto3 -  to enable AWS API calls via Ansible

I make API connection to a cloud or account by using the IAM roles.

I created the VPC.

In three zones I created, there exists 1 private subnet and 1 public subnet each making 6 subnets. with 

2 different Route Tables for Private Route Table and Public Route Table [ Priv_RT and Pub_RT ]

the PublicRT was created with Internet gateway as RT connection.

I created private subnets with Nat Gateway as RT connection.

And of course, the Bastion host I also created with its key pair and Security Group and

then we launch the instance in the security group.

Ran ansible-playbook for both vpc setup file first and then on completion I ran bastionHost playbook as well.
VPC auto matically created an Elastic IP and attached tot he NAT Gateway. which you would have to release on project completion if you so wish to go through my work here. 
Understand that the Bastion Host was created to access resources in the private subnet which are not directly accessible from the Internet.

#Ensure to delete NAT Gateway and release Elastic IP to prevent surprise AWS billing. you would also have to delete the Bastion Host Instance before deleting the VPC, so Clean Up runs smoothly.
