# iac
Infrastructure as Code (IAC) for different providers

## Installation

```bash
# Install awsebcli (required for Elastic Beanstalk deployment)
$ brew install awsebcli

# Install awscli
$ pip install awscli --upgrade --user
```

## Creating a new Elasticbeanstalk Environment

```bash
$ aws elasticbeanstalk create-environment --cli-input-json file://deployments/production.json
```

The content of the file in `deployments/production.json`:

```json
{
    "ApplicationName": "application-name",
    "EnvironmentName": "environment-name",
    "Description": "Production environment for api gateway",
    "CNAMEPrefix": "domain-cname",
    "Tags": [
        {
            "Key": "Application",
            "Value": "environment-name"
        },
        {
            "Key": "Environment",
            "Value": "production"
        },
        {
            "Key": "Deployer",
            "Value": "test@mail.com"
        }
    ],
    "SolutionStackName": "64bit Amazon Linux 2018.03 v2.11.0 running Docker 18.03.1-ce",
    "OptionSettings": [
        {
            "OptionName": "InstanceType",
            "Namespace": "aws:autoscaling:launchconfiguration",
            "Value": "t2.micro"
        },
        {
            "OptionName": "SecurityGroups",
            "ResourceName": "AWSEBAutoScalingLaunchConfiguration",
            "Namespace": "aws:autoscaling:launchconfiguration",
            "Value": "sg-xxxxxxx,sg-yyyyyyy"
        },
        {
            "OptionName": "ELBSubnets",
            "Namespace": "aws:ec2:vpc",
            "Value": "subnet-xxxxxxx,subnet-yyyyyyy"
        },
        {
            "OptionName": "Subnets",
            "ResourceName": "AWSEBAutoScalingGroup",
            "Namespace": "aws:ec2:vpc",
            "Value": "subnet-xxxxxxx,subnet-yyyyyyy"
        },
        {
            "OptionName": "VPCId",
            "ResourceName": "AWSEBSecurityGroup",
            "Namespace": "aws:ec2:vpc",
            "Value": "vpc-xxxxxxx"
        },
        {
            "OptionName": "Notification Endpoint",
            "Namespace": "aws:elasticbeanstalk:sns:topics",
            "Value": "test@mail.com"
        },
        {
            "OptionName": "Notification Protocol",
            "Namespace": "aws:elasticbeanstalk:sns:topics",
            "Value": "email"
        }
    ]
}
```
