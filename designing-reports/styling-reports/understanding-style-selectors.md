---
title: Understanding Style Selectors
page_title: Understanding Style Selectors | for Telerik Reporting Documentation
description: Understanding Style Selectors
slug: telerikreporting/designing-reports/styling-reports/understanding-style-selectors
tags: understanding,style,selectors
published: True
position: 1
---

# Understanding Style Selectors



Style Selectors are used to define how a style will be applied globally to items in a report. Each Style Rule that you create (either in code or using the StyleRule Collection Editor) must be created as one of the following four selectors:


* __TypeSelector
__

* __AttributeSelector
__

* __StyleSelector
__

* __DescendantSelector
__

## Understanding Style Selectors

### TypeSelector

A 
__TypeSelector
__ applies to all report items of a particular type, for example a 
__Telerik.Reporting.TextBox
__ or a 
__Telerik.Reporting.PageFooterSection
__.


When a style is defined as a 
__TypeSelector
__, the formatting for that style is automatically applied to all items on the report that match the type.


### AttributeSelector

An 
__AttributeSelector
__ applies to all report items with a particular attribute (such as Color=Red). 


Using an 
__AttributeSelector 
__Style Rule, you could specify that any report item on the report that has children (for example. where the value of the 
__HasChildren
__ property is equal to 
__True
__) should be 
__Bold
__.


### StyleSelector

A 
__StyleSelector
__ applies to all report items with a particular style name. When defining a 
__StyleSelector
__ style, use the 
__Name
__ property to create a name for the style. Each report item has a 
__StyleName
__ property. By setting the value of 
__StyleName
__ to the name of the 
__StyleSelector
__ Style Rule, that report item will display the attributes of the named style.


### DescendantSelector

A 
__DescendantSelector
__ applies to all parent/child report item combinations. The actual Style Rule for the child can be specified by any type of 
__Selector
__. 


For example, you can specify that any 
__TextBox
__ that exists inside of a 
__ReportHeaderSection
__ should have a particular style using a 
__TypeSelector
__ within the 
__DescendantSelector
__. 


Alternatively, you can create multiple 
__StyleSelector 
__Style Rules with the same Name and that descend from different report item types, such as 
__DetailSection
__ or 
__GroupSection
__. Report items with this Name value in their 
__StyleName
__ property will apply the correct style based on where they are placed in the report , even if they are moved.


# See Also


 * [Using Styles to Customize Reports]({%slug telerikreporting/designing-reports/styling-reports/using-styles-to-customize-reports%})


 * [Creating Style Rules]({%slug telerikreporting/designing-reports/styling-reports/creating-style-rules%})

