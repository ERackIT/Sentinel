_In Progress_  
_Last Updated:_ 22/03/2025
# Ingesting Palo Alto Logs
Logs can either be forwardding using HTTPS or Syslog into your Microsoft Sentinel log analytics workspace.

### Prerequisites
- Prisma Access license  
- Access to an Azure Log Analytics

## Syslog Log Forwarding Method
[Set Up Syslog Log Forwarding to Microsoft Sentinel | Palo Alto](https://docs.paloaltonetworks.com/prisma-access/integration/microsoft-integrations-with-prisma-access/set-up-syslog-forwarding-to-microsoft-sentinel)
  
### Prerequisites

### Instructions
#### Part 1- Data Connector
1. In your Microsoft Sentinel workspace, select Content hub from the left hand pane.
2. Search and select **Palo Alto Networks Cortex Data Lake** and install it.
3. Go to Data connectors and refresh the section to view the Palo Alto Networks Cortex Data Lake (CDL) data connector.
4. 
  
#### Part 2- Configure Linux Syslog agent

## HTTPS Log Forwarding Method
[Set Up HTTPS Log Forwarding to Microsoft Sentinel | Palo Alto](https://docs.paloaltonetworks.com/prisma-access/integration/microsoft-integrations-with-prisma-access/set-up-https-log-forwarding-to-microsoft-sentinel)
  
### Prerequisites
- Visual Studio Code version >= 1.64.1  
- VS Code Extension: Azure Tools and Azure App Service

### Instructions
#### Part 1- Visual Code
1. git clone [cdl-decompress-proxy-sentinel-ingest | Github](https://github.com/PaloAltoNetworks/cdl-decompress-proxy-sentinel-ingest.git) as a ZIP file.
2. Open the folder cdl-decompress-proxy-sentinel-ingest in Visual Studio Code and ensure you navigate to the final folder in the extract called cdl-decompress-proxy-sentinel-ingest-master.  
3. Click the Azure Icon, Sign Into Azure -> Create new Web App.
4. Enter a name.
5. Choose the Python 3.9 runtime stack.
6. Select an appropriate pricing tier. If you chose the advanced option, select the appropriate Azure resources when prompted. The agent web app takes few minutes to be created.  
7. Right Click the Web App created and chose Deploy to Web App.
8. Select the correct folder, which is the final one in your ZIP extract and should already be listed.
9. Deploy when prompted. Visual Studio Code takes few minutes to deploy the web app.  
