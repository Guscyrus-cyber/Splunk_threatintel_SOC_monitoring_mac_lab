**Threat Intelligence SOC Monitoring Lab**

**Lab Goal**

The goal of this lab is to ingest threat intelligence data into Splunk Enterprise and identify known malicious IP addresses, suspicious domains, threat indicators, and potential security threats through dashboards, reports, alerts, detections, lookups, and threat-hunting investigations.

**Creating Threat Intelligence Index**

Description: Create a dedicated Splunk index to store threat intelligence indicators and threat-hunting data.

**Upload Threat Intelligence Dataset**

Dataset: threatintel.log

Index: threatintel

Description: Ingest threat intelligence indicators for monitoring and threat detection activities.


**Verifying Ingestion and Indicators**

Query: index=threatintel

. Was the threat intelligence dataset successfully ingested into Splunk? Yes\
\
. How many threat intelligence indicators exist in the dataset? 10 indicators

| **threat_type**  | **indicator**         | **severity**  |
|------------------|-----------------------|---------------|
| Malicious_IP     | 123.123.123.123       | High          |
| Malicious_IP     | 45.33.32.156          | Critical      |
| Malicious_Domain | maliciousdomain.com   | High          |
| Malicious_Domain | evil-c2.net           | Critical      |
| Threat_Actor     | APT-Shadow            | High          |
| Phishing         | fakebank-login.com    | High          |
| Botnet           | botnet-controller.net | Critical      |
| Malware_Hash     | ABC123XYZ             | High          |
| Benign_IP        | 8.8.8.8               | Informational |
| Benign_Domain    | github.com            | Informational |

The threat intelligence dataset was successfully ingested into Splunk Enterprise with 10 events. Splunk automatically extracted key fields including indicator, threat_type, severity, and description. The dataset contains malicious IP addresses, malicious domains, phishing indicators, botnet infrastructure, a malware hash, a simulated threat actor, and benign indicators for comparison. The results confirm that the threat intelligence feed is searchable and ready for IOC monitoring, alerting, detection rules, dashboards, reports, and threat-hunting analysis.\
The presence of benign indicators such as 8.8.8.8 and github.com provides comparison data, while high-risk indicators such as evil-c2.net, 45.33.32.156, botnet-controller.net, and maliciousdomain.com represent simulated threats for detection and investigation practice.


**Verifying Event Count**

Query:\
\
index=threatintel\
\| stats count

. How many threat intelligence events were ingested into Splunk? 10

**Review Threat Intelligence Data**

Query:

index=threatintel\
\| table \_time host sourcetype \_raw

. What threat indicators are present in the environment?

The threat intelligence dataset contains a mixture of malicious and benign indicators. The malicious indicators include two malicious IP addresses (123.123.123.123, 45.33.32.156), two malicious domains (maliciousdomain.com, evil-c2.net), one phishing domain (fakebank-login.com), one botnet controller (botnet-controller.net), one malware hash (ABC123XYZ), and one threat actor identifier (APT-Shadow). The dataset also includes two benign indicators (8.8.8.8 and github.com) for comparison and validation purposes.\
\
. Which indicators are available for investigation?\
\
The following indicators are available for investigation:

| **Threat Type**  | **Indicator**         | **Severity**  |
|------------------|-----------------------|---------------|
| Malicious_IP     | 123.123.123.123       | High          |
| Malicious_IP     | 45.33.32.156          | Critical      |
| Malicious_Domain | maliciousdomain.com   | High          |
| Malicious_Domain | evil-c2.net           | Critical      |
| Threat_Actor     | APT-Shadow            | High          |
| Phishing         | fakebank-login.com    | High          |
| Botnet           | botnet-controller.net | Critical      |
| Malware_Hash     | ABC123XYZ             | High          |
| Benign_IP        | 8.8.8.8               | Informational |
| Benign_Domain    | github.com            | Informational |

These indicators can be investigated to determine whether any systems have communicated with known malicious infrastructure, accessed suspicious domains, been associated with threat actor activity, or exhibited indicators of malware infection. The benign indicators provide a baseline for distinguishing legitimate activity from potentially malicious activity.

**Identifying Malicious IP Addresses**

Query:

index=threatintel\
malicious

. Which source IP addresses are identified as known malicious indicators?

123.123.123.123\
45.33.32.156\
\
. Which IP addresses should be prioritized for investigation?\
\
Priority Order:

45.33.32.156 — Critical (Botnet Infrastructure)\
123.123.123.123 — High (Known Command and Control Server)

**Searching for Suspicious Domains**

index=threatintel

domain


. Which domains have been identified as suspicious or malicious?

evil-c2.net\
maliciousdomain.com\
\
. Are known malicious domains present in the threat intelligence feed?

1\. Command-and-Control (C2) infrastructure\
2. Malware distribution activity

These two malicious domains and should be prioritized for investigation.

**Identify High-Risk Threats**

Query:

index=threatintel\
high

. Which indicators are classified as high-risk threats?

The following indicators are classified with **High severity** and are considered high-risk threats:

| **Threat Type**  | **Indicator**       | **Description**                  |
|------------------|---------------------|----------------------------------|
| Malware_Hash     | ABC123XYZ           | Ransomware Sample                |
| Phishing         | fakebank-login.com  | Credential Harvesting Site       |
| Threat_Actor     | APT-Shadow          | Threat Actor Infrastructure      |
| Malicious_Domain | maliciousdomain.com | Malware Distribution Domain      |
| Malicious_IP     | 123.123.123.123     | Known Command and Control Server |

. Which threat indicators require immediate analyst attention? \|\
The indicators required immediate analyst attention because they are associated with ransomware activity, phishing infrastructure, threat actor infrastructure, malware distribution, and command-and-control communication\
\
ABC123XYZ\
fakebank-login.com\
APT-Shadow\
maliciousdomain.com\
123.123.123.123

The investigation identified five high-severity threat indicators. These indicators represent malware, phishing infrastructure, threat actor activity, malicious domains, and command-and-control infrastructure. Any occurrence of these indicators within DNS logs, firewall logs, TLS traffic, endpoint logs, or threat intelligence matches should be prioritized for investigation and potential incident response.**\
\
**Search for Known Attackers**

Query:

index=threatintel threat_type=Threat_Actor

. Which indicators are associated with known threat actor?

“APT-Shadow” associated with known threat actor.\
\
. Which threat actors have been observed in the dataset?\
\
“APT-Shadow” was the only threat actor identified in the threat intelligence dataset and is classified as **High severity**.


**Visualization and panel**

Query:


. How many threat intelligence indicators are currently being monitored?\

A total of 10 threat intelligence indicators are currently being monitored. The indicators include malicious IP addresses, malicious domains, phishing infrastructure, botnet infrastructure, a malware hash, a threat actor identifier, and benign indicators used for comparison.

. What is the total volume of threat intelligence events?\
The threat intelligence dataset contains 10 events.


**Report**

. What threat indicators were identified during the investigation?

. Which indicators should be documented for future monitoring?

Query:

index=threatintel

**Dashboard**

Query:

index=threatintel\
\| stats count

\
\
. What threat intelligence indicators are currently available for monitoring?\
\
The threat intelligence dataset contains 10 indicators available for monitoring, including malicious IP addresses, malicious domains, phishing infrastructure, botnet infrastructure, a malware hash, a threat actor identifier, and benign reference indicators. These indicators can be used for detection, alerting, IOC matching, and threat-hunting investigations.

. What is the current threat landscape represented in the dataset?\
\
The current threat landscape includes command-and-control infrastructure, malware distribution domains, phishing activity, botnet infrastructure, ransomware indicators, and threat actor infrastructure. The dataset contains both high-risk and critical-severity indicators, along with benign indicators used to distinguish legitimate activity from potentially malicious activity.


**Alert**

Query:

index=threatintel\
malicious


. Has a known malicious indicator been detected?\

Yes. The alert identified the following known malicious indicators:

123.123.123.123\
45.33.32.156\
maliciousdomain.com\
evil-c2.net

These indicators are associated with command-and-control infrastructure, botnet activity, and malware distribution\

. Are there threat indicators requiring analyst notification?\

Yes. Several threat indicators require analyst notification and monitoring, including:

123.123.123.123 (Known Command and Control Server)\
45.33.32.156 (Botnet Infrastructure)\
maliciousdomain.com (Malware Distribution Domain)\
evil-c2.net (Known C2 Domain)\
\
The alert successfully identified known malicious indicators within the threat intelligence feed. These indicators are associated with high-risk and critical threats and should trigger analyst review, investigation, and continued monitoring for potential matches within network, DNS, firewall, TLS, and endpoint telemetry.

**Detection Rule**

Query:

index=threatintel\
\| search malicious OR attacker OR suspicious

Detection Name: Threat Intelligence Detection

. Can known malicious indicators be automatically detected?\
\
Yes. The threat intelligence dataset contains known malicious indicators that can be automatically detected through Splunk searches, alerts, detection rules, and IOC matching. Examples include malicious IP addresses, malicious domains, botnet infrastructure, phishing domains, and threat actor indicators.

Are any threat intelligence matches present in the environment?\
\
Yes. The dataset contains multiple threat intelligence matches, including:\
\
123.123.123.123 (Known Command and Control Server)

45.33.32.156 (Botnet Infrastructure)

maliciousdomain.com (Malware Distribution Domain)

evil-c2.net (Known C2 Domain)

fakebank-login.com (Phishing Domain)

botnet-controller.net (Botnet Controller)

APT-Shadow (Threat Actor Infrastructure)

ABC123XYZ (Ransomware Sample)\
\
The detection rule successfully identified multiple high-risk and critical indicators within the threat intelligence feed. These indicators represent command-and-control infrastructure, malware distribution activity, phishing infrastructure, botnet activity, ransomware indicators, and threat actor infrastructure, all of which should be prioritized for monitoring and investigation.


**Threat Hunting**

Which indicators represent the highest risk to the environment?

Are there any known malicious IP addresses or domains requiring further investigation?

Which indicators should be escalated for incident response?

What threat intelligence findings could indicate compromise activity?

Query:

index=threatintel\
\| table \_time host sourcetype \_raw

. Which indicators represent the highest risk to the environment?

The highest-risk indicators are:

45.33.32.156 (Critical - Botnet Infrastructure)\
evil-c2.net (Critical - Known C2 Domain)\
botnet-controller.net (Critical - Botnet Controller)\
\
These indicators have a **Critical severity** rating and should be prioritized for immediate investigation.

Are there any known malicious IP addresses or domains requiring further investigation?

Yes. The following malicious indicators require further investigation:

123.123.123.123\
45.33.32.156\
maliciousdomain.com\
evil-c2.net\
fakebank-login.com\
botnet-controller.net

These indicators are associated with command-and-control activity, malware distribution, phishing infrastructure, and botnet operations.\

. Which indicators should be escalated for incident response?\
\
The indicators that should be escalated are:

45.33.32.156\
evil-c2.net\
botnet-controller.net\
ABC123XYZ

because they are associated with botnet infrastructure, command-and-control communications, and ransomware activity.

What threat intelligence findings could indicate compromise activity?

The following findings could indicate compromise activity if observed in network, DNS, firewall, TLS, or endpoint logs:

123.123.123.123 (Known Command and Control Server)\
45.33.32.156 (Botnet Infrastructure)\
maliciousdomain.com (Malware Distribution Domain)\
evil-c2.net (Known C2 Domain)\
fakebank-login.com (Credential Harvesting Site)\
botnet-controller.net (Botnet Controller)\
ABC123XYZ (Ransomware Sample)\
APT-Shadow (Threat Actor Infrastructure)

**Analyst Assessment**

Threat-hunting analysis identified multiple high-risk and critical threat indicators associated with command-and-control infrastructure, malware distribution, phishing activity, botnet operations, ransomware, and threat actor infrastructure. Any occurrence of these indicators within operational logs should be treated as a potential security incident and investigated immediately.






