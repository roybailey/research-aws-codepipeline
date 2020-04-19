# research-aws-codepipeline

Sample of using AWS CodePipeline

## Create your EC2 instance using CloudFormation

To create your EC2 instance using CloudFormation, first save cloud-formation-template.json to your own S3 bucket, 
then update the command below to reference your bucket as well as the name of a Key pair that you own in the 
region that you are working in. 

```
aws cloudformation create-stack --stack-name CodeDeployDemoStack --template-url https://roybaileybiz-codedeploy.s3.amazonaws.com/cloud-formation-template.json --parameters ParameterKey=InstanceCount,ParameterValue=1 ParameterKey=InstanceType,ParameterValue=t2.micro ParameterKey=KeyPairName,ParameterValue=roybaileybiz-n-virginia ParameterKey=OperatingSystem,ParameterValue=Linux ParameterKey=SSHLocation,ParameterValue=0.0.0.0/0 ParameterKey=TagKey,ParameterValue=Name ParameterKey=TagValue,ParameterValue=CodeDeployDemo --capabilities CAPABILITY_IAM
```

## Verify that the Cloud Formation stack has completed
 
```
aws cloudformation describe-stacks --stack-name CodeDeployDemoStack --query "Stacks[0].StackStatus" --output text
```

## Log in to your instance and check that the CodeDeploy agent has installed
  
```
sudo service codedeploy-agent status
```

