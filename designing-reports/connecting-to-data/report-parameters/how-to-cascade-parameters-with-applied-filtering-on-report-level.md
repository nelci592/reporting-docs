---
title: How to Cascade Parameters with applied filtering on Report level
page_title: How to Cascade Parameters with applied filtering on Report level | for Telerik Reporting Documentation
description: How to Cascade Parameters with applied filtering on Report level
slug: telerikreporting/designing-reports/connecting-to-data/report-parameters/how-to-cascade-parameters-with-applied-filtering-on-report-level
tags: how,to,cascade,parameters,with,applied,filtering,on,report,level
published: True
position: 5
---

# How to Cascade Parameters with applied filtering on Report level



To create cascading report parameters with applied filtering on report level follow the steps below:
   	


## 

1. Using the 
[DataSource Wizard]({%slug telerikreporting/designing-reports/report-designer-tools/desktop-designers/tools/data-source-wizards/datasource-wizard%})
 bind the report to SqlDataSource with query:
		        


	
````SQL
				SELECT
					Production.Product.ProductNumber,
					Production.Product.Name AS ProductName,
					Production.Product.ProductSubcategoryID,
					Production.ProductSubcategory.Name AS SubcategoryName
				FROM
					Production.Product
					INNER JOIN Production.ProductSubcategory
						ON Production.Product.ProductSubcategoryID = Production.ProductSubcategory.ProductSubcategoryID
				
````




1. Click the ellipses on the 
__Report.ReportParameters
__ property. This invokes the 
__ReportParameter Collection editor
__.


1. Add new Report Parameter


1. __Name 
__it 
__ProductCategoryID
__.


1. Set the 
__Type
__ of the parameter to 
__Integer
__.


1. Expand the 
__AvailableValues.
__

1. Set the 
__DataSource
__ using the 
__Data Source Wizard
__ to SqlDataSource with query: 
		        


	
````SQL
				SELECT
					ProductCategoryID,
					Name AS CategoryName
				FROM
					Production.ProductCategory
				
````




1. It is not compulsory to set the 
__DataMember
__ property when the data source contains only one table.


1. Set the 
__DisplayMember
__ to 
__= Fields.CategoryName
__ column.


1. Set the 
__ValueMember
__ to 
__= Fields.ProductCategoryID
__.


1. Set the 
__Text
__ to 
__Product Category
__.


1. Set the 
__Visible
__ property to 
__True
__ if needed.


1. Add new Report Parameter


1. __Name 
__it 
__ProductSubcategoryID
__.


1. Set the 
__Type
__ of the parameter to 
__Integer
__.


1. Expand the 
__AvailableValues.
__

1. Set the 
__DataSource
__ using the 
__Data Source Wizard
__ to SqlDataSource with query:
		        


	
````SQL
				SELECT
					ProductCategoryID,
					ProductSubcategoryID,
					Name AS SubcategoryName
				FROM
					Production.ProductSubcategory
				
````




1. It is not compulsory to set the 
__DataMember
__ property when the data source contains only one table.


1. Set the 
__DisplayMember
__ to 
__= Fields.SubcategoryName
__ column.


1. Set the 
__ValueMember
__ to 
__= Fields.ProductSubcategoryID
__.


1. Click on the ellipsis on the 
__Filters
__ property.


1. Add new filter.


1. As 
__Expression
__ choose 
__=Fields.ProductCategoryID.
__

1. As 
__Operator
__ choose 
__equals(=)
__.


1. As Value choose 
__=Parameters.ProductCategoryID.Value
__.


1. Click 
__OK
__.


1. Set the 
__Multivalue
__ to 
__false
__ (or to 
__true
__ if you want to be able to select more than one subcategory at a time).


1. Set the 
__Text
__ to 
__Product Subcategory
__.


1. Set the 
__Visible
__ property to 
__True
__ if needed.


1. Close the 
__ReportParameter Collection Editor
__.


1. Click on the ellipsis on the 
__Filters
__ property of the report to open the 
__Edit Filters
__ dialog.


1. Add new filter.


1. As 
__Expression
__ choose 
__=Fields.ProductSubcategoryID
__.


1. As 
__Operator
__ choose 
__equals(=)
__ (or to 
__IN
__ operator if you have set 
__ProductSubcategoryID
__ parameter as multivalue parameter
__)
__.


1. As Value choose 
__=Parameters.ProductSubcategoryID.Value
__.


1. Click 
__OK
__.


1. Preview the report. Use the Product Category and Product Subcategory parameters to filter the list of products shown in the report.


# See Also

