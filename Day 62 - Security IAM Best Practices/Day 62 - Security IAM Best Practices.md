# Day 62 - Security: IAM Best Practices

Welcome to **Day 62** of the DevOps 90-Day Challenge!
Today, we shift focus to **Security**. In the cloud, **Identity is the new Perimeter**. We will master AWS IAM (Identity and Access Management) to secure our environment.

[![](https://img.youtube.com/vi/placeholder/0.jpg)](https://www.youtube.com)

[Watch the video (Link Pending)]()

---

## Objective

By the end of this session, you will:

* Understand the **Principle of Least Privilege**.
* Differentiate between **Users, Groups, Roles, and Policies**.
* Secure the **Root Account** (MFA).
* Use **IAM Access Analyzer** to find unintended public access.
* Rotate access keys safely.

---

## Tools Used

* **AWS IAM**
* **AWS CLI**
* **MFA Device** (Google Authenticator/Authy)

---

## Key Concepts

### 1. Users vs. Roles
*   **IAM User**: A person or long-term service. Has permanent credentials (password/access keys). *Avoid using these for applications.*
*   **IAM Role**: A temporary identity. Has no password. Anyone who assumes the role gets temporary credentials. *Use this for EC2, Lambda, and cross-account access.*

### 2. Policies
JSON documents that define permissions.
```json
{
    "Effect": "Allow",
    "Action": "s3:ListBucket",
    "Resource": "arn:aws:s3:::my-bucket"
}
```

### 3. The Root Account
The email you used to sign up. It has unlimited power. **Never use it for daily tasks.**
1.  Enable MFA.
2.  Create an Admin IAM User.
3.  Lock away the Root credentials.

---

## Key Concepts Applied

| Concept | Application |
| :--- | :--- |
| **Groups** | Putting all developers in a `Developers` group and attaching policies to the group, not the user. |
| **Inline vs Managed** | Using **Customer Managed Policies** for reusability across multiple roles. |
| **Credential Report** | downloading a CSV to audit who has MFA enabled and when keys were last rotated. |

---

## Bonus (Extra Learning)

*   Set up a **Password Policy** (e.g., minimum 12 chars, requires symbol).
*   Create a policy with a **Condition** (e.g., Allow access only if MFA is present: `aws:MultiFactorAuthPresent: "true"`).

---

## Congratulations!

You’ve hardened your AWS account! Security isn't a feature; it's a mindset. Always start with zero permissions and add only what is strictly necessary.

---

## Try These Next

*   Create a **Cross-Account Role** to allow a user in Account A to manage S3 in Account B.
*   Use **IAM Policy Simulator** to debug why a user is getting "Access Denied".
