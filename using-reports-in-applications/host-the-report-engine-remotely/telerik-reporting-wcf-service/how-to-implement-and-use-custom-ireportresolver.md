---
title: How to Implement and use custom IReportResolver
page_title: How to Implement and use custom IReportResolver | for Telerik Reporting Documentation
description: How to Implement and use custom IReportResolver
slug: telerikreporting/using-reports-in-applications/host-the-report-engine-remotely/telerik-reporting-wcf-service/how-to-implement-and-use-custom-ireportresolver
tags: how,to,implement,and,use,custom,ireportresolver
published: True
position: 4
---

# How to Implement and use custom IReportResolver



The client programs invoke the report rendering from the service using a string report description. Based on the report description the service’s report resolvers try to create an IReportDocument instance needed by the ReportProcessor.
      

The IReportDocument interface represents a report document. This includes a single Report or ReportBook. The IReportDocument returned by the report resolver will be further handled by the ReportProcessor.
      

The service includes default report resolvers that are capable to resolve IReportDocument from relative and physical path that points to trdp or trdx file (report definition serialized in XML) or from assembly qualified name. This way we cover most of the scenarios. However if you have requirements that are not covered by the default report resolvers, such as retrieving report definitions stored in database or building a report book based on the report description, you can plug into the Telerik Reporting Service report resolving workflow.
      

The report resolvers implement the IReportResolver interface. This interface has only one method Resolve with a string argument - the report description. In custom resolver implementations you should use that description as you like in order to map it to IReportDocument instance.
      

If you use the Silverlight report viewer the report description is provided by the __ReportViewer.Report property__.
      
        Extending Telerik Reporting WCF service with custom IReportResolver implementation:
      
                Prerequisites:
              

Web application
                    

Reference to System.ServiceModel.dll assembly
                    

Reference to Telerik.Reporting.Service.dll assembly
                    

Telerik Reports definitions to be exposed through the Reporting Service
                    
                Steps to implement and use custom IReportResolver:
              

Implement the Telerik.Reporting.Service.IReportResolver
                    

	



	



In order to utilize your IReportResolver implementation, create a Telerik.Reporting.Service subclass and in your subclass constructor pass your IReportResolver implementation to the Telerik.Reporting.ServiceBase.ReportResolver property:
                    

	



	



Even if you use your own IReportResolver implementation you can still fallback to the default IReportResolver implementations as shown in the following walkthrough.
            
                Steps to implement and use custom IReportResolver with fallback mechanism:
              

Add to your IReportResolver implementation a constructor with parameter IReportDocument parentResolver. Then use the parentResolver if the custom report resolving mechanism fails.
                    

	



	



Add to Telerik.Reporting.Service subclass the IReportResolver implementations in a chain. Thus the custom one will be executed first, if it fails the second one and so on.
                    

	



	



You can use for fallback the default IReportResolver implementations:
                    

* ReportTypeResolver - Resolves IReportDocument from assembly qualified name

* ReportFileResolver - Resolves IReportDocument from physical path to trdp or trdx file

* ReportFileResolverWeb - Resolves IReportDocument from a relative path to trdp or trdx fileHosting Telerik.Reporting.Service.ReportService subclass in IIS.

Add .svc file (e.g. ReportService.svc) to reference your Telerik.Reporting.Service.ReportService subclass. The file would contain the following line only:
                    

	
							<%@ServiceHost Service="CSharp.SilverlightDemo.Web.CustomReportService , CSharp.SilverlightDemo.Web" %>
							



Register the Reporting Service endpoints with service name your Telerik.Reporting.Service.ReportService subclass  in the web.config:
                    

	



The custom resolver's Resolve method is called on each interaction with the report in the Silverlight ReportViewer e.g.,
            changing report parameters' values or hitting refresh. To avoid unexpected results the recommended
            [report sources]({%slug telerikreporting/designing-reports/report-sources/overview%}) to work with are __UriReportSource__
            and __TypeReportSource__.
          
