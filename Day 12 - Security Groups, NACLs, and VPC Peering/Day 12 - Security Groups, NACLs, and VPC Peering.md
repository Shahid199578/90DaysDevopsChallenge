
# Day 12: Security Groups, NACLs, and VPC Peering

## 🔐 Security Groups (SGs)

Security Groups act as virtual firewalls for your EC2 instances to control inbound and outbound traffic.

### Key Concepts:
- **Stateful:** Responses to allowed inbound traffic are automatically allowed.
- **Instance-level firewall:** Applied directly to EC2 instances.
- **Rules:** Based on protocols, ports, and CIDR IP ranges.

### Practical Example:
```bash
# Allow inbound SSH from a specific IP
aws ec2 authorize-security-group-ingress   --group-id sg-0123456789abcdef0   --protocol tcp --port 22   --cidr 203.0.113.0/24
```

---

## 🌐 Network Access Control Lists (NACLs)

NACLs are stateless firewalls for controlling traffic at the subnet level.

### Key Concepts:
- **Stateless:** Rules apply in both directions independently.
- **Subnet-level firewall:** Controls traffic entering/leaving subnets.
- **Rules:** Numbered, evaluated in order, explicit deny rule support.

### Practical Example:
- Block access from a specific IP at subnet level.
- Allow only HTTP/HTTPS traffic in a public subnet.

---

## 🔗 VPC Peering

VPC Peering allows private connectivity between two VPCs using AWS's backbone.

### Key Concepts:
- **One-to-one relationship:** No transitive routing.
- **Non-overlapping CIDRs:** Required.
- **Route Tables:** Must be updated manually.
- **Security Groups and NACLs:** Must allow traffic.

### Lifecycle:
1. **Initiating-request:** Request created.
2. **Pending-acceptance:** Awaiting peer acceptance.
3. **Provisioning:** Being established.
4. **Active:** Connection is live.
5. **Expired/Rejected/Failed:** Connection failed or not accepted.

### Limitations:
- No transitive peering (A–B, A–C ≠ B–C)
- Cannot share gateways, NATs, or VPNs across peered VPCs
- Manual route table updates needed for communication

### Example Route Table Update for VPC A:
| Destination CIDR | Target        |
|------------------|---------------|
| 10.0.0.0/16      | local         |
| 10.1.0.0/16      | peering-A-B   |
| 10.2.0.0/16      | peering-A-C   |

---

## 📏 Peering Quotas

| Name                                          | Default    | Adjustable |
|-----------------------------------------------|------------|------------|
| Active connections per VPC                    | 50         | Yes (125)  |
| Outstanding peering connection requests       | 25         | Yes        |
| Expiry time for unaccepted requests           | 1 week     | No         |

---

## 🧠 Real-World Use Case

You have a dev VPC and a prod VPC. VPC Peering helps connect both for private service discovery between environments. Ensure:
- Non-overlapping CIDRs
- Proper route tables and SG rules
- Direct peering (no transitive routes)

