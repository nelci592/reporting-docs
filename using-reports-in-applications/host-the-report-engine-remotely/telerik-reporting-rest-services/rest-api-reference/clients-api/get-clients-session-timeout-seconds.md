---
title: Get Clients Session Timeout Seconds
page_title: Get Clients Session Timeout Seconds | for Telerik Reporting Documentation
description: Get Clients Session Timeout Seconds
slug: telerikreporting/using-reports-in-applications/host-the-report-engine-remotely/telerik-reporting-rest-services/rest-api-reference/clients-api/get-clients-session-timeout-seconds
tags: get,clients,session,timeout,seconds
published: True
position: 3
---

# Get Clients Session Timeout Seconds



## Request

	
````URI Template 
            GET /api/reports/clients/sessionTimeout
          
````



## Response


| HTTP Status Code | Description |
| ------ | ------ |
|`200 OK`|Successfully retrieved the clients session timeou|




__Response Body__

The body contains the clients session timeout in seconds
        

## Sample

	
````Request Message 
                GET /api/reports/clients/sessionTimeout HTTP/1.1
              
````



	
````Response Message 
                HTTP/1.1 200 OK

                {"clientSessionTimeout":900}
              
````



# See Also

