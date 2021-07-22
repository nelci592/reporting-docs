---
title: Watermarks
page_title: Watermarks | for Telerik Reporting Documentation
description: Watermarks
slug: telerikreporting/designing-reports/rendering-and-paging/watermarks
tags: watermarks
published: True
position: 3
---

# Watermarks



__Watermarks
__ are text or pictures that appear commingled with the report content. They often add interest or identify status, such
        as marking a generated report as a Draft. You can see watermarks in Print Preview Layout of the report viewers and when printing or
        exporting. You have the ability to set the 
__Opacity
__ of the text or image, specify its 
__Position
__        and whether it is displayed on first (
__PrintOnFirstPage
__) and last page (
__PrintOnLastPage
__).
      


Watermarks are 
[PageSettings](/reporting/api/Telerik.Reporting.Drawing.PageSettings)
 member, processed during the paging of the report. At this moment the report data source is not available anymore, and thus data fields used in expressions would not be evaluated.
      


## Add Text Watermark using Report Designer

To add Text Watermarks to the Report use the following steps:


1. Open a report in 
__Design
__ view.
            


1. You can open the Watermarks collection editor in two ways:


* Click the Report selector button located in the upper left corner of the 
[Visual Studio Report Designer]({%slug telerikreporting/designing-reports/report-designer-tools/desktop-designers/visual-studio-report-designer/overview%})
. This makes the report active in the Properties window.
                  Expand 
__PageSettings
__ and click 
__Watermarks
__ ellipsis in the property grid.
                


* Select the Watermarks item in the report's context menu, which appears when you right-click on the designer surface.
                
Both actions will display the Watermarks collection editor, which is empty by default.
            


1. Click 
__Add
__ button and select TextWatermark.
            


1. In 
__Text
__, type or click the ellipsis to enter text or an 
[Expressions]({%slug telerikreporting/designing-reports/connecting-to-data/expressions/overview%})
 that represents the Text Watermark.
            


1. Format the text by setting 
__Color
__ and 
__Font
__ attributes.
            


1. Set 
__Opacity
__.
            


1. Set 
__Position
__. Available options are 
__Behind
__ and 
__Front
__. Default is 
__Behind
__.
            


1. Set 
__Orientation
__. Available options are 
__Horizontal
__, 
__Vertical
__ and 
__Diagonal
__. Default is 
__Horizontal
__.
            


1. Specify whether it will be displayed on first (
__PrintOnFirstPage
__) and last page (
__PrintOnLastPage
__).
            


1. Click 
__OK
__.
            


## Add Text Watermark programmatically

{{source=CodeSnippets\CS\API\Telerik\Reporting\WatermarksSnippets.cs region=AddNewTextWatermarkSnippet}}
````C#
	
	            Telerik.Reporting.Drawing.TextWatermark textWatermark1 = new Telerik.Reporting.Drawing.TextWatermark();
	            textWatermark1.Color = System.Drawing.Color.Red;
	            textWatermark1.Font.Bold = true;
	            textWatermark1.Font.Italic = false;
	            textWatermark1.Font.Name = "Arial";
	            textWatermark1.Font.Size = Telerik.Reporting.Drawing.Unit.Point(10D);
	            textWatermark1.Font.Strikeout = false;
	            textWatermark1.Font.Underline = false;
	            textWatermark1.Orientation = Telerik.Reporting.Drawing.WatermarkOrientation.Diagonal;
	            textWatermark1.Position = Telerik.Reporting.Drawing.WatermarkPosition.Behind;
	            textWatermark1.PrintOnFirstPage = true;
	            textWatermark1.PrintOnLastPage = true;
	            textWatermark1.Text = "My Test Watermark";
	            textWatermark1.Opacity = 0.3D;
	            report1.PageSettings.Watermarks.Add(textWatermark1);
	
````




{{source=CodeSnippets\VB\API\Telerik\Reporting\WatermarksSnippets.vb region=AddNewTextWatermarkSnippet}}
````VB
	
	        Dim textWatermark1 As New Telerik.Reporting.Drawing.TextWatermark()
	        textWatermark1.Color = System.Drawing.Color.Red
	        textWatermark1.Font.Bold = True
	        textWatermark1.Font.Italic = False
	        textWatermark1.Font.Name = "Arial"
	        textWatermark1.Font.Size = Telerik.Reporting.Drawing.Unit.Point(10.0)
	        textWatermark1.Font.Strikeout = False
	        textWatermark1.Font.Underline = False
	        textWatermark1.Orientation = Telerik.Reporting.Drawing.WatermarkOrientation.Diagonal
	        textWatermark1.Position = Telerik.Reporting.Drawing.WatermarkPosition.Behind
	        textWatermark1.PrintOnFirstPage = True
	        textWatermark1.PrintOnLastPage = True
	        textWatermark1.Text = "My Test Watermark"
	        textWatermark1.Opacity = 0.3
	        report1.PageSettings.Watermarks.Add(textWatermark1)
	
````




## Add Picture Watermark using Report Designer

To add Picture Watermarks to the Report use the following steps:


1. Open a report in 
__Design
__ view.
            


1. You can open the Watermarks collection editor in two ways:


* Click the Report selector button located in the upper left corner of the 
[Visual Studio Report Designer]({%slug telerikreporting/designing-reports/report-designer-tools/desktop-designers/visual-studio-report-designer/overview%})
. This makes the report active in the Properties window.
                  Expand 
__PageSettings
__ and click 
__Watermarks
__ ellipsis in the property grid.
                


* Select the Watermarks item in the report's context menu, which appears when you right-click on the designer surface.
                
Both actions will display the Watermarks collection editor, which is empty by default.
            


1. Click the small arrow on the right side of the 
__Add
__ button and select PictureWatermark from the drop-down menu.
            


1. In 
__Image
__, browse for an image file on your hard drive, input an URI (local path or URL) or an 
[Expressions]({%slug telerikreporting/designing-reports/connecting-to-data/expressions/overview%})
 that evaluates to an image.
              The 
__Image
__ field also accepts a string that represents a Base64-encoded image.
            


1. Set 
__Sizing
__ mode. Available options are Center, Stretch, ScaleProportional and TopLeft. See 
[PictureBox]({%slug telerikreporting/designing-reports/report-structure/picturebox%})
 article for more information on the modes.
            


1. Set 
__Opacity
__.
            


1. Set 
__Position
__. Available options are 
__Behind
__ and 
__Front
__. Default is 
__Behind
__.
            


1. Specify whether it will be displayed on first (
__PrintOnFirstPage
__) and last page (
__PrintOnLastPage
__).
            


1. Click 
__OK
__.
            


## Add Picture Watermark programmatically

{{source=CodeSnippets\CS\API\Telerik\Reporting\WatermarksSnippets.cs region=AddNewPictureWatermarkSnippet}}
````C#
	
	            Telerik.Reporting.Drawing.PictureWatermark pictureWatermark1 = new Telerik.Reporting.Drawing.PictureWatermark();
	            pictureWatermark1.Image = "http://www.telerik.com/images/reporting/cars/NSXGT_7.jpg";
	            pictureWatermark1.Position = Telerik.Reporting.Drawing.WatermarkPosition.Behind;
	            pictureWatermark1.PrintOnFirstPage = true;
	            pictureWatermark1.PrintOnLastPage = true;
	            pictureWatermark1.Sizing = Telerik.Reporting.Drawing.WatermarkSizeMode.ScaleProportional;
	            pictureWatermark1.Opacity = 0.5D;
	            report1.PageSettings.Watermarks.Add(pictureWatermark1);
	
````




{{source=CodeSnippets\VB\API\Telerik\Reporting\WatermarksSnippets.vb region=AddNewPictureWatermarkSnippet}}
````VB
	
	        Dim pictureWatermark1 As New Telerik.Reporting.Drawing.PictureWatermark()
	        pictureWatermark1.Image = "http://www.telerik.com/images/reporting/cars/NSXGT_7.jpg"
	        pictureWatermark1.Position = Telerik.Reporting.Drawing.WatermarkPosition.Behind
	        pictureWatermark1.PrintOnFirstPage = True
	        pictureWatermark1.PrintOnLastPage = True
	        pictureWatermark1.Sizing = Telerik.Reporting.Drawing.WatermarkSizeMode.ScaleProportional
	        pictureWatermark1.Opacity = 0.5
	        report1.PageSettings.Watermarks.Add(pictureWatermark1)
	
````




## Add Background Overlay using Report Designer

Background Overlay is a special kind of Picture Watermark that is designed to facilitate the creation of form type reports.
        It is rendered behind the report contents and takes the whole page area without respecting the page margins.


To add Background Overlay to the Report use the following steps:


1. Open a report in 
__Design
__ view.
            


1. You can open the Watermarks collection editor in two ways:


* Click the Report selector button located in the upper left corner of the 
[Visual Studio Report Designer]({%slug telerikreporting/designing-reports/report-designer-tools/desktop-designers/visual-studio-report-designer/overview%})
. This makes the report active in the Properties window.
                  Expand 
__PageSettings
__ and click 
__Watermarks
__ ellipsis in the property grid.
                


* Select the Watermarks item in the report's context menu, which appears when you right-click on the designer surface.
                
Both actions will display the Watermarks collection editor, which is empty by default.
            


1. Click the small arrow on the right side of the 
__Add
__ button and select BackgroundOverlay from the drop-down menu.
            


1. In 
__Image
__, browse for an image file on your hard drive, input an URI (local path or URL) or an 
[Expressions]({%slug telerikreporting/designing-reports/connecting-to-data/expressions/overview%})
 that evaluates to an image.
              The 
__Image
__ field also accepts a string that represents a Base64-encoded image.
            


1. Set 
__Sizing
__ mode. Available options are Center, Stretch, ScaleProportional and TopLeft. 
              The Background Overlay sets TopLeft as its default Sizing value, which means the image will be displayed without being resized, and positioned in the top left corner of the page area.
              See 
[PictureBox]({%slug telerikreporting/designing-reports/report-structure/picturebox%})
 article for more information on the modes.
            


1. Set 
__Opacity
__. By default the Opacity of the Background Overlay is set to 1.
            


1. Specify whether it will be rendered in the output report document. The default value is 
*false
* which means the Background Overlay will be visible only during design-time.
            


1. Specify whether it will be displayed on first (
__PrintOnFirstPage
__) and last page (
__PrintOnLastPage
__).
              These options are overridden by the 
__RenderInReportDocument
__ option, i.e. if it is set to 
*false
*, 
              the 
__PrintOnFirstPage
__ and 
__PrintOnLastPage
__ options will not be respected.
            


1. Click 
__OK
__. The design surface should display the selected Background Overlay image.
            


## Add Background Overlay programmatically

{{source=CodeSnippets\CS\API\Telerik\Reporting\WatermarksSnippets.cs region=AddNewBackgroundOverlaySnippet}}
````C#
	
	            Telerik.Reporting.Drawing.BackgroundOverlay backgroundOverlay1 = new Telerik.Reporting.Drawing.BackgroundOverlay();
	            backgroundOverlay1.Image = "http://www.telerik.com/images/reporting/cars/NSXGT_7.jpg";
	            backgroundOverlay1.PrintOnFirstPage = true;
	            backgroundOverlay1.PrintOnLastPage = true;
	            backgroundOverlay1.Sizing = Telerik.Reporting.Drawing.WatermarkSizeMode.TopLeft;
	            backgroundOverlay1.RenderInReportDocument = true;
	            backgroundOverlay1.Opacity = 1D;
	            report1.PageSettings.Watermarks.Add(backgroundOverlay1);
	
````




{{source=CodeSnippets\VB\API\Telerik\Reporting\WatermarksSnippets.vb region=AddNewBackgroundOverlaySnippet}}
````VB
	
	        Dim backgroundOverlay1 As New Telerik.Reporting.Drawing.BackgroundOverlay()
	        backgroundOverlay1.Image = "http://www.telerik.com/images/reporting/cars/NSXGT_7.jpg"
	        backgroundOverlay1.PrintOnFirstPage = True
	        backgroundOverlay1.PrintOnLastPage = True
	        backgroundOverlay1.Sizing = Telerik.Reporting.Drawing.WatermarkSizeMode.TopLeft
	        backgroundOverlay1.RenderInReportDocument = True
	        backgroundOverlay1.Opacity = 1
	        report1.PageSettings.Watermarks.Add(backgroundOverlay1)
	
````




## Add Watermark conditionally

Add Watermarks to the Report on even pages only:


* For Text Watermark, in 
__Text
__ property, use the following expression: 
__=IIF(PageNumber %2 = 0, "My Text Watermark", null)
__

* For Picture Watermark, in 
__Image
__ property, use the following expression: 
__=IIF(PageNumber %2 = 0, "C:\MyImageWatermark.png", null)
__

Add Watermarks to the Report via defined page range:


* For Text Watermark, in 
__Text
__ property, use the following expression: 
__=IIF(PageNumber > 2 and PageNumber < 10, "My Text Watermark", null)
__

* For Picture Watermark, in 
__Image
__ property, use the following expression: 
__=IIF(PageNumber > 2 and PageNumber < 10, "C:\MyImageWatermark.png", null)
__

## Design-time support

For better design experience, the watermarks are shown in the designer by default. They can be switched on/off with the watermarks button, located on the toolstrip at the bottom left corner of the designer window.
        
  
  ![report-designer-toolstrip-watermarks-focused](images/Designer/report-designer-toolstrip-watermarks-focused.png)

The value of the text watermarks is not evaluated and it is shown 'as-is' in the designer.
          Note that the position of the watermark in design-time is calculated based on the report size in designer and might differ from the watermark you will see in the previewed report.
        


The value of the picture watermark is evaluated against the designer context and will be shown if possible.
        


## 

>warning Some formats do not support Watermarks. For more information refer to the articles in the Design Considerations for Report Rendering section          


# See Also

