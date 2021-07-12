---
title: How to Implement a Custom Report Source Resolver
page_title: How to Implement a Custom Report Source Resolver | for Telerik Reporting Documentation
description: How to Implement a Custom Report Source Resolver
slug: telerikreporting/using-reports-in-applications/host-the-report-engine-remotely/telerik-reporting-rest-services/rest-service-report-source-resolver/how-to-implement-a-custom-report-source-resolver
tags: how,to,implement,a,custom,report,source,resolver
published: True
position: 1
---

# How to Implement a Custom Report Source Resolver



This article explains how to create a custom report source resolver for the __Telerik Reporting REST service__.
        In this example, the resolver purpose will be to return a T:Telerik.Reporting.XmlReportSource with an XML
        report definition obtained from an SQL Server database.
      How to implement a custom report source resolver:

Create a class which implements the T:Telerik.Reporting.Services.IReportSourceResolver
              interface. Its M:Telerik.Reporting.Services.IReportSourceResolver.Resolve(System.String,Telerik.Reporting.Services.OperationOrigin,System.Collections.Generic.IDictionary{System.String,System.Object}) 
              method will be called whenever the engine needs to create a
              T:Telerik.Reporting.ReportSource instance based on the parameter named *report*.
              The value of the *report* parameter will be initialized with the value of the __Report__ property of the report viewer's ReportSource object.
            

	



	



Find the __ReportSourceResolver property__ in the P:Telerik.Reporting.Services.WebApi.ReportsControllerBase.ReportServiceConfiguration settings of the
              implementation of the T:Telerik.Reporting.Services.WebApi.ReportsControllerBase
              class, and set it to an instance of the custom report source resolver or to a chain of resolver instances including the custom one:
            

	



	



Request the report from the HTML5 Report Viewer on the client:

	
<script type="text/javascript">
	$(document).ready(function () {
            $("#reportViewer1").telerik_ReportViewer({
            	serviceUrl: "api/reports/",
            	reportSource: { report: 1 }                
        });
    });
</script>
				



where x.x.x.x is the version of the HTML5 ReportViewer/Telerik Reporting (e.g. 8.1.14.618).

To create the database use the following script:

	
              USE [master]
              GO
              CREATE DATABASE [Reports]
              CONTAINMENT = NONE
              ON  PRIMARY
              ( NAME = N'Reports', FILENAME = N'C:\Program Files\Microsoft SQL Server\MSSQL11.SQLEXPRESS\MSSQL\DATA\Reports.mdf' , SIZE = 4096KB ,

              MAXSIZE = UNLIMITED, FILEGROWTH = 1024KB )
              LOG ON
              ( NAME = N'Reports_log', FILENAME = N'C:\Program Files\Microsoft SQL Server\MSSQL11.SQLEXPRESS\MSSQL\DATA\Reports_log.ldf' , SIZE = 1024KB

              , MAXSIZE = 2048GB , FILEGROWTH = 10%)
              GO
              USE [Reports]
              GO
              CREATE TABLE [dbo].[Reports](
              [ID] [int] NOT NULL,
              [Definition] [nvarchar](max) NOT NULL
              ) ON [PRIMARY] TEXTIMAGE_ON [PRIMARY]
              GO
            



To enter some data into the database you can manually edit the __Reports__ table.
              XML report definitions can be obtained from the sample __.trdx__ report files installed
              together with the product and are located in
              __[Telerik_Reporting_Install_Dir]\Report Designer\Examples__.
            

In newer versions, all sample reports of the Standalone Report Designer are in TRDP format. You can use the
              *Standalone Report Designer - File - Save As* option to convert them to TRDX files.
            
        How to implement and use custom IReportSourceResolver with fallback mechanism:
      

Add to your IReportSourceResolver implementation a constructor with parameter IReportSourceResolver parentResolver.
              Then use the parentResolver if the custom report source resolving mechanism fails.
            

	
class ReportSourceResolverWithFallBack : IReportSourceResolver
{
    readonly IReportSourceResolver parentResolver;

    public ReportSourceResolverWithFallBack(IReportSourceResolver parentResolver)
    {
        this.parentResolver = parentResolver;
    }

    public ReportSource Resolve(string report)
    {
        ReportSource reportDocument = null;
        reportDocument = this.ResolveCustomReportSource(report);

        if (null == reportDocument && null != this.parentResolver)
        {
            reportDocument = this.parentResolver.Resolve(report);
        }

        return reportDocument;
    }

    public ReportSource ResolveCustomReportSource(string report)
    {
        //TODO implement custom report resolving mechanism
        return null;
    }
}
				



	
Class ReportSourceResolverWithFallBack
    Implements IReportSourceResolver
    ReadOnly parentResolver As IReportSourceResolver

    Public Sub New(parentResolver As IReportSourceResolver)
        Me.parentResolver = parentResolver
    End Sub

    Public Function Resolve(report As String) As ReportSource Implements IReportSourceResolver.Resolve
        Dim reportDocument As IReportDocument = Nothing
        reportDocument = Me.ResolveCustomReportSource(report)

        If reportDocument Is Nothing AndAlso Me.parentResolver IsNot Nothing Then
            reportDocument = Me.parentResolver.Resolve(report)
        End If

        Return reportDocument
    End Function

    Public Function ResolveCustomReportSource(report As String) As ReportSource
        'TODO implement custom report resolving mechanism
        Return Nothing
    End Function
End Class
				



Add to the ReportServiceConfiguration the IReportSourceResolver implementations in a chain. Thus the custom one will be executed
              first, if it fails the second one and so on.
            

	
public class CustomResolverWithFallbackReportsController : ReportsControllerBase
{
    static ReportServiceConfiguration configurationInstance;

    static CustomResolverWithFallbackReportsController()
    {
        var resolver = new ReportSourceResolverWithFallBack()
            .AddFallbackResolver(new TypeReportSourceResolver()
                .AddFallbackResolver(new UriReportSourceResolver(HttpContext.Current.Server.MapPath("~/Reports"))));

        configurationInstance = new ReportServiceConfiguration
        {
            HostAppId = "Application1",
            ReportSourceResolver = resolver,
            Storage = new Telerik.Reporting.Cache.File.FileStorage(),
        };
    }

    public CustomResolverWithFallbackReportsController()
    {
        this.ReportServiceConfiguration = configurationInstance;
    }
}
				



	
Public Class CustomResolverWithFallbackReportsController
    Inherits Telerik.Reporting.Services.WebApi.ReportsControllerBase

    Shared configurationInstance As ReportServiceConfiguration

    Shared Sub New()
        Dim resolver = New ReportSourceResolverWithFallBack() _
            .AddFallbackResolver(New TypeReportSourceResolver() _
                .AddFallbackResolver(New UriReportSourceResolver(HttpContext.Current.Server.MapPath("~/Reports"))))

        Dim reportServiceConfiguration As New ReportServiceConfiguration()
        reportServiceConfiguration.HostAppId = "Application1"
        reportServiceConfiguration.ReportSourceResolver = resolver
        reportServiceConfiguration.Storage = New Telerik.Reporting.Cache.File.FileStorage()
        configurationInstance = reportServiceConfiguration
    End Sub

    Public Sub New()
        Me.ReportServiceConfiguration = configurationInstance
    End Sub
End Class
				



You can use for fallback the default IReportSourceResolver implementations:
            

* TypeReportSourceResolver - Resolves IReportDocument from assembly qualified name

* UriReportSourceResolver - Resolves IReportDocument from physical path to trdp or trdx file
