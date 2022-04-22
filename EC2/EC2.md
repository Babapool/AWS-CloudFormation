# Setting up EC2 service using Cloud Formation

We will use the `yaml` template to launch our cloud formation.
`yaml` templates are easy to write and we only have to worry about the indentation. 

### Things to know about:
- **Resources** : Resources are services or subservices that are going to be launched by the end user.
- **Parameters** : Parameters are options given to the user that they can choose while launching the rsource, eg: which key will be required to access the EC2 instance or the availability zone where you want to launch the subnet. We can acess this using the 
`!Ref parameterName`.
- **Mappings** : These are used when we need to sow values of the parameters depending on the region where the end user is going to launching the resource. Accessed using `!FindInMap`.
- **Output** : It is used to show the custom output/attributes of the service launched as desired by the user. Accessed by `!GetAtt`.

### What does the code do?
- We first create a `VPC`.
- Then we are going to create a `public` and `personal subnet`.
- To make the public subnet we are going to create a `Internet Gateway`.
- This Internet Gateway is attached to the VPC.
- We are then create a  `Route Table`.
- This Route Table is attached to the internet gateway to allow trafiic through `0.0.0.0/0`, i.e. request coming through/from any IP address are going to be routed.
- The Route Table is then associated with the Public Subnet.
- We create a security group allow HTTP,PING,SSH rules.
- An instances is created in the public subnet.
- An instance is created in the private subnet.
- We show the `Instance ID`, `Public IP`, `Private IP` of the instances launced as the `Output`.

You can find more about the sources from the [AWS Cloud Formation EC2 GitHub Repo](https://github.com/awsdocs/aws-cloudformation-user-guide/blob/main/doc_source/AWS_EC2.md).