---
title: How to Create Range Chart
page_title: How to Create Range Chart | for Telerik Reporting Documentation
description: How to Create Range Chart
slug: telerikreporting/designing-reports/report-structure/graph/chart-types/range-charts/how-to-create-range-chart
tags: how,to,create,range,chart
published: True
position: 1
---

# How to Create Range Chart



In this article we will show you how to create a Range chart using the Graph item.
      
  
  ![Range Area Chart](images/Graph/RangeAreaChart.png)

## 

1. Add a new graph item to the report.


1. Set the 
__DataSource
__ property to a new 
                  
__[SqlDataSource]({%slug telerikreporting/designing-reports/report-designer-tools/desktop-designers/tools/data-source-wizards/sqldatasource-wizard/overview%})
__.
                


1. Set the connection string to the demo AdventureWorks database.


1. Set the query to the following one:


	                  SELECT ST.Name, SOH.TotalDue, SOH.OrderDate
                  FROM Sales.SalesOrderHeader AS SOH
                  INNER JOIN Sales.SalesTerritory AS ST ON SOH.TerritoryID = ST.TerritoryID
                




1. You can click on 
__Execute Query...
__ just to check if everything is OK with the database connection.
                  Click 
__Finish
__ when you are ready.
                


1. Open
              
__[                  SeriesGroups
                
](dc4689b1-891a-4f6a-93c7-de089b0ffa5e#SeriesGroupHierarchy)__              collection editor and click 
__Add
__.
            
By default this will add a new static group (group without grouping).
            


1. Set the 
__Name
__ to 
*seriesGroup1
*

1. Open 
              
__[                  CategoryGroups
                
](dc4689b1-891a-4f6a-93c7-de089b0ffa5e#CategoryGroupHierarchy)__ collection editor and click 
__Add
__:
            


1. Set the new group 
__Groupings
__ to: 
*=Fields.Name
*

1. Set the 
__Sortings
__ to 
*=Fields.Name
*

1. Set the 
__Name
__ to 
*categoryGroup1
*

1. Open 
__[                  CoordinateSystems
                
](585fe887-1319-49a5-a848-869286f7c432#CoordinateSystems)__ collection editor and 
__Add
__ a new 
__CartesianCoordinateSystem
__.
            


1. Leave the 
__Name
__ to 
*cartesianCoordinateSystem1
*.
                


1. Set the 
__XAxis
__ to 
__New Axis with Category Scale
__.
                


1. Set the 
__YAxis
__ to 
__New Axis with Numerical Scale
__.
                


1. Open 
__[                  Series
                
](585fe887-1319-49a5-a848-869286f7c432#Series)__ collection editor and 
__Add
__ new 
__AreaSeries
__.
            


1. Set the 
__CategoryGroup
__ to 
__categoryGroup1
__.
                


1. Set the 
__SeriesGroup
__ to 
__seriesGroup1
__.
                


1. Set the 
__CoordinateSystem
__ to 
__cartesianCoordinateSystem1
__.
                


1. Set the 
__Y
__ value to 
*=Sum(IIF(Fields.OrderDate.Year=2002, Fields.TotalDue, 0))
*

1. Set the 
__Y0
__ value to 
*=Sum(IIF(Fields.OrderDate.Year=2003, Fields.TotalDue, 0))
*

1. Set the color palette, the formatting of the labels, the values of the legend and any other improvements as needed.
            
For more information, see 
[Formatting a Graph]({%slug telerikreporting/designing-reports/report-structure/graph/formatting-a-graph/overview%})
.
            


# See Also

