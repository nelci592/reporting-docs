---
title: How to Add LocationMapSeries to the Map Item
page_title: How to Add LocationMapSeries to the Map Item | for Telerik Reporting Documentation
description: How to Add LocationMapSeries to the Map Item
slug: telerikreporting/designing-reports/report-structure/map/how-to/how-to-add-locationmapseries-to-the-map-item
tags: how,to,add,locationmapseries,to,the,map,item
published: True
position: 5
---

# How to Add LocationMapSeries to the Map Item



The [T:Telerik.Reporting.LocationMapSeries]() are used when the data points have a single coordinate pair,
        obtained directly from the data set or by using a [Location provider]({%slug telerikreporting/designing-reports/report-structure/map/structure/location-providers%}).
      Adding a LocationMapSeries instance to the map

To add new PointMap, PieMap or a ColumnMap series to the map follow these steps:
        

1. Open __Series__ collection editor and __Add__ new
              [T:Telerik.Reporting.PointMapSeries](),
              [T:Telerik.Reporting.PieMapSeries]()
              or
              [T:Telerik.Reporting.ColumnMapSeries]()
              item.
            

1. Set the [P:Telerik.Reporting.LocationMapSeries.GeoLocationGroup]() to an existing
              [T:Telerik.Reporting.GeoLocationMapGroup]() instance or create a new one from scratch.
            

1. Set the [P:Telerik.Reporting.MapSeriesBase.SeriesGroup]() to an existing
              [T:Telerik.Reporting.MapGroup]() instance or create a new one from scratch.
            

1. 

* If you are creating a [T:Telerik.Reporting.PointMapSeries](), you can define a SeriesGroup
                  by which your data will be grouped. This might come handy if you want to have a different color for every data point in your series.
                

* If you are creating a [T:Telerik.Reporting.PieMapSeries]() or a
                  [T:Telerik.Reporting.ColumnMapSeries](), you need to define an additional child group,
                  which will be used to determine how the data will be grouped for every data point.
                  The color and count of the pie sectors (or columns when creating a [T:Telerik.Reporting.ColumnMapSeries]())
                  will be determined by the last child group of defined SeriesGroups. In the most cases
                  you would create one series group without grouping (which will result in a static group) and add one child group, with
                  [P:Telerik.Reporting.GroupBase.Groupings]()
                  set to the field you would like to group by.
                

1. Set __Size__ to an expression that will be used to determine the pie sector or the column size.
            

When all the properties are set, the __LocationMapSeries__ instance should look similar to the following one in the 
          __Property Grid__:
          
  ![Map Add Location Map Series](images/Map/Map_AddLocationMapSeries.png)

 * [Pie Charts]({%slug telerikreporting/designing-reports/report-structure/graph/chart-types/pie-charts/overview%})

 * [Column Charts]({%slug telerikreporting/designing-reports/report-structure/graph/chart-types/column-charts/overview%})

 * [Map Overview]({%slug telerikreporting/designing-reports/report-structure/map/structure/overview%})

 * [Map Structure]({%slug telerikreporting/designing-reports/report-structure/map/structure/overview%})

 * [Add ShapeMapSeries to the Map item]({%slug telerikreporting/designing-reports/report-structure/map/how-to/how-to-add-shapemapseries-to-the-map-item%})
