---
title: How to Add filtering to Graph item
page_title: How to Add filtering to Graph item | for Telerik Reporting Documentation
description: How to Add filtering to Graph item
slug: telerikreporting/designing-reports/connecting-to-data/data-items/filtering-data/how-to-add-filtering-to-graph-item
tags: how,to,add,filtering,to,graph,item
published: True
position: 4
---

# How to Add filtering to Graph item



This topic illustrates how to add filters to a Graph item's Filters using the Report Designer or Report API,
        where the filtering occurs after data is retrieved by the report.
      

If you need to filter data on retrieval, see [Using Parameters with Data Source objects]({%slug telerikreporting/designing-reports/connecting-to-data/data-source-components/using-parameters-with-data-source-objects%})

## Adding filters to Graph using Report Designer

1. Open a report in __Design__ view.
            

1. Left-click a __Chart__ item to select it.
            

1. Click __Filters__ ellipsis in the property grid. This displays the current list of filters. By default, the list is empty.
            

1. Click __New__. A new blank filter equation appears.
            

1. In __Expression__, type or select the expression for the field to filter. To open the __Edit Expression__ Dialog, select the <Expression> option.
            

1. In the __Operator__ box, select the operator that you want the filter to use to compare the values in the Expression box and the Value box.
            

1. In the __Value__ box, type the expression or value against which you want the filter to evaluate the value in Expression.
            

1. Click __OK__.
            

## Adding filters to Graph programatically

{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````C#
	
	            Telerik.Reporting.Filter filter1 = new Telerik.Reporting.Filter();
	            filter1.Expression = "=Fields.ProductID";
	            filter1.Operator = Telerik.Reporting.FilterOperator.GreaterThan;
	            filter1.Value = "=10";
	
	            graph1.Filters.Add(filter1);
	
````



{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````VB
	
	        Dim filter1 As New Telerik.Reporting.Filter()
	        filter1.Expression = "=Fields.ProductID"
	        filter1.Operator = Telerik.Reporting.FilterOperator.GreaterThan
	        filter1.Value = "=10"
	
	        graph1.Filters.Add(filter1)
	
	        '#End Region
	
	        Assert.AreEqual(1, graph1.Filters.Count)
	        Assert.AreEqual("=Fields.ProductID", graph1.Filters(0).Expression)
	        Assert.AreEqual(Telerik.Reporting.FilterOperator.GreaterThan, graph1.Filters(0).Operator)
	        Assert.AreEqual("=10", graph1.Filters(0).Value)
	    End Sub
	
	    <TestMethod()> _
	    Public Sub Add_Sorting_To_Graph()
	        Dim graph1 As New Telerik.Reporting.Graph()
	
	        '#region AddNewSortSnippet
	
	        Dim sorting1 As New Telerik.Reporting.Sorting()
	        sorting1.Expression = "=Fields.ProductID"
	        sorting1.Direction = Telerik.Reporting.SortDirection.Asc
	
	        graph1.Sortings.Add(sorting1)
	        '#End Region
	
	        Assert.AreEqual(1, graph1.Sortings.Count)
	        Assert.AreEqual("=Fields.ProductID", graph1.Sortings(0).Expression)
	        Assert.AreEqual(Telerik.Reporting.SortDirection.Asc, graph1.Sortings(0).Direction)
	    End Sub
	End Class



## 

>tip The Graph item has a complex [structure]({%slug telerikreporting/designing-reports/report-structure/graph/structure%}) built by CategoryGroups and SeriesGroups collections, where each collection has its own Filters.            If you need to limit slots, filter the CategoryGroups collection. If you need to filter dynamically created series, filter the SeriesGroups collection.          The [Group Explorer]({%slug telerikreporting/designing-reports/report-designer-tools/desktop-designers/tools/group-explorer%}) can be used for checking the           Graph item's Series and Categories groups.          


# See AlsoT:Telerik.Reporting.ChartT:Telerik.Reporting.FilterT:Telerik.Reporting.FilterCollection

 * [Using Expressions]({%slug telerikreporting/designing-reports/connecting-to-data/expressions/using-expressions/overview%})
