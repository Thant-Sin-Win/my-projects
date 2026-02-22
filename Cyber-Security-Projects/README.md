# Cyber Security SOC Readiness Portfolio

## Overview

This Folder contains practical security monitoring and incident response work completed as part of my transition into cyber security. It includes a Microsoft Sentinel SIEM honeypot project used to detect and respond to simulated brute force login attempts, along with supporting cybersecurity certifications and structured SOC related training completed through TryHackMe.

I completed the Certificate IV in Cyber Security in January 2026 and have undertaken additional hands on lab based learning focused on security operations, threat detection and incident response workflows. This portfolio is intended to demonstrate practical familiarity with SIEM monitoring, security event analysis and automated response in a controlled cloud environment.

---

## SIEM Honeypot Project

A cloud based honeypot environment was deployed within Microsoft Azure to simulate an exposed Remote Desktop Protocol attack surface and capture unauthorised login attempts.

Microsoft Sentinel was integrated to collect and monitor Windows Security Event Logs from the virtual machine. Failed login attempts were analysed to identify potential brute force patterns using Kusto Query Language queries.

Custom analytics rules were created to generate alerts based on suspicious authentication activity. Automated response was implemented using Azure Logic Apps to update Network Security Group rules and block malicious IP addresses following repeated failed login attempts.

Inbound login attempts from multiple global sources were monitored to simulate SOC style incident detection and response workflows.

Project screenshots and related documentation are available in the SIEM_Honeypot_Project folder.

---

## Certifications

Supporting certifications demonstrating foundational knowledge in cyber security, cloud platforms, scripting and data analysis are included in the Certifications folder.

These include:

- Certificate IV in Cyber Security  
- AWS Certified Cloud Practitioner  
- Certified IT Specialist Python  
- Programming and Software Development La Trobe University  
- Microsoft Certified Power BI Data Analyst Associate  
- IBM Data Analyst Professional Certificate  

---

## TryHackMe Practical Training

Structured hands on training was completed through TryHackMe with a focus on SOC relevant concepts and workflows.

Completed learning paths include:

- Network Fundamentals  
- Web Fundamentals  
- Security Operations  
- Penetration Testing  
- SOC Analyst  

Completion certificates for each pathway are included in the TryHackMe folder.

---

## Tools and Technologies

The following tools and platforms were used across project and lab based activities:

- Microsoft Sentinel  
- Microsoft Azure  
- Log Analytics Workspace  
- Azure Logic Apps  
- Network Security Groups  
- Windows Security Event Logs  
- Kusto Query Language  
- Nmap  
- Wireshark  
- Metasploit  
- Hydra  
- Burp Suite  

---

## Purpose

This folder serves as a record of practical cybersecurity learning activities undertaken to build foundational skills in security monitoring, incident detection and response within a Security Operations Centre environment.
