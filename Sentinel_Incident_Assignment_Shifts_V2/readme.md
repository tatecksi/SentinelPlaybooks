# Incident-Assignment-Shifts


author: Jeremy Tan

version: 2.0

This playbook will assign an Incident to an owner based on the Shifts schedule in Microsoft Teams.
An email will be sent to notify the assigned user on the incident assignment.

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Ftatecksi%2FSentinelPlaybooks%2Fmaster%2FSentinel_Incident_Assignment_Shifts_V2%2Fazuredeploy.json)
[![Deploy to Azure Gov](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/deploytoazuregov.png)](https://portal.azure.us/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Ftatecksi%2FSentinelPlaybooks%2Fmaster%2FSentinel_Incident_Assignment_Shifts_V2%2Fazuredeploy.json)





## Pre-requisites:

Ensure you have the following details:


### 1. User account with the Azure Sentinel Responder role
- Create or use an existing user account with the Azure Sentinel Responder role.

- The user account will be used in Azure Sentinel connectors.


### 2. Setup Shifts schedule
- You must have the [Shifts](https://support.microsoft.com/office/get-started-in-shifts-5f3e30d8-1821-4904-be26-c3cd25a497d6) schedule setup in Microsoft Teams.

- The Shifts schedule must be published (**Share with team**).

  <img src="https://github.com/tatecksi/SentinelPlaybooks/blob/master/Sentinel_Incident_Assignment_Shifts/media/pic2.png" width="700" height="350">

### 3. User account for Shifts
- Create or use an existing user account with **Owner** permission in a Team.


### 4. Permission on Azure AD
- There is an Azure AD connector in this Logic App to get details for a user.
- To use the Azure AD connector, you need to **Sign-in** with an account with the following administrator permissions:
    - Group.ReadWrite.All
    - User.ReadWrite.All
    - Directory.ReadWrite.All


### 5. An O365 account to be used to send email notification
- Login details of the O365 account.


## Post Deployment Configuration:

- Once deployed, edit the Logic App and find the connectors (6 in total) that has been marked with <img src="https://github.com/tatecksi/SentinelPlaybooks/blob/master/Sentinel_Incident_Assignment_Shifts_V2/media/pic1.png" width="30" height="30">. 
- Fix these connectors by adding a new connection to each connector within your Logic App and sign in with the accounts described under pre-requisites.
- For the Shifts connector, you need to select the Teams channel with a Shifts schedule.
    
   <img src="https://github.com/tatecksi/SentinelPlaybooks/blob/master/Sentinel_Incident_Assignment_Shifts_V2/media/Pic3.png" width="500" height="120">
    
- Save the Logic App once you have completed the above steps.





## Incident Assignment Logic:

Incidents are assigned to users based on the following criteria:

- Only users who have started their shifts during the time the Logic App runs will be considered.
- Users who still have at least **1** hours left before going off shift. 
  
  You can change this value by modifying the below variable:

    <img src="https://github.com/tatecksi/SentinelPlaybooks/blob/master/Sentinel_Incident_Assignment_Shifts_V2/media/pic4.png" width="500" height="180">

- Users who have had the fewer incidents assigned to them over the past 24 hours will be assigned incident first.

    
    
## Email Notification:

- When an incident is assigned, the incident owner will be notified via email.
- Below is the sample email notification:

   <img src="https://github.com/tatecksi/SentinelPlaybooks/blob/master/Sentinel_Incident_Assignment_Shifts_V2/media/pic6.png" width="500" height="240">

- The email body has a banner with colour mapped to incident's severity (High=red, Medium=orange, Low=yellow and Informational=grey).