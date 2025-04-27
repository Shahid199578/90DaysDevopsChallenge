# Day 13: NAT Gateway, Internet Gateway, and Bastion Host

---

## 1. Internet Gateway (IGW)

### What is an Internet Gateway?
- A **horizontally scaled**, **redundant**, and **highly available** AWS service that enables communication between instances in your VPC and the **internet**.
- It supports both **IPv4** and **IPv6** traffic.




[![](https://img.youtube.com/vi/jgR16ACHw2M/0.jpg)](https://www.youtube.com/watch?v=jgR16ACHw2M)

[Watch the video](https://www.youtube.com/watch?v=jgR16ACHw2M)

### Why do we need an Internet Gateway?
- To allow resources in a **public subnet** to:
  - Initiate **outbound** connections to the internet.
  - Receive **inbound** connections (for example, users accessing a web server).

### How it works:
- Attach an Internet Gateway to your **VPC**.
- Modify the **route table** associated with your **public subnet** to include a route to the Internet Gateway for **0.0.0.0/0** (all IPv4 traffic) or **::/0** (all IPv6 traffic).
- Instances must have a **Public IP** or an **Elastic IP** assigned to be reachable from the internet.

---

## 2. NAT Gateway

### What is a NAT Gateway?
- A **Network Address Translation** (NAT) service that allows **instances in private subnets** to **connect to the internet**, while **preventing the internet from initiating connections back** to them.

### Why do we need a NAT Gateway if we have an Internet Gateway?
| Scenario | Behavior |
|:---|:---|
| Instance in a **public subnet** with a public IP | Connects directly to the internet via Internet Gateway. |
| Instance in a **private subnet** without a public IP | Cannot connect to the internet directly even though the VPC has an IGW. Needs NAT Gateway for outbound traffic. |

**Summary:**  
- Private instances (no public IP) → NAT Gateway → Internet Gateway → Internet

### Types of NAT Gateways
| Type | Description |
|:---|:---|
| Public NAT Gateway | Deployed in a public subnet. It uses an Elastic IP. |
| Private NAT Gateway | Deployed in a private subnet. Does not need an Elastic IP. Used for internal VPC-to-VPC communication without traversing the internet. |

---

### Key Points about NAT Gateway:
- **Outbound connections only** from private instances.
- **Cannot receive inbound** internet traffic.
- **Requires** an **Elastic IP address** (for Public NAT Gateway).
- **Automatically scales** to accommodate your traffic.
- **More secure** than assigning public IPs to private instances.

---

### NAT Gateway Related Quotas
| Quota | Default |
|:---|:---|
| Max number of EIPs (Elastic IPs) per account | Limited; must be available to create NAT Gateway |
| Private NAT Gateway: Max number of private IPv4 addresses | 8 |
| Public NAT Gateway: Max number of Elastic IPs attached | 2 (can request increase) |

---

## 3. Bastion Host (Jump Box)

### What is a Bastion Host?
- A **special-purpose instance** that acts as a **gateway** for accessing instances inside a **private subnet**.
- **Deployed in a public subnet** with a **public IP**.

### Why do we need a Bastion Host?
- Private instances **cannot be accessed directly from the internet**.
- The Bastion Host acts as a **controlled entry point** to the private environment via **SSH (Linux)** or **RDP (Windows)**.

---

### Security Best Practices for Bastion Hosts
| Practice | Description |
|:---|:---|
| Use restrictive security groups | Allow inbound SSH (TCP 22) or RDP (TCP 3389) only from **your known IPs**. |
| Disable password login | Enforce **key-based authentication** (SSH keys). |
| Enable logging | Enable session logging (e.g., using Systems Manager Session Manager). |
| Harden the server | Regularly patch and monitor the Bastion Host. |

---

### What happens if you don't restrict Bastion Host Security Groups properly?
- **High Risk of Attack**:
  - Open SSH or RDP ports to `0.0.0.0/0` (anyone on the internet) makes it vulnerable to brute-force and hacking attempts.
  - Attackers could compromise the Bastion Host and then move laterally inside your private network (a technique called "pivoting").

---

## 4. Internet Gateway vs NAT Gateway: Key Differences

| Feature                     | Internet Gateway (IGW)            | NAT Gateway                         |
|------------------------------|-----------------------------------|-------------------------------------|
| Purpose                      | Bidirectional internet access     | Outbound internet access only       |
| Type of instances it serves  | Instances with public IP          | Instances without public IP         |
| Direction of traffic         | Inbound and outbound              | Outbound only                       |
| Associated with              | Public subnet route table         | Private subnet route table          |
| Elastic IP needed            | No                                | Yes (for Public NAT Gateway)        |
| Supports private connectivity | No | Yes (Private NAT Gateway supports VPC-to-VPC without public internet) |

---

## 5. Practical Lab Activities for Class

### Setup
- Create a **VPC** with:
  - 1 Public Subnet
  - 1 Private Subnet

### Internet Gateway Lab
- Attach an **Internet Gateway** to the VPC.
- Route the **public subnet's** traffic to the Internet Gateway.
- Launch an EC2 instance (public IP) in the public subnet and confirm internet access.

### NAT Gateway Lab
- Create a **NAT Gateway** in the public subnet.
- Route the **private subnet's** traffic to the NAT Gateway.
- Launch an EC2 instance (without a public IP) in the private subnet.
- SSH into the instance through the Bastion Host or Systems Manager and verify outbound internet access (e.g., `yum update`).

### Bastion Host Lab
- Deploy a **Bastion Host** EC2 instance in the public subnet.
- Open inbound SSH port **only from your IP address**.
- SSH into the Bastion Host.
- From Bastion Host, SSH into the private EC2 instance.

---

# Final Summary for Day 13 🚀

- **Internet Gateway** provides direct public access to instances with public IPs.
- **NAT Gateway** allows private instances to reach out to the internet **securely**.
- **Bastion Host** provides **secure remote access** to private instances without exposing them to the internet.
- **Security Groups and Routing are Critical** for proper and secure architecture.
- Always **restrict traffic tightly** to enhance security posture.

---

# 📢 Note:
✅ You can also replace the Bastion Host with **AWS Systems Manager Session Manager** (for even better security — no open SSH ports at all).
