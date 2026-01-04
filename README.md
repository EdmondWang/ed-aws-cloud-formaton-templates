# AWS CloudFormation Templates

This repository contains AWS CloudFormation templates for various AWS resources.

## Structure

```
.
├── README.md
├── templates/
│   └── sample-0-ec2-instance.yaml  # Minimal EC2 instance template
└── .gitignore
```

## Templates

- **sample-0-ec2-instance.yaml**: A minimal CloudFormation template to create an EC2 instance

## Usage

### Deploy via AWS CLI

```bash
# Get the latest Amazon Linux 2023 AMI ID for your region
AMI_ID=$(aws ec2 describe-images \
  --owners amazon \
  --filters "Name=name,Values=al2023-ami-*-x86_64" "Name=state,Values=available" \
  --query 'Images | sort_by(@, &CreationDate) | [-1].ImageId' \
  --output text)

# Create the stack
aws cloudformation create-stack \
  --stack-name my-stack \
  --template-body file://templates/sample-0-ec2-instance.yaml \
  --parameters \
    ParameterKey=InstanceType,ParameterValue=t2.micro \
    ParameterKey=AMIId,ParameterValue=$AMI_ID
```

### Deploy via AWS Console

1. Go to AWS CloudFormation Console
2. Click "Create stack"
3. Upload the template file or provide the template URL
4. Fill in the parameters
5. Follow the wizard to create the stack

## Requirements

- AWS CLI configured with appropriate credentials
- Appropriate IAM permissions to create the resources defined in templates

