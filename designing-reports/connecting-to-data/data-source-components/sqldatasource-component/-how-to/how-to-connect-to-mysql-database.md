---
title: How to Connect to MySQL Database
page_title: How to Connect to MySQL Database | for Telerik Reporting Documentation
description: How to Connect to MySQL Database
slug: telerikreporting/designing-reports/connecting-to-data/data-source-components/sqldatasource-component/-how-to/how-to-connect-to-mysql-database
tags: how,to,connect,to,mysql,database
published: False
position: 5
---

# How to Connect to MySQL Database



You can use the SqlDataSource component to connect to MySQL 
      database. Prior to this, you should install .NET connector. You need access 
      rights to a MySQL Server database with relevant server and authentication 
      information. Then, you can use the SqlDataSource component to provide data 
      to data items (Report, Table, Chart).
To use the SqlDataSource control to connect to MySql database


In Microsoft Visual Studio, open a Telerik Report. From the 
            Telerik Reporting 
{{site.suiteversion
}} group in the Toolbox, select the 
            SqlDataSource component and click on the design surface to add it 
            to the Report.


__Choose your Data Connection
__ dialog box 
            appears.


Click 
__New Connection.
__

In the 
__Add Connection
__ dialog box, 
            click 
__Change
__ to display the Change Data 
            Source dialog box.


In the 
__Data source
__ list, click 
__MySQL 
            Database
__ and then click 
__Ok
__

The 
__Add Connection
__ dialog box is displayed. 
            In the 
__Server name
__ box, type the name of the MySql server.


Type the user name and password to connect with the database.


Select the 
__Save my password
__ box to save 
            authentication information as part of the connection string, select 
            DataBase name and then click 
__OK
__.


You are returned to the 
__Choose Your Data Connection
__ 
            dialog with the new connection string information displayed.


Click 
__Next
__ and Select the 
__Yes, save this connection…
__ check box.
            Enter a name for your connection for when the connection is stored in 
            the application configuration file, and then click 
__Next
__.


Select the database table, view, or stored procedure from 
            which to retrieve results or specify your own SQL statement. 


To test your query, click 
__Next
__, and 
            then click 
__Execute Query
__.


Click 
__Finish
__. The Wizard would close 
            and the SqlDataSource component would be ready for use by the data items

