---
title: How to Add sorting to Table item and Crosstab item
page_title: How to Add sorting to Table item and Crosstab item | for Telerik Reporting Documentation
description: How to Add sorting to Table item and Crosstab item
slug: telerikreporting/designing-reports/connecting-to-data/data-items/ordering-data/how-to-add-sorting-to-table-item-and-crosstab-item
tags: how,to,add,sorting,to,table,item,and,crosstab,item
published: True
position: 2
---

# How to Add sorting to Table item and Crosstab item



To define a sorting for the __Table__ or __Crosstab__ items use the following steps: Adding sorting to Table/Crosstab data item using Report Designer



1. In the [Report Designer]({%slug telerikreporting/designing-reports/report-designer-tools/desktop-designers/visual-studio-report-designer/overview%}),
            right click on a Table/Crosstab and then select Properties.

1. Click the Sorting ellipsis.

1. 

For each sort expression, follow these steps:       
              

1. Click New.

1. Type or select an expression by which to sort the data.

1. From the Direction column drop-down list, choose the sort direction 
               for each expression. ASC sorts the expression in ascending order. DESC sorts 
               the expression in descending order.

1. Click OK.Adding sorting to Table/Crosstab Group (Row/Column Group) using Report Designer



1. 
              Open the [Group Explorer]({%slug telerikreporting/designing-reports/report-designer-tools/desktop-designers/tools/group-explorer%}) window.
            

1. 
              In the [Report Designer]({%slug telerikreporting/designing-reports/report-designer-tools/desktop-designers/visual-studio-report-designer/overview%}),
              select the Table/Crosstab.
              This makes the selected item active in the [Group Explorer]({%slug telerikreporting/designing-reports/report-designer-tools/desktop-designers/tools/group-explorer%}) window.
            

1. Choose a Row/Column Group and click its Sorting ellipsis.

1. 


                For each sort expression, follow these steps:
                

1. Click New.

1. Type or select an expression by which to sort the data.

1. 
                    From the Direction column drop-down list, choose the sort direction
                    for each expression. ASC sorts the expression in ascending order. DESC sorts
                    the expression in descending order.
                  

1. Click OK.Adding sorting to Table/Crosstab data item programatically

{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````C#
	
	            Telerik.Reporting.Sorting sorting1 = new Telerik.Reporting.Sorting();
	            sorting1.Expression = "=Fields.ProductID";
	            sorting1.Direction = Telerik.Reporting.SortDirection.Asc;
	
	            table1.Sortings.Add(sorting1);
	
````



{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````VB
	
	        Dim sorting1 As New Telerik.Reporting.Sorting()
	        sorting1.Expression = "=Fields.ProductID"
	        sorting1.Direction = Telerik.Reporting.SortDirection.Asc
	
	        table1.Sortings.Add(sorting1)
	        '#End Region
	
	        Assert.AreEqual(1, table1.Sortings.Count)
	        Assert.AreEqual("=Fields.ProductID", table1.Sortings(0).Expression)
	        Assert.AreEqual(Telerik.Reporting.SortDirection.Asc, table1.Sortings(0).Direction)
	    End Sub
	
	    <TestMethod()> _
	Public Sub Add_Grouping_To_Table()
	        Dim table1 As New Telerik.Reporting.Table()
	
	        '#region AddNewGroupSnippet
	
	        Dim group1 As New Telerik.Reporting.TableGroup()
	        group1.Name = "RowGroup1"
	        group1.Groupings.Add(New Telerik.Reporting.Grouping("=Fields.ProductID"))
	
	        ' If you need to filter the members of the group, apply filtering
	        group1.Filters.Add(New Telerik.Reporting.Filter("=Fields.ProductID", Telerik.Reporting.FilterOperator.Equal, "=10"))
	
	        ' If you need to order the members of the group, apply sorting
	        group1.Sortings.Add(New Telerik.Reporting.Sorting("=Fields.ProductID", Telerik.Reporting.SortDirection.Asc))
	
	        Dim textBox1 As New Telerik.Reporting.TextBox()
	        table1.Items.Add(textBox1)
	        group1.ReportItem = textBox1
	
	        table1.RowGroups.Add(group1)
	        '#End Region
	
	        Assert.AreEqual(1, table1.RowGroups.Count)
	        Assert.AreEqual("=Fields.ProductID", table1.RowGroups(0).Groupings(0).Expression)
	
	        Assert.AreEqual("=Fields.ProductID", table1.RowGroups(0).Filters(0).Expression)
	        Assert.AreEqual(Telerik.Reporting.FilterOperator.Equal, table1.RowGroups(0).Filters(0).[Operator])
	        Assert.AreEqual("=10", table1.RowGroups(0).Filters(0).Value)
	
	        Assert.AreEqual("=Fields.ProductID", table1.RowGroups(0).Sortings(0).Expression)
	        Assert.AreEqual(Telerik.Reporting.SortDirection.Asc, table1.RowGroups(0).Sortings(0).Direction)
	    End Sub
	End Class

T:Telerik.Reporting.TableT:Telerik.Reporting.SortingT:Telerik.Reporting.SortingCollection

 * [How to Add groups to Table item and Crosstab item]({%slug telerikreporting/designing-reports/connecting-to-data/data-items/grouping-data-/how-to-add-groups-to-table-item-and-crosstab-item%})
