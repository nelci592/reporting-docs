---
title: How to Create Area Chart
page_title: How to Create Area Chart | for Telerik Reporting Documentation
description: How to Create Area Chart
slug: telerikreporting/designing-reports/report-structure/graph/chart-types/area-charts/how-to-create-area-chart
tags: how,to,create,area,chart
published: True
position: 1
---

# How to Create Area Chart



In this article we will show you how to create an Area chart using the Graph item.
      


1. Add a new graph item to the report.


1. Set the 
__DataSource
__ property to a new 
__[SqlDataSource]({%slug telerikreporting/designing-reports/report-designer-tools/desktop-designers/tools/data-source-wizards/sqldatasource-wizard/overview%})
__.


1. Set the connection string to the demo AdventureWorks database.


1. Set the query to the following one:


	                  SELECT SOD.LineTotal, SOH.OrderDate, PC.Name AS Category
                  FROM Sales.SalesOrderHeader AS SOH 
                  INNER JOIN Sales.SalesOrderDetail AS SOD ON SOH.SalesOrderID = SOD.SalesOrderID 
                  INNER JOIN Production.Product AS P ON SOD.ProductID = P.ProductID 
                  INNER JOIN Production.ProductSubcategory AS PS ON P.ProductSubcategoryID = PS.ProductSubcategoryID 
                  INNER JOIN Production.ProductCategory AS PC ON PS.ProductCategoryID = PC.ProductCategoryID
                




1. You can click on 
__Execute Query...
__ just to check if everything is OK with the database connection.
                  Click 
__Finish
__ when you are ready.
                


1. Open 
            
__[                SeriesGroups
              
](dc4689b1-891a-4f6a-93c7-de089b0ffa5e#SeriesGroupHierarchy)__ collection editor and click 
__Add
__:


1. Set the 
__Groupings
__ to: 
*=Fields.OrderDate.Year
*

1. Set the 
__Sortings
__ to: 
*=Fields.OrderDate.Year
*

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
            


1. Set the 
__Groupings
__ to: 
*=Fields.OrderDate.Month
*

1. Set the 
__Sortings
__ to 
*=Fields.OrderDate.Month
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
__ArrangeMode
__ to 
__Stacked
__.
                


1. Set the 
__Y
__ value to 
*=ISNULL(Sum(Fields.LineTotal), 0) / 1000.0
*

1. Set the color palette, the formatting of the labels, the values of the legend and any other improvements as needed.
            
For more information, see 
[Formatting a Graph]({%slug telerikreporting/designing-reports/report-structure/graph/formatting-a-graph/overview%})
.
            

