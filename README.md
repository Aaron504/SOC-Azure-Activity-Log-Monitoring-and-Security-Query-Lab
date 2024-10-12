# SOC Azure Activity Log Monitoring and Security Query Lab
<p align="center">

  ![Screenshot 2024-10-12 105733](https://github.com/user-attachments/assets/cbd80f5c-f06f-4872-83ed-038611e065c7)


In this lab, I exported Azure Activity Logs to a Log Analytics Workspace to monitor and analyze critical events. I generated logs by creating and deleting resource groups, then ran custom KQL queries to track key activities, such as the deletion of critical resource groups, changes to network security groups, and general deletion activities. Additionally, I queried Microsoft Defender for Cloud Security Events and observed management plane activities. This lab demonstrates my ability to monitor, audit, and analyze Azure activity logs, providing essential security oversight for cloud infrastructure.






<h2>Environments and Technologies Used</h2>

- Log Analytics Workspaces
- Resource Groups
- Active Directory Domain Services
- KQL (Kusto Query Language)

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1 - Export Azure Activity Logs to Log Analytics Workspace
- Step 2 - Generate some logs 
- Step 3 - Create a new Resource Group named “Scratch-Resource-Group”
- Step 4 - Create another new Resource Group named “Critical-Infrastructure-Wastewater”
- Step 5 - Test Lab Queries


<h2>Deployment and Configuration Steps</h2>

- Export Azure Activity Logs to Log Analytics Workspace
![Screenshot 2024-10-12 110437](https://github.com/user-attachments/assets/529c8c2a-91f7-4fae-b558-b9e4d52ec3b4)

- Generate some logs
![Screenshot 2024-10-12 112003](https://github.com/user-attachments/assets/3604b6be-2b05-4e36-bb01-b6dc2c948922)

- Create a new Resource Group named “Scratch-Resource-Group”
![Screenshot 2024-10-12 111132](https://github.com/user-attachments/assets/8e1ee544-2f3a-4767-b071-90de0235cc8f)

- Create another new Resource Group named “Critical-Infrastructure-Wastewater”
![Screenshot 2024-10-12 111412](https://github.com/user-attachments/assets/e48f31ff-85bd-44ef-ba99-3b48d5927a93)

<h2>Test Lab Queries</h2>
- // Querying for the deletion of critical Resource Groups
AzureActivity
| where ResourceGroup startswith "Critical-Infrastructure-"
| order by TimeGenerated

![Screenshot 2024-10-12 112607](https://github.com/user-attachments/assets/71cf57ed-f276-4ca7-b34c-8e9148b1687d)

- // Deletion activities within a certain timespan
AzureActivity
| where OperationNameValue endswith "DELETE"
| where ActivityStatusValue == "Success"
| where TimeGenerated > ago(30m)
| order by TimeGenerated

![Screenshot 2024-10-12 114038](https://github.com/user-attachments/assets/9806b9aa-bee3-4383-aadd-a7d1c799dbce)

- // Just stuff happening on the Management Plane
AzureActivity
| where CategoryValue != "Administrative"

![Screenshot 2024-10-12 114255](https://github.com/user-attachments/assets/9115288b-63da-485f-8059-6119eb45afa6)









