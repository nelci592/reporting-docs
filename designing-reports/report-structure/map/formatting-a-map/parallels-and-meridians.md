---
title: Parallels and Meridians
page_title: Parallels and Meridians | for Telerik Reporting Documentation
description: Parallels and Meridians
slug: telerikreporting/designing-reports/report-structure/map/formatting-a-map/parallels-and-meridians
tags: parallels,and,meridians
published: True
position: 1
---

# Parallels and Meridians



The parallels and meridians represent the coordinate system grid, called 
*graticule
*.
        You can format the graticule using the 
__Property Browser
__.
      
Graticule Step


Both parallels and meridians define a step that determines the density of their lines. By default the step value is 
__NaN
__, which
          causes the graticule lines to be automatically adjusted depending on the current map extent.
          The smaller the extent is, the smaller the graticule step becomes.
        
To change the Parallels or Meridians step:


Click the map item that you want to change.
                The selected map properties are listed in the 
__Property Browser
__.
              


Expand the 
__Parallels/Meridians property
__.
              


Select the 
__Step
__ property and set it to the desired value.
              


When you are done, press 
__Enter
__.
              
Graticule Style


You can change the parallels and meridians style by selecting the property and using the 
__Property Browser
__ change Style properties.
        
To change the Parallels or Meridians style:


Click the map item that you want to change.
                  The selected map properties are listed in the 
__Property Browser
__.
                


Expand the 
__Parallels/Meridians property
__.
                


In the 
__Style property
__, click the 
__Edit Collection (…) button
__.
                


The Edit style dialog opens.
                


When you are done, click OK.
                


# See Also
[GraticuleLine](/reporting/api/Telerik.Reporting.GraticuleLine)
[Style](/reporting/api/Telerik.Reporting.Drawing.Style)


 * [Map Overview]({%slug telerikreporting/designing-reports/report-structure/map/structure/overview%})


 * [Map Structure]({%slug telerikreporting/designing-reports/report-structure/map/structure/overview%})

