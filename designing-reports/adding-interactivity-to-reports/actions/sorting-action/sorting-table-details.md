---
title: Sorting Table Details
page_title: Sorting Table Details | for Telerik Reporting Documentation
description: Sorting Table Details
slug: telerikreporting/designing-reports/adding-interactivity-to-reports/actions/sorting-action/sorting-table-details
tags: sorting,table,details
published: True
position: 1
---

# Sorting Table Details



This document demonstrates how to enable interactive sorting with the 
__Standalone Report Designer
__ or with the 
__Visual Studio Report Designer
__. 
      


## Prerequisites

To follow the steps in this guide, you need the following:
        


* A Telerik Reporting installation with an enabled 
[Examples feature
](6E821131-83F3-45A4-BB6E-1530223D1E38#installingReporting)

* Microsoft SQL Server with AdventureWorks
        			


## Procedure

The following steps describe how to add an interactive 
__sort
__ button to a column header in the 
__Detail Section
__ of a report. 
          This enables a user to click on the button and sort the table rows by the value displayed in that column.
        


1. Locate the 
__Product Catalog
__ sample report and open it 
              with the 
__Standalone Report Designer
__ or with the 
__Visual Studio Report Designer
__.
            
Depending on the Report Designer of your choice, you will locate the 
__Product Catalog
__ sample report in one of the following folders:
            


* Examples for the Standalone Report Designer - %PROGRAMFILES(x86)%\Progress\Telerik Reporting {Version}\Report Designer\Examples
                


* Examples for the Visual Studio Report Designer – %PROGRAMFILES(x86)%\Progress\Telerik Reporting {Version}\Examples\CSharp\
                


>note Replace  __{Version}__  in the Examples path with your Telerik Reporting version.              


1. In the Report Designer, make sure you use 
__Design View
__.
            


1. Select the 
__List Price
__ text box - this is the column header where we want to add an interactive sorting button.
            


1. In the 
__Properties
__ window, open the 
__Action
__ editor.
            


1. Select the 
__Sorting
__ action.
            


1. Click the 
__Select sort targets
__ button. The 
__Edit Sorting Action targets
__ window appears.
            


1. Click the 
__New
__ button to add a new target.
            


1. Select 
__table1 (Table)
__ in the drop-down and click 
__OK
__.
            


1. In the 
__Sort expressions
__ drop-down menu, select the field that corresponds to the column for which you are defining a sorting action.
              In this case, use the 
__=Fields.ListPrice
__ expression and click 
__OK
__.
            


>note Specifying a sort expression is required.


To verify the sorting action:
        


1. Preview the report


1. Navigate to 
__Bikes
__ in the document map


1. Click the 
__List Price
__ column interactive sorting button.
            

