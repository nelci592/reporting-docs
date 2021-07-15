---
title: Using Section Events
page_title: Using Section Events | for Telerik Reporting Documentation
description: Using Section Events
slug: telerikreporting/using-reports-in-applications/program-the-report-definition/report-events/using-section-events
tags: using,section,events
published: True
position: 3
---

# Using Section Events



## 

The various report __Section__ objects expose these events:
        




| Event | Description |
| ------ | ------ |
| __ItemDataBinding__ |Fires just before the section is bound to data.|
| __ItemDataBound__ |Fires just after the section is bound to data|






In ItemDataBinding and ItemDataBound events use the "sender" argument of the event handler to get a
          reference to the section object. From the section object you can reference any of the items the section contains,
          i.e. TextBoxes, PictureBoxes, etc. You can also use the section DataObject property to access the data fields
          for the section.
        

>tip Be aware that the "sender" section object is of type             __Telerik.Reporting.Processing.ReportItemBase__ , not the            definition item  __Telerik.Reporting.ReportItemBase__ .          


The example below demonstrates getting a reference to the detail section of the report and finding a specific
          TextBox within the section. The example also shows retrieving data source column values for the section and
          using it to alter the TextBox. 

The second example demonstrates getting a reference to the detail section of the report, finding all its children and setting a BackgroundColor to them:

	



	



	



	


