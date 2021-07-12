---
title: How to Configure an MSSQL Database Storage
page_title: How to Configure an MSSQL Database Storage | for Telerik Reporting Documentation
description: How to Configure an MSSQL Database Storage
slug: telerikreporting/using-reports-in-applications/host-the-report-engine-remotely/telerik-reporting-rest-services/rest-service-storage/how-to-configure-an-mssql-database-storage
tags: how,to,configure,an,mssql,database,storage
published: True
position: 1
---

# How to Configure an MSSQL Database Storage



This article will explain how to configure an MSSQL database for report engine storage.How to configure an MSSQL database storage:

Ensure a database instance is available for report engine storage.
            This may be a dedicated database or a shared database for both app data
            and report engine storage.

Start the __Telerik Database Cache Configurator__
            tool located in the *{Telerik Reporting installation folder}/Tools* folder.
          

In *Choose database usage* combo-box select the "Configure REST service storage database" option.
            

In *Choose target backend* combo-box select the "Microsoft SQL Server" option.
            

In *Specify connection string* text box enter the connection string that references the target database. 
              You can also click the *Build* button and create the connection string using the *Connection properties* form.
            

Click on the *Create schema* button to start the database schema creation.
            

A message box should be displayed, confirming that the storage tables are successfully created. Use the connection string specified above when initializing an instance of T:Telerik.Reporting.Cache.MsSqlServerStorage in your application.
            

In case you want to cleanup the storage tables in an existing database, use the button *Clear cache data*.
            

 * [Overview]({%slug telerikreporting/using-reports-in-applications/host-the-report-engine-remotely/telerik-reporting-rest-services/rest-service-storage/overview%})
