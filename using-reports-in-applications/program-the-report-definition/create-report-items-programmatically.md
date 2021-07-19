---
title: Create Report Items Programmatically
page_title: Create Report Items Programmatically | for Telerik Reporting Documentation
description: Create Report Items Programmatically
slug: telerikreporting/using-reports-in-applications/program-the-report-definition/create-report-items-programmatically
tags: create,report,items,programmatically
published: True
position: 3
---

# Create Report Items Programmatically



## 

To create a report item in code, instantiate a report item object, set its properties, and add it to the Items collection of the section where you wish the control to appear. For example, this code will add two __TextBox__ report items to a report:

````
Telerik.Reporting.Panel panel1 = new Telerik.Reporting.Panel();
Telerik.Reporting.TextBox textBox1 = new Telerik.Reporting.TextBox();

// panel1

panel1.Location = new Telerik.Reporting.Drawing.PointU(new Telerik.Reporting.Drawing.Unit(1.0, Telerik.Reporting.Drawing.UnitType.Cm), new Telerik.Reporting.Drawing.Unit(1.0, Telerik.Reporting.Drawing.UnitType.Cm));
panel1.Size = new Telerik.Reporting.Drawing.SizeU(new Telerik.Reporting.Drawing.Unit(8.5, Telerik.Reporting.Drawing.UnitType.Cm), new Telerik.Reporting.Drawing.Unit(3.5, Telerik.Reporting.Drawing.UnitType.Cm));
panel1.Style.BorderStyle.Default = Telerik.Reporting.Drawing.BorderType.Solid;

// textBox1

textBox1.Location = new Telerik.Reporting.Drawing.PointU(new Telerik.Reporting.Drawing.Unit(0, Telerik.Reporting.Drawing.UnitType.Cm), new Telerik.Reporting.Drawing.Unit(0, Telerik.Reporting.Drawing.UnitType.Cm));
textBox1.Name = "NameDataTextBox";
textBox1.Size = new Telerik.Reporting.Drawing.SizeU(new Telerik.Reporting.Drawing.Unit(5.0, Telerik.Reporting.Drawing.UnitType.Cm), new Telerik.Reporting.Drawing.Unit(0.6, Telerik.Reporting.Drawing.UnitType.Cm));
textBox1.Style.BorderStyle.Default = Telerik.Reporting.Drawing.BorderType.Solid;
textBox1.StyleName = "Data";
textBox1.Value = "=Fields.CustomerID";

panel1.Items.AddRange(new Telerik.Reporting.ReportItemBase[] {textBox1});
detail.Items.AddRange(new Telerik.Reporting.ReportItemBase[] {panel1});
			````



````
Dim panel1 As New Telerik.Reporting.Panel()
Dim textBox1 As New Telerik.Reporting.TextBox()

'panel1

panel1.Location = New Telerik.Reporting.Drawing.PointU(New Telerik.Reporting.Drawing.Unit(1, Telerik.Reporting.Drawing.UnitType.Cm), New Telerik.Reporting.Drawing.Unit(1, Telerik.Reporting.Drawing.UnitType.Cm))
panel1.Size = New Telerik.Reporting.Drawing.SizeU(New Telerik.Reporting.Drawing.Unit(8.5, Telerik.Reporting.Drawing.UnitType.Cm), New Telerik.Reporting.Drawing.Unit(3.5, Telerik.Reporting.Drawing.UnitType.Cm))
panel1.Style.BorderStyle.Default = Telerik.Reporting.Drawing.BorderType.Solid

'textBox1

textBox1.Location = New Telerik.Reporting.Drawing.PointU(New Telerik.Reporting.Drawing.Unit(0, Telerik.Reporting.Drawing.UnitType.Cm), New Telerik.Reporting.Drawing.Unit(0, Telerik.Reporting.Drawing.UnitType.Cm))
textBox1.Name = "NameDataTextBox"
textBox1.Size = New Telerik.Reporting.Drawing.SizeU(New Telerik.Reporting.Drawing.Unit(5, Telerik.Reporting.Drawing.UnitType.Cm), New Telerik.Reporting.Drawing.Unit(0.6, Telerik.Reporting.Drawing.UnitType.Cm))
textBox1.Style.BorderStyle.Default = Telerik.Reporting.Drawing.BorderType.Solid
textBox1.StyleName = "Data"
textBox1.Value = "=Fields.CustomerID"

panel1.Items.AddRange(New Telerik.Reporting.ReportItemBase() {textBox1})
detail.Items.AddRange(New Telerik.Reporting.ReportItemBase() {panel1})
		````



# See AlsoT:Telerik.Reporting.TextBoxT:Telerik.Reporting.PictureBoxT:Telerik.Reporting.PanelT:Telerik.Reporting.SubReportT:Telerik.Reporting.ShapeT:Telerik.Reporting.TableT:Telerik.Reporting.CheckBox
