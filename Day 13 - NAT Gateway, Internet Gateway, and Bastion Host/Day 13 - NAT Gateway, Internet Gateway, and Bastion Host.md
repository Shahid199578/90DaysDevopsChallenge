# Day 13 - NAT Gateway, Internet Gateway, and Bastion Host

## 1. Internet Gateway (IGW)

- **Purpose**: Allows communication between instances in your VPC and the internet.
- **Key Points**:
  - Attach an Internet Gateway to your VPC.
  - Update route tables to direct internet traffic (`0.0.0.0/0`) to the IGW.
  - Only instances with a **public IP** can access the internet through the IGW.

---

## 2. NAT Gateway

- **Purpose**: Allow instances in a **private subnet** to access the internet (for software updates, etc.) **without exposing them to incoming internet connections**.
- **Key Points**:
  - Public NAT Gateway: Deployed in a **public subnet**, uses an **Elastic IP**.
  - Private NAT Gateway: Communicates privately without an Elastic IP (used for private VPC connectivity).
  - NAT Gateway **only allows outbound** internet access; **does NOT accept inbound** connections.
  
- **Why NAT Gateway if there is already an Internet Gateway?**
  - Internet Gateway works only for instances with public IPs.
  - Instances in **private subnets do not have public IPs**.
  - NAT Gateway allows **outbound internet** while keeping instances **private**.

- **Related Quotas**:
  - Max 2 Elastic IPs per NAT Gateway (default).
  - Max 8 private IPv4 addresses for Private NAT Gateway.
  - Need enough EIPs available to create Public NAT Gateway.

---

## 3. Bastion Host (Jump Box)

- **Purpose**: Securely connect to instances in **private subnets** using **SSH** or **RDP**.

- **Key Points**:
  - Deployed in a **public subnet** with a **public IP**.
  - Acts as a "bridge" to SSH into private EC2 instances.
  - Bastion Host must have very **restricted Security Groups**:
    - Allow inbound SSH (TCP 22) **only from specific IPs** (your office/home IP).
    - No open access (`0.0.0.0/0`) unless absolutely necessary and monitored.

- **Security Risks**:
  - If Bastion Host Security Group is **too open**, attackers could attempt brute-force attacks.
  - Always limit **allowed IP addresses** and use **key-based authentication** (not password login).

---

## Internet Gateway vs NAT Gateway: Key Differences

| Feature                     | Internet Gateway (IGW)            | NAT Gateway                         |
|------------------------------|-----------------------------------|-------------------------------------|
| Purpose                      | Allow internet access (bidirectional) | Allow private subnet outbound access only |
| Type of instances it serves  | Instances with public IP          | Instances without public IP         |
| Direction of traffic         | Inbound and Outbound              | Only Outbound                      |
| Associated with              | Route table for public subnets    | Route table for private subnets     |
| Needs Elastic IP             | No                                | Yes (for public NAT)                |

---

## Quick Lab Activities

- **Create a VPC** with public and private subnets.
- **Deploy a NAT Gateway** in the public subnet.
- **Launch an EC2 Instance** in the private subnet without a public IP.
- **Test outbound internet access** from the private instance (e.g., `yum update`).
- **Create a Bastion Host** in the public subnet.
- **SSH** from your laptop to the Bastion Host, then **SSH into the private EC2**.
- **Verify** that private EC2 has outbound access but is not accessible directly from the internet.
