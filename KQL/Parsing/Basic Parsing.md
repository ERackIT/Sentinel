# How to Parse 
To parse a field from one field into one or more fields/columns, you need to find paramaters that are going to be consistent across entries.
This is ideal for when you need to create alerts based on events from a log ingestion tool or tool that doesn't have a very good parserband is condencing multiple fields into one.

## Breakdown

<ins>**KQL Query**</ins>  
  
**TableName**  
**|**  parse  _Column_ with * "start point" _newColumn_name_ "end point" null    

    
|  | Description |
| --- | --- |
| `TableName` | replace this with the table your events are coming into |
| `parse` | the command
| `Column` | replace with the name of the field/column that has the data you need to parse out into another field/column(s) |
| `with *` | this tells it to search through the field until it reaches the start point |
| `"start point"` | this is where you put the parameter |
| `newColumn_name` | replace this with whatever you want the new field/column to be named |
| `end point"` | this is where you put the end of the parameter. *eg* ";" |
| `null` | this will dump anything that's left in the field *this isn't always necessary, but issues may occur without it* |

**For parameters that contain quotations (")**  
Use a backslash before a quotation mark so the quotation will be included in the search instead of closing out the parameter  

**TableName**   
**|**  parse  _Column_ with * "\"" _newColumn_name_ "\"" null    

## Example  

### Example entry in a Syslog table
_"142>1 2025-05-12T21:17:55.004Z devicename.example.com eventslog - ID72 [exampleUSERID@11562 iut="8" eventSource="System" eventID="4087"]"_

### Example of how you might parse it

**Syslog**  
**|**  parse  *SyslogMessage* with * " " TimeGenerated "Z" null  
**|**  parse  *SyslogMessage* with * "Z " DeviceName " " null  
**|**  parse  *SyslogMessage* with * "[" UserID " " null  
**|**  parse  *SyslogMessage* with * "iut=\"" IUT "\"" null   
**|**  parse  *SyslogMessage* with * "eventSource=\"" eventSource "\"" null  
**|**  parse  *SyslogMessage* with * "eventID=\"" eventID "\"" null  
**|** distinct TimeGenerated, DeviceName, UserID, IUT, eventSource, eventID  


