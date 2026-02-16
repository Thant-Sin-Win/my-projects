# SIEM-SOAR Honeypot Lab

## Project Summary

This project simulates real-world Remote Desktop Protocol (RDP)
brute-force attacks against an internet-exposed Windows virtual machine
deployed in Microsoft Azure.

Microsoft Sentinel was used to monitor incoming security logs and detect
repeated failed login attempts from external IP addresses. Upon
detection of suspicious activity, an automated containment response was
initiated through an Azure Logic App playbook.

The playbook extracts the attacker's source IP address from the incident
and dynamically creates an inbound deny rule within the associated
Network Security Group (NSG), preventing further RDP access from the
identified source address.

This project demonstrates an end-to-end SIEM and SOAR workflow for
threat detection and automated network-level response.

------------------------------------------------------------------------

## Detection Logic

SecurityEvent \| where EventID == 4625 \| summarize FailedAttempts =
count() by IpAddress, Account, bin(TimeGenerated, 5m) \| where
FailedAttempts \>= 5

------------------------------------------------------------------------

## SOAR Workflow

1.  External host performs repeated RDP login attempts\
2.  Windows Security Logs record failed login events\
3.  Sentinel analytic rule detects suspicious activity\
4.  Incident is generated within Microsoft Sentinel\
5.  Automation Rule triggers response playbook\
6.  Playbook extracts attacker IP address\
7.  REST API call is made to Azure NSG\
8.  Inbound deny rule is created for TCP port 3389\
9.  Further RDP attempts from the same IP are blocked

------------------------------------------------------------------------

## Evidence

### Phase 1 -- Exposure

**Figure 1 -- Public RDP Exposure in NSG** ![NSG RDP
Exposure](Screenshots/01_nsg_rdp_exposed.png)

**Figure 2 -- VM Public IP Configuration** ![VM Public
IP](Screenshots/02_vm_public_ip.png)

------------------------------------------------------------------------

### Phase 2 -- Detection

**Figure 3 -- Security Event Logs Ingested** ![Security
Logs](Screenshots/03_security_event_logs.png)

**Figure 4 -- Analytic Rule Configuration** ![Analytic
Rule](Screenshots/04_analytic_rule.png)

**Figure 5 -- Incident Generated in Sentinel** ![Incident
Generated](Screenshots/05_incident_generated.png)

------------------------------------------------------------------------

### Phase 3 -- Automation

**Figure 6 -- Automation Rule** ![Automation
Rule](Screenshots/06_automation_rule.png)

**Figure 7 -- Logic App Run History** ![Playbook
Run](Screenshots/07_playbook_run.png)

**Figure 8 -- HTTP Action Success Response** ![HTTP
Success](Screenshots/08_http_success.png)

------------------------------------------------------------------------

### Phase 4 -- Containment

**Figure 9 -- NSG Deny Rule Created** ![NSG Deny
Rule](Screenshots/09_nsg_deny_rule.png)

**Figure 10 -- Incident Timeline Updated** ![Incident
Timeline](Screenshots/10_incident_timeline.png)

------------------------------------------------------------------------

For implementation details, please refer to:

TECHNICAL_DETAILS.md
