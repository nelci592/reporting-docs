---
title: Manual Setup
page_title: Manual Setup | for Telerik Reporting Documentation
description: Manual Setup
slug: telerikreporting/using-reports-in-applications/display-reports-in-applications/web-application/html5-asp.net-web-forms-report-viewer/manual-setup
tags: manual,setup
published: True
position: 3
---

# Manual Setup



This tutorial shows how to use HTML5 ASP.NET Web Forms Report Viewer in ASP.NET 4 Web Forms applications.
      

## Prerequisites

* Review the HTML5 Report Viewer [System Requirements]({%slug telerikreporting/using-reports-in-applications/display-reports-in-applications/web-application/html5-report-viewer/requirements-and-browser-support%}).
            

* Copy of the "Product Catalog.trdx" report file from __[TelerikReporting_InstallDir]\ReportDesigner\Examples__
              in the folder used by the T:Telerik.Reporting.Services.WebApi.ReportFileResolver
              in the Reporting REST service implementation.
            

* Entry with the default connection string used by Telerik Reporting sample reports in the __web.config__ file
              of the project hosting the Reporting REST service:
            

	
````xml
<connectionStrings>
	 <add name="Telerik.Reporting.Examples.CSharp.Properties.Settings.TelerikConnectionString"
	            connectionString="Data Source=(local);Initial Catalog=AdventureWorks;Integrated Security=SSPI"
	            providerName="System.Data.SqlClient" />
</connectionStrings>
								
````



* (Optional) Telerik Kendo UI custom distribution for Telerik Reporting (located in {Telerik Reporting installation path}\Html5\ReportViewer\js) or Kendo UI mainstream distribution downloaded locally or via [Kendo UI CDN service](http://docs.telerik.com/kendo-ui/install/cdn). You must load only one version of Telerik Kendo UI styles and scripts on the page.
              For more information see [](143e5c03-e69d-416f-9ac0-85c397b22b8e#KendoWidgetsRequirements)If Kendo UI is not provided HTTPHandler will provide the required Kendo UI styles and scripts.
            

## Using HTML5 ASP.NET Web Forms Report Viewer in a web application

The following steps produce a view with settings similar to these of the local WebFormsDemo project,
          installed by default under __[TelerikReporting_InstallDir]\Examples__.
          The structure used in this tutorial is a WebForm that does not use a Master page.
        

>tip All path references in the described steps should be adapted according            to your project setup. For more information please refer to the MSDN article            [ASP.NET Web Project Paths](http://msdn.microsoft.com/en-us/library/ms178116.aspx)


Create new ASP.NET Web Forms Application.

Add new WebForm that does not use a Master page.

To ensure that the browser will start in the latest rendering mode verify the page is using the following DOCTYPE directive:
                #_HTML_

	
````html
							<!DOCTYPE html>
							
````



>tip The above DOCTYPE directive should be considered with your custom requirements. More details about the used in the tutorial settings for the page can be found in the                    [Defining document compatibility](http://msdn.microsoft.com/en-us/library/cc288325(v=vs.85).aspx) MSDN article.                  


Initialize the browser’s viewport in the <head> element:#_HTML_

	
````html
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1" />
				
````



The viewport META tag is used to control layout on mobile browsers.



(Optional) The default viewer implementation depends externally on __jQuery__.
                  Add link to jQuery in the <head> element:
                #_HTML_

	
````html
	<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
									
````



>note jQuery must be loaded only once on the page. Before adding jQuery, verify that it is not already loaded.                  


If jQuery is not provided HTTPHandler will provide automatically the required script.
              

(Optional) Add references to Telerik Kendo UI scripts and styles in the <head> element:#_HTML_

	
````html
<!-- the required Kendo styles -->                  
<link href="https://kendo.cdn.telerik.com/
````



Switch to the Design view of the Web Form and drag the viewer from Visual Studio Toolbox onto the designer surface.
                  The ReportsController will be automatically added to your project,
                  along with references to the required Telerik Reporting assemblies.
                

Configure the HTML5 ASP.NET Web Forms Report Viewer ReportSource using Visual Studio Property Grid. 
                For this you can use the  "Product Catalog.trdp" report file (Prerequisites).

>tip If you use a UriReportSource, the Identifier must point to a TRDP/TRDX file's path that will be mapped to the                        folder used by the T:Telerik.Reporting.Services.WebApi.ReportFileResolver                        in the Reporting REST service implementation.                      


>tip Verify the modified settings are written in the markup. If not, the viewer will use the default settings visible in Visual Studio                    Property Grid                  


Set the viewer width and height.
                

(Optional) If you set the viewer's __ Deferred__ to __true__, render the deferred initialization
                  statement for the Report Viewer (remember that they must be rendered after jQuery):
                

	
````xml
<telerik:DeferredScripts runat="server"></telerik:DeferredScripts>
								
````



Finally the WebForm should look like this (note that the Report Parameter 'CultureID' value will be modified as passed from the viewer) :#_HTML_

	
````html
<%@ Register TagPrefix="telerik" Assembly="Telerik.ReportViewer.Html5.WebForms" Namespace="Telerik.ReportViewer.Html5.WebForms" %>

<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>Telerik HTML5 Web Forms Report Viewer Demo</title>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>

    <link href="https://kendo.cdn.telerik.com/
````


