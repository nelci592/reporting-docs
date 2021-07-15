---
title: How to Set ReportSource for SubReport
page_title: How to Set ReportSource for SubReport | for Telerik Reporting Documentation
description: How to Set ReportSource for SubReport
slug: telerikreporting/designing-reports/report-sources/how-to-set-reportsource-for-subreport
tags: how,to,set,reportsource,for,subreport
published: True
position: 2
---

# How to Set ReportSource for SubReport



This article includes details how to specify a __sub report__ for a [SubReport item]({%slug telerikreporting/designing-reports/report-structure/subreport%}).
        You will need a [Report Source]({%slug telerikreporting/designing-reports/report-sources/overview%}) object.
      

## Set the Report Source through the Report Designer

1. In Design view, right-click a SubReport item to which you want to set a report source and click __Properties__.
            

1. In the item's __Properties__, click __ReportSource__.
            

1. A "Load a Report from" dialog appears which allows you to select a __ReportSource__.
            

1. Select the type of report source you would use to specify a report. For this example we would use __Instance Report Source__,
              click that option and select the report that would serve as detail report.
            If you have to specify parameters for the report, follow the next step.

1. Click __Edit Parameters__ button - __Edit Parameters__ dialog appears. Click __New__.
              In the __Parameter Name__ column select the name of a report parameter in the detail report.
              In the __Parameter Value__, type or select the value to pass to the parameter in the detail report.
            

## Set the Report Source programatically

{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````C#
	            var instanceReportSource = new Telerik.Reporting.InstanceReportSource();
	
	            // Assigning the Report object to the InstanceReportSource
	            instanceReportSource.ReportDocument = new Telerik.Reporting.Examples.CSharp.Invoice();
	
	            // Adding the initial parameter values
	            instanceReportSource.Parameters.Add(new Telerik.Reporting.Parameter("OrderNumber", "SO43659"));
````



{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````VB
	        Dim instanceReportSource As New Telerik.Reporting.InstanceReportSource()
	
	        ' Assigning the Report object to the InstanceReportSource
	        instanceReportSource.ReportDocument = New Invoice()
	
	        ' Adding the initial parameter values
	        instanceReportSource.Parameters.Add(New Telerik.Reporting.Parameter("OrderNumber", "SO43659"))
	        '#End Region
	
	        Assert.IsNotNull(instanceReportSource)
	    End Sub
	
	    <TestMethod>
	    Public Sub Create_TypeName_ReportSource_Snippet()
	        '#Region "CreateTypeReportSourceSnippet"
	        Dim typeReportSource As New Telerik.Reporting.TypeReportSource()
	
	        ' Specifying the assembly qualified name of the Report class for the TypeName of the report source
	        typeReportSource.TypeName = GetType(Invoice).AssemblyQualifiedName
	
	        ' Adding the initial parameter values
	        typeReportSource.Parameters.Add(New Telerik.Reporting.Parameter("OrderNumber", "SO43659"))
	        '#End Region
	
	        Assert.IsNotNull(typeReportSource)
	    End Sub
	
	    <TestMethod>
	    Public Sub Create_Uri_ReportSource_Snippet()
	        '#Region "CreateUriReportSourceSnippet"
	        Dim uriReportSource As New Telerik.Reporting.UriReportSource()
	
	        ' Specifying an URL or a file path
	        uriReportSource.Uri = "SampleReport.trdp"
	
	        ' Adding the initial parameter values
	        uriReportSource.Parameters.Add(New Telerik.Reporting.Parameter("OrderNumber", "SO43659"))
	        '#End Region
	
	        Assert.IsNotNull(uriReportSource)
	    End Sub
	
	    <TestMethod>
	    Public Sub Create_Xml_ReportSource_Snippet()
	        '#Region "CreateXmlReportSourceSnippet"
	        Dim xmlReportSource As New Telerik.Reporting.XmlReportSource()
	
	        ' Specifying the XML markup of the report
	        xmlReportSource.Xml = "<?xml version='1.0' encoding='utf-8'?>" &
	                                    "<Report Width='3in' Name='userReport1' xmlns='http://schemas.telerik.com/reporting/2012/2'>" &
	                                      "<Items>" &
	                                        "<DetailSection Height='1in' Name='detailSection1'>" &
	                                          "<Items>" &
	                                            "<TextBox Value='=Parameters.OrderNumber.Value' Size='2in, 0.4in' Location='0.5in, 0.3in' Name='textBox1' />" &
	                                          "</Items>" &
	                                        "</DetailSection>" &
	                                      "</Items>" &
	                                      "<PageSettings>" &
	                                        "<PageSettings PaperKind='Letter' Landscape='False'>" &
	                                          "<Margins>" &
	                                            "<MarginsU Left='1in' Right='1in' Top='1in' Bottom='1in' />" &
	                                          "</Margins>" &
	                                        "</PageSettings>" &
	                                      "</PageSettings>" &
	                                      "<ReportParameters>" &
	                                        "<ReportParameter Name='OrderNumber'>" &
	                                          "<AvailableValues />" &
	                                        "</ReportParameter>" &
	                                      "</ReportParameters>" &
	                                    "</Report>"
	
	        ' Adding the initial parameter values
	        xmlReportSource.Parameters.Add(New Telerik.Reporting.Parameter("OrderNumber", "SO43659"))
	        '#End Region
	
	        Assert.IsNotNull(xmlReportSource)
	    End Sub
	
	    <TestMethod>
	    Public Sub Set_Values_For_Unique_Or_Mergable_ReportParameters_In_ReportSource_Snippet()
	        '#Region Set_Values_For_Unique_Or_Mergable_ReportParameters_In_ReportSource_Snippet
	        Dim typeReportSource As New Telerik.Reporting.TypeReportSource()
	        typeReportSource.TypeName = GetType(MyReportBook).AssemblyQualifiedName
	
	        ' Passing a value for unique Or repeating report parameter that should have one And the same value
	        ' for all reports part of the report book thru the report source
	        typeReportSource.Parameters.Add(New Telerik.Reporting.Parameter("ProductCategory", "Bikes"))
	        '#End Region
	
	        Assert.IsNotNull(typeReportSource)
	    End Sub
	
	
	    <TestMethod>
	    Public Sub Set_Values_For_NotMergable_ReportParameters_In_ReportSource_Snippet()
	        '#Region Set_Values_For_NotMergable_ReportParameters_In_ReportSource_Snippet
	        Dim typeReportSource As New Telerik.Reporting.TypeReportSource()
	        typeReportSource.TypeName = GetType(MyReportBook).AssemblyQualifiedName
	
	        ' Passing a value for Not mergeable report parameter targeting the FIRST report in the report book
	        ' thru the report source
	        typeReportSource.Parameters.Add(New Telerik.Reporting.Parameter("reports(0).ClientID", 102))
	
	        ' Passing a value for Not mergeable report parameter targeting the SECOND report in the report book
	        ' thru the report source
	        typeReportSource.Parameters.Add(New Telerik.Reporting.Parameter("reports(1).ClientID", 103))
	        '#End Region
	
	        Assert.IsNotNull(typeReportSource)
	    End Sub
	
	
	    Class MyReportBook
	        Inherits Telerik.Reporting.ReportBook
	    End Class
	
	    Class Invoice
	        Inherits Report
	    End Class
	
	End Class



## 

The [Standalone Report Designer]({%slug telerikreporting/designing-reports/report-designer-tools/desktop-designers/standalone-report-designer/overview%}) includes only XmlReportSource and UriReportSource options due to the format
          of the produced reports.
          In [Visual Studio Report Designer]({%slug telerikreporting/designing-reports/report-designer-tools/desktop-designers/visual-studio-report-designer/overview%}) you can use all available [Report Sources]({%slug telerikreporting/designing-reports/report-sources/overview%}).
        

>tip If the report will be displayed in an HTML5 Viewer or Silverlight ReportViewer, the main report is rendered in HTML (XAML respectively) and it is loaded at the client.            The sub report is considered as a content of the main report and its Report Source is resolved internally,            withouit additional calls to the Reporting REST service (Reporting WCF Service respectively).          


# See Also

 * [How to: Create a Master-Detail Report Using a SubReport Item]({%slug telerikreporting/designing-reports/report-structure/how-to/how-to-create-a-master-detail-report-using-a-subreport-item%})

 * [How to: Create a Master-Detail Report Using a Table]({%slug telerikreporting/designing-reports/report-structure/how-to/how-to-create-a-master-detail-report-using-a-table%})
