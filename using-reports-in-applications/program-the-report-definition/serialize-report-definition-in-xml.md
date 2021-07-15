---
title: Serialize Report Definition in XML
page_title: Serialize Report Definition in XML | for Telerik Reporting Documentation
description: Serialize Report Definition in XML
slug: telerikreporting/using-reports-in-applications/program-the-report-definition/serialize-report-definition-in-xml
tags: serialize,report,definition,in,xml
published: True
position: 7
---

# Serialize Report Definition in XML



__Telerik Reporting__ supports serialization/deserialization of the report definition as plain
        __XML__. This is useful in various
        different scenarios and opens many possibilities that are not easily accomplished otherwise. For example, this allows
        adding or modifying reports in your application without recompiling or redeploying it. Another typical scenario is
        saving/loading of dynamically generated report definitions or transferring them over the network.
      

>note In order to better handle report definition resources we also provide a          T:Telerik.Reporting.ReportPackager          that serializes the report definition in XML and packages it together with its resources in a file with zip compression.          For more information see: [Package Report Definition]({%slug telerikreporting/using-reports-in-applications/program-the-report-definition/package-report-definition%}).        


## Class Report Definition

The __XML__ serialization/deserialization of report definitions is achieved through the dedicated
          T:Telerik.Reporting.XmlSerialization.ReportXmlSerializer
          class. To illustrate how a report is serialized and deserialized, let us start with a simple dynamically generated class report definition:
        

{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````C#
	            var report = new Report1();
	
	            report.Width = Telerik.Reporting.Drawing.Unit.Inch(4);
	
	            var detailSection = new Telerik.Reporting.DetailSection();
	
	            detailSection.Height = Telerik.Reporting.Drawing.Unit.Inch(0.2);
	            report.Items.Add(detailSection);
	
	            var numberTextBox = new Telerik.Reporting.TextBox();
	
	            numberTextBox.Value = "=Fields.ProductNumber";
	            numberTextBox.Left = Telerik.Reporting.Drawing.Unit.Inch(0);
	            numberTextBox.Top = Telerik.Reporting.Drawing.Unit.Inch(0);
	            numberTextBox.Width = Telerik.Reporting.Drawing.Unit.Inch(2);
	            numberTextBox.Height = Telerik.Reporting.Drawing.Unit.Inch(0.2);
	            detailSection.Items.Add(numberTextBox);
	
	            var nameTextBox = new Telerik.Reporting.TextBox();
	
	            nameTextBox.Value = "=Fields.Name";
	            nameTextBox.Left = Telerik.Reporting.Drawing.Unit.Inch(2);
	            nameTextBox.Top = Telerik.Reporting.Drawing.Unit.Inch(0);
	            nameTextBox.Width = Telerik.Reporting.Drawing.Unit.Inch(2);
	            nameTextBox.Height = Telerik.Reporting.Drawing.Unit.Inch(0.2);
	            detailSection.Items.Add(nameTextBox);
	
	            var dataSource = new Telerik.Reporting.SqlDataSource();
	
	            dataSource.ConnectionString = "Data Source=.\\SqlExpress;Initial Catalog=AdventureWorks;Integrated Security=True";
	            dataSource.SelectCommand = "select ProductNumber, Name from Production.Product";
	            report.DataSource = dataSource;
````



{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````VB
	        Dim report As New Report1()
	
	        report.Width = Telerik.Reporting.Drawing.Unit.Inch(4)
	
	        Dim detailSection As New Telerik.Reporting.DetailSection()
	
	        detailSection.Height = Telerik.Reporting.Drawing.Unit.Inch(0.2)
	        report.Items.Add(detailSection)
	
	        Dim numberTextBox As New Telerik.Reporting.TextBox()
	
	        numberTextBox.Value = "=Fields.ProductNumber"
	        numberTextBox.Left = Telerik.Reporting.Drawing.Unit.Inch(0)
	        numberTextBox.Top = Telerik.Reporting.Drawing.Unit.Inch(0)
	        numberTextBox.Width = Telerik.Reporting.Drawing.Unit.Inch(2)
	        numberTextBox.Height = Telerik.Reporting.Drawing.Unit.Inch(0.2)
	        detailSection.Items.Add(numberTextBox)
	
	        Dim nameTextBox As New Telerik.Reporting.TextBox()
	
	        nameTextBox.Value = "=Fields.Name"
	        nameTextBox.Left = Telerik.Reporting.Drawing.Unit.Inch(2)
	        nameTextBox.Top = Telerik.Reporting.Drawing.Unit.Inch(0)
	        nameTextBox.Width = Telerik.Reporting.Drawing.Unit.Inch(2)
	        nameTextBox.Height = Telerik.Reporting.Drawing.Unit.Inch(0.2)
	        detailSection.Items.Add(nameTextBox)
	
	        Dim dataSource As New Telerik.Reporting.SqlDataSource()
	
	        dataSource.ConnectionString = "Data Source=.\SqlExpress;Initial Catalog=AdventureWorks;Integrated Security=True"
	        dataSource.SelectCommand = "select ProductNumber, Name from Production.Product"
	        report.DataSource = dataSource
	        '#End Region
	    End Sub
	
	    <TestMethod()> _
	    Public Sub TextWriter_Serialization_Snippet()
	        Dim report As New Report1()
	
	        '#Region "TextWriterSerializationSnippet"
	        Using fs As New System.IO.FileStream("Report.xml", System.IO.FileMode.Create)
	            Using writer As System.IO.TextWriter = New System.IO.StreamWriter(fs, System.Text.Encoding.UTF8)
	                Dim xmlSerializer As New Telerik.Reporting.XmlSerialization.ReportXmlSerializer()
	
	                xmlSerializer.Serialize(writer, report)
	            End Using
	        End Using
	        '#End Region
	    End Sub
	
	    <TestMethod()> _
	    Public Sub Stream_Serialization_Snippet()
	        Dim report As New Report1()
	
	        '#Region "StreamSerializationSnippet"
	        Using stream As System.IO.Stream = New System.IO.FileStream("Report.xml", System.IO.FileMode.Create)
	            Dim xmlSerializer As New Telerik.Reporting.XmlSerialization.ReportXmlSerializer()
	
	            xmlSerializer.Serialize(stream, report)
	        End Using
	        '#End Region
	    End Sub
	
	    <TestMethod()> _
	    Public Sub FileName_Serialization_Snippet()
	        Dim report As New Report1()
	
	        '#Region "FilePathSerializationSnippet"
	        Dim xmlSerializer As New Telerik.Reporting.XmlSerialization.ReportXmlSerializer()
	
	        xmlSerializer.Serialize("Report.xml", report)
	        '#End Region
	    End Sub
	
	    <TestMethod()> _
	    Public Sub XmlWriter_Serialization_Snippet()
	        Dim report As New Report1()
	
	        '#Region "XmlWriterSerializationSnippet"
	        Using xmlWriter As System.Xml.XmlWriter = System.Xml.XmlWriter.Create("SerializedReport.xml")
	            Dim xmlSerializer As New Telerik.Reporting.XmlSerialization.ReportXmlSerializer()
	
	            xmlSerializer.Serialize(xmlWriter, report)
	        End Using
	        '#End Region
	    End Sub
	
	    <TestMethod()> _
	    <DeploymentItem("Report1.xml")> _
	    Public Sub TextReader_Deserialization_Snippet()
	        '#Region "TextReaderSerializationSnippet"
	        Using fileStream As New System.IO.FileStream("Report1.xml", System.IO.FileMode.Open, System.IO.FileAccess.Read)
	            Using textReader As System.IO.TextReader = New System.IO.StreamReader(fileStream)
	                Dim xmlSerializer As New Telerik.Reporting.XmlSerialization.ReportXmlSerializer()
	
	                Dim report As Telerik.Reporting.Report = DirectCast(xmlSerializer.Deserialize(textReader), Telerik.Reporting.Report)
	            End Using
	        End Using
	        '#End Region
	    End Sub
	
	    <TestMethod()> _
	    <DeploymentItem("Report1.xml")> _
	    Public Sub Stream_Deserialization_Snippet()
	        '#Region "StreamDeserializationSnippet"
	        Using fileStream As New System.IO.FileStream("Report1.xml", System.IO.FileMode.Open, System.IO.FileAccess.Read)
	            Dim xmlSerializer As New Telerik.Reporting.XmlSerialization.ReportXmlSerializer()
	
	            Dim report As Telerik.Reporting.Report = DirectCast(xmlSerializer.Deserialize(fileStream), Telerik.Reporting.Report)
	        End Using
	        '#End Region
	    End Sub
	
	    <TestMethod()> _
	    <DeploymentItem("Report1.xml")> _
	    Public Sub InputUri_Deserialization_Snippet()
	        '#Region "InputUriDeserializationSnippet"
	        Dim xmlSerializer As New Telerik.Reporting.XmlSerialization.ReportXmlSerializer()
	
	        Dim report As Telerik.Reporting.Report = DirectCast(xmlSerializer.Deserialize("Report1.xml"), Telerik.Reporting.Report)
	        '#End Region
	    End Sub
	
	    <TestMethod()> _
	    <DeploymentItem("Report1.xml")> _
	    Public Sub XmlReader_Deserialization_Snippet()
	        '#Region "XmlReaderDeserializationSnippet"
	        Dim settings As New XmlReaderSettings()
	        settings.IgnoreWhitespace = True
	
	        Using xmlReader As System.Xml.XmlReader = System.Xml.XmlReader.Create("Report1.xml", settings)
	            Dim xmlSerializer As New Telerik.Reporting.XmlSerialization.ReportXmlSerializer()
	
	            Dim report As Telerik.Reporting.Report = DirectCast(xmlSerializer.Deserialize(xmlReader), Telerik.Reporting.Report)
	        End Using
	        '#End Region
	    End Sub
	End Class



## Serialize to XML

The following sample code snipped demonstrates how to serialize the above report definition to an XML file:

{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````C#
	            using (System.Xml.XmlWriter xmlWriter = System.Xml.XmlWriter.Create("SerializedReport.xml"))
	            {
	                Telerik.Reporting.XmlSerialization.ReportXmlSerializer xmlSerializer =
	                    new Telerik.Reporting.XmlSerialization.ReportXmlSerializer();
	
	                xmlSerializer.Serialize(xmlWriter, report);
	            }
````



{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````VB
	        Using xmlWriter As System.Xml.XmlWriter = System.Xml.XmlWriter.Create("SerializedReport.xml")
	            Dim xmlSerializer As New Telerik.Reporting.XmlSerialization.ReportXmlSerializer()
	
	            xmlSerializer.Serialize(xmlWriter, report)
	        End Using
	        '#End Region
	    End Sub
	
	    <TestMethod()> _
	    <DeploymentItem("Report1.xml")> _
	    Public Sub TextReader_Deserialization_Snippet()
	        '#Region "TextReaderSerializationSnippet"
	        Using fileStream As New System.IO.FileStream("Report1.xml", System.IO.FileMode.Open, System.IO.FileAccess.Read)
	            Using textReader As System.IO.TextReader = New System.IO.StreamReader(fileStream)
	                Dim xmlSerializer As New Telerik.Reporting.XmlSerialization.ReportXmlSerializer()
	
	                Dim report As Telerik.Reporting.Report = DirectCast(xmlSerializer.Deserialize(textReader), Telerik.Reporting.Report)
	            End Using
	        End Using
	        '#End Region
	    End Sub
	
	    <TestMethod()> _
	    <DeploymentItem("Report1.xml")> _
	    Public Sub Stream_Deserialization_Snippet()
	        '#Region "StreamDeserializationSnippet"
	        Using fileStream As New System.IO.FileStream("Report1.xml", System.IO.FileMode.Open, System.IO.FileAccess.Read)
	            Dim xmlSerializer As New Telerik.Reporting.XmlSerialization.ReportXmlSerializer()
	
	            Dim report As Telerik.Reporting.Report = DirectCast(xmlSerializer.Deserialize(fileStream), Telerik.Reporting.Report)
	        End Using
	        '#End Region
	    End Sub
	
	    <TestMethod()> _
	    <DeploymentItem("Report1.xml")> _
	    Public Sub InputUri_Deserialization_Snippet()
	        '#Region "InputUriDeserializationSnippet"
	        Dim xmlSerializer As New Telerik.Reporting.XmlSerialization.ReportXmlSerializer()
	
	        Dim report As Telerik.Reporting.Report = DirectCast(xmlSerializer.Deserialize("Report1.xml"), Telerik.Reporting.Report)
	        '#End Region
	    End Sub
	
	    <TestMethod()> _
	    <DeploymentItem("Report1.xml")> _
	    Public Sub XmlReader_Deserialization_Snippet()
	        '#Region "XmlReaderDeserializationSnippet"
	        Dim settings As New XmlReaderSettings()
	        settings.IgnoreWhitespace = True
	
	        Using xmlReader As System.Xml.XmlReader = System.Xml.XmlReader.Create("Report1.xml", settings)
	            Dim xmlSerializer As New Telerik.Reporting.XmlSerialization.ReportXmlSerializer()
	
	            Dim report As Telerik.Reporting.Report = DirectCast(xmlSerializer.Deserialize(xmlReader), Telerik.Reporting.Report)
	        End Using
	        '#End Region
	    End Sub
	End Class



## Deserialize from XML

The corresponding code that can be used to deserialize the report definition from the file is shown below:

{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````C#
	            System.Xml.XmlReaderSettings settings = new System.Xml.XmlReaderSettings();
	            settings.IgnoreWhitespace = true;
	
	            using (System.Xml.XmlReader xmlReader = System.Xml.XmlReader.Create("Report1.xml", settings))
	            {
	                Telerik.Reporting.XmlSerialization.ReportXmlSerializer xmlSerializer =
	                    new Telerik.Reporting.XmlSerialization.ReportXmlSerializer();
	
	                Telerik.Reporting.Report report = (Telerik.Reporting.Report)
	                    xmlSerializer.Deserialize(xmlReader);
	            }
````



{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````VB
	        Dim settings As New XmlReaderSettings()
	        settings.IgnoreWhitespace = True
	
	        Using xmlReader As System.Xml.XmlReader = System.Xml.XmlReader.Create("Report1.xml", settings)
	            Dim xmlSerializer As New Telerik.Reporting.XmlSerialization.ReportXmlSerializer()
	
	            Dim report As Telerik.Reporting.Report = DirectCast(xmlSerializer.Deserialize(xmlReader), Telerik.Reporting.Report)
	        End Using
	        '#End Region
	    End Sub
	End Class



## XML Report Definition

and the resulting XML file would look like this:

{{source=System.Xml.XmlAttribute region=}}


