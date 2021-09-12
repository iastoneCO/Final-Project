# Blue Team: Summary of Operations

## Table of Contents
- Network Topology
- Description of Targets
- Monitoring the Targets
- Patterns of Traffic & Behavior
- Suggestions for Going Further

### Network Topology
The following machines were identified on the network:

- Hypervisor Host Machine 
  - **Operating System**: Microsoft Azure Windows
  - **Purpose**: Hypervisor
  - **IP Address**: 192.168.1.1
- ELK
  - **Operating System**: Linux Debian 6.7
  - **Purpose**: Elasticsearch, Kibana Search
  - **IP Address**: 192.168.1.100
- Capstone
  - **Operating System**: Linux Debian 6.7 
  - **Purpose**: Filebeat and Metricbeat installed and will forward logs to the ELK machine. 
  - **IP Address**: 192.168.1.105
  - Kali
  - **Operating System**: Linux
  - **Purpose**: attack to Windows machine.
  - **IP Address**: 192.168.1.90
- Target 1
  - **Operating System**: Linux
  - **Purpose**: HTTP Server - a vulnerable wordprocess server.
  - **IP Address**: 192.168.1.110
- Target 2
  - **Operating System**: Linux
  - **Purpose**: HTTP Server
  - **IP Address**: 192.168.1.115

### Description of Targets


The target of this attack was: `Target 1` (IP Address: 192.168.1.110).

Target 1 is an Apache web server and has SSH enabled, so ports 80 and 22 are possible ports of entry for attackers. As such, the following alerts have been implemented:

### Monitoring the Targets

Traffic to these services should be carefully monitored. To this end, we have implemented the alerts below:

#### Excessive HTTP errors 
_TODO: Replace `Alert 1` with the name of the alert._

Alert 1 is implemented as follows:
  - **Metric**: http.response.status_code > 400 
  - **Threshold**: 5 in last 5 minutes
  - **Vulnerability Mitigated**: The security team could identify attack and block the IP addresses, change the password or should close the port 22. 
  - **Reliability**: No, this alert generate lots of false positives. It's high reliability.

#### HTTP Request Size Monitor
Alert 2 is implemented as follows:
  - **Metric**: http.request.bytes
  - **Threshold**: 3500 in last 1 minutes
  - **Vulnerability Mitigated**: The number of HTTP request size through a filter from controlling the system also have protects against DDoS attacks. 
  - **Reliability**: No, this alert doesn't generate lots of false positives. It's high reliability.

#### CPU Usage Monitor
Alert 3 is implemented as follows:
  - **Metric**: system.process.cpu.total.pct
  - **Threshold**: 0.5 in last 5 minutes
  - **Vulnerability Mitigated**: It's 50% percentage by controlling the CPU usuage. It will trigger a memory dump of stored information is generated. 
  - **Reliability**: Yes: this alert does generate lots of false positives because the CPU can spike even. It's low reliability.

### Suggestions for Going Further (Optional)

- Each alert above pertains to a specific vulnerability/exploit. Recall that alerts only detect malicious behavior, but do not stop it. For each vulnerability/exploit identified by the alerts above, suggest a patch. E.g., implementing a blocklist is an effective tactic against brute-force attacks. It is not necessary to explain _how_ to implement each patch.

The logs and alerts generated during the assessment suggest that this network is susceptible to several active threats, identified by the alerts above. In addition to watching for occurrences of such threats, the network should be hardened against them. The Blue Team suggests that IT implement the fixes below to protect the network:

- Vulnerability 1 - Excessive HTTP errors
  - **Patch**: Require a strong password policy in the user account settings, and update to use a different password for every account. 
  - **Why It Works**: In fact, around 90% of user-generated passwords are considered weak and easily vulnerable to hacking. The users are forced to create stronger passwords and avoid those that can be easily guessed.


- Vulnerability 2 - HTTP Request Size Monitor
  - **Patch**: Use intrucsion prevention and threat management system, use firewalls, VPN access, anti-spam, load balancing, LAN-scanning, Postman's proxy inspect HTTP in responses with a content-type, 
  - **Why It Works**: Implement strong access control checks, Authentication and authorization policies should be role-based, and Restrict access to unwanted URLs.

- Vulnerability 3 - CPU Usage Monitor
  - **Patch**: Host Instrucion Prevention System to Identify DOS Attack.
  - **Why It Works**: 
       - Block Malware and Malicious code by Monitoring the behavior of the code.

       - Attempts to disrupt service to a specific system or person, e.g., blocking user access by repeated

       - Attempts to "flood" web applications, thereby preventing legitimate user traffic
