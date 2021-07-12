---
title: Report Book Parameters
page_title: Report Book Parameters | for Telerik Reporting Documentation
description: Report Book Parameters
slug: telerikreporting/designing-reports/report-book/report-book-parameters
tags: report,book,parameters
published: True
position: 1
---

# Report Book Parameters



## Report Book Parameters

Often one or more reports that are part of a report book will contain report parameters.
          The report book is shown as a single document in the report viewer and the parameters area represents the visible report parameters defined in all child reports.
        

Telerik Reporting provides a mechanism known as parameter merging.
          If the P:Telerik.Reporting.IReportParameter.Name
          and P:Telerik.Reporting.IReportParameter.Type
          of two (or more) parameters from different reports are the same,
          then they are considered equivalent and are displayed as a single parameter in the viewer's Parameters Area.
        

>note When one or more parameters are merged the UI settings of the __first__ one are used for the generated input control in the parameters area.
>
![](images/ReportBook3_MergedParameters.png)

You can control parameter merging via the
          P:Telerik.Reporting.IReportParameter.Mergeable boolean
          property of the ReportParameter class. The default value of the Mergeable property is true. Set
          the Mergeable property to false if you want to prevent a parameter from being merged with its equivalent ones.
        ![](images/ReportBook4_MergedParameters2.png)

## Passing Values for Report Parameters in a Reportbook thru ReportSource

* __When report parameters have unique names or the target parameters are merged:__
              If a parameter is distinguishable by its Name property or the Name denotes several merged parameters,
              refer to the parameter directly by the value of its Name property.
            

	



	



* __When report parameters have repeating names but they are not merged:__
              In this case you need to refer to the individual occurrence of the parameter in a particular report.
              This is done by denoting the target report by its zero-based index inside the report book.
            

	



	



>tip If you do not use the specified syntax and you refer to the report parameter directly by Name property's value,
                the value will be set only for the first occurrence of report parameter in the report book.
>


# See Also
