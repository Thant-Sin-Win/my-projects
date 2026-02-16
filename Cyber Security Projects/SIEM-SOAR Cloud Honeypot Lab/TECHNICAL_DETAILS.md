# Technical Implementation Details

## Environment Configuration

The lab environment was implemented in Microsoft Azure using:

-   Azure Virtual Machine (Internet-facing Windows Server)
-   Network Security Group (Inbound RDP control on TCP 3389)
-   Log Analytics Workspace
-   Microsoft Sentinel
-   Automation Rule
-   Azure Logic App

RDP (TCP 3389) was intentionally exposed to simulate brute-force login
attempts.

------------------------------------------------------------------------

## Log Collection

Windows Security Logs were forwarded to the Log Analytics Workspace
using the Azure Monitoring Agent.

Relevant events:

-   Event ID 4625 -- Failed Login Attempt
-   Event ID 4624 -- Successful Login

------------------------------------------------------------------------

## Analytic Rule

SecurityEvent \| where EventID == 4625 \| summarize FailedAttempts =
count() by IpAddress, Account, bin(TimeGenerated, 5m) \| where
FailedAttempts \>= 5

------------------------------------------------------------------------

## Automation Rule

Trigger: Incident created

Condition: Analytic rule name contains "Brute Force Attack Detected"

Action: Run Playbook -- Auto-Block-BruteForce-Attacker-IP

------------------------------------------------------------------------

## Playbook Workflow

-   Microsoft Sentinel Incident Trigger
-   Delay (1 minute)
-   Iterate through Incident relatedEntities
-   Condition check for IP entity
-   HTTP action to Azure NSG REST API

------------------------------------------------------------------------

## Evidence

### Detection

**Figure 3 -- Security Event Logs** ![Security
Logs](Screenshots/03_security_event_logs.png)

**Figure 5 -- Generated Incident** ![Incident
Generated](Screenshots/05_incident_generated.png)

------------------------------------------------------------------------

### Automation

**Figure 7 -- Logic App Run History** ![Playbook
Run](Screenshots/07_playbook_run.png)

**Figure 8 -- HTTP Action Success** ![HTTP
Success](Screenshots/08_http_success.png)

------------------------------------------------------------------------

### Containment

**Figure 9 -- NSG Deny Rule Created** ![NSG Deny
Rule](Screenshots/09_nsg_deny_rule.png)

------------------------------------------------------------------------

## Implementation Challenges

-   Entity extraction returned empty list due to enrichment delay\
    Resolved by adding delay after trigger

-   HTTP 403 error due to missing RBAC permission\
    Resolved by assigning Network Contributor role

-   NSG rule not appearing due to incorrect resource group path\
    Resolved by updating REST API URI

-   Duplicate priority value during rule creation\
    Resolved by implementing dynamic priority logic

------------------------------------------------------------------------

## Current Limitations

Correlation-based detection of successful login following multiple
failed attempts requires multi-event logic and has not yet been
implemented.
