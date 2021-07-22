---
title: How to Connect to an Oracle Database
page_title: How to Connect to an Oracle Database | for Telerik Reporting Documentation
description: How to Connect to an Oracle Database
slug: telerikreporting/designing-reports/connecting-to-data/data-source-components/sqldatasource-component/-how-to/how-to-connect-to-an-oracle-database
tags: how,to,connect,to,an,oracle,database
published: False
position: 4
---

# How to Connect to an Oracle Database



You can use the Telerik SqlDataSource component to connect to an Oracle
        database. You connect the component to an Oracle database by first establishing
        connection information in the config file, and then by referencing the
        connection information in a SqlDataSource control.
      
To use the SqlDataSource control to connect to an Oracle database


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
__ list, click Oracle
              Database and then click 
__Ok
__.
            


The 
__Add Connection
__ dialog box is displayed. In the
              
__Server name
__ box, type the name of the Oracle server.
            


Type the user name and password to connect with the database.


Select 
__Save my password
__ box to save
              authentication information as part of the connection string, and
              then click 
__OK
__.
            


You are returned to the 
__Choose Your Data Connection
__              dialog with the new connection string information displayed.
            


Click 
__Next
__ and Select the
              
__Yes, save this connection…
__ check box.
              Enter a name for your connection for when the connection is stored
              in the application configuration file, and then click 
__Next
__.
            


Select the database table, view, or stored procedure from which
              to retrieve results or specify your own SQL statement.
            


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
            

