---
title: "Azure Stream Analytics"
featuredImage: ./images/azurestreamanalytics.png
description: "Microsoft Azure Stream Analytics is a serverless scalable complex event processing engine by Microsoft that enables users to develop and run real-time analytics on multiple streams of data from sources such as devices, sensors, web sites, social media, and other applications.Users can set up alerts to detect anomalies, predict trends, trigger necessary workflows when certain conditions are observed, and make data available to other downstream applications and services for presentation, archiving, or further analysis."
slug: /content/tools/azurestreamanalytics
page: toolsandservices
tags: [Data Processing, Data Engineering]
---
# Azure Stream Analytics
## Pre-requisites:
- Create and configure an Event Hub Namespace. 
- Create and configure an Event Hub. 
- Configure Event Hub security.
## Create Stream Analytics Job
### Input
#### Event Hub
- Get the event hub Connection String Primary Key (CSPK). This information is available with the team that creates/administers the event hub. The CSPK will look like the following Endpoint=sb://**NAMESPACE**.servicebus.windows.net/;SharedAccessKeyName=**POLICY_NAME**;SharedAccessKey=**POLICY_KEY**;EntityPath=**EVENT_HUB_NAME**
- Go to the Stream Analyticsjob, create a new Input of type Event Hub. Enter the following values 

|**Input Alias** | User defined name for this input |
|:--|:--|
|**Service Bus Namespace** | NAMESPACE from the above string | 
|**Event Hub name** | EVENT_HUB_NAME from the above string | 
|**Event Hub policy name** | POLICY_NAME from the above string | 
|**Event Hub policy key** | POLICY_KEY from the above string| 
|**Event serialisation format** | JSON |
### Create Output
#### Azure Data Lake Storage
Create a new sink of type ADLS, and enter the following details 
| **Output Alias** | Choose a friendly name for this output | 
|:--|:--| 
| **Account Name** | ADLS Name | 
| **Path Prefix Pattern** | Relative path from the root of the ADLS. Also include `{date}` and `{time}` in the path. These help in creating subfolders for the date and the hour within ADLS.| 
| **Date Format** | YYYY-MM-DD | 
| **Time Format** | HH | 
| **Event Serialisation Format** | JSON | 
| **Format** | Line Separated | 
| **Authentication Mode** | Managed Identity. To make this work, get the MI of the ASA job; in ADLS the ASA job should be given write access to the ADLS folder |
### Query
- ASA uses an SQL-like language to express the movement of data from the source to the sink. A simple query is like "SELECT * INTO [Output] FROM [Input]"
## External Documents
- [Microsoft Documentation](https://docs.microsoft.com/en-in/azure/stream-analytics/)
- [GitHub Lab Exercise](https://github.com/MicrosoftLearning/DP-200-Implementing-an-Azure-Data-Solution/blob/master/instructions/dp-200-06_instructions.md)
