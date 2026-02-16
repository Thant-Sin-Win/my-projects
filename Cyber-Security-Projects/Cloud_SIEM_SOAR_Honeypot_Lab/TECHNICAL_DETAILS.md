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

**Brute Force Attack Detected**

SecurityEvent \| where EventID == 4625 \| summarize FailedAttempts =
count() by IpAddress, Account, bin(TimeGenerated, 5m) \| where
FailedAttempts \>= 5  
<br><br>
**Successful Login After Multiple Failures**

let window = 15m;
let threshold = 5;
let failures = SecurityEvent
| where EventID == 4625
| where IpAddress != "-" and isnotempty(IpAddress)
| extend Ip=tostring(IpAddress), UserName=tostring(TargetUserName)
| project FailureTime=TimeGenerated, Ip, UserName;
let successes = SecurityEvent
| where EventID == 4624
| where IpAddress != "-" and isnotempty(IpAddress)
| extend Ip=tostring(IpAddress), UserName=tostring(TargetUserName)
| project SuccessTime=TimeGenerated, Ip, UserName;
successes
| join kind=inner failures on Ip, UserName
| where FailureTime between (SuccessTime - window .. SuccessTime)
| summarize FailedCount=count() by SuccessTime, Ip, UserName
| where FailedCount >= threshold
| project SuccessTime, IpAddress=Ip, User=UserName, FailedCount
| order by SuccessTime desc

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

## Entity Extraction

Initial implementation using the default IP extraction method returned
an empty result due to the playbook executing prior to incident
enrichment.

This was resolved by:

-   Adding a delay after the incident trigger
-   Iterating through the relatedEntities field directly

------------------------------------------------------------------------

## NSG Rule Creation

Azure Management REST API was used to dynamically create inbound deny
rules to block attacker IP addresses from accessing TCP port 3389.

Authentication was handled using the Logic App system-assigned Managed
Identity with Network Contributor role assigned at the Network Security
Group resource level.

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

Correlation-based detection of successful login following multiple failed authentication attempts has been implemented through the use of Security Event IDs 4625 and 4624.

However, automated containment for this compromise scenario has not yet been integrated into the current SOAR playbook workflow. At present, automated response actions are triggered based on threshold-based detection of repeated failed authentication attempts.

Future work will include:

- Integration of automated containment for successful authentication following multiple failed login attempts
- Additional automation conditions for compromise-based detections
- Workbook-based attacker IP geo-visualisation (configuration unsuccessful due to mapping limitations)
