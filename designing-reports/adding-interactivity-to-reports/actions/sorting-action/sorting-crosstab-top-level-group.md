---
title: Sorting Crosstab Top-Level Group
page_title: Sorting Crosstab Top-Level Group | for Telerik Reporting Documentation
description: Sorting Crosstab Top-Level Group
slug: telerikreporting/designing-reports/adding-interactivity-to-reports/actions/sorting-action/sorting-crosstab-top-level-group
tags: sorting,crosstab,top-level,group
published: True
position: 3
---

# Sorting Crosstab Top-Level Group



Prerequisites:
      


* Reporting installation with the Examples feature 
        			


* MS SQL server with AdventureWorks
        			


The examples are located in (Replace: Reporting X with your installation version)
      


* Standalone Report Designer - %PROGRAMFILES(x86)%\Reporting X\Report Designer\Examples
        			


* Visual Studio Integrated Designer – %PROGRAMFILES(x86)%\Reporting X\Examples\CSharp\
        			


## 

Add an interactive sorting button to crosstab header (top-level static group or corner item) 
        	to enable interactive sort for top level group in a crosstab. The order of the child groups remains unchanged.
        	


1. Open in report design view the Product Sales example report.
        		


1. In report design view, select the crosstab corner with (USD IN THOUSANDS) text;
        		


1. From 
__Properties window
__ open the 
__Actions
__ editor.
        		


1. Select 
__Sorting
__ option.
        		


1. Click 
__Edit sort targets
__ button to open Edit Sorting Action targets editor.
        		


1. Click 
__New
__ to add a new target.
        		


1. Select the target dynamic group (ProductCategory) from the drop down. 
        		


1. Click 
__OK
__.
        		


1. In the Sort expressions drop-down select the field that corresponds to the column for which you are defining a sorting action. 
        		In this example this is  =Fields.ProductCategory.
        		
Specifying a sort expression is required.


1. Click 
__OK
__.
        		


To verify the sorting action, preview the report, and then click the interactive sorting button. 
        	

