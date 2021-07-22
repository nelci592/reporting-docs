---
title: Setting the Page Footer
page_title: Setting the Page Footer | for Telerik Reporting Documentation
description: Setting the Page Footer
slug: telerikreporting/getting-started/setting-the-page-footer
tags: setting,the,page,footer
published: True
position: 5
---

# Setting the Page Footer



This article is part of the Demo report guide on getting started with Telerik Reporting and demonstrates
        how to display the current date and time as well as the 
[Overview]({%slug telerikreporting/designing-reports/report-structure/barcode/overview%})
 item.
      


## 

1. Click 
__pageFooterSection
__ and add a Textbox which will display the current date and time.
            


1. Set the 
__Value
__ property 
__Expression
__ to the 
Date
 and 
Time
 function
              
=Now()
.
            


1. From the bar, select 
__Insert
__ > 
__Barcode
__ to add a Barcode item.
            


1. Place the 
[https://docs.telerik.com/reporting/report-items-barcode-general
]() link in the 
__Value
__              field of the 
__Barcode
__.
            


1. Set the 
__BackgroundColor
__ of the footer to 
242, 242, 242
.
            


## Previewing the Result

Preview the result by clicking 
__Preview
__ > 
__PrintPreview
__.
        
  
  ![Footer Added](images/FooterAdded.PNG)

## Next Steps

* [Integrating the Report in VS App]({%slug telerikreporting/getting-started/integrating-the-report-in-vs-app%})


* [Parameterizing the Graph]({%slug telerikreporting/getting-started/parameterizing-the-graph%})


* [How to Add Column Graph]({%slug telerikreporting/getting-started/how-to-add-column-graph%})


## Previous Steps

* [First Steps]({%slug telerikreporting/getting-started/first-steps%})


* [Creating the Demo Report]({%slug telerikreporting/getting-started/creating-the-demo-report%})


* [Setting the Page Header]({%slug telerikreporting/getting-started/setting-the-page-header%})


* [Creating the Table and Populating it with Data]({%slug telerikreporting/getting-started/creating-the-table-and-populating-it-with-data%})


* [Creating the Graph]({%slug telerikreporting/getting-started/creating-the-graph%})

