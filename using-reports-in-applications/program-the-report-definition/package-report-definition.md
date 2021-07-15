---
title: Package Report Definition
page_title: Package Report Definition | for Telerik Reporting Documentation
description: Package Report Definition
slug: telerikreporting/using-reports-in-applications/program-the-report-definition/package-report-definition
tags: package,report,definition
published: True
position: 6
---

# Package Report Definition



The T:Telerik.Reporting.ReportPackager
        serializes the report definition in XML and with a zip compression packages the definition and its resources.
        The resources are in their native format and archived for better performance.
        This way the definition is faster to handle and more compact.
        This is the default report document format for the [Overview]({%slug telerikreporting/designing-reports/report-designer-tools/overview%}).
      

## Packaging .TRDX report definition

The following sample code snipped demonstrates how to package a predefined .TRDX (XML) report definition:

{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````C#
	            var reportPackager = new ReportPackager();
	            using (var targetStream = System.IO.File.Create("PackagedReport2.trdp"))
	            {
	                var xmlString = System.IO.File.ReadAllText("Report1.trdx");
	                reportPackager.Package(xmlString, targetStream);
	            }
````



{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````VB
	        Dim reportPackager = New ReportPackager()
	        Using targetStream = System.IO.File.Create("PackagedReport3.trdp")
	            Dim xmlString = System.IO.File.ReadAllText("Report1.trdx")
	            reportPackager.Package(xmlString, targetStream)
	        End Using
	        '#End Region
	    End Sub
	
	    <TestMethod> _
	    <DeploymentItem("Report1.trdp")> _
	    Public Sub UnpackageTrdpSnippet()
	        '#Region "UnpackageTrdpSnippet"
	        Dim reportPackager = New ReportPackager()
	        Using sourcetStream = System.IO.File.OpenRead("Report1.trdp")
	            Dim report = reportPackager.Unpackage(sourcetStream)
	        End Using
	        '#End Region
	    End Sub
	End Class
	



## Packaging CLR report definition

The following sample code snipped demonstrates how to package a predefined CLR report definition:

{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````C#
	            var report = new Report1();
	            var reportPackager = new ReportPackager();
	            using (var targetStream = System.IO.File.Create("PackageReport1.trdp"))
	            {
	                reportPackager.Package(report, targetStream);
	            }
````



{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````VB
	        Dim report = New Report1()
	        Dim reportPackager = New ReportPackager()
	        Using targetStream = System.IO.File.Create("PackagedReport2.trdp")
	            reportPackager.Package(report, targetStream)
	        End Using
	        '#End Region
	    End Sub
	
	    <TestMethod>
	    <DeploymentItem("Report1.trdx")>
	    Public Sub CreatePackageFromXmlReportSnippet()
	        '#Region "CreatePackageFromXmlReportSnippet"
	        Dim reportPackager = New ReportPackager()
	        Using targetStream = System.IO.File.Create("PackagedReport3.trdp")
	            Dim xmlString = System.IO.File.ReadAllText("Report1.trdx")
	            reportPackager.Package(xmlString, targetStream)
	        End Using
	        '#End Region
	    End Sub
	
	    <TestMethod> _
	    <DeploymentItem("Report1.trdp")> _
	    Public Sub UnpackageTrdpSnippet()
	        '#Region "UnpackageTrdpSnippet"
	        Dim reportPackager = New ReportPackager()
	        Using sourcetStream = System.IO.File.OpenRead("Report1.trdp")
	            Dim report = reportPackager.Unpackage(sourcetStream)
	        End Using
	        '#End Region
	    End Sub
	End Class
	



## Unpackaging

The following sample code snipped demonstrates how to unpackage a predefined .TRDP report definition:

{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````C#
	            var reportPackager = new ReportPackager();
	            using (var sourceStream = System.IO.File.OpenRead("Report1.trdp"))
	            {
	                var report = (Report)reportPackager.UnpackageDocument(sourceStream);
	            }
````



{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````VB
	        Dim reportPackager = New ReportPackager()
	        Using sourcetStream = System.IO.File.OpenRead("Report1.trdp")
	            Dim report = reportPackager.Unpackage(sourcetStream)
	        End Using
	        '#End Region
	    End Sub
	End Class
	



# See Also

 * [Overview]({%slug telerikreporting/designing-reports/report-designer-tools/overview%})
