---
title: Using Report Events
page_title: Using Report Events | for Telerik Reporting Documentation
description: Using Report Events
slug: telerikreporting/using-reports-in-applications/program-the-report-definition/report-events/using-report-events
tags: using,report,events
published: True
position: 2
---

# Using Report Events



## 

The __Report__ object exposes these events:
        




| Event | Description |
| ------ | ------ |
| __ItemDataBinding__ |Fires just before the report is bound to data.|
| __NeedDataSource__ |Fires when the report does not have data source set.|
| __ItemDataBound__ |Fires just after the report is bound to data|






The example below shows the NeedDataSource event assigning the report __DataSource__ at runtime. This event only fires when the __DataSource__ is null.
        

{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````C#
	        void report_NeedDataSource(object sender, EventArgs e)
	        {
	            Telerik.Reporting.Processing.Report processingReport = (Telerik.Reporting.Processing.Report)sender;
	            object processingParameterValue = processingReport.Parameters["parameter1"].Value;
	            processingReport.DataSource = GetData(processingParameterValue);
	        }
	
	        static object GetData(object value)
	        {
	            // Implement your custom data retrieval logic instead
	            return new string[] { "Sofia", "London", "Tokyo" };
	        }
````



{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````VB
	    Private Sub report_NeedDataSource(sender As Object, e As EventArgs)
	        Dim processingReport As Telerik.Reporting.Processing.Report = DirectCast(sender, Telerik.Reporting.Processing.Report)
	        Dim processingParameterValue As Object = processingReport.Parameters("parameter1").Value
	        processingReport.DataSource = GetData(processingParameterValue)
	    End Sub
	
	    Private Shared Function GetData(value As Object) As Object
	        ' Implement your custom data retrieval logic instead
	        Return New String() {"Sofia", "London", "Tokyo"}
	    End Function
	    '#End Region
	End Class


