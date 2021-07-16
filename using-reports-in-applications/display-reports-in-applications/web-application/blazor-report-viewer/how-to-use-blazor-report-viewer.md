---
title: How to Use Blazor Report Viewer
page_title: How to Use Blazor Report Viewer | for Telerik Reporting Documentation
description: How to Use Blazor Report Viewer
slug: telerikreporting/using-reports-in-applications/display-reports-in-applications/web-application/blazor-report-viewer/how-to-use-blazor-report-viewer
tags: how,to,use,blazor,report,viewer
published: True
position: 1
---

# How to Use Blazor Report Viewer



>important The following article guides you how to use Blazor Report Viewer in a          [Blazor](https://dotnet.microsoft.com/apps/aspnet/web-apps/blazor)          web application.        


## 

* [Visual Studio 2019, version 16.4 or later](https://www.visualstudio.com/vs/)

* Existing ASP.NET Core 3.1 Blazor Server App or ASP.NET Core 3.1-hosted Blazor WebAssembly App
            

* The report viewer consumes reports generated and served from a running Reports Web Service.
              Such can be referenced from another application or Telerik Report Server instance
              or it can be hosted locally in the Blazor application.
              In case you need to host it locally follow the article [How to Host Reports Service in ASP.NET Core 3.1]({%slug telerikreporting/using-reports-in-applications/host-the-report-engine-remotely/telerik-reporting-rest-services/asp.net-core-web-api-implementation/how-to-host-reports-service-in-asp.net-core-3.1%}).
            

## 
        Adding the HTML5 Report Viewer component
      

1. Add NuGet package reference to the __Telerik.ReportViewer.Blazor__ (or __Telerik.ReportViewer.Blazor.Trial__)
              package hosted on the Progress Telerik proprietary NuGet feed.
              Make sure you have the needed NuGet feed added to VS setting using the article [How to add the Telerik private NuGet feed to Visual Studio]({%slug telerikreporting/using-reports-in-applications/how-to-add-the-telerik-private-nuget-feed-to-visual-studio%}).
            

1. Make sure app configuration inside the __Configure__ method of the __Startup.cs__
              can serve static files:
            

	
app.UseStaticFiles();
            



1. Add JavaScript dependencies to the __head__ element of the
              __Pages/_Host.cshtml__ (Blazor Server) or __wwwroot/index.html__ (Blazor WebAssembly):
            #_CSHTML_

	
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>

    @* For Reports service hosted in the same project: *@
    <script src="/api/reports/resources/js/telerikReportViewer"></script>

    @* For Reports service hosted in another application / Report Server use absolute URI: *@
    @*<script src="https://demos.telerik.com/report-server/api/reports/resources/js/telerikReportViewer"></script>*@
              



1. Add
              [Telerik Kendo UI Sass-Based Themes](https://docs.telerik.com/kendo-ui/styles-and-layout/sass-themes)
              to the __head__ element of the
              __Pages/_Host.cshtml__ (Blazor Server) or __wwwroot/index.html__ (Blazor WebAssembly).
              The Razor syntax for a server application differs and you need to escape the __@__ symbol as __@@__:
            #_CSHTML_

	
    <link rel="stylesheet" href="https://unpkg.com/@progress/kendo-theme-default@latest/dist/all.css" />
              

Alternatively you can use the
              [Kendo UI Less-Based Themes](https://docs.telerik.com/kendo-ui/styles-and-layout/appearance-styling)
              (Kendo UI Less-Based Themes are not compatible with Telerik UI for Blazor and should not be used together):
            #_CSHTML_

	
    <link href="https://kendo.cdn.telerik.com/



1. Add the dedicated __interop.js__ dependency at the end of the __body__ element of the
              __Pages/_Host.cshtml__ (Blazor Server) or __wwwroot/index.html__ (Blazor WebAssembly):
            #_CSHTML_

	
    <script src="_content/Telerik.ReportViewer.Blazor/interop.js" defer></script>

    @* Or this one if using the Telerik.ReportViewer.Blazor.Trial package *@
    @*<script src="_content/Telerik.ReportViewer.Blazor.Trial/interop.js" defer></script>*@
              



1. If using Reports web service (either locally hosted or in another application) use the following snippet to place the viewer component in
              a razor page like __Pages/Index.razor__. Note that when referencing the Reports service from another application
              the ServiceUrl setting should be the absolute URI to the service. Remember to set the actual __ReportSource__ along with eventual parameters:
            #_razor_

	
@page "/"
@using Telerik.ReportViewer.Blazor

<style>
    #rv1 {
        position: relative;
        width: 1200px;
        height: 600px;
    }

</style>

<ReportViewer ViewerId="rv1"
              ServiceUrl="/api/reports"
              ReportSource="@(new ReportSourceOptions()
                              {
                                  Report = "YOUR_REPORT_HERE.trdp"
                              })"
              Parameters="@(new ParametersOptions { Editors = new EditorsOptions { MultiSelect = EditorType.ComboBox, SingleSelect = EditorType.ComboBox } })"
              ScaleMode="@(ScaleMode.Specific)"
              Scale="1.0" />
              



1. If displaying reports from a Report Server instance use the following snippet to place the viewer component in
              a razor page like __Pages/Index.razor__. Remember to set the actual __ReportServer__
              and __ReportSource__ settings:
            #_razor_

	
@page "/"
@using Telerik.ReportViewer.Blazor

<style>
    #rv1 {
        position: relative;
        width: 1200px;
        height: 600px;
    }

</style>

<ReportViewer ViewerId="rv1"
              ReportServer="@(new ReportServerOptions {  Url = "https://demos.telerik.com/report-server/", Username = "demouser", Password = "demopass" })"
              ReportSource="@(new ReportSourceOptions()
                              {
                                  Report = "Published/Dashboard"
                              })"
              ScaleMode="@(ScaleMode.Specific)"
              Scale="1.0" />
              



1. Use the rest of the parameters exposed on the Blazor viewer component to setup its appearance and behavior as desired.
            

1. Finally, run the project to see the rendered report.
            