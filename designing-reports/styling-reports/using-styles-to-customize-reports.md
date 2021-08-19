---
title: Using Styles to Customize Reports
page_title: Using Styles to Customize Reports | for Telerik Reporting Documentation
description: Using Styles to Customize Reports
slug: telerikreporting/designing-reports/styling-reports/using-styles-to-customize-reports
tags: using,styles,to,customize,reports
published: True
position: 0
---

# Using Styles to Customize Reports



Telerik __Reporting__ uses a built-in styling model that is similar to CSS. The model provides for very fine-grained visual customization of all elements of a report directly in the Report designer. This CSS-like mechanism offers full control over such things as the background, colors, borders, and images for every item on your report. You can assign styles by using CSS selectors such as Type, Attribute, Style, and Descendent.

## Creating a Style Sheet for a Report

To create a style sheet for a report, follow these steps:

1. Open the report in design view.

1. Select the Report object.

1. Click in the__StyleSheet__property, click the ellipsis button to open the StyleRule Collection Editor.

1. Click__Add__to add a new__StyleRule__.

1. Expand the__Style__property and customize your new__StyleRule__. For example, the screenshot below shows a__StyleRule__that specifies a yellow background, blue text, and bold Times New Roman font.  

  ![](images/Style1.png)

1. Click in the__Selectors__property, click the ellipsis button to open the TypeSelector Collection Editor.

1. Click the drop-down arrow on the__Add__button and select the type of selector to add. 
        		See the type of selectors in[Understanding Style Selectors]({%slug telerikreporting/designing-reports/styling-reports/understanding-style-selectors%})

1. Use the properties area of the TypeSelector Collection Editor to customize the new selector. For example, the screenshot below shows a__StyleSelector__named__DataField__which applies to__TextBox__report items only.  

  ![](images/Style2.png)

1. Click__OK__when you are done adding selectors for the current StyleRule.

1. Click__OK__when you are done adding StyleRules for the report's StyleSheet.

## Assigning Styles to Report Items

Telerik __Reporting__ will automatically apply styles that use __TypeSelectors__, __AttributeSelectors__, or __DescendantSelectors__ to the appropriate report items. For example, if you add a style to the report's __StyleSheet__ with a __TypeSelector__ of __Telerik.Reporting.TextBox__, that style will be inherited by all text box report items on the report.

To apply a style that uses a __StyleSelector __to a report item, select the report item and set its __StyleName__ property to the __StyleName__ property of the __StyleSelector__.

# See Also


 * [Understanding Style Selectors]({%slug telerikreporting/designing-reports/styling-reports/understanding-style-selectors%})

 * [Creating Style Rules]({%slug telerikreporting/designing-reports/styling-reports/creating-style-rules%})

 * [Exporting and Reusing Style Sheets]({%slug telerikreporting/designing-reports/styling-reports/exporting-and-reusing-style-sheets%})
