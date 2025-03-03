# Auth & API Setup

## IAM
  Create an Microsoft Entra application identity for your logic apps to authenticate against Microsoft Entra ID.
  You only have to set up this identity one time for your directory. 

For example, you can choose to use the same identity for all your logic apps, even though you can create unique identities for each logic app
  https://learn.microsoft.com/en-us/azure/logic-apps/logic-apps-custom-api-authentication?tabs=azure-portal
  
  See above for portal instructions


## PowerShell Prerequisites
  1. PowerShell Module
     Install Az module (https://learn.microsoft.com/en-us/powershell/azure/install-azps-windows?view=azps-13.2.0&tabs=windowspowershell&pivots=windows-psgallery)
  2. App Registration Permissions
     Sufficient permissions to create an app in Microsoft Entra ID (https://learn.microsoft.com/en-us/entra/identity/role-based-access-control/permissions-reference)

## Powershell _(as administrator)_
  1. Connect-AzAccount
  2. Add-AzAccount
  3. $SecurePassword = Read-Host -AsSecureString
  4. Set a password and press Enter
  5. New-AzADApplication -DisplayName "MyLogicAppID" -Password $SecurePassword
  6. Make sure to copy the Tenant ID (GUID for your Microsoft Entra tenant), the Application ID, and the password that you used.


## API Connector
  Create an API connection in Azure API Management sevices
  https://learn.microsoft.com/en-us/azure/api-management/import-and-publish#import-and-publish-a-backend-api

