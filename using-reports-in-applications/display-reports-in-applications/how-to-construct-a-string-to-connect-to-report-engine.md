---
title: How to Construct a string to connect to Report Engine
page_title: How to Construct a string to connect to Report Engine | for Telerik Reporting Documentation
description: How to Construct a string to connect to Report Engine
slug: telerikreporting/using-reports-in-applications/display-reports-in-applications/how-to-construct-a-string-to-connect-to-report-engine
tags: how,to,construct,a,string,to,connect,to,report,engine
published: True
position: 5
---

# How to Construct a string to connect to Report Engine



When using WinForms or WPF Report Viewer, its connection to a Report Server or REST service instance should be additionally set.
        This topic lists the supported keywords for each report engine type and explains how to construct a connection string with or without using helper classes.
      

All the keywords and their values are case insensitive where applicable.
      

## Embedded Report Engine


| Keyword | Value |
| ------ | ------ |
|`Engine`|Embedde|




__Example:__`engine=embedded`

You can use a T:Telerik.ReportViewer.Common.EmbeddedConnectionInfo instance to help you create the connection string or
          leave it empty - the viewer will use the embedded report engine by default.
        

	



	



## Report Server Engine


| Keyword | Value |
| ------ | ------ |
|`Engine`|ReportServer|
|`Uri`| *required* ; The URI of the Report Server instance|
|`Username`| *optional* ; The user name used to connect to Report Server. If omitted, the __Guest__ account will be used, if it is enabled.|
|`Password`| *optional* ; The password associated with the user name.|
|`Timeout`| *optional* ; The timeout for rendering a document measured in seconds. The default value is 100 seconds. Value of 0 indicates no expiration.|
|`KeepClientAlive`| *optional True/False* . Sets whether the client will be kept alive. When set to true expiration of the client will<br/>                be prevented by continually sending a request to the server, determined by the Reporting REST service's __ClientSessionTimeout__ . The default value is True|




__Example:__`engine=ReportServer;uri=http://localhost:83;username=admin;password=pass;timeout=30;keepClientAlive=true`

You can use a T:Telerik.ReportViewer.Common.ReportServerConnectionInfo instance to help you create the connection string.
        

	



	



## REST Service Engine


| Keyword | Value |
| ------ | ------ |
|`Engine`|RestService|
|`Uri`| *required* ; The URI of the REST Service instance.|
|`Token`| *optional* ; If provided, a *Bearer* token will be set in the *Authorization* header for every request to the REST service.|
|`UseDefaultCredentials`| *optional, True/False* ; If provided, the client will send the default credentials with its requests. The default value is *False* .|
|`Timeout`| *optional* ; The timeout for rendering a document measured in seconds. The default value is 100 seconds. Value of 0 indicates no expiration.|
|`KeepClientAlive`| *optional True/False* . Sets whether the client will be kept alive. When set to true expiration of the client will<br/>                be prevented by continually sending a request to the server, determined by the Reporting REST service's __ClientSessionTimeout__ . The default value is True|




__Example:__`engine=RestService;uri=http://localhost:18103/api/reports;token=authToken;useDefaultCredentials=true;timeout=30;keepClientAlive=true`

You can use a T:Telerik.ReportViewer.Common.RestServiceConnectionInfo instance to help you create the connection string.
        

	



	



# See AlsoT:Telerik.ReportViewer.Common.EmbeddedConnectionInfoT:Telerik.ReportViewer.Common.ReportServerConnectionInfoT:Telerik.ReportViewer.Common.RestServiceConnectionInfo
