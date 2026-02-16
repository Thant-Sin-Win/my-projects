# SIEM-SOAR Honeypot Lab

## Project Summary

This project was developed to simulate real-world Remote Desktop
Protocol (RDP) brute-force attacks against an internet-exposed Windows
virtual machine deployed in Microsoft Azure. The virtual machine was
intentionally configured as a honeypot in order to attract unauthorised
authentication attempts from external sources.

Microsoft Sentinel was used to monitor incoming security logs and detect
repeated failed login attempts originating from external IP addresses.
Upon detection of suspicious activity, an automated containment response
was initiated through an Azure Logic App playbook.

The playbook extracts the attacker's source IP address from the incident
context and dynamically creates an inbound deny rule within the
associated Network Security Group (NSG). This prevents further RDP
access from the identified source address.

This project demonstrates a basic end-to-end SIEM and SOAR workflow for
threat detection and automated network-level response within a cloud
environment.

------------------------------------------------------------------------

## Project Objectives

-   Detect brute-force authentication attempts against an
    internet-facing Windows VM
-   Generate incidents within Microsoft Sentinel
-   Enrich incidents with attacker IP information
-   Automatically initiate containment actions upon detection
-   Dynamically create NSG rules to block attacker IP addresses
-   Demonstrate automated response using Azure Logic Apps

------------------------------------------------------------------------

## Current Implementation Status

Completed:

-   Deployment of internet-facing Windows virtual machine
-   Forwarding of Windows Security Event logs to Log Analytics Workspace
-   Enabling Microsoft Sentinel for monitoring
-   Creation of analytic rule for failed login detection (Event ID 4625)
-   Creation of analytic rule for successful login after multiple failed attempts (Event ID 4624)
-   Automatic incident generation within Sentinel
-   Creation of automation rule to trigger playbook
-   Development of Logic App playbook
-   Extraction of attacker IP address from incident
-   REST API call to Azure NSG using Managed Identity
-   Assignment of Network Contributor role to Logic App
-   Dynamic creation of inbound deny rule for TCP 3389
-   Verification of playbook execution
-   Confirmation of deny rule creation in NSG
-   Blocking of subsequent RDP attempts from attacker IP

Not Implemented:

-   Workbook-based geo-visualisation of attacker IPs (Configuration attempt unsuccessful due to mapping limitations)

------------------------------------------------------------------------

## Detection Logic

The following query was used to detect repeated failed login attempts:

SecurityEvent \| where EventID == 4625 \| summarize FailedAttempts =
count() by IpAddress, Account, bin(TimeGenerated, 5m) \| where
FailedAttempts \>= 5

------------------------------------------------------------------------

## SOAR Workflow

1.  External host performs repeated RDP login attempts
2.  Windows Security Logs record failed login events
3.  Sentinel analytic rule detects suspicious activity
4.  Incident is generated within Microsoft Sentinel
5.  Automation Rule triggers response playbook
6.  Playbook extracts attacker IP address
7.  REST API call is made to Azure NSG
8.  Inbound deny rule is created for TCP port 3389
9.  Further RDP attempts from the same IP are blocked

------------------------------------------------------------------------

## Engineering Challenges Encountered

-   Incident triggered before IP entity was available\
    Resolved by adding a delay after incident trigger

-   HTTP 403 error from Azure Management API\
    Resolved by assigning Network Contributor role to Logic App identity

-   NSG rule not visible despite successful response\
    Resolved by correcting resource group path in REST API URI

-   Priority conflict during rule creation\
    Resolved by implementing dynamic priority assignment

------------------------------------------------------------------------

## Scope and Limitations

Detection of successful authentication following multiple failed login attempts has been implemented using correlation of Security Event IDs 4624 and 4625, as demonstrated in Figure 4 and Figure 5.

However, automated containment for this compromise scenario has not yet been integrated into the current SOAR playbook workflow. At present, automated response actions are triggered based on threshold-based detection of repeated failed authentication attempts.

Future development will extend automation capabilities to include dynamic containment upon detection of successful authentication following multiple failed login attempts.

------------------------------------------------------------------------

## Next Steps

- Integrate automated containment for successful login following multiple failed authentication attempts
- Extend playbook trigger conditions to include compromise-based detections
- Implement attacker IP geo-visualisation using Sentinel Workbooks
- Harden test access controls to avoid account lockout during simulation

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

**Figure 10 -- RDP Access Blocked After Automated Containment Action** ![Incident
Timeline](Screenshots/10_Failed_RDP.png)

------------------------------------------------------------------------

For implementation details, please refer to:

TECHNICAL_DETAILS.md
