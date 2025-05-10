# Day 16 - Introduction to AWS CloudWatch
Here's the **Markdown** format for **Day 16: Introduction to AWS CloudWatch**:

````markdown
# 🌩️ **Day 16: Introduction to AWS CloudWatch**

## 🎯 **Learning Objectives**
By the end of this session, you should be able to:

- Understand the purpose and benefits of AWS CloudWatch.
- Explore core components: Metrics, Logs, Alarms, Dashboards, and Events.
- Learn how to monitor EC2 instances using CloudWatch.
- Configure CloudWatch Agent to collect system logs.
- Analyze logs and metrics for troubleshooting.


[![](https://img.youtube.com/vi/FX_z74uHWaM/0.jpg)](https://www.youtube.com/watch?v=FX_z74uHWaM)

[Watch the video](https://www.youtube.com/watch?v=FX_z74uHWaM)

---

## 🧠 **What is AWS CloudWatch?**

AWS CloudWatch is a monitoring and observability service that provides the following features:

- **Metrics**: Collects numerical data, such as CPU utilization and network traffic.
- **Alarms**: Set thresholds to trigger actions when certain metrics are exceeded.
- **Logs**: Collects, stores, and analyzes log files from your AWS resources.
- **Dashboards**: Customizable visual panels to display your metrics and logs.

---

## 🧱 **Core Components of AWS CloudWatch**

| Component      | Description                                   |
| -------------- | --------------------------------------------- |
| **Metrics**    | Numeric data like CPU utilization, memory usage, etc. |
| **Alarms**     | Allows you to set thresholds for metrics and trigger actions (like sending notifications) when the threshold is breached. |
| **Logs**       | Collects logs from various AWS resources and applications. |
| **Dashboards** | Allows you to create custom dashboards to visualize your metrics and logs in real-time. |
| **Events**     | Responds to changes in the AWS environment by automating tasks or triggering actions. |

---

## 🧪 **Lab Tasks**

### ✅ **Lab Task 1: View EC2 Metrics in CloudWatch**

1. Launch an EC2 instance (if not already running).
2. Go to **CloudWatch > Metrics**.
3. Select **EC2 > Per-Instance Metrics**.
4. View metrics such as:
   - CPUUtilization
   - Disk Read/Write
   - Network In/Out

### ✅ **Lab Task 2: Create a CloudWatch Alarm**

1. Navigate to **CloudWatch > Alarms**.
2. Create a new Alarm:
   - Metric: `EC2 > CPUUtilization`
   - Set the threshold to `> 70%` for the selected EC2 instance.
3. Set the action: Send a notification (create an SNS topic if needed).

### ✅ **Lab Task 3: Enable Detailed Monitoring (Optional)**

1. Stop the EC2 instance.
2. Enable **detailed monitoring** during instance modification.
3. Restart the instance and confirm that the metrics are now available at 1-minute intervals.

### ✅ **Lab Task 4: Collect and View System Logs**

1. Install CloudWatch Agent:
   ```bash
   sudo yum install amazon-cloudwatch-agent -y
````

2. Create a configuration file (JSON) for the agent.
3. Start the agent and verify that logs appear in **CloudWatch Logs**.

### ✅ **Lab Task 5: Create a CloudWatch Dashboard**

1. Go to **CloudWatch > Dashboards**.
2. Create a dashboard that includes:

   * EC2 CPU graph
   * Network In/Out graph
   * Custom metric (optional)

---

## 🛠️ **Commands Summary**

| Task                     | Command                                                                          |
| ------------------------ | -------------------------------------------------------------------------------- |
| Install CloudWatch Agent | `sudo yum install amazon-cloudwatch-agent -y`                                    |
| Start CloudWatch Agent   | `sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -a start` |
| View Logs                | Navigate to **CloudWatch Console > Logs**                                        |
| Create Alarm             | Navigate to **CloudWatch Console > Alarms > Create Alarm**                       |

---

## 📌 **Tip**

* To semulate real-time CPU spikes, run a stress test on the EC2 instance:

  ```bash
  sudo apt install stress -y
  stress --cpu 1 --timeout 300
  ```
* Then, observe the spike in CloudWatch metrics.

---

## 🔄 **Summary**

* AWS CloudWatch offers a comprehensive solution for monitoring and managing AWS resources.
* Key features include Metrics, Alarms, Logs, Dashboards, and Events.
* Hands-on labs provide experience with EC2 metrics, system logs, and configuring CloudWatch Dashboards.

---

## ✨ **Next Steps**

In the next session, we will dive deeper into **Setting Alarms, Dashboards, and Metrics**.

