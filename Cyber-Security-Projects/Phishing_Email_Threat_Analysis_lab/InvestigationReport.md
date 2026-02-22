# Phishing Email Investigation Report

## Executive Summary

On 18 February 2026, a suspicious email was reported by an employee to the IT Security Team for investigation. The email claimed to originate from the Enterprise IT Support Team and instructed the recipient to reset their corporate password through an embedded hyperlink.

An investigation was conducted to determine the legitimacy of the email and identify any Indicators of Compromise (IOCs). Based on the findings, the email was assessed to be a credential harvesting phishing attempt with a Medium severity risk level due to the potential impact on enterprise account security.

---

## Incident Description

The reported email warned the recipient of suspicious login attempts on their corporate account and advised immediate password reset through a provided external link. The sender email address, `it-support@company-securemail.com`, impersonated an internal IT support function, which is a common social engineering technique used in phishing campaigns.

The email also contained urgency-based messaging, stating that failure to comply within 12 hours would result in permanent account suspension.

---

## Investigation Findings

Email header analysis was conducted using MXToolbox to identify the sending server and originating IP address. The header indicated that the email originated from the domain `example.com` with the sending IP address `93.184.216.34`.

IP reputation analysis was performed using VirusTotal, and domain registration details were obtained through a Whois lookup.

URL analysis of the embedded hyperlink (`https://example.com/reset-password`) was attempted using URLScan. The scan was prevented by platform restrictions likely due to domain protection policies applied to reserved or high-reputation domains. This limitation was documented as part of the investigation.

Multiple phishing indicators were identified, including suspicious sender impersonation and urgency-driven language intended to induce user action.

---

## Indicators of Compromise (IOCs)

The following IOCs were identified during the investigation:

- Sending IP Address: 93.184.216.34  
- Domain: example.com  
- Suspicious URL: https://example.com/reset-password  
- Sender Email Address: it-support@company-securemail.com  
- Email Subject: Urgent Password Reset Required  

---

## Threat Severity Assessment

The reported email was assessed as a Medium severity phishing incident. The email exhibited characteristics consistent with credential harvesting attempts, including the request for password reset via an external link and the use of urgency-based messaging.

Although no confirmed compromise has been reported at this stage, successful execution of this phishing attempt could result in unauthorized access to corporate systems, account takeover, data exfiltration, and potential lateral movement within the enterprise network.

---

## Recommended Mitigation Actions

1. Block the domain `example.com` at the enterprise web proxy or firewall level.  
2. Block the sender email address `it-support@company-securemail.com`.  
3. Advise affected users not to click on the provided link or disclose corporate credentials.  
4. Initiate organisation-wide phishing awareness reminders if required.  

---

## Conclusion

The investigation determined that the reported email represents a phishing attempt aimed at harvesting corporate user credentials. Prompt reporting by the employee enabled timely analysis and mitigation recommendations to prevent potential compromise.

Continuous user awareness training and proactive email monitoring are recommended to reduce the likelihood of similar phishing incidents impacting enterprise security in the future.
