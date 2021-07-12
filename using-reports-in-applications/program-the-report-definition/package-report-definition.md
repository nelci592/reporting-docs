---
title: Package Report Definition
page_title: Package Report Definition | for Telerik Reporting Documentation
description: Package Report Definition
slug: telerikreporting/using-reports-in-applications/program-the-report-definition/package-report-definition
tags: package,report,definition
published: True
position: 6
---

# Package Report Definition



The T:Telerik.Reporting.ReportPackager
        serializes the report definition in XML and with a zip compression packages the definition and its resources.
        The resources are in their native format and archived for better performance.
        This way the definition is faster to handle and more compact.
        This is the default report document format for the [Overview]({%slug telerikreporting/designing-reports/report-designer-tools/overview%}).
      

## Packaging .TRDX report definition

The following sample code snipped demonstrates how to package a predefined .TRDX (XML) report definition:

	



	



## Packaging CLR report definition

The following sample code snipped demonstrates how to package a predefined CLR report definition:

	



	



## Unpackaging

The following sample code snipped demonstrates how to unpackage a predefined .TRDP report definition:

	



	



# See Also

 * [Overview]({%slug telerikreporting/designing-reports/report-designer-tools/overview%})
