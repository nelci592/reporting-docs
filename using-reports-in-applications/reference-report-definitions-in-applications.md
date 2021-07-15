---
title: Reference Report Definitions in Applications
page_title: Reference Report Definitions in Applications | for Telerik Reporting Documentation
description: Reference Report Definitions in Applications
slug: telerikreporting/using-reports-in-applications/reference-report-definitions-in-applications
tags: reference,report,definitions,in,applications
published: True
position: 1
---

# Reference Report Definitions in Applications



The article elaborates on how to specify which report definition to be used by the report engine when rendering the report in an application.
      

## Report Source

To specify and pass a report definition to the report engine it is required to use a wrapper in the form of a
          report source object. This wrapper contains information about how to fetch the
          report definition and what parameter values to use when the report is processed.
          It is important to know the different report source types and when/how to use them. Please refer to
          [Report Sources]({%slug telerikreporting/designing-reports/report-sources/overview%}) for detailed information.
        

## Reference Reports in Report Viewers

The report viewer is a UI component which is used to specify a report definition via a report source, send the report source for processing
          and rendering to the report engine, and then display the rendered report document in the application.
          Depending on the application type the report viewer can be communicating with a remote report engine via a service, or directly with a
          report engine embedded in the same application as the report viewer control. Regardless of this, the report to be displayed
          is specified by setting a report source property of the report viewer.
        

When working with an embedded report engine, the report source property accepts objects of the
          T:Telerik.Reporting.ReportSource type.
        

When working with a remote report engine via a service, the
          T:Telerik.Reporting.ReportSource
          type might not be available, especially in client-server scenarios where the report engine is hosted in a different application.
          In such scenarios an intermediate report source has to be described (JSON object, custom C# type, etc.).
          The service which is responsible for accessing the report engine will try to translate this intermediate report source to an actual
          T:Telerik.Reporting.ReportSource object.
        

For more details and examples on the different report sources, please refer to
          [How to Set ReportSource for Report Viewers]({%slug telerikreporting/using-reports-in-applications/display-reports-in-applications/how-to-set-reportsource-for-report-viewers%}).
        

## Reference Reports in Report Processor

When the report engine is embedded in the current application (i.e. the *Telerik.Reporting* assembly is referenced)
          it is possible to use the Report Processor to manually render
          (M:Telerik.Reporting.Processing.ReportProcessor.RenderReport(System.String,Telerik.Reporting.ReportSource,System.Collections.Hashtable))
          or print
          (M:Telerik.Reporting.Processing.ReportProcessor.PrintReport(Telerik.Reporting.ReportSource,System.Drawing.Printing.PrinterSettings))
          a report. For this purpose it is required to pass an argument of ReportSource type which uniquely identifies the report.
        

For this example we will use a TypeReportSource. The TypeReportSource specifies the report by its Assembly Qualified Name. The Reporting Engine uses [Reflection](https://msdn.microsoft.com/en-us/library/ms173183(v=vs.110).aspx) to create an instance of the report class through its default parameterless constructor.
        

	



	



# See Also

 * [Report Sources]({%slug telerikreporting/designing-reports/report-sources/overview%})
