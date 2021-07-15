---
title: Checkbox
page_title: Checkbox | for Telerik Reporting Documentation
description: Checkbox
slug: telerikreporting/designing-reports/report-structure/checkbox
tags: checkbox
published: True
position: 13
---

# Checkbox



The CheckBox report item is used to display both text and a check mark on a report. This screenshot shows a CheckBox report item with CheckAlign property set to TopCenter and text aligned to Top and left.  
  ![](images/checkboxitem1.jpg)



## Growing and Shrinking

By default, CheckBox items are a set size. If you want to allow a CheckBox to expand vertically based on its contents,
          set the P:Telerik.Reporting.TextItemBase.CanGrow property to True (default value).
          If you want to allow a CheckBox to shrink based on its contents set the
          P:Telerik.Reporting.TextItemBase.CanShrink property to
          True (default value is False). The CheckBox would always grow to accomodate the first line of text even when CanGrow is False.
        

## Embedded expressions

The text part of the Checkbox report item supports [
            embedded
            expressions
          ]({%slug telerikreporting/designing-reports/connecting-to-data/expressions/using-expressions/overview%}) for mail merge functionality. Embedded expressions give you the freedom to get and insert data-driven
          information directly into the CheckBox.Text property to produce customized reports and mail merging.
        

A view where each CheckBox is initialized with CheckAlign varying from TopLeft to BottomRight:   
  ![](images/checkboxitem2.jpg)





The check mark image depends on the value set in the __Value__ property. By default it would accept  =true or =false. At design time the __Value__ property can be initialized with an expression which later at runtime is evaluated to one of the System.Windows.Forms.CheckState values e.g.:
        

=IsNull(Fields.Quantity, 0) > 100 which would return true or false and would check and uncheck the check mark respectively.
        

Also if your data fields return two/three distinctive values, which are not true/false you can change the TrueValue/FalseValue/IndeterminateValue properties to match your field values directly.
        

## Example: 

You have a Status field that has three values:

* Approved 

* DisApproved 

* NotSet   
  ![](images/checkboxEval1.png)

In such case it is more convenient to use those values directly instead of trying to evaluate them as true/false. You can do that easily by using the TrueValue/FalseValue/IndeterminateValue properties:  
  ![](images/checkboxEval2.png)

And here is the final result:  
  ![](images/CheckBoxEval3.png)





# See AlsoT:Telerik.Reporting.CheckBoxP:Telerik.Reporting.CheckBox.CheckAlignP:Telerik.Reporting.CheckBox.CheckedImageP:Telerik.Reporting.CheckBox.UncheckedImageP:Telerik.Reporting.CheckBox.FalseValueP:Telerik.Reporting.CheckBox.IndeterminateImageP:Telerik.Reporting.CheckBox.IndeterminateValueP:Telerik.Reporting.CheckBox.TextP:Telerik.Reporting.CheckBox.TrueValue