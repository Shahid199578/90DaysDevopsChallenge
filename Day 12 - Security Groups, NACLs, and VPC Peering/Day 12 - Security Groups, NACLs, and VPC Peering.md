# AWS Day 12: Security Groups, NACLs, and VPC Peering

---

## 🔐 1. Security Groups (SGs)

### ✅ What is a Security Group?
A virtual firewall that controls **inbound and outbound** traffic for **EC2 instances** and **Elastic Network Interfaces (ENIs)** at the **instance level**.

### 🔑 Key Features:
- **Stateful:** If you allow inbound traffic, the response traffic is automatically allowed.
- **Attached to resources**, not subnets.
- **Multiple rules supported** for different types of traffic.
- **Default behavior:** All traffic is denied until explicitly allowed.

### 📌 When to Use:
- For **fine-grained control** over access to individual instances.
- **Example:** Allow SSH (port 22) from your IP only.

### 🧱 Example Rules:
| Type     | Protocol | Port Range | Source        |
|----------|----------|-------------|----------------|
| Inbound  | TCP      | 22          | My IP          |
| Inbound  | TCP      | 80          | 0.0.0.0/0      |
| Outbound | All      | All         | 0.0.0.0/0      |

### 📌 Common Use Cases:
- Allow HTTP/HTTPS for web servers
- Allow SSH only from office IP
- Block all else by default

---

## 🚧 2. Network Access Control Lists (NACLs)

### ✅ What is a NACL?
A **subnet-level firewall** that controls **inbound and outbound traffic** for all resources within a subnet.

### 🔑 Key Features:
- **Stateless:** Must define both **inbound and outbound rules**.
- **Rules evaluated in number order** (lower rule number = higher priority).
- **Supports Allow and Deny rules.**
- Applied to **entire subnets**.

### 📌 When to Use:
- Add **extra layer of security**.
- Block **known malicious IP ranges**.

### 🧱 Example Rules:
| Rule # | Type  | Protocol | Port | Source          | Allow/Deny |
|--------|-------|----------|------|------------------|-------------|
| 100    | HTTP  | TCP      | 80   | 0.0.0.0/0        | ALLOW       |
| 110    | SSH   | TCP      | 22   | 203.0.113.0/24   | ALLOW       |
| *      | All   | All      | All  | 0.0.0.0/0        | DENY        |

### 🆚 SG vs NACL
| Feature            | Security Group       | NACL                  |
|--------------------|-----------------------|------------------------|
| Level              | Instance-level        | Subnet-level           |
| Stateful           | ✅ Yes                | ❌ No                  |
| Rules              | Only Allow            | Allow + Deny           |
| Evaluation Order   | All at once           | Rule order (low → high) |
| Use Case           | App/resource access   | Subnet-level control   |

---

## 🔄 3. VPC Peering

### 🌐 What is it?
A networking connection between **two VPCs** that enables **private communication** via AWS’s internal network.

### ✅ Key Points:
- Works **within the same AWS account** or **across accounts**.
- **No overlapping CIDR blocks.**
- **No transitive peering**.
- Requires **route table updates**.

### 📌 Use Cases:
- Connect microservices in different VPCs
- Separate environments (dev/test/prod)
- Cross-account/region connectivity

### 🧱 Steps to Setup:
1. Create VPC-A (`10.0.0.0/16`) and VPC-B (`192.168.0.0/16`)
2. Request a **peering connection** from VPC-A to VPC-B
3. Accept the request in VPC-B
4. Update route tables:
   - VPC-A → add route to `192.168.0.0/16` → peering ID
   - VPC-B → add route to `10.0.0.0/16` → peering ID
5. Update **SGs and NACLs** to allow traffic

### 🔁 VPC Peering Lifecycle
| State               | Description                                           | Action/Visibility                            |
|---------------------|-------------------------------------------------------|-----------------------------------------------|
| Initiating-request  | Request created                                       | Visible to requester                          |
| Failed              | Request failed due to overlap/permissions            | Visible for 2 hours                           |
| Pending-acceptance  | Awaiting approval                                     | Expires in 7 days                             |
| Expired             | No action taken                                       | Visible for 2 days                            |
| Rejected            | Accepter rejected                                     | 2 days (requester), 2 hours (accepter)        |
| Provisioning        | AWS is configuring                                    | Temporary state                               |
| Active              | Connection is ready                                   | Can be deleted, not rejected                  |

### 🧮 VPC Peering Quotas
| Name                                         | Default | Adjustable |
|----------------------------------------------|---------|-------------|
| Active VPC peering connections per VPC       | 50      | ✅ Yes       |
| Outstanding peering requests per VPC         | 25      | ✅ Yes       |
| Expiry for unaccepted peering request        | 7 days  | ❌ No        |

---

## 🧪 Hands-On Lab: Configure SG, NACL, and VPC Peering

### 🛠️ Prerequisites:
- Two VPCs: `devops-vpc-a` and `devops-vpc-b`

### ✅ Part 1: Create Security Group
1. Name: `web-sg`
2. Inbound:
   - HTTP (80) from `0.0.0.0/0`
   - SSH (22) from your IP
3. Outbound: All traffic allowed
4. Attach to EC2 instance in a public subnet

### ✅ Part 2: Create Network ACL
1. Go to **VPC > Network ACLs**
2. Create or select a NACL
3. Inbound Rules:
   - Allow TCP 22 and 80
4. Outbound Rules:
   - Allow all
5. Associate with the EC2’s subnet

### ✅ Part 3: VPC Peering
1. Go to **VPC Dashboard > Peering Connections**
2. Create request from `devops-vpc-a` to `devops-vpc-b`
3. Accept the request in `devops-vpc-b`
4. Update route tables in both VPCs
5. Verify connectivity (use ICMP or SSH)

---

## 💡 Real-World Use Cases

### Security Groups:
- Allow only app tier to access databases
- Restrict public access to internal services

### NACLs:
- Block malicious IPs at subnet level
- Prevent internal lateral movement during attacks

### VPC Peering:
- Enable shared logging/monitoring VPC
- Isolate environments but allow communication

---

## 🔒 Tips & Best Practices
- SGs are **your first line of defense**
- Use NACLs for **additional subnet-level protection**
- Document peering connections and rules
- Apply **consistent naming conventions**
  - e.g., `dev-app-sg`, `qa-db-nacl`
- Regularly audit and optimize rules

---

## 📌 Summary Comparison Table

| Feature        | Security Groups        | NACLs                  | VPC Peering             |
|----------------|-------------------------|--------------------------|--------------------------|
| Level          | Instance                | Subnet                   | VPC                      |
| Type           | Stateful                | Stateless                | Private connectivity     |
| Rules          | Allow only              | Allow + Deny             | Needs route updates      |
| Scope          | ENIs (instance level)   | Subnets                  | Entire VPCs              |

