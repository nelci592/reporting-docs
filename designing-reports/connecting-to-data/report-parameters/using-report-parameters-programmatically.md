---
title: Using Report Parameters programmatically
page_title: Using Report Parameters programmatically | for Telerik Reporting Documentation
description: Using Report Parameters programmatically
slug: telerikreporting/designing-reports/connecting-to-data/report-parameters/using-report-parameters-programmatically
tags: using,report,parameters,programmatically
published: True
position: 3
---

# Using Report Parameters programmatically



## 

In the report viewing application you can populate the values of 
        __ReportParameters__ collection members prior to displaying the report.

	



	



At runtime you can access the report parameters through the 
        P:Telerik.Reporting.Processing.Report.Parameters
        dictionary. Each T:Telerik.Reporting.Processing.Parameter
        object contains resolved available values, current value and label. 
        The label returns the currently selected DisplayMember
        from the available values (if available values are defined).

>note Prior to version 2010 Q1 the processing report exposes a dictionary           containing only the current values of the report parameters.
Example:

1. Create a __Telerik Report__

1. Use the instructions from the [How to: Connect to a SQL Server Database Using Stored Procedure]({%slug telerikreporting/designing-reports/connecting-to-data/data-source-components/sqldatasource-component/-how-to/how-to-connect-to-a-sql-server-database-using-stored-procedure%}) 
  article to bind to the __uspGetManagerEmployees__ stored procedure from the __AdventureWorks__ table. 

1. Leave the Value for the __@ManagerID__ data source parameter empty and finish the wizard.

1. Create the following layout for the report
    
  ![](images/DesignParameters008.png)

1. [Add a report 
   parameter]({%slug telerikreporting/designing-reports/connecting-to-data/report-parameters/how-to-add-report-parameters%}) and name it __ManagerID__.

1. Change its Type to Integer.

1. Set its Visible property to True.

1. Expand the __AvailableValues__ and bind it to 
  __SqlDataSource__ component with
  the following query:
  

	



1. Set the __ValueMember__ to __= Fields.ManagerID__.

1. Set the __DisplayMember__ to __= Fields.Name__.

1. Add grouping for the report with __= Fields.ManagerID__ as grouping expression.

1. Wire the [NeedDataSource event]({%slug telerikreporting/designing-reports/connecting-to-data/data-items/using-the-needdatasource-event-to-connect-data%}) of the report.

1. In the report.cs file set the __DataSource__ property
   to __null__ (__Nothing__ in VB.NET) 
   so that NeedDataSource event is fired.

1. Add the following code to the NeedDataSource event handler:
   

	



	



1. [Display the Report]({%slug telerikreporting/quickstart/displaying-reports-in-winforms-report-viewer%})
   in a report viewer.

1. Select a parameter from the available values in the parameter editor 
   and click __Preview__.
     
  ![](images/DesignParameters009.png)

# See Also