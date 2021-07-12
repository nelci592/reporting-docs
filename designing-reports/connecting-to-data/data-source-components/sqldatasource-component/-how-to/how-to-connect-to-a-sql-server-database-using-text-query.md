---
title: How to Connect to a SQL Server Database Using Text Query
page_title: How to Connect to a SQL Server Database Using Text Query | for Telerik Reporting Documentation
description: How to Connect to a SQL Server Database Using Text Query
slug: telerikreporting/designing-reports/connecting-to-data/data-source-components/sqldatasource-component/-how-to/how-to-connect-to-a-sql-server-database-using-text-query
tags: how,to,connect,to,a,sql,server,database,using,text,query
published: False
position: 0
---

# How to Connect to a SQL Server Database Using Text Query



You can connect to a Microsoft SQL Server database using the Telerik
      __SqlDataSource__ component. To do this, you need a connection string and access
      rights to a SQL Server database. Then, you can use the SqlDataSource component
      to provide data to data items (Report, Table, Chart).To connect to a SQL Server database using the SqlDataSource component

In Microsoft Visual Studio, open a Telerik Report. From the 
            Telerik Reporting suiteversion group in the Toolbox, select the 
            SqlDataSource component and click on the design surface to add it 
            to the Report.

__Choose your Data Connection__ dialog box appears.

Click __New Connection__If the __Change Data Source__ dialog box appears, click 
            __Microsoft SQL Server__, and then click __Continue__.

In the __Add Connection__ dialog box, 
            click __Change__.

In the __Change Data Source__ dialog box, click Microsoft SQL Server,
            and then click __OK__.

In the __Server name__ box, enter the name for your SQL Server database,
            and then under __Logon to the server__, enter the logon credentials.

For the logon credentials, select the option that is appropriate for accessing and running the SQL Server database (either by using Microsoft Windows integrated security or by providing a specific ID and password) and, if it is required, enter a user name and password.

In the __Select or enter a database name__ list,
            enter a valid database on the server e.g. __AdventureWorks__.

Optionally, click __Test connection__ to verify that your 
            connection works.

Click __OK__, Click __Next__ 
            to continue and select __Yes, save this connection…__. 
            Enter a name for your connection for when it is stored in the application 
            configuration file, and then click __Next.__

Select the database table or view from which to retrieve results or specify your own SQL statement.

To test your query, click __Next__, and then 
            click __Execute Query__.

Click __Finish__. The Wizard would close 
            and the SqlDataSource component would be ready for use by the data 
            items.
