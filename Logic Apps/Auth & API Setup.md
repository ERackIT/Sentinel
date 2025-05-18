# Auth & API Setup

## IAM
[Authenticate access and connections to Azure resources with managed identities in Azure Logic Apps | Microsoft Learn](https://learn.microsoft.com/en-us/azure/logic-apps/authenticate-with-managed-identity?tabs=consumption)
  
 Create an Microsoft Entra managed identity for your logic apps to authenticate against Microsoft Entra ID.
  You only have to set up this identity one time for your directory. 

For example, you can choose to use the same identity for all your logic apps, even though you can create unique identities for each logic app. See above for full portal instructions

### Prerequisits

#### Azure Roles
 - Managed Identity Contributor 

### Instructions
#### Create a managed identity
1. In the Azure portal search box, enter _managed identities_. From the results list, select **Managed Identities**.
2. On the **Managed Identities** page toolbar, select **Create**.
3. On the **Create User Assigned Managed Identity** page, select the _subscription_ and _resource group_ of your Microsoft Sentinel instance.
4. Select a **Region**.
5. Give your managed identity a name.
6. Select **Review + Create**.

#### Add user-assigned identity to logic app in the Azure portal
1. In the Azure portal, open your logic app resource.
2. On the logic app menu, under **Settings**, select **Identity**.
3. On the **Identity** page, select **User assigned**, and then select **Add**.
4. Search for the managed identity that you created.


#### Assign role-based access to a managed identity using the Azure portal  
  To use a managed identity for authentication, some Azure resources, such as Azure storage accounts, require that you assign that identity to a role that has the appropriate permissions on the target resource. Other Azure resources, such as key vaults, support multiple options. You can choose either role-based access or an access policy that has the appropriate permissions on the target resource for that identity.
1. In the Azure portal, open the resource where you want to use the identity.
2. On the resource menu, select Access control (IAM) > Add > Add role assignment.
3. Assign the necessary role to your managed identity. On the Role tab, assign a role that gives your identity the required access to the current resource.
4. Next, choose the managed identity where you want to assign the role. Under Assign access to, select Managed identity > Add members.

##### _Example_  
Allowing your logic app to add comments on a Microsoft Sentinel Incident:  
1. Navigate to the resource group that your Microsoft Sentinel instance is in.
2. Select **Access control (IAM) > Add > Add role assignment**.
3. Search and select _Microsoft Sentinel Responder_ > **Next**.
4. Assign access to **Managed identity**.
5. _Select members_ > select the managed identity you created.
6. **Review + assign**


#### Authenticate access with managed identity  
After you enable the managed identity for your logic app resource and give that identity access to the Azure target resource or service, you can use that identity in triggers and actions that support managed identities.
1. In the Azure portal, open your Consumption logic app resource.
2. If you haven't done so yet, add the trigger or action that supports managed identities.
3. On the trigger or action that you added, follow these steps:
  
   _For a Built-in connector operation that support managed identity authentication:_
   a. From the Advanced parameters list, add the Authentication property, if the property doesn't already appear. Now, both the Authentication property and the Authentication Type list appear on the action.
   b. From the Authentication Type list, select Managed Identity.
   c. From the Managed Identity list, select the identity that you created.
  
   _For a Managed connector operation that support managed identity authentication:_  
   a. On the Create Connection pane, from the Authentication list, select Managed Identity.  
   b. On the next pane, for Connection Name, provide a name to use for the connection.  
   c. For the authentication type, choose one of the following options based on your managed connector:
     
   **Single-authentication:** These connectors support only one authentication type, which is the managed identity in this case.  
   i. From the Managed Identity list, select the currently enabled managed identity.  
   ii. When you're ready, select Create New.
     
   **Multi-authentication:** These connectors support multiple authentication types, but you can select and use only one type at a time.  
   i. From the Authentication Type list, select Logic Apps Managed Identity.  
   ii. When you're ready, select Create New.  



## API Connector
  Create an API connection in Azure API Management sevices
  https://learn.microsoft.com/en-us/azure/api-management/import-and-publish#import-and-publish-a-backend-api

