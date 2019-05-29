### Prerequisites

In order to install Soda on an AWS account the following prerequisites 

##### Parameters

* Target client name: used for {client-name}.sodadata.io & the in various infrastructure things.  Lower case and dashes, no spaces.  Eg `coca-cola`
* AWS account id
* AWS account credentials

##### Credentials
We need `aws_access_key_id` & `aws_secret_access_key` in order to install 
Soda on the account.  The credentials should allow for programmatic access.

##### Permissions
The credentials given should have following permissions:
* TODO specify more detailed
* RDS database: create, start, etc
* EMR cluster: create, start, etc
* Fargate cluster: create, start, etc
* CloudWatch: ... 

### Procedure

##### Add AWS credentials
In file `~/.aws/credentials` add a section with the credentials like this
```
[client-name]
aws_access_key_id = ***
aws_secret_access_key = ***
```

##### Add variables in the terraform repo
In the `config` folder in [the terraform repo](https://github.com/shape-ai/terraform),
add a folder `{client-name}`.  

Copy one of the existing client folders.

**TODO** create a template folder that can be used as the neutral basis to prevent errors

Replace the client-name in the `terraform.tfvars` file

##### Add the client to the terraform build variables

In `config/build/terraform.tfvars` add the account id at the bottom.

##### Enable access in build account to run the terraform updates in the target client account 

In the terraform root folder execute the following command to review the changes:
```
make plan component=build env=build
``` 

If ok, then run 
```
make apply component=build env=build`
``` 

##### Make a certificate
Go to AWS ACM & create certificate for {client-name}.sodadata.io and *.{client-name}.sodadata.io

Enter a DNS record for the each of the 2 certificates on Godaddy

##### Datadog
Set the AWS parameter with the datadog API key
```
aws ssm put-parameter --name '/datadog/DD_API_KEY' --type String --value 'secret' --region eu-west-1
```

##### Install VPC network
`make plan component=network env=nnip-dev`
`make apply component=network env=nnip-dev`

##### Create the AWS component stack
`make plan component=shape-server env=nnip-dev`
`make apply component=shape-server env=nnip-dev`

