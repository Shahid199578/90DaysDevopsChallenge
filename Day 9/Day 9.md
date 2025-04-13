# Day 9: Deep Dive into AWS Storage Services — EBS & S3

---

## What You'll Learn Today

✅ Understand Amazon EBS and Amazon S3  
✅ Compare block vs. object storage  
✅ Create & manage EBS volumes and snapshots  
✅ Work with S3 buckets, lifecycle rules, and access policies  
✅ CLI and GUI walkthroughs  
✅ Real-world use cases  
✅ Best practices  
✅ Hands-on Labs  

---

## Amazon Elastic Block Store (EBS)

### What is EBS?

Amazon EBS provides **block storage** volumes for EC2 instances. Think of it as a **virtual hard drive** you attach to EC2 machines.

| Feature         | Description |
|----------------|-------------|
| Type           | Block Storage |
| Use Case       | OS boot volumes, databases |
| Attachability  | Only to one EC2 instance at a time |
| Backup         | Snapshots (stored in S3) |
| Durability     | Replicated within AZ |

---

### Types of EBS Volumes

| Volume Type     | Use Case                         | Performance |
|-----------------|----------------------------------|-------------|
| gp3 (General Purpose SSD) | Default, general workloads           | Balanced |
| io2/io1 (Provisioned IOPS SSD) | High-performance DBs              | High IOPS |
| st1 (Throughput HDD)     | Streaming, big data                 | High throughput |
| sc1 (Cold HDD)           | Infrequent access                  | Low-cost |

---

### EBS Hands-on (GUI)

#### 1. Create EBS Volume
- Go to EC2 → **Elastic Block Store** → Volumes → **Create Volume**
- Choose type (e.g., `gp3`), size (e.g., 10 GiB)
- Availability Zone must match your EC2 instance

#### 2. Attach Volume to EC2
- Select volume → Actions → Attach Volume
- Choose the EC2 instance

#### 3. Format and Mount (EC2 Instance)
```bash
sudo lsblk                   # List block devices
sudo mkfs -t ext4 /dev/xvdf  # Format
sudo mkdir /data
sudo mount /dev/xvdf /data
```

#### 4. Create Snapshot (Backup)
- Go to Volume → Actions → Create Snapshot

---

### EBS Hands-on (CLI)

```bash
# Create volume
aws ec2 create-volume \
  --availability-zone us-east-1a \
  --size 10 \
  --volume-type gp3

# Attach to EC2 instance
aws ec2 attach-volume \
  --volume-id vol-xxxx \
  --instance-id i-xxxx \
  --device /dev/sdf

# Create snapshot
aws ec2 create-snapshot \
  --volume-id vol-xxxx \
  --description "My backup"
```

---

## Amazon Simple Storage Service (S3)

### What is S3?

Amazon S3 is **object storage**, ideal for storing files, images, backups, and logs. It’s **scalable**, **durable**, and **cost-effective**.

| Feature         | Description |
|-----------------|-------------|
| Type            | Object Storage |
| Durability      | 99.999999999% (11 9's) |
| Access          | Global, via HTTPS |
| Capacity        | Virtually unlimited |
| Files = Objects | Objects stored in Buckets |

---

### Key S3 Concepts

- **Bucket**: Container for storing objects.
- **Object**: File + metadata.
- **Key**: Unique name for each object.
- **Storage Classes**: Standard, Intelligent-Tiering, Glacier, etc.
- **Versioning**: Track multiple versions of files.
- **Lifecycle Rules**: Automatically transition or delete objects.

---

### S3 Hands-on (GUI)

#### 1. Create Bucket
- Go to S3 → **Create Bucket**
- Name it uniquely (e.g., `shahid-devops-bucket`)
- Choose region (e.g., `us-east-1`)
- Disable "Block All Public Access" if needed

#### 2. Upload File
- Open bucket → Upload → Add files

#### 3. Set Lifecycle Rule
- Go to bucket → Management → Lifecycle Rules → Add Rule
- Example: Move to Glacier after 30 days, delete after 365 days

#### 4. Enable Versioning
- Bucket → Properties → Enable versioning

---

### S3 Hands-on (CLI)

```bash
# Create bucket
aws s3 mb s3://shahid-devops-bucket

# Upload file
aws s3 cp myfile.txt s3://shahid-devops-bucket/

# Sync directory
aws s3 sync ./local-dir s3://shahid-devops-bucket/

# List contents
aws s3 ls s3://shahid-devops-bucket/

# Enable versioning
aws s3api put-bucket-versioning \
  --bucket shahid-devops-bucket \
  --versioning-configuration Status=Enabled
```

---

## Security Best Practices (S3 & EBS)

| Area        | Best Practice |
|-------------|---------------|
| IAM       | Least privilege policies |
| Encryption | Enable encryption (AES-256 or KMS) |
| Access     | Avoid public buckets unless needed |
| Monitoring | Use CloudTrail and S3 Access Logs |
| Backup     | Use versioning and snapshots |

---

## Lifecycle Policy Example (S3)

| Action             | Day |
|--------------------|-----|
| Transition to Infrequent Access | 30  |
| Transition to Glacier          | 90  |
| Delete Object                  | 365 |

---

## 💼 Real-World Use Cases

| Service | Use Case |
|--------|----------|
| EBS    | Databases (MySQL, MongoDB), boot volumes |
| S3     | Static website hosting, app backups, logging, media files, CDN origin |

---

## Hands-on Lab

### Lab 1: EBS Volume
- Launch EC2
- Create and attach EBS
- Format, mount, and store files
- Take snapshot and restore

### Lab 2: S3 Lifecycle
- Create bucket with versioning
- Upload files
- Set lifecycle rule to Glacier + delete
- Test file retrieval and version history

---

## Summary

- **EBS = Block storage**, tightly coupled with EC2.
- **S3 = Object storage**, highly scalable and global.
- Understand **types, encryption, access**, and **automation features** (snapshots, lifecycle rules).
- Practice both **CLI and GUI** workflows.
