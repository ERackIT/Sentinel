## Exfiltration Hunting Queries

Looks for emails sent to an email address that contains some of the Sender name
```kql
//Looks for emails sent to an email address that contains some of the Sender name
let RecipientExclusions = dynamic([".gov.au"]);
let SenderExclusions = dynamic(["procurements@company.com.au", "postmaster@company.com.au","accounts@company.com.au","marty.holden@company.com.au"]);
EmailEvents
| where RecipientEmailAddress !endswith "@company.com.au"
| where SenderFromAddress !in (SenderExclusions)
| where SenderFromAddress != "accounts@company.com.au"
| parse RecipientEmailAddress with * "@" RecipientDomain
| where RecipientDomain !in (RecipientExclusions)
| extend parsedD61Email = replace(@"@company.com.au", "", SenderFromAddress)
| parse parsedD61Email with FirstName "." LastName
| where RecipientEmailAddress contains FirstName or RecipientEmailAddress contains LastName
| where Subject !contains 'payslip' and Subject !contains LastName
| project-reorder SenderFromAddress, RecipientEmailAddress, Subject, AttachmentCount//, parsedD61Email, LastName

```

Looks for files being copied to a USB/external drive.
```kql
//Looks for files being copied to a USB/external drive.
let TimeStamp =  now(); // or datetime('2026-04-17T00:00:00.000Z');
let UsbDriveMount = DeviceEvents
| where TimeGenerated between (ago(30d) .. TimeStamp)
| where ActionType=="UsbDriveMounted"
| extend ParsedFields=parse_json(AdditionalFields)
| project DeviceId, DeviceName, DriveLetter=ParsedFields.DriveLetter, MountTime=TimeGenerated,
ProductName=ParsedFields.ProductName,SerialNumber=ParsedFields.SerialNumber,Manufacturer=ParsedFields.Manufacturer
| order by DeviceId asc, MountTime desc;
let FileCreation = DeviceFileEvents
| where TimeGenerated between (ago(30d) .. TimeStamp)
| where InitiatingProcessAccountName != "system"
| where ActionType == "FileCreated"
| where FolderPath !startswith "C:\\"
| where FolderPath !startswith "\\"
| project ReportId,DeviceId,InitiatingProcessAccountDomain,
InitiatingProcessAccountName,InitiatingProcessAccountUpn,
FileName, FolderPath, SHA256, TimeGenerated, SensitivityLabel, IsAzureInfoProtectionApplied
| order by DeviceId asc, TimeGenerated desc;
FileCreation 
| where TimeGenerated between (ago(30d) .. TimeStamp)
| lookup kind=inner (UsbDriveMount) on DeviceId
| where FolderPath startswith DriveLetter
| where TimeGenerated >= MountTime
| partition hint.strategy=native by ReportId ( top 1 by MountTime )
| order by DeviceId asc, TimeGenerated desc
| extend HostName = iff(DeviceName has '.', substring(DeviceName, 0, indexof(DeviceName, '.')), DeviceName)
| extend DnsDomain = iff(DeviceName has '.', substring(DeviceName, indexof(DeviceName, '.') + 1), "")
| extend FileHashAlgorithm = 'SHA256'
```

Looks for users personal and company SharePoint activity.
```kql
//Looks for users personal and company SharePoint activity.
let TimeStamp =  now(); // or datetime('2026-04-17T00:00:00.000Z');
OfficeActivity
| where TimeGenerated between (ago(30d) .. TimeStamp)
| where EventSource == "SharePoint" and OfficeWorkload has_any("SharePoint", "OneDrive") and Operation has_any ("FileDownloaded", "FileSyncDownloadedFull", "FileSyncUploadedFull", "FileUploaded")
| where OfficeObjectId startswith "https://company-my.sharepoint.com/personal/[firstname]_[lastname]" or UserId  == "[firstname].[lastname]@company.com.au"
| project-reorder Operation, OfficeObjectId, UserDomain, ItemType, SourceFileName
```

