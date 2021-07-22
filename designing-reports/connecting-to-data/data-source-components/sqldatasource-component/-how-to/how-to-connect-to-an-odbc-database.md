---
title: How to Connect to an ODBC Database
page_title: How to Connect to an ODBC Database | for Telerik Reporting Documentation
description: How to Connect to an ODBC Database
slug: telerikreporting/designing-reports/connecting-to-data/data-source-components/sqldatasource-component/-how-to/how-to-connect-to-an-odbc-database
tags: how,to,connect,to,an,odbc,database
published: False
position: 3
---

# How to Connect to an ODBC Database



You can use the Telerik SqlDataSource component to connect to any 
      ODBC–compliant data source. You connect the component to an ODBC data 
      source by specifying the appropriate ODBC driver in the connection string 
      along with relevant server and authentication information.
To use the SqlDataSource control to connect to an ODBC database


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
__ to display the Change Data Source dialog box.


In the 
__Change Data Source
__ dialog box, 
            click Microsoft ODBC Data Source, and then click 
__OK
__.


The 
__Add Connection
__ dialog box is displayed.
            If you have an existing ODBC data source, click 
__Use user or 
            system data source name
__ and select an existing ODBC data source from the list.


If you do not have an existing ODBC data source, click 
__Use 
            connection string
__ and then type the connection string 
            or click 
__Build
__ to display the 
            
__Select Data Source
__ dialog box where you can build an
            ODBC data source name (DSN).


If necessary, enter the user name and password required to 
            connect to the database.


Click 
__Test connection
__ to verify the connection to the ODBC data
            source, and then close the 
__Add Connection
__ dialog box to return to the
            Configure Data Source wizard.


Click 
__Next
__ and Select the 
__Yes, save 
            this connection…
__ check box. Enter a name for your connection for when the connection is stored 
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

