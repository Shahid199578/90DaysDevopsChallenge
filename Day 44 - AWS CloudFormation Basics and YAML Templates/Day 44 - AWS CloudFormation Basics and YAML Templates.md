# Day 44 - AWS CloudFormation Basics and YAML Templates

Welcome to **Day 44** of the DevOps 90-Day Challenge!
Today, we’ll explore **AWS CloudFormation**, a native IaC service, and learn how to write **YAML templates** to automate AWS resource provisioning.

[![](https://img.youtube.com/vi/LzXWXAVfw34/0.jpg)](https://www.youtube.com/watch?v=LzXWXAVfw34)

[Watch the video](https://www.youtube.com/watch?v=LzXWXAVfw34)

---

## Objective

By the end of this session, you will:

* Understand **CloudFormation basics**.
* Write simple **YAML templates** for AWS resources.
* Deploy stacks and manage infrastructure using CloudFormation.

---

## Tools Used

* **AWS Management Console**
* **CloudFormation** service
* **YAML Templates**

---

## Key Concepts

### 1. CloudFormation Basics

* AWS service to **provision infrastructure as code**
* Supports **YAML** and **JSON** templates
* Key concepts:

  * **Stack**: Collection of resources deployed together
  * **Template**: YAML/JSON file defining resources
  * **Parameters**: Inputs to make templates reusable
  * **Outputs**: Return values from stack

---

### 2. Sample YAML Template

```yaml
AWSTemplateFormatVersion: '2010-09-09'
Description: Simple EC2 Instance

Parameters:
  InstanceType:
    Type: String
    Default: t2.micro
    Description: EC2 instance type

Resources:
  MyEC2Instance:
    Type: AWS::EC2::Instance
    Properties:
      InstanceType: !Ref InstanceType
      ImageId: ami-0abcdef1234567890
      Tags:
        - Key: Name
          Value: CloudFormationDemo
          
Outputs:
  InstanceId:
    Description: ID of the EC2 instance
    Value: !Ref MyEC2Instance
```

---

### 3. Deploy CloudFormation Stack

1. Go to **AWS Console → CloudFormation → Create Stack**
2. Upload your YAML template
3. Provide stack **name** and **parameters**
4. Click **Create Stack**
5. Monitor **stack events** until `CREATE_COMPLETE`

---

### 4. Verify

* Check **EC2 console** → instance created
* Review **Outputs** tab → instance ID returned

---

## Key Concepts Applied

| Concept    | Example Used                   |
| ---------- | ------------------------------ |
| Stack      | Collection of resources        |
| Template   | YAML file defining EC2         |
| Parameters | InstanceType input             |
| Outputs    | InstanceId returned from stack |

---

## Bonus (Extra Learning)

* Add **S3 bucket** resource to the same stack
* Use **Conditions** to create optional resources
* Implement **UpdateStack** to modify resources safely

---

## Congratulations!

You’ve learned the basics of **AWS CloudFormation** and created your **first YAML template**! 
This is foundational for automating AWS infrastructure without writing imperative scripts.

---

## Try These Next

* Create **multi-resource stacks** (EC2 + S3 + Security Group)
* Use **mappings** to select AMIs per region
* Experiment with **nested stacks** for modular infrastructure

