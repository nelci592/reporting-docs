---
title: Configure the Export Formats Overview
page_title: Overview | for Telerik Reporting Documentation
description: Overview
slug: telerikreporting/using-reports-in-applications/export-and-configure/configure-the-export-formats/overview
tags: overview
published: True
position: 0
---

# Configure the Export Formats Overview



In Telerik Reporting, the export formats take predefined parameters called *device information settings* that are used to configure a rendering extension.

You can specify device information settings in a variety of ways.
        Firstly, you can specify application-wide settings using the <Telerik.Reporting> configuration section. For more
        information about specifying rendering parameters globally, see [extensions Element]({%slug telerikreporting/using-reports-in-applications/export-and-configure/configure-the-report-engine/extensions-element%}).
      

Alternatively, you can specify device information settings per particular report as part of its definition, configuring the
        P:Telerik.Reporting.Report.RuntimeSettings
        report property. Besides setting the export parameters for particular extension it allows hiding it and changing its description
        when listed to the end-user. The property in question can be set up from the report designer tools as well.
        In case of a report book document the settings of the first report in the book get respected.
      

When exporting a report programmatically, the respective method takes a
        [HashTable](http://msdn.microsoft.com/en-us/library/system.collections.hashtable.aspx)
        argument representing the desired export parameters for this particular rendering operation:
        M:Telerik.Reporting.Processing.ReportProcessor.RenderReport(System.String,Telerik.Reporting.ReportSource,System.Collections.Hashtable).
      
