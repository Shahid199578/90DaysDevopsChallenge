# Day 17 - Setting Alarms, Dashboards, and Metrics

## 🎯 Objective

Deep dive into CloudWatch Alarms, Dashboards, and Custom Metrics. Learn to:

* Set CloudWatch alarms to monitor AWS resources
* Create visual dashboards to observe trends
* Push custom business/application metrics


[![](https://img.youtube.com/vi/PMMAyPLXdGc/0.jpg)](https://www.youtube.com/watch?v=PMMAyPLXdGc)

[Watch the video](https://www.youtube.com/watch?v=PMMAyPLXdGc)

---

## 🧠 Key Concepts

| Feature                               | Description                                                             |
| ------------------------------------- | ----------------------------------------------------------------------- |
| **Alarms**                            | Trigger actions (e.g., email, Lambda) based on metric thresholds        |
| **Dashboards**                        | Visual panels to monitor metrics across services                        |
| **Custom Metrics**                    | Push your own data points for business/app tracking (e.g., login count) |
| **SNS (Simple Notification Service)** | Used to notify users when alarms are triggered                          |

---

## 💡 Use Cases

* **User logins per hour** – Track app usage
* **Queue length (SQS, Redis)** – Monitor message build-up
* **Order volume** – Business KPI visualization

---

## 🧪 Labs Overview

You will perform multiple hands-on labs to solidify understanding.

---

## ✅ Lab 1: Create a CloudWatch Alarm for EC2 CPU Usage

### Steps:

1. Launch EC2 instance
2. Navigate: **CloudWatch > Alarms > Create Alarm**
3. Metric: `EC2 → Per-Instance Metrics → CPUUtilization`
4. Set condition: CPU > 70% for 5 minutes
5. Create SNS topic and confirm email subscription
6. Launch stress test on EC2:

```bash
sudo apt install stress -y
stress --cpu 1 --timeout 300
```

7. Watch alarm status in CloudWatch

---

## ✅ Lab 2: Push a Custom Metric – Track User Logins

```bash
aws cloudwatch put-metric-data \
  --namespace "MyApp/Metrics" \
  --metric-name "UserLogins" \
  --value 1 \
  --unit Count
```

➡️ Run multiple times to simulate logins

---

## ✅ Lab 3: Monitor Application Queue Length

```bash
aws cloudwatch put-metric-data \
  --namespace "MyApp/Queues" \
  --metric-name "JobQueueLength" \
  --value 50 \
  --unit Count
```

➡️ Simulate varying queue values using a loop

---

## ✅ Lab 4: Create a CloudWatch Dashboard

1. Go to **CloudWatch > Dashboards**
2. Name dashboard: `MyApp-Monitoring`
3. Add widgets:

   * Line graph: `UserLogins`
   * Gauge: `JobQueueLength`
   * Number: `OrdersPlaced`

---

## ✅ Lab 5: Push Business Metric – Orders Placed

```bash
aws cloudwatch put-metric-data \
  --namespace "MyApp/Business" \
  --metric-name "OrdersPlaced" \
  --value 12 \
  --unit Count
```

➡️ Add more data points later to simulate activity

---

## ✅ Lab 6: Create Alarm for Custom Metric – Queue Length

1. Go to **CloudWatch > Alarms > Create**
2. Choose `MyApp/Queues` → `JobQueueLength`
3. Condition: > 50
4. Action: SNS topic
5. Test:

```bash
aws cloudwatch put-metric-data \
  --namespace "MyApp/Queues" \
  --metric-name "JobQueueLength" \
  --value 60 \
  --unit Count
```

---

## ✅ Lab 7: Clean Up Resources

```bash
aws cloudwatch delete-dashboards --dashboard-names MyApp-Monitoring
```

Delete any unnecessary alarms or SNS topics from console

## 📘 Homework

1. Create a dashboard for your own project idea.
2. Push three different custom metrics with meaningful names.
3. Create an alarm that notifies on a specific threshold for one of them.


