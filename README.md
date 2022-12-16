## infrastructure

This infrastructure includes Public/Private subnets, VPC, HostedZones, SSL Certificates, SecurityGroups, IAM Roles, RDS, S3 buckets, DynamoDB, Cloudwatch, SNS, Lambda FUnction, Load Balancers, AutoScaling Groups, Customer Managed Encryption Keys and Respective Policies.

Follow below commands to create infrastructure stack in your aws account via CLI. Make sure to add Parameter Values wherever necessary. If you have a default profile setup, you don't need to add ***--profile demo*** to below commands. Stack name can be changed to anything, I've kept it as **test** for the sake of demo.

### Cloning the repo
```
git clone git@github.com:swaroop-giri-002928636/infrastructure.git
cd infrastructure
```

### Import SSL Certificate
```
  aws acm import-certificate --certificate fileb://certificate.crt \
      --certificate-chain fileb://ca_bundle.crt \
      --private-key fileb://private.key --profile demo
```

### Create Stack
```
aws cloudformation create-stack --stack-name test --template-body file://csye6225-infra.yml --profile demo --parameter ParameterKey=AppAMIImage,ParameterValue="" ParameterKey=CertificateARN,ParameterValue="" ParameterKey=HostedZoneIDs,ParameterValue="" --capabilities CAPABILITY_NAMED_IAM
```
### Check Stacks
```
aws cloudformation describe-stacks --profile demo
```
### Delete contents of bucket before deleting stack
```
aws s3 rm s3://bucket-name --recursive --profile demo
```
### Delete Stack
```
aws cloudformation delete-stack --stack-name test --profile demo
```
