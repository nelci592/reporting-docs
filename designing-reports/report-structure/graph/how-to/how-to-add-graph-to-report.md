---
title: How to add Graph to Report
page_title: How to add Graph to Report | for Telerik Reporting Documentation
description: How to add Graph to Report
slug: telerikreporting/designing-reports/report-structure/graph/how-to/how-to-add-graph-to-report
tags: how,to,add,graph,to,report
published: True
position: 0
---

# How to add Graph to Report



The simplest way to add a __Graph__ item to your report is to run the Graph Wizard for Visual Studio report designer or to run 
        a *new Bar*, *Column*, *Area*, *Line*, 
        *Pie*, *Scatter*, or *Others* chart wizard in the standalone designer. 
        After you add a Graph item to the design surface, you can click the chart elements to edit the selected element's properties in the 
        *Properties* grid or in the standalone Report Designer you can use the ribbon tools.        
      To add a graph to a report by using the Visual Studio report designer Graph Wizard

Open the Visual Studio toolbox and select Graph Wizard from the Telerik Reporting tab.

Click on the design surface where you want the upper-left corner of the graph item.
              The Graph Wizard opens.
            

Follow the steps in the Graph Wizard.

When you finish the wizard a new Graph item will be created on the design surface. To add a graph to a report by using the standalone Report Designer Graph Wizard

Open the *Insert* tab from the ribbon bar and select the desired chart type.
            The graph will be placed in the center of the selected container.

Follow the steps in the Graph Wizard.

When you finish the wizard a new Graph item will be created on the design surface. 

>note Please note that the datapoint labels in the produced chart can be invisible because their default visibility depends on the selected chart type.          All charts that have visible axes, which can give you information about the measured value, have their labels visibility set to           __False__  by default. However, on some chart types like the [Pie Charts]({%slug telerikreporting/designing-reports/report-structure/graph/chart-types/pie-charts/overview%})          the labels are visible by default, while the axes are invisible.
To insert a graph to a report

>note Graph item for direct insertion is only available in the Visual Studio report designer.For the     		standalone report designer, please use a Graph wizard for the specific chart type.


Open the Visual Studio toolbox and select Graph item from the *Telerik Reporting* tab.

Click on the design surface where you want the upper-left corner of the graph item.

The graph item is initialized on the selected design surface.

Open the Property Grid.

Set the DataSource property to one of the available [Data Source Components]({%slug telerikreporting/designing-reports/connecting-to-data/data-source-components/overview%}).

Set up a Coordinate System with its x-axis and y-axis.
