# Day 87 - Debugging and Troubleshooting Production Systems

Welcome to **Day 87** of the DevOps 90-Day Challenge!
Everything is broken. The customers are angry. What do you do? Today we learn the **Art of Troubleshooting**.

[![](https://img.youtube.com/vi/placeholder/0.jpg)](https://www.youtube.com)

[Watch the video (Link Pending)]()

---

## Objective

By the end of this session, you will:

* Master the **Troubleshooting Methodology**.
* Use standard Linux debugging tools (`strace`, `lsof`, `tcpdump`, `top`).
* Debug Networking (DNS, Firewalls).
* Debug Application Crashes (OOMKill, Segfaults).

---

## Tools Used

* **Linux CLI**
* **Wireshark / tcpdump**
* **Dig / nslookup**
* **Syslog / Journalctl**

---

## Key Concepts

### 1. The Methodology (USE Method)
For every resource (CPU, Disk, Network), check:
*   **U**tilization: How busy is it? (100%?)
*   **S**aturation: Is there a queue?
*   **E**rrors: Are there errors?

### 2. Network Debugging
"It's always DNS."
1.  Can I ping it? (Connectivity).
2.  Can I resolve the name? (DNS).
3.  Is the port open? (`telnet` or `nc`).
4.  Is the SSL cert valid? (`openssl s_client`).

### 3. Application Debugging
*   **Interactive Debugging**: `kubectl exec -it pod -- bash`.
*   **Logs**: `tail -f /var/log/syslog`.
*   **Processes**: `ps aux | grep java`.

---

## Key Concepts Applied

| Concept | Example Used |
| :--- | :--- |
| **OOMKilled** | Identifying that a pod died because it exceeded its memory limit (exit code 137). |
| **Connection Refused** | Determining that the web server process isn't running vs firewall blocking. |
| **Disk Full** | `df -h` shows 100%. `du -sh *` finds the log file eating the space. |

---

## Bonus (Extra Learning)

*   Use `strace` to attach to a running process and see what files it's trying to open.
*   Debug a "Slow" website using Chrome DevTools (Network Tab) + Server Logs.

---

## Congratulations!

You are now a Detective. Troubleshooting is 90% of the job. Being calm under pressure and methodical is what makes a Senior Engineer.

---

## Try These Next

*   Simulate a CPU spike using `stress` and identifying the culprit.
*   Capture packets with `tcpdump` and analyze them in Wireshark.
