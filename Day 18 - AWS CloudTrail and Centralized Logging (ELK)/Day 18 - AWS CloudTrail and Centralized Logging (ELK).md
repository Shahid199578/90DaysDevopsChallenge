# Day 18 - AWS CloudTrail and Centralized Logging (ELK)

## Part 1: AWS CloudTrail – Monitoring AWS API Calls

### What is AWS CloudTrail?
AWS CloudTrail is a service that enables governance, compliance, and operational and risk auditing of your AWS account. It records all API calls made on your account through the AWS Console, CLI, SDKs, and other services.

### Key Features
- Tracks API activity (who did what, when, and from where).
- Stores logs in S3 securely.
- Supports multi-region trails.
- Can send events to CloudWatch Logs for alerting.

### Use Cases in DevOps & AWS
- **Security Auditing:** Detect unauthorized access.
- **Operational Monitoring:** Track changes to critical infrastructure.
- **Compliance:** Prove change history during audits.
- **Automation Triggers:** Use Lambda to respond to CloudTrail events.

### Key Concepts
- **Trail:** Configuration to deliver events to S3.
- **Event:** A record of an AWS API action.
- **Management Events:** Admin actions like launching instances.
- **Data Events:** Data-level actions like reading S3 objects.

### Example CLI
```bash
aws cloudtrail lookup-events --max-results 5
```

### 🧪 Lab Task 1: Enable CloudTrail
1. Go to AWS CloudTrail Console.
2. Create a new trail:
    - Name: MyTrail
    - Enable for all regions
    - Store logs in new S3 bucket
    - Enable log file validation
3. View logs in the S3 bucket.

---

## Part 2: Centralized Logging with ELK Stack

### What is the ELK Stack?
- **Elasticsearch:** Search and analytics engine.
- **Logstash:** Log collection and processing engine.
- **Kibana:** Visualization and dashboard tool.
- **Filebeat:** Lightweight shipper for logs (optional, part of Elastic Stack).

### Why Use ELK in DevOps?
- Centralizes logs from EC2, ECS, etc.
- Real-time visibility into infrastructure and apps.
- Enables root cause analysis and alerting.

### ELK Architecture & Data Flow
```text
App Logs -> Filebeat -> Logstash -> Elasticsearch -> Kibana
AWS Logs -> CloudWatch -> Logstash -> Elasticsearch -> Kibana
```

### Component Overview
#### Elasticsearch
- Fast, scalable log storage and indexing.
- Supports filtering and full-text search.

#### Logstash
- Parses and enriches logs.
- Configured using pipelines and filters.

#### Kibana
- UI to search, filter, and visualize logs.
- Create dashboards and real-time insights.

### 💼 Use Cases in AWS
| Use Case | ELK Role |
|----------|----------|
| Debug EC2 or Lambda | Use Filebeat/CloudWatch logs |
| ECS Logs Monitoring | Use Fluentd/Filebeat |
| Detect Login Attempts | Analyze CloudTrail logs |
| HTTP Errors Dashboard | Visualize via Kibana |
| Anomaly Detection | Alerts based on thresholds |

---

## 🧪 Lab Task 2: Deploy ELK Stack on EC2

### Requirements
- 1 Ubuntu EC2 instance (t2.medium or higher)
- Open ports: 5044, 5601, 9200

### Steps
```bash
# Install Java
sudo apt update
sudo apt install openjdk-11-jdk -y

# Install Elasticsearch
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-9.0.0-amd64.deb
sudo dpkg -i elasticsearch-9.0.0-amd64.deb
sudo systemctl enable --now elasticsearch

# Install Logstash
wget https://artifacts.elastic.co/downloads/logstash/logstash-9.0.0.deb
sudo dpkg -i logstash-9.0.0.deb
sudo systemctl enable --now logstash

# Install Kibana
wget https://artifacts.elastic.co/downloads/kibana/kibana-9.0.0-amd64.deb
sudo dpkg -i kibana-9.0.0-amd64.deb
sudo systemctl enable --now kibana
```

Access Kibana at: `http://<EC2-Public-IP>:5601`

---

## 🧪 Lab Task 3: Ingest CloudTrail Logs into ELK

### Create Logstash Config (cloudtrail.conf)
```conf
input {
  s3 {
    bucket => "your-cloudtrail-bucket"
    access_key_id => "YOUR_ACCESS_KEY"
    secret_access_key => "YOUR_SECRET_KEY"
    region => "us-east-1"
  }
}
filter {
  json {
    source => "message"
  }
}
output {
  elasticsearch {
    hosts => ["localhost:9200"]
    index => "cloudtrail-logs"
  }
}
```

### Run Logstash
```bash
sudo /usr/share/logstash/bin/logstash -f cloudtrail.conf
```

### Verify Logs
```bash
curl -X GET "localhost:9200/_cat/indices?v"
```

---

## 🧪 Lab Task 4: Visualize Logs in Kibana

1. Access Kibana: `http://<EC2-Public-IP>:5601`
2. Go to **Stack Management > Index Patterns**
3. Create a pattern: `cloudtrail-logs*`
4. Explore logs in **Discover**
5. Build dashboards in **Visualize**

---

## 🧠 Summary

| Topic | Description |
|-------|-------------|
| CloudTrail | Tracks AWS API activity |
| ELK Stack | Log collection and analysis |
| Elasticsearch | Search and index logs |
| Logstash | Pipeline for parsing logs |
| Kibana | UI for visualization |
| DevOps Use | Debugging, Monitoring, Alerting |

