**# Day 4: AWS S3 (Simple Storage Service)**

## **1. Introduction to S3**
- AWS S3 provides **scalable object storage**.
- Stores data in **buckets**.
- Ideal for backups, data lakes, and static websites.

## **2. S3 Storage Classes**
- **Standard**: High availability, used for frequently accessed data.
- **Intelligent-Tiering**: Automatically moves data between hot and cold storage.
- **Standard-IA (Infrequent Access)**: Lower cost for infrequent data.
- **Glacier**: Archival storage with retrieval delay.

## **3. S3 Bucket Policies and Permissions**
- IAM policies control access to S3 resources.
- **Bucket policies** allow or deny permissions at the bucket level.
- **ACLs (Access Control Lists)** grant permissions to individual objects.

## **4. S3 Data Management**
- **Versioning**: Keeps multiple versions of an object.
- **Lifecycle Policies**: Automatically transitions data between storage classes.
- **Replication**: Cross-region or same-region data replication.

## **5. S3 Security and Best Practices**
- **Enable encryption** for data protection (SSE-S3, SSE-KMS).
- **Restrict public access** to avoid data leaks.
- **Use CloudTrail** for logging S3 API calls.
- **Enable MFA delete** for extra security.

## **6. Hosting a Static Website on S3**
- Enable **static website hosting** in the S3 bucket settings.
- Configure **index.html** and **error.html**.
- Set bucket policy to allow public read access.
- Use **CloudFront** for content distribution.
