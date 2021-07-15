---
title: How to Add filtering to Report
page_title: How to Add filtering to Report | for Telerik Reporting Documentation
description: How to Add filtering to Report
slug: telerikreporting/designing-reports/connecting-to-data/data-items/filtering-data/how-to-add-filtering-to-report
tags: how,to,add,filtering,to,report
published: True
position: 2
---

# How to Add filtering to Report



This topic illustrates how to add filters to the Report's Filters collection using the Report Designer or Report API,
        where the filtering occurs after data is retrieved by the report.
      

If you need to filter data on retrieval, see [Using Parameters with Data Source objects]({%slug telerikreporting/designing-reports/connecting-to-data/data-source-components/using-parameters-with-data-source-objects%})

## Adding filters to Report using Report Designer

To add filters to the Report use the following steps:

1. Open a report in __Design__ view.
            

1. Click the Report selector button located in the upper left hand
              of the [Report Designer]({%slug telerikreporting/designing-reports/report-designer-tools/desktop-designers/visual-studio-report-designer/overview%}).
              This makes the report active in the Properties window.
            

1. Click __Filters__ ellipsis in the property grid. This displays the current list of filters. By default, the list is empty.
            

1. Click __New__. A new blank filter equation appears.
            

1. In __Expression__, type or select the expression for the field to filter. To open the __Edit Expression__ Dialog, select the <Expression> option.
            

1. In the __Operator__ box, select the operator that you want the filter to use to compare the values in the Expression box and the Value box.
            

1. In the __Value__ box, type the expression or value against which you want the filter to evaluate the value in Expression.
            

1. Click __OK__.
            

## Adding filters to Report programatically

{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````C#
	
	            Telerik.Reporting.Filter filter1 = new Telerik.Reporting.Filter();
	            filter1.Expression = "=Fields.ProductID";
	            filter1.Operator = Telerik.Reporting.FilterOperator.GreaterThan;
	            filter1.Value = "=10";
	
	            report1.Filters.Add(filter1);
	            
````



{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````VB
	
	        Dim filter1 As New Telerik.Reporting.Filter()
	        filter1.Expression = "=Fields.ProductID"
	        filter1.Operator = Telerik.Reporting.FilterOperator.GreaterThan
	        filter1.Value = "=10"
	
	        report1.Filters.Add(filter1)
	
	        '#End Region
	
	        Assert.AreEqual(1, report1.Filters.Count)
	        Assert.AreEqual("=Fields.ProductID", report1.Filters(0).Expression)
	        Assert.AreEqual(Telerik.Reporting.FilterOperator.GreaterThan, report1.Filters(0).Operator)
	        Assert.AreEqual("=10", report1.Filters(0).Value)
	    End Sub
	
	    <TestMethod()> _
	Public Sub Add_Sorting_To_Report()
	        Dim report1 As New Report1()
	
	        '#region AddNewSortSnippet
	
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



## 

>tip The Report can have a complex structure due to added groups.            You can filter data per group by using the corresponding group's Filters collection.          The [Group Explorer]({%slug telerikreporting/designing-reports/report-designer-tools/desktop-designers/tools/group-explorer%}) can be used for checking the            Report's structure and the each group's properties.          


# See AlsoT:Telerik.Reporting.ReportT:Telerik.Reporting.FilterT:Telerik.Reporting.FilterCollection

 * [Using Expressions]({%slug telerikreporting/designing-reports/connecting-to-data/expressions/using-expressions/overview%})
