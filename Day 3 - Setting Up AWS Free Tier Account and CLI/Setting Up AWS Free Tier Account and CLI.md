## 1. Introduction to AWS Free Tier and CLI

### Why Use AWS Free Tier?
AWS Free Tier offers free access to AWS services for 12 months, allowing you to experiment and build without incurring charges. It includes:
- **Compute Services**: EC2, Lambda, Lightsail.
- **Storage Services**: S3, EBS.
- **Database Services**: RDS, DynamoDB.
- **Monitoring Services**: CloudWatch.


[![](https://img.youtube.com/vi/E0hm3tkNqAg/0.jpg)](https://www.youtube.com/watch?v=E0hm3tkNqAg)

[Watch the video](https://www.youtube.com/watch?v=E0hm3tkNqAg)

### Why Use AWS CLI?
The AWS Command Line Interface (CLI) allows you to interact with AWS services directly from your terminal or command prompt. It offers:
- Efficient automation through scripts.
- Direct access to AWS APIs.
- The ability to manage and configure AWS resources without using the web console.

## 2. Setting Up Your AWS Free Tier Account

### Step 1: Creating an AWS Account
1. Visit the AWS Free Tier Page.
2. Click on **Create a Free Account** or **Sign Up**.
3. Enter your email address, create a strong password, and choose an AWS account name.
   - **Example:**
     - Email: `youremail@example.com`
     - Password: `yourSecurePassword123`
     - Account Name: `ShahidDevOps`

### Step 2: Setting Up Account Details
1. Choose the Account Type:
   - **Personal**: Suitable for individual use and experimentation.
   - **Professional**: Suitable for business or team usage.
2. Enter your Personal Information:
   - Full Name, Address, Country, Phone Number.
3. Click **Continue**.

### Step 3: Adding Payment Information
- AWS requires a valid credit or debit card for verification.
- **Important:** AWS will charge a refundable $1 to verify your card.
- Enter your card details and billing address.
- Click **Verify and Continue**.

### Step 4: Verifying Your Identity
1. Choose your preferred verification method (**SMS** or **voice call**).
2. Enter your phone number and click **Send SMS**.
3. Enter the verification code you receive.
4. Complete the CAPTCHA and click **Continue**.

### Step 5: Selecting a Support Plan
- Choose **Basic Support (Free)**.
- This plan includes:
  - 24/7 customer service.
  - Access to AWS documentation and community forums.
- Click **Complete Sign Up**.

### Step 6: Accessing the AWS Console
1. Sign in to the **AWS Management Console**.
2. Use your registered email and password.
3. Explore the AWS Console to get familiar with the interface.

## 3. Installing AWS CLI

### 📌 Why Use AWS CLI?
- Easily automate repetitive tasks.
- Manage multiple AWS accounts using profiles.
- Gain complete control from your terminal.

### Step 1: Downloading AWS CLI

#### For Windows
1. Visit the **AWS CLI Downloads** page.
2. Download the **Windows 64-bit MSI installer**.
3. Run the installer and follow the steps.

#### For Linux and Mac
1. Download the AWS CLI package:
   ```bash
   curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
   ```
2. Unzip the package:
   ```bash
   unzip awscliv2.zip
   ```
3. Install AWS CLI:
   ```bash
   sudo ./aws/install
   ```
4. Verify the installation:
   ```bash
   aws --version
   ```

## 4. Configuring AWS CLI

### Step 1: Generate IAM User Access Keys
1. Open the **AWS Management Console**.
2. Navigate to **IAM (Identity and Access Management)**.
3. Select **Users > Add users**.
4. Enter a username (e.g., `cli-user`).
5. Choose **Programmatic access** as the access type.
6. Attach policies:
   - Select **AdministratorAccess** for full permissions.
7. Review and click **Create User**.
8. Download the `.csv` file containing the **Access Key ID** and **Secret Access Key**.

### Step 2: Configure AWS CLI with Credentials
Run the following command:
```bash
aws configure
```
You will be prompted to enter the following details:
- **AWS Access Key ID**: (from the `.csv` file)
- **AWS Secret Access Key**: (from the `.csv` file)
- **Default region name**: (e.g., `us-east-1`)
- **Default output format**: (e.g., `json`)

## 5. Verifying AWS CLI Configuration

### Check AWS Identity
```bash
aws sts get-caller-identity
```
- The output should display your AWS account ID and user ARN.

### List Available S3 Buckets
```bash
aws s3 ls
```

### Create an S3 Bucket
```bash
aws s3 mb s3://shahid-devops-bucket
```

### Upload a Test File
```bash
echo "Hello AWS!" > hello.txt
aws s3 cp hello.txt s3://shahid-devops-bucket/
```

## 6. Troubleshooting Common Issues

| Issue | Solution |
|--------|----------|
| `aws: command not found` | Ensure AWS CLI is correctly installed and added to your PATH. |
| Invalid Access Key or Secret Key | Double-check credentials using `aws configure` or update via IAM console. |
| Permission denied errors | Make sure your IAM user has the required policies attached. |
| Network connectivity issues | Check your internet connection and VPC settings. |

## 7. Best Practices for AWS CLI

- **Secure Access Keys:**
  Use environment variables instead of hardcoding them:
  ```bash
  export AWS_ACCESS_KEY_ID=your-access-key
  export AWS_SECRET_ACCESS_KEY=your-secret-key
  ```
- **Use Named Profiles:**
  Manage multiple accounts with profiles:
  ```bash
  aws configure --profile dev
  aws s3 ls --profile dev
  ```
- **Rotate Keys Regularly:**
  Periodically update your keys to enhance security.
- **Limit Permissions:**
  Follow the **principle of least privilege** when attaching IAM policies.

## 8. Hands-On Activity

### Task 1: Create an S3 Bucket via CLI
```bash
aws s3 mb s3://my-devops-series-bucket
```

### Task 2: Upload a File to the S3 Bucket
```bash
aws s3 cp sample.txt s3://my-devops-series-bucket
```

### Task 3: List the Uploaded File
```bash
aws s3 ls s3://my-devops-series-bucket
```

### Task 4: Delete the S3 Bucket
```bash
aws s3 rb s3://my-devops-series-bucket --force
```

