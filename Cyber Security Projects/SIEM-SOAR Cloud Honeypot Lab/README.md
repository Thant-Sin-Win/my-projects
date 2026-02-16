# SIEM-SOAR Honeypot Lab

## Automated Detection and Containment of RDP Brute-Force Attacks using Microsoft Sentinel

### Project Summary

This project implements an internet-exposed Windows virtual machine as a
controlled honeypot to simulate real-world brute-force activity against
Remote Desktop Protocol (RDP). Microsoft Sentinel is used to detect
repeated failed authentication attempts from external IP addresses and
to automatically initiate a containment response through an Azure Logic
App playbook.

The response workflow extracts the attacker's source IP address from the
incident context and programmatically creates an inbound deny rule in
the associated Network Security Group (NSG), blocking further RDP access
from that address.

This repository documents the current implementation status and serves
as an ongoing work-in-progress as additional correlation and automation
logic are developed.

------------------------------------------------------------------------

### Project Objectives

-   Detect brute-force authentication attempts against an
    internet-facing Windows VM\
-   Generate actionable incidents in Microsoft Sentinel\
-   Enrich incidents with attacker IP entities\
-   Automatically initiate a containment response upon incident
    creation\
-   Dynamically create NSG rules to block attacker IPs at the network
    layer\
-   Demonstrate an end-to-end SOAR workflow within Azure

------------------------------------------------------------------------

### Current Implementation Status

  -----------------------------------------------------------------------
  Capability                                Status
  ----------------------------------------- -----------------------------
  Deploy Windows VM as internet-facing      Completed
  honeypot (RDP exposed)                    

  Forward Windows SecurityEvent logs to Log Completed
  Analytics                                 

  Enable Microsoft Sentinel on workspace    Completed

  Create analytic rule for repeated failed  Completed
  logons (EventID 4625)                     

  Automatic incident generation in Sentinel Completed

  Create Automation Rule (Run playbook on   Completed
  incident creation)                        

  Develop Logic App playbook                Completed
  (incident-triggered)                      

  Extract attacker IP from                  Completed
  Incident.relatedEntities                  

  Call Azure Management API via HTTP        Completed
  (Managed Identity)                        

  Assign Network Contributor role to Logic  Completed
  App Identity                              

  Dynamically create NSG inbound deny rule  Completed
  (TCP 3389)                                

  Verify playbook run (HTTP 2xx response)   Completed

  Confirm deny rule creation in NSG         Completed

  Block subsequent RDP attempts from        In Progress
  attacker IP                               

  Detect successful login after multiple    Not Implemented
  failures                                  

  Workbook map for attacker                 Not Implemented
  geo-visualisation                         
  -----------------------------------------------------------------------

------------------------------------------------------------------------

### Detection Logic (KQL)

    SecurityEvent
    | where EventID == 4625
    | summarize FailedAttempts = count()
        by IpAddress, Account, bin(TimeGenerated, 5m)
    | where FailedAttempts >= 5

------------------------------------------------------------------------

### SOAR Workflow

1.  External host performs repeated RDP authentication attempts\
2.  Windows Security Logs record failed logons (EventID 4625)\
3.  Sentinel analytic rule detects suspicious activity\
4.  Incident is created in Microsoft Sentinel\
5.  Automation Rule triggers the response playbook\
6.  Logic App extracts attacker IP from incident context\
7.  Playbook issues REST API call to Azure NSG\
8.  NSG inbound deny rule is created for TCP 3389\
9.  Subsequent RDP attempts from the same IP are blocked

------------------------------------------------------------------------

### Engineering Challenges Encountered

  -----------------------------------------------------------------------
  Issue           Observation                  Resolution
  --------------- ---------------------------- --------------------------
  Incident        Entity extraction returned   Delay added after incident
  triggered       empty list                   trigger
  before IP                                    
  entity was                                   
  available                                    

  HTTP 403 from   Playbook identity lacked     Assigned Network
  ARM API         permissions                  Contributor role

  NSG rule not    Incorrect resource group in  Updated NSG resource path
  visible despite REST URI                     
  success                                      
  response                                     

  Priority        Static priority overlapped   Implemented dynamic
  conflict on     existing rule                priority
  rule creation                                
  -----------------------------------------------------------------------

------------------------------------------------------------------------

### Evidence

The following screenshots are included in the /Screenshots directory:

-   Figure 1: Public RDP exposure in NSG\
-   Figure 2: Sentinel Analytic Rule Configuration\
-   Figure 3: Generated Incident in Microsoft Sentinel\
-   Figure 4: Automation Rule (Playbook Trigger)\
-   Figure 5: Logic App Run History (HTTP Action)\
-   Figure 6: NSG Inbound Deny Rule Created

------------------------------------------------------------------------

### Scope and Limitations

Detection of successful authentication following multiple failed
attempts requires multi-event correlation across SecurityEvent 4624 and
4625 and has not yet been automated within the current playbook
workflow.

Further work will focus on extending the analytic logic and automation
conditions to address this scenario.

------------------------------------------------------------------------

### Next Steps

-   Implement correlation rule for successful login after multiple
    failures\
-   Extend playbook trigger conditions to cover additional incident
    types\
-   Revisit workbook geo-visualisation for attacker IP mapping\
-   Harden test access controls to avoid account lockout during
    simulation

------------------------------------------------------------------------

### Technical Implementation

For implementation details, refer to:

TECHNICAL_DETAILS.md
