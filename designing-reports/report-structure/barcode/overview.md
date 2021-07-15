---
title: Barcode Overview
page_title: Overview | for Telerik Reporting Documentation
description: Overview
slug: telerikreporting/designing-reports/report-structure/barcode/overview
tags: overview
published: True
position: 0
---

# Barcode Overview



The Barcode item is used for automatic barcode generation directly from a numeric or character data. This article elaborates on how to create and use barcodes in a report.

## Setting up a barcode

* In order to specify the type of the barcode use the P:Telerik.Reporting.Barcode.Encoder  property.
            After choosing the desired encoder you can further adjust its specific settings if availabe:  
  ![barcode-encoder-property](images/Barcodes/barcode-encoder-property.png)

* The value which is encoded is set through the
              P:Telerik.Reporting.Barcode.Value property.
              It can be a static string or an expression which is evaluated at runtime:
              
  ![barcode-value-property](images/Barcodes/barcode-value-property.png)

* The width (size) of the barcode elements is specified in two ways:

* Using the P:Telerik.Reporting.Barcode.Module property
                

* Auto calculated from the size of the item when the P:Telerik.Reporting.Barcode.Stretch proprty is set to true
                  
  ![barcode-module-stretch-property](images/Barcodes/barcode-module-stretch-property.png)

* Additionally you can further adjust the barcode appearance:

* Align the bars to the item's edges through the P:Telerik.Reporting.Barcode.BarAlign property.
                  
  ![barcode-baralign-property](images/Barcodes/barcode-baralign-property.png)This property is not applicable when the P:Telerik.Reporting.Barcode.Stretch property is set to true.
                

* Rotate the barcode throught the P:Telerik.Reporting.Barcode.Angle property.
                  
  ![barcode-angle-property](images/Barcodes/barcode-angle-property.png)When the angle is not divisable by 90 degrees and the P:Telerik.Reporting.Barcode.Stretch property is true,
                  the barcode will be scaled down so that it fits into the item bounds.
                

* To include a checksum in the barcode use the P:Telerik.Reporting.Barcode.Checksum property.
                  Note that in some symbologies there is either no checksum or the checksum is part of its specification.
                  In these cases this property will have no effect.
                

## Examples

{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````cs
	            var encoder = new Telerik.Reporting.Barcodes.Code128AEncoder();
	
	            // Set any specific encoder settings...
	            encoder.ShowText = false; // The default value is true.
	
	            this.barcode1.Encoder = encoder;
	            this.barcode1.Angle = 90;
	            this.barcode1.BarAlign = Telerik.Reporting.Drawing.HorizontalAlign.Left;
	            this.barcode1.Checksum = true;
	            this.barcode1.Module = Telerik.Reporting.Drawing.Unit.Point(3);
	            this.barcode1.Stretch = false;
	            this.barcode1.Value = "1234567890";
````



{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````vbnet
	        Dim encoder = New Telerik.Reporting.Barcodes.Code128AEncoder()
	
	        ' Set any specific encoder settings...
	        encoder.ShowText = False 'The default value is True
	
	        Me.barcode1.Encoder = encoder
	        Me.barcode1.Angle = 90
	        Me.barcode1.BarAlign = Telerik.Reporting.Drawing.HorizontalAlign.Left
	        Me.barcode1.Checksum = True
	        Me.barcode1.Module = Telerik.Reporting.Drawing.Unit.Point(3)
	        Me.barcode1.Stretch = False
	        Me.barcode1.Value = "1234567890"
	        '#End Region
	
	        Assert.IsNotNull(Me.barcode1.Encoder)
	    End Sub
	
	    <TestMethod()>
	    Public Sub Set_QRCodeEncoder_Settings()
	
	        '#region Barcode_QRCodeEncoder_Settings
	        Dim encoder = New Telerik.Reporting.Barcodes.QRCodeEncoder()
	
	        encoder.Version = 10
	        encoder.ErrorCorrectionLevel = Telerik.Reporting.Barcodes.QRCode.ErrorCorrectionLevel.M
	        encoder.ECI = Telerik.Reporting.Barcodes.QRCode.ECIMode.CP437
	        encoder.Mode = Telerik.Reporting.Barcodes.QRCode.CodeMode.Alphanumeric
	        encoder.FNC1 = Telerik.Reporting.Barcodes.QRCode.FNC1Mode.SecondPosition
	        encoder.ApplicationIndicator = "00"
	
	        Me.barcode1.Encoder = encoder
	        '#End Region
	
	        Assert.IsNotNull(Me.barcode1.Encoder)
	
	    End Sub
	
	    <TestMethod()>
	    Public Sub Set_PDF417Encoder_Settings()
	
	        '#Region "Barcode_PDF417Encoder_Settings"
	        Dim encoder = New Telerik.Reporting.Barcodes.PDF417Encoder()
	
	        encoder.Columns = 3
	        encoder.Rows = 3
	        encoder.Encoding = Telerik.Reporting.Barcodes.PDF417.EncodingMode.Auto
	        encoder.ErrorCorrectionLevel = 2
	
	        Me.barcode1.Encoder = encoder
	        '#End Region
	
	        Assert.IsNotNull(Me.barcode1.Encoder)
	    End Sub
	
	    <TestMethod()>
	    Public Sub Set_DataMatrixEncoder_Settings()
	
	        '#Region "Barcode_DataMatrixEncoder_Settings"
	        Dim encoder = New Telerik.Reporting.Barcodes.DataMatrixEncoder()
	
	        encoder.Encodation = Telerik.Reporting.Barcodes.DataMatrix.Encodation.Ascii
	        encoder.SymbolSize = Telerik.Reporting.Barcodes.DataMatrix.SymbolSize.SquareAuto
	        encoder.TextEncoding = System.Text.UTF8Encoding.UTF8
	
	        Me.barcode1.Encoder = encoder
	        '#End Region
	
	        Assert.IsNotNull(Me.barcode1.Encoder)
	    End Sub
	End Class



# See AlsoT:Telerik.Reporting.BarcodeP:Telerik.Reporting.Barcode.EncoderP:Telerik.Reporting.Barcode.ValueP:Telerik.Reporting.Barcode.ModuleP:Telerik.Reporting.Barcode.StretchP:Telerik.Reporting.Barcode.BarAlignP:Telerik.Reporting.Barcode.AngleP:Telerik.Reporting.Barcode.Checksum
