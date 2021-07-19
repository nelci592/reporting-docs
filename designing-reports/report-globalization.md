---
title: Report Globalization
page_title: Report Globalization | for Telerik Reporting Documentation
description: Report Globalization
slug: telerikreporting/designing-reports/report-globalization
tags: report,globalization
published: True
position: 11
---

# Report Globalization



Telerik Reporting offers the possibility to control the way numbers, dates and currencies are displayed and to layout text in different directions.

A report is globalized with the help of a [System.Globalization.CultureInfo](http://msdn2.microsoft.com/en-us/library/system.globalization.cultureinfo.aspx) object. You can specify a Culture for the entire
[T:Telerik.Reporting.Report]()
by setting its 
[P:Telerik.Reporting.Report.Culture]()
property. This will force all 
[T:Telerik.Reporting.TextBox]() items to respect the assigned Culture. But you are not limited by one culture per report. You can mix an unlimited number of cultures, by setting the 
[P:Telerik.Reporting.TextItemBase.Culture]()
 property of a specific 
[T:Telerik.Reporting.TextBox](). This will override the Report's Culture.

## Culture Inheritance

When determining what Culture to use for formatting strings and text direction, the rendering engine will inspect the those objects in the following order:

1. The Culture of the __TextBox__.

1. If the TextBox has no Culture defined, the Culture of the __Report__ is used.

1. If the Report has no Culture defined, the Culture of the __CurrentThread__ is used.

>tip         	The Culture of the CurrentThread is determined by the Regional Settings of the machine the application is running on. (Control Panel->Regional Settings->Regional Options->Standards And Formats)        


## Culture Dependant Properties

* __String Formatting__

Culture affects the way strings are formatted in Telerik Reporting. For example, if you set the British Culture (en-GB) for a TextBox and set its 
     [P:Telerik.Reporting.Processing.TextItemBase.Format]()
to Currency ({0:C2}) you will see values like: £43.21. Same applies for dates, times and numbers.

* __Text Direction (LTR/RTL)__

Middle Eastern languages such as Hebrew and Arabic are generally written from right to left. If your TextBox will contain text written using a RTL script, then you simply need to specify the appropriate Culture, for example "he" for Hebrew and "ar" for Arabic.
