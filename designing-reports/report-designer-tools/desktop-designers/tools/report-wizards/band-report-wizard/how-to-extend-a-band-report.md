---
title: How to extend a Band Report
page_title: How to extend a Band Report | for Telerik Reporting Documentation
description: How to extend a Band Report
slug: telerikreporting/designing-reports/report-designer-tools/desktop-designers/tools/report-wizards/band-report-wizard/how-to-extend-a-band-report
tags: how,to,extend,a,band,report
published: True
position: 2
---

# How to extend a Band Report



This topic will extend the example 
[Creating a Simple Report]({%slug telerikreporting/designing-reports/report-designer-tools/desktop-designers/tools/report-wizards/band-report-wizard/how-to-use-the-report-wizard-to-create-a-band-report%})
 to show several unique Telerik Reporting features including:
      


* In Place Editing.


* Copying and pasting styles.


* Conditional formatting.


* Navigating and sizing report items.


* Resizing report sections.


* Adding Text, Shape and PictureBox report items to the report designer.


* Using the Data Explorer.


* Using the Report Explorer.


Use the report design created in 
[Creating a Simple Report]({%slug telerikreporting/designing-reports/report-designer-tools/desktop-designers/tools/report-wizards/band-report-wizard/how-to-use-the-report-wizard-to-create-a-band-report%})
 as a starting point.
      


1. Double click the "ProductList" TextBox report item in the report header. This will activate
            the "in place" editor, allowing you to enter text right in the designer without having to find the
            appropriate property in the Property Window. Add a space so the TextBox reads "Product List".
          
  
  ![](images/QuickStart021.png)

1. __Zoom
__ to 150% from the 
__Zoom Combo Box
__            in the lower left corner of the design surface.
          


* For 
[Visual Studio Report Designer]({%slug telerikreporting/designing-reports/report-designer-tools/desktop-designers/visual-studio-report-designer/overview%})
:
              
From the 
__ToolBox
__ window drag a 
__TextBox
__ item to the report
                header just to the right of the "Quantity" column. While dragging the TextBox, the
                
__Snap Lines
__ will aid you in positioning it so it aligns
                nicely with its neighbors.
              
  
  ![](images/QuickStart023.png)

* For 
[Standalone Report Designer]({%slug telerikreporting/designing-reports/report-designer-tools/desktop-designers/standalone-report-designer/overview%})
:
              
Select the target 
[report section]({%slug telerikreporting/designing-reports/report-structure/overview%})
 and from the Insert tab click on the TextBox item.
                The TextBox item is added to the selected report section and with dragging you can position the TextBox in the correct location.
              
Double-click the 
__TextBox
__ 
            and enter "Reorder".
          


1. Select the "Quantity" TextBox and copy the style rule applied in the 
__StyleName
__ property. Select the "Reorder" field and paste the style rule in its 
__StyleName
__ property.
          


1. In these next steps you define a circle Shape item that reacts to changes in the data
            so that when inventory falls below 50% of the "reorder point" quantity the circle will be
            filled in red.
          
Add a new 
__Shape
__ item to the detail section just below the "Reorder"
            column. In the 
__Properties
__ window set the 
__Size.Width
__            property to "0.1in" and the 
__Size.Height
__ property to "0.1in". Right click the
            
__Shape
__ item and select 
__Conditional Formatting
__            from the context menu.
          
  
  ![](images/QuickStart025.png)

1. The 
__Conditional Formatting Rules
__ dialog will display.
          


* Click the 
__New Rule
__ button and a new row will be added in the grid.
              


* The 
__Edit Filters
__ dialog will display on clicking in the Filters cell. 
              


* Click the 
__New
__ button to create a rule. Use the drop down lists to set 
                
__Expression
__ to Fields.Quantity, 
__Operator
__ 
                to "<" and 
__Value
__ to "```<Expression>```". When you select 
                "```<Expression>```" the 
__Edit Expression
__ dialog displays. 
                This dialog allows you to select from predefined data (i.e. constants, database fields, report parameters, etc.) 
                and create an expression with them.
              


* Select 
__Fields
__ from the list on the bottom right of the dialog.
              


* Double-click "ReorderPoint" from the bottom middle list to add it to the expression.
              


* Add to the expression at the top of the dialog so the complete expression reads "= Fields.ReorderPoint * .5". This rule will fire when the quantity of a product falls below half of the ReorderPoint value. Click 
__OK
__ to close the 
__Edit Expression
__ dialog.
              
  
  ![](images/QuickStart026.png)

* On the 
__Conditional Formatting Rules
__ dialog click the 
__Style
__ button to display the 
__Style Builder
__ dialog.
              


* Click 
__Background
__ from the list on the left and select "Red" from the 
__Background Color
__ drop down list.
              


* Click 
__OK
__ to close the dialog.Click 
__OK
__ twice more to close the remaining rule dialogs.
              
  
  ![](images/QuickStart027.png)

1. Press 
__F6
__ to build the report.
          


1. Click the 
__Preview
__ button to display the report.
            Scroll through the data and notice that the "Quantity" values that are below 50% of the
            "Reorder point" are displayed in red.
          
  
  ![](images/QuickStart028.png)

1. The last set of steps to building this report design add an image item to the
            report and format the page footer. These last steps also use the
            
[Data Explorer]({%slug telerikreporting/designing-reports/report-designer-tools/desktop-designers/tools/data-explorer%})
            and the 
[Report Explorer]({%slug telerikreporting/designing-reports/report-designer-tools/desktop-designers/tools/report-explorer%})
.
          
From the 
[Telerik Reporting menu]({%slug telerikreporting/designing-reports/report-designer-tools/desktop-designers/visual-studio-report-designer/telerik-reporting-menu%})
            select the 
[Data Explorer]({%slug telerikreporting/designing-reports/report-designer-tools/desktop-designers/tools/data-explorer%})
.
          
  
  ![](images/QuickStart029.png)

1. Select the "ThumbNailPhoto" column from the
            
[Data Explorer]({%slug telerikreporting/designing-reports/report-designer-tools/desktop-designers/visual-studio-report-designer/overview%})
            list and drag it to the detail section of the report designer, just to the right of the "Reorder" column.
            Notice that this step automatically creates a
            
[PictureBox]({%slug telerikreporting/designing-reports/report-structure/picturebox%})
 report item.
          


1. After dropping the ThumbNailPhoto the DetailSection will be automatically resized to
            accommodate the entire PictureBox item:
          
  
  ![](images/QuickStart030.png)

1. The 
[Report Explorer]({%slug telerikreporting/designing-reports/report-designer-tools/desktop-designers/tools/report-explorer%})
            provides a hierarchical view of all the report sections and items in the report design. This allows
            you to easily locate items that might otherwise be difficult to find in a visually complex report.
          
From the 
[
              Telerik
              Reporting menu
            ]({%slug telerikreporting/designing-reports/report-designer-tools/desktop-designers/visual-studio-report-designer/telerik-reporting-menu%})
 select the 
[Report Explorer]({%slug telerikreporting/designing-reports/report-designer-tools/desktop-designers/tools/report-explorer%})
.
          


1. Click "pageFooterSection1" to select the report page footer.
          


1. In the 
__Properties
__ window set the 
__Style.BackgroundColor
__            property to "LightGray".
          
  
  ![](images/QuickStart031.png)

1. Click the 
__Preview
__ button to view the report. Scroll through
            the report pages to find records that have images.
          
  
  ![](images/QuickStart033.png)
