---
title: restReportService Element
page_title: restReportService Element | for Telerik Reporting Documentation
description: restReportService Element
slug: telerikreporting/using-reports-in-applications/export-and-configure/configure-the-report-engine/restreportservice-element
tags: restreportservice,element
published: True
position: 5
---

# restReportService Element



The __restReportService__ element specifies the configuration settings for the REST report service.
        In order for this element to be respected the corresponding Reports service implementation should pass a
        T:Telerik.Reporting.Services.ConfigSectionReportServiceConfiguration
        instance instead of a
        T:Telerik.Reporting.Services.ReportServiceConfiguration
        instance. For example, initializing the 
        P:Telerik.Reporting.Services.WebApi.ReportsControllerBase.ReportServiceConfiguration for the 
        T:Telerik.Reporting.Services.WebApi.ReportsControllerBase instance would look like this:
      

	
        configurationInstance = new ConfigSectionReportServiceConfiguration
        {
          HostAppId = "Html5DemoApp",
          ReportSourceResolver = resolver,
        };
        



Note that the initialization block does not have the 
        P:Telerik.Reporting.Services.IReportServiceConfiguration.Storage property set, because it would 
        override the values obtained from the configuration file.
      

## Attributes and Elements

__<restReportService> element__



|Attributes|*  __hostAppId__ – optional string attribute. Specifies the unique constant name of the application hosting the reports service.<br/>                    When not set the report service utilizes the[AppDomainSetup.ApplicationName Property](https://msdn.microsoft.com/en-us/library/vstudio/system.appdomainsetup.applicationname(v=vs.100).aspx">AppDomainSetup.ApplicationName Property)for the current application domain.<br/>                    This however is not sufficient for each application setup. Set a value for this property in order to provide an unique name among all apps<br/>                    implementing the report service that will be deployed in the same environment.<br/>*  __workerCount__ – optional integer attribute. Specifies the count of the worker threads that render report documents.<br/>                    The default value is equal to the logical processors available on the server machine.<br/>*  __clientSessionTimeout__ – optional integer attribute. Specifies the value in minutes indicating how long a client<br/>                    session will be preserved in the service storage after the last interaction from this client. The value must be greater than zero.<br/>                    The default value is 15 minutes.<br/>*  __reportSharingTimeout__ – optional integer attribute. Specifies the value in minutes indicating how long a rendered report document<br/>                    will be viable for reuse for all clients. The value must be greater than or equal to zero.<br/>                    A zero value will prevent rendered report document reuse. The default value is zero.<br/>*  __exceptionsVerbosity__ – optional string attribute.<br/>                    Specifies the verbosity level of the exception information returned in the response when an exception occurs during report rendering.<br/>                    The supported values are *normal* and *detailed* .<br/>                    When set to *normal* , the response will contain only the exception message.<br/>                    When set to *detailed* , the response will contain the exception type and stack trace.<br/>                    The default value is *normal* .|
|Child elements|*  __reportResolver__ – specifies the report source resolver implementation that will be used for report resolving from the service.<br/>*  __storage__ – specifies the storage implementation that will be used for internal storage from the report service.|
|Parent element| __Telerik.Reporting__ – specifies the root element of the Telerik Reporting configuration settings. Only a single restReportService child element can be used inside<br/>                the Telerik.Reporting root element|




__<reportResolver> element__



|Attributes|*  __provider__ <br/>*  __file__ <br/>*  __directory__ - string parameter. Specifies the physical directory where reports are located.<br/>                            Used as path prefix when relative path is passed for resolving.<br/>*  __type__ |
|Child elements| __parameters__ – specifies a collection of parameters for the current provider. Only one __parameters__ child element can be<br/>                used in the __provider__ parent element.|
|Parent element| __restReportService__|




__<storage> element__



|Attributes|*  __provider__ <br/>*  __redis__ <br/>*  __configuration__ - string parameter. String prefix that should be applied on each key stored in the Redis database.<br/>                            This allows shared usage of one Redis database.<br/>*  __databaseNumber__ - optional integer parameter. Determines the number of the database that should be used.<br/>*  __msSqlServer__ <br/>*  __connectionString__ - string parameter. The connection string to the backend storage.<br/>*  __file__ <br/>*  __directory__ - optional string parameter. The directory which will contain the files representing the stored values.<br/>*  __database__ <br/>*  __backendName__ - string parameter. Specifies which database engine should be used.<br/>*  __connectionString__ - string parameter. A connection string that should be used to connect to the cache database.|
|Child elements| __parameters__ – specifies a collection of parameters for the current provider. Only one __parameters__ child element can be<br/>                used in the __provider__ parent element.|
|Parent element| __restReportService__|




## Examples

XML-based configuration file:

	
<configuration>
…
  <Telerik.Reporting>
    <restReportService hostAppId="Application1" workerCount="4" reportSharingTimeout="10" clientSessionTimeout="10" exceptionsVerbosity="detailed">
      <reportResolver provider="type" />
      <storage provider="file">
        <parameters>
          <parameter name="directory" value="C:\Temp\RestServiceStorage" />
        </parameters>
      </storage>
      <!--<storage provider="Redis">
        <parameters>
          <parameter name="configuration" value="localhost:10001" />
          <parameter name="databaseNumber" value="1" />
        </parameters>
      </storage>-->
      <!--<storage provider="Redis2"> Used for StackExchange.Redis version 2.0+
        <parameters>
          <parameter name="configuration" value="localhost:10001" />
          <parameter name="databaseNumber" value="1" />
        </parameters>
      </storage>-->
      <!--<storage provider="MSSQLServer">
        <parameters>
          <parameter name="connectionString" value="Data Source=(local)\SQLEXPRESS;Initial Catalog=RestServiceStorage;Integrated Security=SSPI" />
        </parameters>
      </storage>-->    
      </restReportService>
  </Telerik.Reporting>
…
</configuration>




JSON-based configuration file:

	
  "telerikReporting": {          
    "restReportService": {
      "hostAppId": "Application1",
      "workerCount": 4,
      "reportSharingTimeout": 10,
      "clientSessionTimeout": 10,
      "exceptionsVerbosity": "detailed",
      "reportResolver": {
        "provider": "type"
      },
      "storage": {
        "provider": "file",
        "parameters": [
          {
            "name": "directory",
            "value": "c:\\temp"
          }
        ]
      }
    },
  }




# See Also

 * [How to implement the ReportsController in an application]({%slug telerikreporting/using-reports-in-applications/host-the-report-engine-remotely/telerik-reporting-rest-services/asp.net-web-api-implementation/how-to-implement-the-reportscontroller-in-an-application%})

 * [How to Add Telerik Reporting REST ServiceStack to Web Application]({%slug telerikreporting/using-reports-in-applications/host-the-report-engine-remotely/telerik-reporting-rest-services/servicestack-implementation/how-to-add-telerik-reporting-rest-servicestack-to-web-application%})