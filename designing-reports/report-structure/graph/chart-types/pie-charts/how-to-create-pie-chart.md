---
title: How to Create Pie Chart
page_title: How to Create Pie Chart | for Telerik Reporting Documentation
description: How to Create Pie Chart
slug: telerikreporting/designing-reports/report-structure/graph/chart-types/pie-charts/how-to-create-pie-chart
tags: how,to,create,pie,chart
published: True
position: 1
---

# How to Create Pie Chart



In this article we will show you how to create a Pie chart using the Graph item.
      


## 

1. Add a new graph item to the report.


1. Set the 
__DataSource
__ property to a new 
                  
__[SqlDataSource]({%slug telerikreporting/designing-reports/report-designer-tools/desktop-designers/tools/data-source-wizards/sqldatasource-wizard/overview%})
__.
                


1. Set the connection string to the demo AdventureWorks database.


1. Set the query to the following one:


	                  SELECT S.Name AS StoreName, SOH.SubTotal
                  FROM Sales.Customer AS CU 
                  INNER JOIN Sales.SalesOrderHeader AS SOH ON CU.CustomerID = SOH.CustomerID 
                  INNER JOIN Sales.Store AS S ON CU.CustomerID = S.CustomerID
                




1. You can click on 
__Execute Query...
__ just to check if everything is OK with the database connection.
                  Click 
__Finish
__ when you are ready.
                


1. Open 
              
__[                  SeriesGroups
                
](dc4689b1-891a-4f6a-93c7-de089b0ffa5e#SeriesGroupHierarchy)__ collection editor and click 
__Add
__:
            


1. Set the new group 
__Groupings
__ to: 
*=Fields.StoreName
*

1. Set the 
__Sortings
__ to: 
*=Sum(Fields.SubTotal)
*

1. Set the 
__Filters
__ to: 
*=Sum(Fields.SubTotal) Top N =10
*

1. Set the 
__Name
__ to 
*seriesGroup1
*

1. Open 
              
__[                  CategoryGroups
                
](dc4689b1-891a-4f6a-93c7-de089b0ffa5e#CategoryGroupHierarchy)__ collection editor and click 
__Add.
__By default this will add a new static group (group without grouping).
            


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
__PolarCoordinateSystem
__.
            


1. Leave the 
__Name
__ to 
*polarCoordinateSystem1
*.
                


1. Set the 
__RadialAxis
__ to 
__New Axis with Category Scale
__.
                


1. Expand RadialAxis node.
Expand Scale node.
Set SpacingSlotCount to 0.
Expand the axis Style node.
Set Visible to False.


1. Set the 
__AngularAxis
__ to 
__New Axis with Numerical Scale
__.
                


1. Expand AngularAxis node.
Expand the axis Style node.
Set Visible to False.


1. Open 
__[                  Series
                
](585fe887-1319-49a5-a848-869286f7c432#Series)__ collection editor and 
__Add
__ new 
__BarSeries
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
__polarCoordinateSystem1
__.
                


1. Set the 
__ArrangeMode 
__ to 
__Stacked100
__.
                


1. Set the 
__X
__ value to 
*=Sum(Fields.SubTotal)
*

1. Set the 
__DataPointLabel
__ to 
*=Sum(Fields.SubTotal)/1000.0
*

1. Set the 
__DataPointLabelFormat
__ to 
*{0:C0}K
*

1. Set the color palette, the formatting of the labels, the values of the legend and any other improvements as needed.
            
For more information, see 
[Formatting a Graph]({%slug telerikreporting/designing-reports/report-structure/graph/formatting-a-graph/overview%})
.
            


# See Also

