# Incident-Assignment-Shifts-Timer-Trigger


author: Jeremy Tan

version: 1.0

This Timer playbook will assign an Incident to an owner based on the Shifts schedule in Microsoft Teams.

An email will be sent to notify the assigned user on the incident assignment.

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Ftatecksi%2FSentinelPlaybooks%2Fmaster%2FSentinel_Incident_Assignment_Shifts_Timer_Trigger%2Fazuredeploy.json)
[![Deploy to Azure Gov](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/deploytoazuregov.png)](https://portal.azure.us/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Ftatecksi%2FSentinelPlaybooks%2Fmaster%2FSentinel_Incident_Assignment_Shifts_Timer_Trigger%2Fazuredeploy.json)





## Pre-requisites:

Ensure you have the following details:


### 1. User account or Service Principal with Azure Sentinel Responder role
- Create or use an existing user account/Service Principal with Azure Sentinel Responder role.

- The account will be used in Azure Sentinel connectors (Update incident).


### 2. Setup Shifts schedule
- You must have the [Shifts](https://support.microsoft.com/office/get-started-in-shifts-5f3e30d8-1821-4904-be26-c3cd25a497d6) schedule setup in Microsoft Teams.

- The Shifts schedule must be published (**Share with team**).

  <img src="https://github.com/tatecksi/SentinelPlaybooks/blob/master/Sentinel_Incident_Assignment_Shifts_Timer_Trigger/media/pic2.png" width="700" height="350">

### 3. User account with Owner role in Microsoft Teams
- Create or use an existing user account with **Owner** role in a Team.

- The user account will be used in Shifts connector (List all shifts).


### 4. User account with Log Analytics Reader role
- Create or use an existing user account with Log Analytics Reader role on the Azure Sentinel workspace.

- The user account will be used in Azure Monitor Logs connector (Run query and list results).


### 5. An O365 account to be used to send email notification
- The user account will be used in O365 connector (Send an email).


## Post Deployment Configuration:

### 1. Enable Managed Identity and configure role assignment
- Once deployed, go to the Logic App's blade and click on **Identity** under Settings.
- Select **On** under the **System assigned** tab. Click **Save** and select **Yes** when prompted.

  <img src="https://github.com/tatecksi/SentinelPlaybooks/blob/master/Sentinel_Incident_Assignment_Shifts_Timer_Trigger/media/Pic8.png" width="1000" height="360">
   <br />    
   
- Click on **Azure role assignments** to assign role to the Managed Identity.

 <img src="https://github.com/tatecksi/SentinelPlaybooks/blob/master/Sentinel_Incident_Assignment_Shifts_Timer_Trigger/media/Pic9.png" width="1200" height="280">
   <br />  
   
- Click on **+ Add role assignment**. 
- Select **Resource group** under Scope and select the **Subscription** and **Resource group** where the Azure Sentinel Workspace is located. 
  Select **Azure Sentinel Reader** under Role and click **Save**.

 
   

### 2. Configure connections
- Edit the Logic App or go to Logic app designer.
- Expand each step to find the connectors (4 in total) with <img src="https://github.com/tatecksi/SentinelPlaybooks/blob/master/Sentinel_Incident_Assignment_Shifts_Timer_Trigger/media/pic1.png" width="30" height="30">. 
- Fix these connectors by adding a new connection to each connector and sign in with the accounts described under pre-requisites.
- For the Shifts connector, you need to select the Teams channel with a Shifts schedule.
    
   <img src="https://github.com/tatecksi/SentinelPlaybooks/blob/master/Sentinel_Incident_Assignment_Shifts_Timer_Trigger/media/Pic3.png" width="500" height="140">
   <br />    
   
   Click on the **X** sign for the drop-down list to appear.   
   
   <img src="https://github.com/tatecksi/SentinelPlaybooks/blob/master/Sentinel_Incident_Assignment_Shifts_Timer_Trigger/media/Pic7.png" width="500" height="200">
   
    
- Save the Logic App once you have completed the above steps.





## Incident Assignment Logic:

- The Logic App will run every 5 minutes to check for new incidents in the last 10 minutes without assignees (both values are configurable in the Logic App's variables).

The Logic App will get the available analysts on Shift and distribute the incidents accordingly.

  <img src="https://github.com/tatecksi/SentinelPlaybooks/blob/master/Sentinel_Incident_Assignment_Shifts_Timer_Trigger/media/Pic10.png" width="550" height="300">



- Users who still have at least **1** hours left before going off shift. 
  
  You can change this value by modifying the below variable:

    <img src="https://github.com/tatecksi/SentinelPlaybooks/blob/master/Sentinel_Incident_Assignment_Shifts_Timer_Trigger/media/pic4.png" width="500" height="180">

- Users who have had the fewer incidents assigned to them on the current shift will be assigned incident first.

    
    
## Email Notification:

- When an incident is assigned, the incident owner will be notified via email.
- Below is the sample email notification:

   <img src="https://github.com/tatecksi/SentinelPlaybooks/blob/master/Sentinel_Incident_Assignment_Shifts_Timer_Trigger/media/pic6.png" width="500" height="240">

- The email body has a banner with colour mapped to incident's severity (High=red, Medium=orange, Low=yellow and Informational=grey).
