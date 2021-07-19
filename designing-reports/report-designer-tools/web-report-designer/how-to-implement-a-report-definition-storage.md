---
title: How to implement a report definition storage
page_title: How to implement a report definition storage | for Telerik Reporting Documentation
description: How to implement a report definition storage
slug: telerikreporting/designing-reports/report-designer-tools/web-report-designer/how-to-implement-a-report-definition-storage
tags: how,to,implement,a,report,definition,storage
published: True
position: 5
---

# How to implement a report definition storage



This article describes how to use the Web Report Designer to design reports that are stored in a custom storage location.
      

## Overview

Out-of-the-box we provide a __FileDefinitionStorage__ that is configured to use the file system.
          To open reports stored differently, you need to implement the __IDefinitionStorage__ interface.
          This will enable the web designer to load reports from a custom location, such as a database, cloud, in-memory, etc.
        

The *byte[]* returned by the *GetDefinition* method of the
          *IDefinitionStorage* will be processed by the virtual *GetReport*
          method of the *ReportDesignerController*. The default implementation of the
          *GetReport* method utilizes the *definitionId*s returned by the
          *ListDefinitions* method of the *IDefinitionStorage* to identify
          the type of the report definition in the *byte[]*. If the
          *definitionId* contains the extension '.trdp', the report will be treated as a TRDP package.
          Otherwise, the *byte[]* is regarded as an XML report definition, i.e. a TRDX report. For that
          reason, by default, if the *GetDefinition* method returns a report definition packed with the
          T:Telerik.Reporting.ReportPackager, the corresponding
          *definitionId* must finish with the '.trdp' extension. If a different behavior is required,
          it will be necessary to overload the *GetReport* method of the
          *ReportDesignerController*.
        

## Implement Custom Storage

The purpose of the report definition storage is to describe how to browse, open, save, and delete reports from
          the Web Report Designer. The storage is configured as a setting of the __ReportDesignerController__.
        

	
````c#
public ReportDesignerController()
{
    ...

    this.ReportDesignerServiceConfiguration = new ReportDesignerServiceConfiguration
    {
        DefinitionStorage = new FileDefinitionStorage(this.reportsPath)
        SettingsStorage = new FileSettingsStorage(Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.ApplicationData), "Telerik Reporting"))
    };
}
          
````



The default implementation of the storage demonstrated above is the __FileDefinitionStorage__. It provides functionality for working with
          TRDP/TRDX report files stored on the server-side file system.
          To load the reports from a database, for example, change the implementation of the definition storage like this:
        

	
````c#
public class DbDefinitionStorage : IDefinitionStorage
{
    /// <summary>
    /// Lists all report definitions.
    /// </summary>
    /// <returns>A list of all report definitions present in the storage.</returns>
    public IEnumerable<string> ListDefinitions()
    {
        // Retrieve all available reports in the database and return their unique identifiers.
    }

    /// <summary>
    /// Finds a report definition by its id.
    /// </summary>
    /// <param name="definitionId">The report definition identifier.</param>
    /// <returns>The bytes of the report definition.</returns>
    public byte[] GetDefinition(string definitionId)
    {
        // Retrieve the report definition bytes from the database.
    }

    /// <summary>
    /// Creates new or overwrites an existing report definition with the provided definition bytes.
    /// </summary>
    /// <param name="definitionId">The report definition identifier.</param>
    /// <param name="definition">The new bytes of the report definition.</param>
    public void SaveDefinition(string definitionId, byte[] definition)
    {
        // Save the report definiton bytes to the database.
    }

    /// <summary>
    /// Deletes an existing report definition.
    /// </summary>
    /// <param name="definitionId">The report definition identifier.</param>
    public void DeleteDefinition(string definitionId)
    {
        // Delete the report definition from the database.
    }
}
          
````



Then you can set the new definition storage implementation in the __ReportDesignerController__.
        

	
````c#
public ReportDesignerController()
{
    ...

    this.ReportDesignerServiceConfiguration = new ReportDesignerServiceConfiguration
    {
        DefinitionStorage = new DbDefinitionStorage()
        SettingsStorage = new FileSettingsStorage(Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.ApplicationData), "Telerik Reporting"))
    };
}
          
````


