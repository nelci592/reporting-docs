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



The 
__OpenAccessDataSource
__ component enables data items to connect to an 
__Telerik Data Access Model
__. This allows
        seamless integration of 
__Telerik Reporting
__ with applications or web sites that utilize 
__Telerik Data Access
__.
        There are several main benefits when using the 
__OpenAccessDataSource
__ component for connecting to a
        
__Telerik Data Access Model
__:
      


* __Dedicated design-time support
__: the 
__OpenAccessDataSource
__ component has its own set of design-time editors,
            tool windows, and a configuration wizard. In addition to this, 
__OpenAccessDataSource
__ adds
            support for entity schema in 
__Data Explorer
__ and live data preview of the report in
            
__Report Designer
__.
          


* __Configuring database connectivity
__: the 
__OpenAccessDataSource
__ component
            offers an additional level of control over the database connectivity of the 
__Telerik Data Access Model
__. You can
            specify a connection string or a named connection from the configuration file of the main application or web site.
            That ensures 
__OpenAccessDataSource
__ can establish a valid database connection both at design-time and when
            running the report in production.
          


* __Maintaining OpenAccessContext lifecycle
__: the 
__OpenAccessDataSource
__ component
            allows the option to maintain the entire lifecycle of the 
__OpenAccessContext
__ automatically. It can create its
            own instance of the 
__OpenAccessContext
__ internally, keep it alive for the duration of the report generation process,
            and then destroy it automatically when it is no longer needed by the reporting engine.
          


## Supported developer platforms

* .NET Framework 4.0 and above
            


# See Also

