---
title: Serialize Report Definition in XML
page_title: Serialize Report Definition in XML | for Telerik Reporting Documentation
description: Serialize Report Definition in XML
slug: telerikreporting/using-reports-in-applications/program-the-report-definition/serialize-report-definition-in-xml
tags: serialize,report,definition,in,xml
published: True
position: 7
---

# Serialize Report Definition in XML



__Telerik Reporting__ supports serialization/deserialization of the report definition as plain
        __XML__. This is useful in various
        different scenarios and opens many possibilities that are not easily accomplished otherwise. For example, this allows
        adding or modifying reports in your application without recompiling or redeploying it. Another typical scenario is
        saving/loading of dynamically generated report definitions or transferring them over the network.
      

>note In order to better handle report definition resources we also provide aT:Telerik.Reporting.ReportPackagerthat serializes the report definition in XML and packages it together with its resources in a file with zip compression.
          For more information see:[Package Report Definition]({%slug telerikreporting/using-reports-in-applications/program-the-report-definition/package-report-definition%}).
>


## Class Report Definition

The __XML__ serialization/deserialization of report definitions is achieved through the dedicated
          T:Telerik.Reporting.XmlSerialization.ReportXmlSerializer
          class. To illustrate how a report is serialized and deserialized, let us start with a simple dynamically generated class report definition:
        

	



	



## Serialize to XML

The following sample code snipped demonstrates how to serialize the above report definition to an XML file:

	



	



## Deserialize from XML

The corresponding code that can be used to deserialize the report definition from the file is shown below:

	



	



## XML Report Definition

and the resulting XML file would look like this:

	


