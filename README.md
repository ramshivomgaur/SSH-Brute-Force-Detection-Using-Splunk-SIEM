# SSH-Brute-Force-Detection-Using-Splunk-SIEM
A Hands-On Cybersecurity Project
📌 Overview

This project demonstrates how to detect an SSH brute-force attack using Splunk SIEM in a controlled, virtualized cybersecurity lab.

The setup includes:

A Splunk Enterprise server

A Linux machine acting as a log source (victim)

A Kali Linux machine acting as an attacker

The goal is to simulate a real brute-force attack, forward logs to Splunk, and analyze/detect malicious behavior.

🎯 Objectives

Configure Splunk Enterprise as a SIEM

Forward system authentication logs from a Linux machine

Simulate SSH brute-force attacks using Hydra

Detect suspicious activity using Splunk SPL queries

Build a mini SOC-style analysis workflow

🏗️ Architecture Diagram
+--------------------+        Log Forwarding        +-----------------------+
| Linux Machine      | ---------------------------> | Splunk Enterprise     |
| (Victim)           |        (Syslogs/Auth Logs)   | (SIEM Server)         |
+--------------------+                               +-----------------------+
          ^                                                     |
          | SSH Brute-Force Attack                              |
          |                                                     |
+--------------------+                                          |
| Kali Linux         | ------------------------------------------ 
| (Attacker)         | Hydra SSH attack tool                     
+--------------------+                                          


NOTE: All IP addresses and credentials used in the real setup are intentionally omitted.

⚙️ Technologies Used

Splunk Enterprise

Splunk Universal Forwarder

Linux (log source)

Kali Linux (attack simulation)

Hydra (SSH brute-force tool)

VirtualBox (virtual lab environment)

SSH (OpenSSH server)

🛠️ Setup & Configuration Summary
🔹 1. Configure Virtualization Networking

Host-Only Adapter – internal lab network

NAT Adapter – Internet access

This ensures isolated lab communication while allowing tool installation.

🔹 2. Install and Configure Splunk Enterprise

Enabled receiving on a dedicated port

Created a custom index for SSH logs

Splunk was prepared to ingest logs from remote machines.

🔹 3. Install Splunk Universal Forwarder on Linux

Added Splunk server as a forwarding target

Configured monitoring of auth.log (SSH authentication events)

Verified forwarding status via CLI

The log source was successfully connected to Splunk.

🔹 4. Enable SSH Server on Linux (Victim)

Installed and enabled OpenSSH

Confirmed SSH port was listening

This machine became the target of the simulated attack.

🔹 5. Simulate SSH Brute-Force Attack (Kali)

Created username and password wordlists

Used Hydra to attempt SSH brute-force

Generated real failed login attempts

All attempts were captured inside the victim’s authentication log.

🔹 6. Analyze Events in Splunk

Used SPL searches to detect:

Failed login attempts

Repeated authentication failures

Possible brute-force patterns

Usernames and source IPs involved

Examples:

search index=* "Failed password"


More advanced detection:

"Failed password"
| rex "from (?<src_ip>\d+\.\d+\.\d+\.\d+).* for (?<user>\S+)"
| stats count AS attempts by src_ip user

📊 Results

SSH brute-force attempts were successfully simulated

Syslog authentication events were sent to Splunk

Splunk SIEM identified repeated failed logins

Attack patterns (e.g., high-frequency failures) were clearly visible

The environment functioned like a real SOC detection scenario

🧠 Skills Gained

Security Monitoring & Log Analysis

SIEM Deployment (Splunk)

Linux Security & SSH Hardening Concepts

Threat Detection

Brute-Force Attack Simulation

Virtual Networking Configuration

Incident Investigation Workflow

🏁 Conclusion

This hands-on project successfully demonstrates how Splunk SIEM can detect brute-force attacks by analyzing real authentication logs.
It serves as an excellent practical exercise for SOC analysts, cybersecurity students, and security enthusiasts.
