# Sentinel_Incident_Assignment_Shifts


author: Jeremy Tan

This playbook will assign Incident owner based on Shifts schedule in Microsoft Teams.

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https%3A%2F%2Fraw.githubusercontent.com%2Ftatecksi%2FSentinelPlaybooks%2Fmaster%2FSentinel_Incident_Assignment_Shifts%2FSentinel_Incident_Assignment_Shifts.json)


## Pre-requisites:

### 1. Sentinel Workspace details
Kindly obtain the following information:

a. Workspace Name

b. Workspace Resource Group Name

### 2. Service Principal
Create or use existing Service Principal with Azure Sentinel Responder role.

Steps to create a new Service Principal:

Perform the following steps as instructed in this [link](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal):

a. Register an application with Azure AD and create a service principal

b. Create a new application secret

c. Assign a role to the application (assign **Azure Sentinel Responder** role to it)


### 3. Shifts for Teams
[Shifts](https://support.microsoft.com/en-us/office/get-started-in-shifts-5f3e30d8-1821-4904-be26-c3cd25a497d6) schedule has been setup in Microsoft Teams.



## Post Deployment Configurations:



## Incident Assignment Logics:

