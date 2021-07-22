---
title: How to Connect to a SQL Server Database Using Stored Procedure
page_title: How to Connect to a SQL Server Database Using Stored Procedure | for Telerik Reporting Documentation
description: How to Connect to a SQL Server Database Using Stored Procedure
slug: telerikreporting/designing-reports/connecting-to-data/data-source-components/sqldatasource-component/-how-to/how-to-connect-to-a-sql-server-database-using-stored-procedure
tags: how,to,connect,to,a,sql,server,database,using,stored,procedure
published: False
position: 1
---

# How to Connect to a SQL Server Database Using Stored Procedure



You can connect to a Microsoft SQL Server database using the Telerik
      
__SqlDataSource
__ component. To do this, you need a connection string and access
      rights to a SQL Server database. Then, you can use the SqlDataSource component
      to provide data to data items (Report, Table, Chart).
To connect to a SQL Server database using the SqlDataSource component


In Microsoft Visual Studio, open a Telerik Report. From the 
            Telerik Reporting 
{{site.suiteversion
}} group in the Toolbox, select the 
            SqlDataSource component and click on the design surface to add it 
            to the Report.


__Choose your Data Connection
__ dialog box appears.


Click 
__New Connection
__If the 
__Change Data Source
__ dialog box appears, click 
            
__Microsoft SQL Server
__, and then click 
__Continue
__.


In the 
__Add Connection
__ dialog box, 
            click 
__Change
__.


In the 
__Change Data Source
__ dialog box, click Microsoft SQL Server,
            and then click 
__OK
__.


In the 
__Server name
__ box, enter the name for your SQL Server database,
            and then under 
__Logon to the server
__, enter the logon credentials.


For the logon credentials, select the option that is appropriate for accessing and running the SQL Server database (either by using Microsoft Windows integrated security or by providing a specific ID and password) and, if it is required, enter a user name and password.


In the 
__Select or enter a database name
__ list,
            enter a valid database on the server e.g. 
__AdventureWorks
__.


Optionally, click 
__Test connection
__ to verify that your 
            connection works.


Click 
__OK
__, Click 
__Next
__ 
            to continue and select 
__Yes, save this connection…
__. 
            Enter a name for your connection for when it is stored in the application 
            configuration file, and then click 
__Next.
__

Select the stored procedure from which to retrieve results
            e.g. 
__uspGetEmployeeManagers
__ and click Next.


If the stored procedure has a parameter, the 
__Configure Data 
            Source Parameters
__ step shows. You can leave the sql parameter value 
            blank and continue, create an expression or create a report parameter
            as values. Choosing the last option would give you ability to use the
            built-in report parameters to specify value at run time. The 
            SqlDataSource component submits the text in the SelectCommand property
            to the database, and the database returns the result of the stored 
            procedure back to the SqlDataSource component. Any data items that are 
            bound to the data source component would display the result set on your 
            report.


To test your query, click 
__Next
__, and then 
            click 
__Execute Query
__.


Click 
__Finish
__. The Wizard would close 
            and the SqlDataSource component would be ready for use by the data 
            items.

