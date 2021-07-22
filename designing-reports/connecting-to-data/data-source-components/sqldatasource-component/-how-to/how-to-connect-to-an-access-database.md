---
title: How to Connect to an Access Database
page_title: How to Connect to an Access Database | for Telerik Reporting Documentation
description: How to Connect to an Access Database
slug: telerikreporting/designing-reports/connecting-to-data/data-source-components/sqldatasource-component/-how-to/how-to-connect-to-an-access-database
tags: how,to,connect,to,an,access,database
published: False
position: 2
---

# How to Connect to an Access Database



You can connect to a Microsoft Access database using the Telerik 
      SqlDataSource component. To do this, you need a connection string and an 
      Access data file. Then, you can use the SqlDataSource component to provide 
      data to data items (Report, Table, Chart).
To connect to an Access database using the SqlDataSource control


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
__New Connection
__If the 
__Change Data Source
__ dialog box appears, click 
            
__Microsoft Access Database File
__, and then click 
__Continue
__.


In the 
__Add Connection
__ dialog box, 
            click 
__Change
__, in the 
__Change
            Data Sourc
__e dialog box, click 
__Microsoft 
            Access Database File
__, and
            then click OK.


In the 
__Database file name
__ box, enter a path to the Access database,
            and then under 
__Log on to the database
__, enter your logon credentials, 
            if they are required.


Optionally, click 
__Test connection
__ to 
            verify that the connection to the Access database succeeds.


Click 
__OK
__ and notice that in the 
__Data Connection
__ - 
            ```<Datasourcename>``` combobox, your new connection is selected.


Click 
__Next
__ and Select the 
            
__Yes, save this connection…
__ check box,
            enter a name for your connection for when the connection is stored in 
            the application configuration file, and then click 
__Next
__.


Select the database table from which to retrieve results or enter your own SQL 
            statement.


To test your query, click 
__Next
__, and then
            click 
__Execute Query
__

Click 
__Finish
__. The Wizard would close and the SqlDataSource 
            component would be ready for usage by the data items.


>note Parametrized Access Queries (stored procedures) are not supported, because 	the OLE DB provider cannot retrieve the procedures' parameter information.

