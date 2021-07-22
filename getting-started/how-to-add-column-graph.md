---
title: How to Add Column Graph
page_title: How to Add Column Graph | for Telerik Reporting Documentation
description: How to Add Column Graph
slug: telerikreporting/getting-started/how-to-add-column-graph
tags: how,to,add,column,graph
published: True
position: 8
---

# How to Add Column Graph



This article is part of the Demo report guide on getting started with Telerik Reporting and demonstrates
        how to add a new graph which will display the top five stores per year and per quarter.
      


## 

1. Go to 
__Insert
__ > 
__Bar
__ > 
__Clustered Bar
__.
            


1. From 
__Graph Wizard
__, drag 
__StoreName
__ to 
__Categories
__,
              
__OrderDate
__ to 
__Series
__, and 
__Sum(LineTotal)
__ to 
__Values
__.
            


1. Sort and filter the series groups and the category groups. You can also set specific colors through the 
__Color palette
__ option.
            
Set the series groups in the folowing way:
            


* __Grouping
__: 
=Quarter(Fields.OrderDate)


* __Sorting
__: 
=Quarter(Fields.OrderDate) ASC
Set the cetagories grpups in the following way:
            


* __Filtering
__:
                


* __Expression
__: 
=Sum(Fields.LineTotal)


* __Operator
__: 
Top N


* __Value
__: 
=5


* __Sorting
__: 
=Quarter(Fields.OrderDate) ASC


## Previewing the Result

Preview the result by clicking 
__Preview
__ > 
__PrintPreview
__.
        
  
  ![FinalGS](images/FinalGS.PNG)

## Previous Steps

* [First Steps]({%slug telerikreporting/getting-started/first-steps%})


* [Creating the Demo Report]({%slug telerikreporting/getting-started/creating-the-demo-report%})


* [Setting the Page Header]({%slug telerikreporting/getting-started/setting-the-page-header%})


* [Creating the Table and Populating it with Data]({%slug telerikreporting/getting-started/creating-the-table-and-populating-it-with-data%})


* [Creating the Graph]({%slug telerikreporting/getting-started/creating-the-graph%})


* [Setting the Page Footer]({%slug telerikreporting/getting-started/setting-the-page-footer%})


* [Integrating the Report in VS App]({%slug telerikreporting/getting-started/integrating-the-report-in-vs-app%})


* [Parameterizing the Graph]({%slug telerikreporting/getting-started/parameterizing-the-graph%})


## See Also

[Overview]({%slug telerikreporting/designing-reports/overview%})

