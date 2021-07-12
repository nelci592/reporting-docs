---
title: Using Report Events
page_title: Using Report Events | for Telerik Reporting Documentation
description: Using Report Events
slug: telerikreporting/using-reports-in-applications/program-the-report-definition/report-events/using-report-events
tags: using,report,events
published: True
position: 2
---

# Using Report Events



## 

The __Report__ object exposes these events:
        




| Event | Description |
| ------ | ------ |
| __ItemDataBinding__ |Fires just before the report is bound to data.|
| __NeedDataSource__ |Fires when the report does not have data source set.|
| __ItemDataBound__ |Fires just after the report is bound to data.|



The example below shows the NeedDataSource event assigning the report __DataSource__ at runtime. This event only fires when the __DataSource__ is null.
        

	



	


