---
title: Creating the Table and Populating it with Data
page_title: Creating the Table and Populating it with Data | for Telerik Reporting Documentation
description: Creating the Table and Populating it with Data
slug: telerikreporting/getting-started/creating-the-table-and-populating-it-with-data
tags: creating,the,table,and,populating,it,with,data
published: True
position: 3
---

# Creating the Table and Populating it with Data



This article is part of the Demo report guide on getting started with Telerik Reporting and demonstrates how to add an
        
[
          SqlDataSource component
        ]({%slug telerikreporting/designing-reports/connecting-to-data/data-source-components/sqldatasource-component/overview%})
        and present the fetched data into a table item.
      


## Adding the SqlDatasource Component

This guide uses the 
__AdventureWorks
__ database that is provided by Telerik Reporting.
          The data sources that will be added to the report will generate their data representations.
        


1. Select 
__Data
__ > 
__SQL Data Source
__ > 
__Existing data connections
__ > 
__local:/Telerik.reporting.Examples.CSharp.Properties
__.
            
  
  ![3](images/3.PNG)

1. Click 
__Next
__ > 
__Use as a shared connection
__ > 
__Next
__.
            


1. On the screen that loads, fill in the 
__Select Statement
__ field with the following query.
              The query will extract only the first 14 employees and they will be listed in ascending order according to their id, that is,
              the employee with 
id=1
 will be the first one, the employee with 
id=2
 will come second, and so on.
            


	              SELECT
              [HumanResources].[vEmployee].[EmployeeID] ,
              [HumanResources].[vEmployee].[FirstName],
              [HumanResources].[vEmployee].[LastName],
              [HumanResources].[vEmployee].[JobTitle],
              [HumanResources].[vEmployee].[Phone]
              FROM [HumanResources].[vEmployee]
              WHERE [HumanResources].[vEmployee].[EmployeeID] <= 14
              ORDER BY 1 ASC
            




1. From the grid with the properties, change the name of the data source to 
*tableDataSource
* so you can later refer it and render its data in the report.
            


## Creating the Table

1. Click the 
__datailSection
__.
            


1. From the bar, select 
__Insert
__.
            


1. Select 
__Table
__ > 
__Table Wizard
__ > 
__tableDataSource
__.
            


1. On the screen that loads, mark all columns and drag them to the 
__Table Columns
__. Click 
__Next
__.
            


1. From the window that opens, select a predefined style for your table.
            


1. Click 
__Next
__ and 
__Finish
__.
            


1. Apply some 
__Styling
__. For example, change the 
__BorderColor
__ of the table and choose another 
__Font
__ of the text.
            


1. Add the title of the table.
            


## Previewing the Result

Preview the result by clicking 
__Preview
__ > 
__PrintPreview
__.
        


* The generated report uses the 
__Segoe UI
__ font.
            


* The color of its table title is 
__0, 105, 104
__.
            


* [Shapes]({%slug telerikreporting/designing-reports/report-structure/shape%})
 are used for the lines next to the table title.
            


* The 
__BorderColor
__ of the table is 
__34, 181, 115
__.
            
  
  ![Employees](images/Employees.PNG)

## Next Steps

* [Creating the Graph]({%slug telerikreporting/getting-started/creating-the-graph%})


* [Setting the Page Footer]({%slug telerikreporting/getting-started/setting-the-page-footer%})


* [Integrating the Report in VS App]({%slug telerikreporting/getting-started/integrating-the-report-in-vs-app%})


* [Parameterizing the Graph]({%slug telerikreporting/getting-started/parameterizing-the-graph%})


* [How to Add Column Graph]({%slug telerikreporting/getting-started/how-to-add-column-graph%})


## Previous Steps

* [First Steps]({%slug telerikreporting/getting-started/first-steps%})


* [Creating the Demo Report]({%slug telerikreporting/getting-started/creating-the-demo-report%})


* [Setting the Page Header]({%slug telerikreporting/getting-started/setting-the-page-header%})


## See Also

* [Understanding Crosstab Areas]({%slug telerikreporting/designing-reports/report-structure/table/crosstab/list/understanding-crosstab-areas%})

