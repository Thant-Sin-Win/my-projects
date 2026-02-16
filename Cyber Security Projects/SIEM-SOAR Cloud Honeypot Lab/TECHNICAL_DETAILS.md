# Technical Implementation Details

## Environment Configuration

The lab environment was implemented in Microsoft Azure using the
following components:

-   Azure Virtual Machine (Internet-facing Windows Server)
-   Network Security Group (Inbound RDP control on TCP 3389)
-   Log Analytics Workspace (Centralised log collection)
-   Microsoft Sentinel (SIEM platform)
-   Automation Rule (Playbook trigger)
-   Azure Logic App (SOAR response playbook)

RDP (TCP 3389) was intentionally exposed to the public internet to
simulate brute-force login attempts.

------------------------------------------------------------------------

## Log Collection

Windows Security Logs were forwarded to the Log Analytics Workspace
using the Azure Monitoring Agent.

Relevant events collected:

-   Event ID 4625 -- Failed Login Attempt
-   Event ID 4624 -- Successful Login

------------------------------------------------------------------------

## Analytic Rule Configuration

A scheduled analytics rule was created in Microsoft Sentinel to detect
repeated failed authentication attempts using the following query:

SecurityEvent \| where EventID == 4625 \| summarize FailedAttempts =
count() by IpAddress, Account, bin(TimeGenerated, 5m) \| where
FailedAttempts \>= 5

Alert grouping was enabled to generate incidents upon detection.

------------------------------------------------------------------------

## Automation Rule

An automation rule was configured with the following settings:

Trigger: When incident is created

Condition: Analytic rule name contains "Brute Force Attack Detected"

Action: Run Playbook -- Auto-Block-BruteForce-Attacker-IP

------------------------------------------------------------------------

## Playbook Design

The Logic App playbook was configured with an incident-triggered
workflow consisting of:

-   Microsoft Sentinel Incident Trigger
-   Delay (1 minute)
-   Iteration through Incident relatedEntities
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

## Implementation Challenges

-   Entity extraction returned an empty list due to enrichment delay\
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

Future work will include:

-   Detection using Event ID 4624 following repeated 4625 events
-   Additional automation conditions
-   Workbook-based attacker IP geo-visualisation
