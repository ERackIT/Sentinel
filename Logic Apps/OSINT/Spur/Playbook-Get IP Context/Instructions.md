# Check IP - Setup
*Instructions in progress ( Last updated: March 5,2025)*  

As of February 2025, there is no Spur connector in Azure Logic Apps, so creating your own Spur custom connector will give you better functionality to create multiple Spur logic apps. See [Spur/Create Custom Connector/Instructions.md](https://github.com/ERackIT/Sentinel/blob/main/Logic%20Apps/Spur/Create%20Custom%20Connector/Instructions.md)

### Purpose
These instructions will take you through creating a playbook for your Sentinel SIEM that will add a note to an incidient with the context of the IP addresses in incident.

### References
https://docs.spur.us/context-api?id=context-api

## Logic App Configuration

### Create Playbook
1. In your Microsoft Sentinel, navigate to **Configuration** and select **Automation**.
2. Select **+ Create** dropdown from the top bar, then **Playbook with incident trigger**.
3. Give your playbook a name. Example: *SEN-LAW-PB-SPUR-CheckIP* (Sentinel-LogAnalyticWorkspace-Playbook-SPUR-CheckIP)
4. Select **Next: Connections >**.
5. Select **Next: Review and create >**.

### Design Playbook
1. In the logic app, Select **Development Tools**, then **Logic app designer**.
   
#### Configure Spur API Key
2. In the toolbar, Select **Parameters**.
3. Select **+ Create parameter**  
   i. **Name:** 'APIKey'  
   ii. **Type:** *String*  
   iii. **Default value:** *insert your SPUR API Key*  
4. Close out of **Parameters** pane.
5. '*Microsoft Sentinel incident*' should be floating in the designer window as the trigger point, Select *+*, then **Add an action**.
6. Search '*variable*' and Select **Initialize variable**.
7. In the **Initialize variable** pane, click into **Initialize variable** and rename to '*Set API Key*'. 
8. Under **Parameters**  
   i. **Name:** 'Spur API Key'  
   ii. **Type:** *String*  
   iii. **Value:** '@parameters('APIKey')'  
9. Click out of the **Set API Key** pane, and select the **+** underneath the **Set API Key** variable.

#### Initialise Variables
