# Day 45 - Writing Reusable CloudFormation Templates

Welcome to **Day 45** of the DevOps 90-Day Challenge!
Yesterday, you learned basic CloudFormation templates.
Today, we’ll focus on **reusable and modular templates**, which allow you to scale and manage AWS infrastructure efficiently.

[![](https://img.youtube.com/vi/3w49Ad7ftCs/0.jpg)](https://www.youtube.com/watch?v=3w49Ad7ftCs)

[Watch the video](https://www.youtube.com/watch?v=3w49Ad7ftCs)
---

## Objective

By the end of this session, you will:

* Create **modular CloudFormation templates**.
* Use **parameters, mappings, and outputs** for reusability.
* Implement **nested stacks** for complex infrastructures.

---

## Tools Used

* **AWS CloudFormation**
* **YAML Templates**
* **AWS CLI** (optional)

---

## Key Concepts

### 1. Parameters for Reusability

* Use **parameters** to make templates flexible

```yaml
Parameters:
  InstanceType:
    Type: String
    Default: t2.micro
    Description: EC2 instance type
```

* Change the input value per environment (dev/staging/prod)

---

### 2. Mappings

* Define **static values** that vary by region, environment, or account

```yaml
Mappings:
  RegionMap:
    us-east-1:
      AMI: ami-0abcdef1234567890
    ap-south-1:
      AMI: ami-0fedcba9876543210
```

* Access mapping with `!FindInMap`

```yaml
ImageId: !FindInMap [RegionMap, !Ref "AWS::Region", AMI]
```

---

### 3. Outputs for Inter-Stack Communication

* Use **outputs** to share information with other stacks

```yaml
Outputs:
  InstanceId:
    Description: EC2 instance ID
    Value: !Ref MyEC2Instance
```

---

### 4. Nested Stacks

* Split templates into **child stacks** for modularity

```yaml
Resources:
  NetworkStack:
    Type: AWS::CloudFormation::Stack
    Properties:
      TemplateURL: https://s3.amazonaws.com/mybucket/network.yaml
```

* Parent stack deploys multiple **child templates**

---

### 5. Sample Reusable Template

```yaml
AWSTemplateFormatVersion: '2010-09-09'
Description: Reusable EC2 Template

Parameters:
  Environment:
    Type: String
    Default: dev

Mappings:
  EnvMap:
    dev:
      InstanceType: t2.micro
    prod:
      InstanceType: t2.large

Resources:
  MyEC2Instance:
    Type: AWS::EC2::Instance
    Properties:
      InstanceType: !FindInMap [EnvMap, !Ref Environment, InstanceType]
      ImageId: ami-0abcdef1234567890

Outputs:
  InstanceId:
    Value: !Ref MyEC2Instance
```

---

### 6. Deploy the Template

```bash
aws cloudformation create-stack \
    --stack-name reusable-demo \
    --template-body file://reusable-ec2.yaml \
    --parameters ParameterKey=Environment,ParameterValue=prod
```

---

### 7. Verify

* Check **EC2 console** → instance type matches environment
* Stack outputs available in **Outputs tab**

---

## Key Concepts Applied

| Concept       | Example Used                               |
| ------------- | ------------------------------------------ |
| Parameters    | Environment input (dev/prod)               |
| Mappings      | InstanceType per environment               |
| Outputs       | EC2 instance ID                            |
| Nested Stacks | Split templates for modular infrastructure |

---

## Bonus (Extra Learning)

* Create **child templates** for VPC, Security Groups, and EC2
* Reuse the **same template** for multiple accounts/environments
* Integrate CloudFormation templates with **CI/CD pipeline**

---

## Congratulations!

You’ve learned to write **reusable and modular CloudFormation templates**!
This enables scalable and maintainable infrastructure automation on AWS.

---

## Try These Next

* Implement **nested stacks** for VPC, EC2, and S3
* Test parameters and mappings in different regions
* Automate **stack creation via Terraform or Jenkins pipeline**

