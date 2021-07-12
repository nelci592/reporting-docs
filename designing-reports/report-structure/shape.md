---
title: Shape
page_title: Shape | for Telerik Reporting Documentation
description: Shape
slug: telerikreporting/designing-reports/report-structure/shape
tags: shape
published: True
position: 14
---

# Shape



The Shape report item is used to display one of a selection of predefined shapes on a report. The screenshot below
        shows a Shape report item with ShapeType="Right Arrow" on the report design surface.
      ![](images/Shape.png)

You can use shapes to create visual effects within a report. You can set display and other properties to this item by
        using the Properties pane.
      

__ShapeType Property modes:__

* Ellipse
          

* Vertical Line
          

* Horizontal Line
          

* Slant Line
          

* BackSlant Line
          

* Triangle
          

* Square
          

* Pentagon
          

* Hexagon
          

* Octagon
          

* 3-ray star
          

* 4-ray star
          

* 5-ray star
          

* 6-ray star
          

* 8-ray star
          

* Top Arrow
          

* Bottom Arrow
          

* Left Arrow
          

* Right Arrow
          

* Cross
          

The Shape report item supports creating a custom shapes programmatically. The following code snippet shows how to inherit the
        T:Telerik.Reporting.Drawing.Shapes.ShapeBase class and provide a custom set of __PointF__ array
        that will form the shape. The points coordinates are relative and do not depend on the item's size or position in the report.
      

	



	



The Shape item can be created at runtime and added to a report item container (section, panel, etc.). 
        The snippet below shows how to instantiate a Shape item of __CustomShape__ type:
      

	



	



# See Also

 * [Using Styles to Customize Reports]({%slug telerikreporting/designing-reports/styling-reports/using-styles-to-customize-reports%})T:Telerik.Reporting.ShapeP:Telerik.Reporting.Shape.ShapeTypeP:Telerik.Reporting.Shape.Stretch
