---
title: Parameterizing the Graph
page_title: Parameterizing the Graph | for Telerik Reporting Documentation
description: Parameterizing the Graph
slug: telerikreporting/getting-started/parameterizing-the-graph
tags: parameterizing,the,graph
published: True
position: 7
---

# Parameterizing the Graph



This article is part of the Demo report guide on getting started with Telerik Reporting.
        It demonstrates how to add a report parameter and change the 
graphDataSource
 of the graph
        so that the user can select a year based on which the graph will display the top five stores.
      


## 

1. Add a new SqlDatasource component for the graph with the following query:
            


	              SELECT DISTINCT YEAR(OrderDate) AS Year
              FROM         Sales.SalesOrderHeader
              ORDER BY Year
            




1. Rename the data source to 
__yearDataSource
__.
            


1. Right-click outside the report. Select 
__Report Parameters
__ to add the 
[Overview]({%slug telerikreporting/designing-reports/connecting-to-data/report-parameters/overview%})
 of the year.
            


1. Set 
__ReportYear
__ as in the following way:
            
  
  ![RP](images/RP.PNG)

1. Right-click 
__graphDataSource
__. Select 
__Configure
__ and click 
__Next
__              until the 
__Configure data source command
__ is displayed.
            


1. Change the 
WHERE
 clause in the following way:
            


	              WHERE  (YEAR(SOH.OrderDate) = @Year)
            




1. Set 
__Configure data source parameters
__ dialog in the following way:
            
  
  ![CDP](images/CDP.PNG)

1. Set 
__Configure Design Time Parameters
__:
            


* __Name
__: 
@Year


* __Value
__: 
2002
As a result, the year that will be displayed by default will be 2002.


1. Click 
__Next
__ and 
__Finish
__.
            


## Previewing the Result

Preview the result by clicking 
__Preview
__ > 
__PrintPreview
__.
        
  
  ![Report Parameter Preview](images/ReportParameterPreview.PNG)

## Next Steps

* [How to Add Column Graph]({%slug telerikreporting/getting-started/how-to-add-column-graph%})


## Previous Steps

* [First Steps]({%slug telerikreporting/getting-started/first-steps%})


* [Creating the Demo Report]({%slug telerikreporting/getting-started/creating-the-demo-report%})


* [Setting the Page Header]({%slug telerikreporting/getting-started/setting-the-page-header%})


* [Creating the Table and Populating it with Data]({%slug telerikreporting/getting-started/creating-the-table-and-populating-it-with-data%})


* [Creating the Graph]({%slug telerikreporting/getting-started/creating-the-graph%})


* [Setting the Page Footer]({%slug telerikreporting/getting-started/setting-the-page-footer%})


* [Integrating the Report in VS App]({%slug telerikreporting/getting-started/integrating-the-report-in-vs-app%})

