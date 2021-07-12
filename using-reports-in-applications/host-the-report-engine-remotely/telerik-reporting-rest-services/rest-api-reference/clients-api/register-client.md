---
title: Register Client
page_title: Register Client | for Telerik Reporting Documentation
description: Register Client
slug: telerikreporting/using-reports-in-applications/host-the-report-engine-remotely/telerik-reporting-rest-services/rest-api-reference/clients-api/register-client
tags: register,client
published: True
position: 0
---

# Register Client



## Request#_URI Template_

	 
            POST /api/reports/clients
          



## Response


| HTTP Status Code | Description |
| ------ | ------ |
|`200 OK`|Report instance successfully created|

__Response Body__

The body contains the newly registered client’s identifier string.
        

## Sample#_Request Message_

	 
                POST /api/reports/clients HTTP/1.1
              

#_Response Message_

	 
                HTTP/1.1 201 Created

                “a5f3”
              



# See Also
