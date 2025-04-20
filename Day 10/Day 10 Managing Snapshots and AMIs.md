**Introduction**

In AWS, Snapshots and AMIs (Amazon Machine Images) are crucial for creating backups, restoring data, and launching instances with pre-configured environments. Managing snapshots and AMIs efficiently ensures that your infrastructure is highly available, fault-tolerant, and easily recoverable.


[![](https://img.youtube.com/vi/pyJZmn2sTJE/0.jpg)](https://www.youtube.com/watch?v=pyJZmn2sTJE)

[Watch the video](https://www.youtube.com/watch?v=pyJZmn2sTJE)

**Snapshots in AWS**

**What Are Snapshots?**

A **snapshot** is a backup of your Amazon EBS volume stored in Amazon S3. Snapshots are incremental, meaning only the blocks that have changed since the last snapshot are saved, which helps optimize storage costs.

**Why Use Snapshots?**

1. **Data Backup:** Safely back up your EBS volumes to restore later.

2. **Disaster Recovery:** Recover from failures and data loss.

3. **Migration:** Move data between regions or accounts.

4. **Version Control:** Keep different states of your data.

**How Snapshots Work:**

-   **First snapshot**: Full copy of the EBS volume.
-   **Subsequent snapshots**: Incremental (only changes are saved).

**Amazon Machine Images (AMIs)**

**What Are AMIs?**

An **AMI (Amazon Machine Image)** is a pre-configured template that contains:

1. **Operating System:** Windows, Linux, etc.

2. **Application Server:** Pre-installed software.

3. **System Configuration:** Custom settings and packages.

4. **Data Volumes:** Additional EBS volumes (if needed).

`AMIs are used to launch EC2 instances and can be created from an existing instance or a snapshot.`

----------

**Why Use AMIs?**

1. **Instance Replication:** Launch identical EC2 instances quickly.

2. **Backup and Recovery:** Save the state of an instance.

3. **Environment Consistency:** Use the same configuration across multiple instances.

4. **Faster Deployments:** Reduce launch time with pre-configured images.

**Hands-On: Create EBS Snapshot via Console (GUI)**

**Prerequisites:**

-   **One running EC2 instance with an EBS volume.**

**Steps:**

1.  **Go to EC2 Dashboard → Volumes.**
2.  **Select your EBS volume.**
3.  **Click Actions → Create Snapshot.**
4.  **Add a description and click Create Snapshot.**
5.  **Go to Snapshots to view it.**

**Creating an EBS Snapshot (CLI)**

 **Describe Volumes:**

aws ec2 describe-volumes

**Create Snapshot:**

aws ec2 create-snapshot --volume-id vol-12345678 --description "Backup of my EBS volume"

**Check Snapshot Status:**

aws ec2 describe-snapshots --snapshot-ids snap-12345678

**Restoring from a Snapshot (GUI)**

**Go to Snapshots:**

Select the snapshot you want to restore.
**Create Volume:**

Click **Actions** → **Create Volume**.

Choose the **availability zone** and **volume type**.

Click **Create Volume**.

**Attach Volume:**

Attach the newly created volume to an EC2 instance.

**Restoring from a Snapshot (CLI)**

**Create Volume from Snapshot:**

aws ec2 create-volume --snapshot-id snap-12345678 --availability-zone us-east-1a --volume-type gp2

**Attach the Volume:**

aws ec2 attach-volume --volume-id vol-87654321 --instance-id i-12345678 --device /dev/sdf

----------

**Creating an AMI from an Instance (GUI)**

**Open EC2 Dashboard:**

Go to **AWS Management Console**.

Choose **EC2**.

**Select Instance:**

Click on **Instances**.

Right-click the instance you want to create an AMI from.

**Create Image:**

 **Image and Templates** → **Create Image**.

Enter a **name and description**.

Select **No reboot** if you don’t want the instance to restart.

Click **Create Image**.

**View AMI:**

Go to **AMIs** under **Images** to see your newly created image.

----------

**Creating an AMI from an Instance (CLI)**

**Create AMI:**

aws ec2 create-image --instance-id i-12345678 --name "MyCustomAMI" --no-reboot

 **List AMIs:**

aws ec2 describe-images --owners self

----------

**Launching an Instance from an AMI (GUI)**

 **Go to AMIs:**

 Select **Images** → **AMIs**.

 **Select Your AMI:**

 Right-click the AMI and select **Launch**.

 **Configure Instance:**

 Choose the instance type and configure details.

 Click **Launch**.

----------

**Launching an Instance from an AMI (CLI)**

 **Run Instance:**

aws ec2 run-instances --image-id ami-12345678 --instance-type t2.micro --key-name MyKeyPair

 **Check Running Instances:**

aws ec2 describe-instances

----------

**Managing AMIs**

**Deregistering Unused AMIs**

 **Deregister AMI:**

aws ec2 deregister-image --image-id ami-12345678

 **Delete Snapshot of the AMI:**

aws ec2 delete-snapshot --snapshot-id snap-87654321

**Sharing AMIs Across Accounts**

 **Modify Image Attribute:**

aws ec2 modify-image-attribute --image-id ami-12345678 --launch-permission "Add=[{UserId=123456789012}]"

 **Copying AMI to Another Region:**

aws ec2 copy-image --source-image-id ami-12345678 --source-region us-east-1 --region us-west-2 --name "CopiedAMI"

----------

**Automate Snapshots using Lifecycle Manager**

**AWS Console → EC2 → Lifecycle Manager**

1.  Create Lifecycle Policy.
2.  Choose **resource type** = Volume.
3.  Set **schedule** (e.g., daily, every 12 hrs).
4.  Define **retention rules** (e.g., keep 7 snapshots).
5.  Review & Create.

`✅ No Lambda or scripting needed — all managed by AWS!`

**Real-Time Use Cases**

**1. Automated Backups with Snapshots**

 Set up **AWS Lambda** with **CloudWatch Events** to take periodic EBS snapshots.

 Ideal for **database backups** and critical system data.

**2. Creating Golden AMIs**

 Create a **base AMI** with all necessary configurations and packages.

 Launch multiple instances from the AMI for consistent environments.

**3. Disaster Recovery**

 Use **Snapshots** to restore data quickly.

 Use **AMIs** to spin up replacement instances after a failure.

----------

**Best Practices**

 **Automate Snapshots:**

 Use AWS Backup or AWS Lambda to automate snapshot creation and cleanup.

 **Tag Snapshots and AMIs:**

 Use tags to easily identify snapshots and AMIs, especially when dealing with multiple instances.

 **Monitor Snapshot Usage:**

 Regularly check and delete outdated or unnecessary snapshots to reduce costs.

 **Optimize AMI Storage:**

 Delete old AMIs and associated snapshots to save on storage charges.

----------

**Hands-On Summary**

 **Creating and Managing Snapshots:**

 Took EBS snapshots using both GUI and CLI.

 Restored volumes from snapshots.

 **Creating and Managing AMIs:**

 Created an AMI from an existing EC2 instance.

 Launched new instances using the AMI.

 Managed AMI versions and shared AMIs between accounts.

 **Automated Backup:**

 Implemented automated snapshot creation using AWS Lambda.