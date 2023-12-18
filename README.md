 

<img width="838" alt="Screenshot 2023-11-30 at 1 25 41 PM" src="https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/9f4e358f-36d7-42e9-a883-5321a4956105">

![Password copy](https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/f1225476-95ea-4545-b3f4-a833e9d6afab)

<img width="986" alt="Diagnostic setting" src="https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/a1e05929-98b9-48ce-bf4b-a060c87f2a42">

![Screenshot 2023-11-30 at 9 47 47 PM copy](https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/afebd439-2d1c-4b56-8fc9-1020c2d7601d)

![Screenshot 2023-11-30 at 10 12 53 PM copy](https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/202d032b-f3da-42c4-ae7d-9196e88e60ba)

<img width="403" alt="Screenshot 2023-12-11 at 12 47 37 PM" src="https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/ca24210e-629e-4b8e-bed3-ec287a51a687">

 <img width="889" alt="ShyGuy" src="https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/07ba61ce-6f6e-482b-8fe9-725c75ae6be5">

 <img width="883" alt="Diagnostic setting" src="https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/2982e8d8-4141-48fd-bd77-2463f8b12fe4">

<img width="871" alt="Microsoft Sentinel  Settings" src="https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/17fffd1d-b711-4f6d-a7aa-62d1ed3d3f73">

<img width="324" alt="Actions" src="https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/3f920b4f-5480-4f58-a738-a2b1304838c8"

# SIEM Implementation in Azure Cloud

The objective of this project is to deploy a Microsoft SIEM (Security Information and Event Management) within the Azure Cloud environment. The focus is on enhancing cybersecurity through advanced threat detection capabilities and customized configurations. This involves deploying Microsoft Sentinel and integrating various methods, such as custom KQL (Kusto Query Language) analytics rules, to strengthen defenses against emerging threats.

## Deployment

**Steps for Deployment:**
1. **Access Repository:** Visit Azure/Azure-Sentinel on GitHub.
2. **Deploy to Azure:** Use the "Deploy to Azure" button on the repository.
3. **Configuration Setup:** Review detailed instructions in the repository's documentation for configuring Microsoft Sentinel to suit specific needs.

<img width="646" alt="Screenshot 2023-12-17 at 11 35 37 PM" src="https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/a6e23da5-f5fc-4c10-a33a-f39c0e2cdc6c">

## Viewing Logged Activity

1. Access the logs section to execute queries using KQL for viewing logged activities, tracking essential properties, and investigating incidents.

AzureActivity - returns the Activity log data 
```kusto
AzureActivity
```

This query checks interactive user logon and provides information on auth requirements, client usage, and location details 
```kusto
AADNonInteractiveUserSignInLogs
```

![Microsoft Sentinel  Logs](https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/4393da27-8291-4b5d-b91b-4c01e5424607)

## Analytics Settings

1. Monitor high-security threats like file deletions in the Microsoft Sentinel Analytics settings.
2. Activate User and Entity Behavior Analytics (UEBA) to detect atypical behavior using AI.

![Microsoft Sentinel  Analytics](https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/b7f3b457-db5e-437f-878a-498c859b6fb6)

## Creating Watchlist

1. Add a watchlist by selecting "New" and utilizing a CSV file for external data correlation.
2. Utilize watchlists in search and detection processes within Microsoft Sentinel.

<img width="1094" alt="Screenshot 2023-12-10 at 9 24 15 PM" src="https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/8dc5e943-28aa-4aec-94b4-5fd130e28f43">

![Watchlist wizard copy](https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/b68d9376-8bf7-4ad1-bd01-a9dc1c4f6516)

To use a watchlist in search query, write a Kusto query that uses the _GetWatchlist('watchlist-name') function
```kusto
_GetWatchlist('Tor-IP-Addr’)
```
<img width="925" alt="Screenshot 2023-11-29 at 11 07 13 PM" src="https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/a9c44d40-9873-4e00-bb95-e4771b85a12d">

## Analysis Detection Rule

Create scheduled query rules using KQL to specify criteria for threat detection.

<img width="852" alt="Analytics rule wizard - Create a new Scheduled rule" src="https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/273977d9-3eb0-46c9-bf38-6e9fc23d5e75">

This query specifies the data to be sought, retrieves a list of IP addresses, along with other associated fields, and stores it as a variable named TorNodes.
```kusto
let TorNodes = _GetWatchlist ('Tor-IP-Addr')
	| project TorIP = IpAddress) ;
SigninLogs
| where IPAddress in (TorNodes)
| where ResultType != 5026
| project
TimeGenerated,
Location,
IPAddress,
UserDisplayName,
UserPrincipalName,
UserId,
LocationDetails,
RiskState,
RiskLevelDuringSignIn,
AuthenticationRequirement,
ClientAppUsed,
ConditionalAccessPolicies
```

## Incident Handling

- Observe incidents in Microsoft Sentinel's Incidents section.
- Allocate incidents to specific users, define severity, and manage them effectively.

![Microsoft Sentinel  Analytics copy](https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/bbe2ffc0-13c2-4ce7-bb13-d7f3f4bfe2d9)

<img width="949" alt="Screenshot 2023-11-30 at 8 24 29 PM" src="https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/68984d50-c709-4b0f-9cc8-ca6a5cf3d3ef">

![Screenshot 2023-11-30 at 8 56 01 PM copy](https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/fad62461-5f76-4d3e-b31c-147443217fce)

## Investigation of Cybersecurity Incidents

1. Explore detailed incident pages to view entities, descriptions, events, and related information.
2. Investigate further using log data to identify patterns or anomalies.

<img width="1440" alt="Screenshot 2023-11-30 at 9 24 27 PM" src="https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/12a494bd-086f-4768-bc10-39d72d21359c">

<img width="250" alt="Screenshot 2023-12-10 at 11 00 59 PM" src="https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/4af28be7-d162-467b-99c0-d5526d966e61">

![Screenshot 2023-11-30 at 9 29 52 PM copy](https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/c41ea16e-0af3-4a20-a773-291f0deb45b0)

<img width="607" alt="AbuselPDB » 79 137 202 92" src="https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/ef839dd7-c08f-48ef-8d8a-62d214ee649d">

<img width="999" alt="Screenshot 2023-11-30 at 9 45 09 PM" src="https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/0eb79b98-2054-4f73-a6f6-44ca8f8e5900">

## Remediation Steps

Take prompt actions for remediation in case of security breaches:

1. **Quarantine:** Immediately disable the compromised account "ShyGuy" by navigating to Microsoft Entra > Manage > Users > Click on user > Edit > Account Status > Disable “Account enabled”
2. **Review User Permissions:** Conduct a thorough review of user accounts and permissions across the network and environment, particularly within the administrator's group. Remove unauthorized access and limit privileges to necessary functionalities.
3. **Forensic Analysis:** Perform in-depth forensic analysis on the compromised host and associated network logs to understand the extent of the intrusion and identify potential points of entry.
4. **Patch and Update Systems:** Ensure that all systems, including software and applications, are up-to-date with the latest security patches and configurations to mitigate known vulnerabilities.
5. **Re-enable resources:** Re-enable any resources that were disableed. For example, navigate to og Analytics workspace > select instance > monitor > diagnostic setting > +add diagnostic setting and Microsoft sentinel > configuration settings > settings > auditing and health monitoring
6. **Security Awareness Training:** Conduct security awareness training sessions for employees to educate them on identifying and reporting suspicious activities or security threats.
7. **Incident Response Plan:** Review and update the incident response plan to include steps for handling similar security incidents promptly in the future.
10. **Continuous Monitoring and Analysis:** Implement robust monitoring tools and practices to continuously analyze network traffic for abnormal activities or potential threats.
11. **Close Incident:** Following the implementation of remediation measures, proceed to close the incident(s) and add comments.

These remediation actions should be carried out promptly and in coordination with the organization's IT security team to effectively mitigate the risks posed by the identified security breach.
