---
title: How to Pass Values to Report Parameters
page_title: How to Pass Values to Report Parameters | for Telerik Reporting Documentation
description: How to Pass Values to Report Parameters
slug: telerikreporting/using-reports-in-applications/display-reports-in-applications/web-application/html5-report-viewer/customizing/how-to-pass-values-to-report-parameters
tags: how,to,pass,values,to,report,parameters
published: True
position: 4
---

# How to Pass Values to Report Parameters



This topic explains how to use custom parameters UI to update the report parameters instead of using the report viewer's default
        implementation of the parameters area. The report and all required parameters for it are packed in a ReportSource object.
        To update the report source the [ReportViewer.reportSource(rs)]({%slug telerikreporting/using-reports-in-applications/display-reports-in-applications/web-application/html5-report-viewer/api-reference/reportviewer/methods/reportsource(rs)%}) method is used.
      

To give an example we will use the Invoice report from our examples and will update its __OrderNumber__ parameter
        from a custom parameter UI.
      Pass values to report parameters

>tip All path references in the described steps should be adapted according
            to your project setup. For more information please refer to the MSDN article[ASP.NET Web Project Paths](http://msdn.microsoft.com/en-us/library/ms178116.aspx)
>


Add a new html page CustomParameters.html to the CSharp.Html5Demo or VB.Html5Demo project.

Add the references to all required JavaScript libraries and stylesheets:#_HTML_

	
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <title>Telerik HTML5 Report Viewer</title>
    <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1" />

    <script src="https://code.jquery.com/jquery-3.3.1.min.js"></script>
    
    <link href="/kendo/styles/kendo.common.min.css" rel="stylesheet" />
    <link href="/kendo/styles/kendo.blueopal.min.css" rel="stylesheet" />

    <script src="/ReportViewer/js/telerikReportViewer.kendo-



Add the custom parameter UI - a dropdown selector with a few values:#_HTML_

	
    <div id="invoiceIdSelector">
        <label for="invoiceId">Invoices</label>
        <select id="invoiceId" title="Select the Invoice ID">
            <option value="SO51081">SO51081</option>
            <option value="SO51082" selected="selected">SO51082</option>
            <option value="SO51083">SO51083</option>
        </select>
    </div>
        



Add the ReportViewer placeholder#_HTML_

	
    <div id="reportViewer1">
        loading...
    </div>
        



Now initialize the report viewer. We will use the minimal set of all
                  [possible options]({%slug telerikreporting/using-reports-in-applications/display-reports-in-applications/web-application/html5-report-viewer/api-reference/report-viewer-initialization%}).
                  Please note how the value from the custom UI is used to set the __OrderNumber__ report parameter initially:
                

	
        $(document).ready(function () {
            $("#reportViewer1").telerik_ReportViewer({
                serviceUrl: "api/reports/",
                reportSource: {
                    report: "Telerik.Reporting.Examples.CSharp.Invoice, CSharp.ReportLibrary",
                    parameters: { OrderNumber: $('#invoiceId option:selected').val() }
                },
                ready: function () {
                    //this.refreshReport();
                }
            });
        });
        



Add code that updates the ReportSource parameters collection with the selected __Invoice Id__ from
                  the dropdown box:
                

	
            $('#invoiceId').change(function () {
                var viewer = $("#reportViewer1").data("telerik_ReportViewer");
                viewer.reportSource({
                    report: viewer.reportSource().report,
                    parameters: { OrderNumber: $(this).val() } 
                });
                //setting the HTML5 Viewer's reportSource, causes a refresh automatically
                //if you need to force a refresh for other case, use:
                //viewer.refreshReport();
            });
        



The HTML page that we have just created should looks like this:#_HTML_

	
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <title>Telerik HTML5 Report Viewer Demo With Custom Parameter</title>
    
    <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1" />

    <script src="https://code.jquery.com/jquery-3.3.1.min.js"></script>
    
    <link href="https://kendo.cdn.telerik.com/



Run the project and verify that the __Invoice Id__ selection really updates the report.
                

 * [How To: Create a Custom Parameter Editor]({%slug telerikreporting/using-reports-in-applications/display-reports-in-applications/web-application/html5-report-viewer/customizing/how-to-create-a-custom-parameter-editor%})
