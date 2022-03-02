# Blue Team: Summary of Operations

## Table of Contents
- Network Topology
- Description of Targets
- Monitoring the Targets
- Patterns of Traffic & Behavior
- Suggestions for Going Further

### Network Topology

The following machines were identified on the network:
- ML-REFVM-684427
  - Windows
  - Environment Host
  - 192.168.1.1
- Kali
  - Linux
  - Pentest Machine
  - 192.168.1.90
- ELK
  - Linux
  - ELK Stack Server
  - 192.168.1.100
- Target1
  - Linux 
  - Vulnerable web server
  - 192.168.1.110

### Description of Targets

The target of this attack was: `Target 1` (192.168.1.110)

Target 1 is an Apache web server and has SSH enabled, so ports 80 and 22 are possible ports of entry for attackers. As such, the following alerts have been implemented:

### Monitoring the Targets

Traffic to these services should be carefully monitored. To this end, we have implemented the alerts below:

#### Name of Alert 1

Alert 1 is implemented as follows:
  - **Metric**: Excessive HTTP Errors
  - **Threshold**: When the http response code is over 400 for more than 5 mintues
  - **Vulnerability Mitigated**: Availability 
  - **Reliability**: High

#### Name of Alert 2
Alert 2 is implemented as follows:
  - **Metric**: HTTP Request Size 
  - **Threshold**: When total bytes of http requests are above 3500 for last minute
  - **Vulnerability Mitigated**: DDOS attack
  - **Reliability**: Medium

#### Name of Alert 3
Alert 3 is implemented as follows:
  - **Metric**: CPU Usage Monitor
  - **Threshold**: CPU process total percentage is above 0.5 for last 5 mintues
  - **Vulnerability Mitigated**: DDOS attack
  - **Reliability**: Low

