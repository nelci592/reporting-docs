---
title: How to Add sorting to Report
page_title: How to Add sorting to Report | for Telerik Reporting Documentation
description: How to Add sorting to Report
slug: telerikreporting/designing-reports/connecting-to-data/data-items/ordering-data/how-to-add-sorting-to-report
tags: how,to,add,sorting,to,report
published: True
position: 1
---

# How to Add sorting to Report



To define a sorting for the __Report__ item use the following steps:
    	Adding sorting to Report using Report Designer



1. Click the Report selector button located in the upper left hand
            of the [Report Designer]({%slug telerikreporting/designing-reports/report-designer-tools/desktop-designers/visual-studio-report-designer/overview%}).
            This makes the report active in the Properties window.
  

1. Click the Sorting ellipsis.

1. 

For each sort expression, follow these steps:       
              

1. Click New.

1. Type or select an expression by which to sort the data.

1. From the Direction column drop-down list, choose the sort direction 
               for each expression. ASC sorts the expression in ascending order. DESC sorts 
               the expression in descending order.

1. Click OK.Adding sorting to Report Group using Report Designer



1. 
              Open the [Group Explorer]({%slug telerikreporting/designing-reports/report-designer-tools/desktop-designers/tools/group-explorer%}) window.
            

1. 
              Click the Report selector button located in the upper left corner
              of the [Report Designer]({%slug telerikreporting/designing-reports/report-designer-tools/desktop-designers/visual-studio-report-designer/overview%}).
              This makes the report active in the [Group Explorer]({%slug telerikreporting/designing-reports/report-designer-tools/desktop-designers/tools/group-explorer%}) window.
            

1. Choose a Report Group and click its Sorting ellipsis.

1. 


                For each sort expression, follow these steps:
                

1. Click New.

1. Type or select an expression by which to sort the data.

1. 
                    From the Direction column drop-down list, choose the sort direction
                    for each expression. ASC sorts the expression in ascending order. DESC sorts
                    the expression in descending order.
                  

1. Click OK.Adding sorting to Report programatically



{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````C#
	
	            Telerik.Reporting.Sorting sorting1 = new Telerik.Reporting.Sorting();
	            sorting1.Expression = "=Fields.ProductID";
	            sorting1.Direction = Telerik.Reporting.SortDirection.Asc;
	
	            report1.Sortings.Add(sorting1);
	
````





{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````VB
	
	        Dim sorting1 As New Telerik.Reporting.Sorting()
	        sorting1.Expression = "=Fields.ProductID"
	        sorting1.Direction = Telerik.Reporting.SortDirection.Asc
	
	        report1.Sortings.Add(sorting1)
	        '#End Region
	
	        Assert.AreEqual(1, report1.Sortings.Count)
	        Assert.AreEqual("=Fields.ProductID", report1.Sortings(0).Expression)
	        Assert.AreEqual(Telerik.Reporting.SortDirection.Asc, report1.Sortings(0).Direction)
	    End Sub
	
	    <TestMethod()> _
	Public Sub Add_Grouping_To_Report()
	        Dim report1 As New Report1()
	
	        '#region AddNewGroupSnippet
	
	        Dim group1 As New Telerik.Reporting.Group()
	        group1.Name = "group1"
	        group1.Groupings.Add(New Telerik.Reporting.Grouping("=Fields.ProductID"))
	        Dim groupFooterSection1 As New Telerik.Reporting.GroupFooterSection()
	        Dim groupHeaderSection1 As New Telerik.Reporting.GroupHeaderSection()
	        group1.GroupFooter = groupFooterSection1
	        group1.GroupHeader = groupHeaderSection1
	        'if you need to filter the data, apply filtering
	        group1.Filters.Add(New Telerik.Reporting.Filter("=Fields.ProductID", Telerik.Reporting.FilterOperator.Equal, "=10"))
	        'if you need to sort the data, apply sorting
	        group1.Sortings.Add(New Telerik.Reporting.Sorting("=Fields.ProductID", Telerik.Reporting.SortDirection.Asc))
	
	        report1.Groups.Add(group1)
	        '#End Region
	
	        Assert.AreEqual(1, report1.Groups.Count)
	        Assert.AreEqual("=Fields.ProductID", report1.Groups(0).Groupings(0).Expression)
	
	        Assert.AreEqual("=Fields.ProductID", report1.Groups(0).Filters(0).Expression)
	        Assert.AreEqual(Telerik.Reporting.FilterOperator.Equal, report1.Groups(0).Filters(0).[Operator])
	        Assert.AreEqual("=10", report1.Groups(0).Filters(0).Value)
	
	        Assert.AreEqual("=Fields.ProductID", report1.Groups(0).Sortings(0).Expression)
	        Assert.AreEqual(Telerik.Reporting.SortDirection.Asc, report1.Groups(0).Sortings(0).Direction)
	    End Sub
	
	    <TestMethod()> _
	    Public Sub Add_ReportParameter_To_Report()
	        Dim report1 As New Report1()
	
	        '#Region "AddNewReportParameterSnippet"
	
	        Dim reportParameter1 As New Telerik.Reporting.ReportParameter()
	        reportParameter1.Name = "Parameter1"
	        reportParameter1.Text = "Enter Value for Parameter1"
	        reportParameter1.Type = Telerik.Reporting.ReportParameterType.Integer
	        reportParameter1.AllowBlank = False
	        reportParameter1.AllowNull = False
	        reportParameter1.Value = "=10"
	        reportParameter1.Visible = True
	        report1.ReportParameters.Add(reportParameter1)
	
	        '#End Region
	
	        Dim objectDataSource1 As New Telerik.Reporting.ObjectDataSource()
	
	        '#Region Define_AvailableValues_for_ReportParameter_Snippet()
	
	        reportParameter1.AvailableValues.DataSource = objectDataSource1
	        reportParameter1.AvailableValues.ValueMember = "= Fields.EmployeeID"
	        reportParameter1.AvailableValues.DisplayMember = "= Fields.FirstName"
	        Dim filter1 As New Telerik.Reporting.Filter()
	        filter1.Expression = "=Fields.ProductCategory"
	        filter1.Operator = Telerik.Reporting.FilterOperator.Equal
	        filter1.Value = "=Parameters.ProductCategory"
	        reportParameter1.AvailableValues.Filters.AddRange(New Telerik.Reporting.Filter() {filter1})
	        Dim sorting1 As New Telerik.Reporting.Sorting()
	        sorting1.Expression = "=Fields.ProductSubcategory"
	        sorting1.Direction = Telerik.Reporting.SortDirection.Asc
	        reportParameter1.AvailableValues.Sortings.AddRange(New Telerik.Reporting.Sorting() {sorting1})
	
	        '#End Region
	
	        Assert.AreEqual(1, report1.ReportParameters.Count)
	        Assert.AreEqual("Parameter1", report1.ReportParameters(0).Name)
	        Assert.AreEqual("Enter Value for Parameter1", report1.ReportParameters(0).Text)
	        Assert.AreEqual("=10", report1.ReportParameters(0).Value)
	
	    End Sub
	
	End Class

T:Telerik.Reporting.ReportT:Telerik.Reporting.SortingT:Telerik.Reporting.SortingCollection

 * [How to Add groups to Report]({%slug telerikreporting/designing-reports/connecting-to-data/data-items/grouping-data-/how-to-add-groups-to-report%})
