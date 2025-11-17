🚀 SSH Brute-Force Detection Using Splunk SIEM

A Hands-On Cybersecurity Project

📌 Overview

This project demonstrates how to detect an SSH brute-force attack using Splunk SIEM.
A virtual cybersecurity lab was created using:

Splunk Enterprise (SIEM Server)

Linux machine (Log Source / SSH Target)

Kali Linux (Attacker using Hydra)

The goal was to simulate an attack, forward logs, and detect malicious activity using SPL queries.

🎯 Objectives

Configure Splunk to receive logs from a Linux host

Forward authentication logs via Splunk Universal Forwarder

Simulate SSH brute-force attempts

Detect failed login events using SPL

Build a real SOC-style detection workflow

🏗️ Architecture
Linux Machine (Victim) → Splunk Enterprise (SIEM)
        ↑
        └────── Kali Linux (Attacker using Hydra)

🛠️ Lab Setup Summary
✔ VirtualBox Networking

Host-Only Adapter → internal lab network

NAT Adapter → Internet access

✔ Splunk Enterprise (Server)

Installed Splunk Enterprise

Enabled receiving on a dedicated port

Created a custom index for SSH logs

✔ Linux Machine (Victim)

Installed Splunk Universal Forwarder

Configured to forward /var/log/auth.log

Enabled and started OpenSSH server

✔ Kali Linux (Attacker)

Installed Hydra

Created username & password lists

Launched SSH brute-force attempts

🔥 Attack Simulation

Hydra was used to generate SSH brute-force attempts:

hydra -L users.txt -P passwords.txt -t 4 -V <target-ip> ssh


These attempts created:

Failed login events

Multiple username trials

Authentication errors

All captured in the victim’s auth logs.

🕵️ Detection in Splunk
Basic search:
"Failed password"

Extract attacker IP & username:
"Failed password"
| rex "from (?<src_ip>\d+\.\d+\.\d+\.\d+).* for (?<user>\S+)"
| stats count by src_ip user

Brute-force behavior detection:
"Failed password"
| stats count AS attempts by src_ip
| where attempts > 10

📊 Results

Brute-force attempts successfully simulated

Linux logs forwarded to Splunk

Splunk visualized failed logins

Attack patterns were clearly identified

🧠 Skills Demonstrated

SIEM configuration (Splunk)

Linux log analysis

Attack simulation

Threat detection

SOC investigation workflow

Virtual networking

🏁 Conclusion

This project replicates a real SOC detection scenario by combining log forwarding, brute-force simulation, and analysis using Splunk.
It showcases strong practical cybersecurity and SIEM skills.
