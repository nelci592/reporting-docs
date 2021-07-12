---
title: Embedded Report Engine
page_title: Embedded Report Engine | for Telerik Reporting Documentation
description: Embedded Report Engine
slug: telerikreporting/using-reports-in-applications/call-the-report-engine-via-apis/embedded-report-engine
tags: embedded,report,engine
published: True
position: 0
---

# Embedded Report Engine



## Requirements

To export a report, you can use the __M:Telerik.Reporting.Processing.ReportProcessor.RenderReport(System.String,Telerik.Reporting.ReportSource,System.Collections.Hashtable)__ method of the T:Telerik.Reporting.Processing.ReportProcessor class.
          This method converts the contents of the report to a byte array in the specified format, which you can then use
          with other classes such as
          [MemoryStream](http://msdn.microsoft.com/en-us/library/system.io.memorystream.aspx)
          or [FileStream](http://msdn.microsoft.com/en-us/library/system.io.filestream.aspx)
          .
        

The M:Telerik.Reporting.Processing.ReportProcessor.RenderReport(System.String,Telerik.Reporting.ReportSource,System.Collections.Hashtable)
          method has two overloads, the first is used when rendering a single stream, the second when rendering multiple streams. The
          available extensions used as first argument of the M:Telerik.Reporting.Processing.ReportProcessor.RenderReport(System.String,Telerik.Reporting.ReportSource,System.Collections.Hashtable)
          method are listed in the [Export Formats]({%slug telerikreporting/using-reports-in-applications/export-and-configure/export-formats%}) article.

        

## Exporting a report to a single document format

Some formats (MHTML, PDF, XLS(X), RTF, DOCX, PPTX, CSV) produce a single document which is handled by the first overload of the
          M:Telerik.Reporting.Processing.ReportProcessor.RenderReport(System.String,Telerik.Reporting.ReportSource,System.Collections.Hashtable):
        

	



	



>note When you export programmatically to __XPS__ , you should use a separate STA thread which is
            required by the underlying WPF UI elements that we use to create the XAML representation of the report.
>


## Exporting a report to a multi document format

Some formats produce multiple files, for example HTML outputs all pages and related resources (images)
          in separate streams. In order to render a report in a non-single document format (HTML and IMAGE except TIFF) one should use
          the second M:Telerik.Reporting.Processing.ReportProcessor.RenderReport(System.String,Telerik.Reporting.ReportSource,System.Collections.Hashtable,Telerik.Reporting.Processing.CreateStream,System.String@)
          overload that accepts a T:Telerik.Reporting.Processing.CreateStream callback. For this example we're going to render to JPEG, but you can
          render a report in all graphic formats that GDI+ supports natively - this includes BMP, GIF, JPEG,
          PNG, TIFF and metafile (EMF). The [Windows Forms Application]({%slug telerikreporting/using-reports-in-applications/display-reports-in-applications/windows-forms-application/overview%}) uses internally
          metafile for rendering the reports for viewing, and
          TIFF for exporting. The rest of the formats are available only through code using the ReportProcessor.Render method
          where you should specify "IMAGE" as export format and the additional output format that is the actual graphic
          format - BMP, GIF, JPEG. Here is an example that renders a report as a JPEG image:
        

	



	



# See AlsoM:Telerik.Reporting.Processing.ReportProcessor.RenderReport(System.String,Telerik.Reporting.ReportSource,System.Collections.Hashtable)
