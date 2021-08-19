---
title: OpenAccessDataSource Component Overview
page_title: Overview | for Telerik Reporting Documentation
description: Overview
slug: telerikreporting/designing-reports/connecting-to-data/data-source-components/openaccessdatasource-component/overview
tags: overview
published: True
position: 0
---

# OpenAccessDataSource Component Overview



The __OpenAccessDataSource__ component enables data items to connect to an __Telerik Data Access Model__. This allows         seamless integration of __Telerik Reporting__ with applications or web sites that utilize __Telerik Data Access__.         There are several main benefits when using the __OpenAccessDataSource__ component for connecting to a         __Telerik Data Access Model__:       

* __Dedicated design-time support__: the__OpenAccessDataSource__component has its own set of design-time editors,
            tool windows, and a configuration wizard. In addition to this,__OpenAccessDataSource__adds
            support for entity schema in__Data Explorer__and live data preview of the report in__Report Designer__.

* __Configuring database connectivity__: the__OpenAccessDataSource__component
            offers an additional level of control over the database connectivity of the__Telerik Data Access Model__. You can
            specify a connection string or a named connection from the configuration file of the main application or web site.
            That ensures__OpenAccessDataSource__can establish a valid database connection both at design-time and when
            running the report in production.

* __Maintaining OpenAccessContext lifecycle__: the__OpenAccessDataSource__component
            allows the option to maintain the entire lifecycle of the__OpenAccessContext__automatically. It can create its
            own instance of the__OpenAccessContext__internally, keep it alive for the duration of the report generation process,
            and then destroy it automatically when it is no longer needed by the reporting engine.

## Supported developer platforms

* .NET Framework 4.0 and above             

# See Also

