# Building a SOC + Honeynet in Azure (Live Traffic)
<img width="622" alt="image" src="https://github.com/user-attachments/assets/03664a5b-3f47-496f-b1af-ab311dedafbd">


## Introduction

In this project, I build a mini honeynet in Azure and ingest log sources from various resources into a Log Analytics workspace, which is then used by Microsoft Sentinel to build attack maps, trigger alerts, and create incidents. I measured some security metrics in the insecure environment for 24 hours, apply some security controls to harden the environment, measure metrics for another 24 hours, then show the results below. The metrics we will show are:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
<img width="702" alt="image" src="https://github.com/user-attachments/assets/34b35156-4f18-4798-923c-bbfa213bc21c">


## Architecture After Hardening / Security Controls
<img width="718" alt="image" src="https://github.com/user-attachments/assets/e68dc610-981b-457d-ada4-509d5aab3bff">


The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For the "BEFORE" metrics, all resources were originally deployed, exposed to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls wide open, and all other resources are deployed with public endpoints visible to the Internet; aka, no use for Private Endpoints.

For the "AFTER" metrics, Network Security Groups were hardened by blocking ALL traffic with the exception of my admin workstation, and all other resources were protected by their built-in firewalls as well as Private Endpoint

## Attack Maps Before Hardening / Security Controls
<img width="815" alt="(BEFORE) nsg-malicious-allowed-in" src="https://github.com/user-attachments/assets/df69442b-1515-443d-a3d9-088afb043a49">
<img width="758" alt="(BEFORE) windows-rdp-auth-fail" src="https://github.com/user-attachments/assets/26d4d8de-2188-4098-b3b4-b836300dfb1b">
<img width="774" alt="(BEFORE) Linux_SSH_Auth_Fail" src="https://github.com/user-attachments/assets/ea169970-870d-41bd-9e08-5ca507266491">


## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2024-01-24 19:41:11
Stop Time  2024-01-25 19:41:11

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 65468
| Syslog                   | 4614
| SecurityAlert            | 2
| SecurityIncident         | 147
| AzureNetworkAnalytics_CL | 1843

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2024-01-29 20:20:09
Stop Time	 2024-01-30 20:20:09

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 17411
| Syslog                   | 6
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, a mini honeynet was constructed in Microsoft Azure and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. It is noteworthy that the number of security events and incidents were drastically reduced after the security controls were applied, demonstrating their effectiveness.

It is worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the 24-hour period following the implementation of the security controls.
# Azure-Soc
