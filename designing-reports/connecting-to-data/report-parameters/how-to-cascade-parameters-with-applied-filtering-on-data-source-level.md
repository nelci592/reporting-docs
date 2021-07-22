---
title: How to Cascade Parameters with applied filtering on data source level
page_title: How to Cascade Parameters with applied filtering on data source level | for Telerik Reporting Documentation
description: How to Cascade Parameters with applied filtering on data source level
slug: telerikreporting/designing-reports/connecting-to-data/report-parameters/how-to-cascade-parameters-with-applied-filtering-on-data-source-level
tags: how,to,cascade,parameters,with,applied,filtering,on,data,source,level
published: True
position: 6
---

# How to Cascade Parameters with applied filtering on data source level



To create cascading report parameters with applied filtering on data source level follow the steps below:
   	


## Cascading Parameters with applied filtering on Datasource level

1. Using the 
[Data Source Wizard]({%slug telerikreporting/designing-reports/report-designer-tools/desktop-designers/tools/data-source-wizards/datasource-wizard%})
 bind the report to 
__SqlDataSource
__ with query:
		        


	
````SQL
SELECT        Production.Product.ProductNumber, Production.Product.Name AS ProductName, 
              Production.ProductSubcategory.Name AS SubcategoryName
FROM          Production.Product 
              INNER JOIN Production.ProductSubcategory 
                   ON Production.Product.ProductSubcategoryID = Production.ProductSubcategory.ProductSubcategoryID
WHERE        (Production.Product.ProductSubcategoryID = @ProductSubcategoryID)
				
````


				Note that there is a 
__WHERE
__ clause that filters the datasource based on the ProductSubcategoryID parameter.
			


1. Click the 
__Next
__ button and the 
			
__"Configure Data Source Parameters"
__			step of the 
__SqlDataSource
__ appears. Set the 
			
__DbType
__ of the ProductSubcategoryID
			parameter to 
__Int32
__ and select "New Report Parameter" for the Value.


1. This invokes the 
__Report Parameter Editor
__.


1. Name the new parameter 
__ProductSubcategoryID
__.


1. Set the 
__Text
__ to Product SubCategory.


1. Set the 
__Type
__ of the parameter to Integer.


1. Set the 
__Visible
__ property to True.


1. Expand the 
__AvailableValues
__.


1. Start the Data Source Wizard and set the DataSource for the parameter to the following query: 
		        


	
````SQL
SELECT        ProductSubcategoryID, 
              Name AS SubcategoryName
FROM          Production.ProductSubcategory
WHERE        (ProductCategoryID = @ProductCategoryID)
				
````


			Note that there is a 
__WHERE
__ clause that filters the data source based on the ProductCategoryID parameter.
			


1. Click the 
__Next
__ button and the 
			
__"Configure Data Source Parameters"
__ step of 
			the 
__SqlDataSource
__ appears. Set the 
			
__DbType
__ of the 
__ProductCategoryID
__ 
			parameter to 
__Int32
__ and select "
__New Report 
			Parameter
__" for the 
__Value
__.


1. This invokes the 
__Report Parameter Editor
__. 


1. Name the new parameter 
__ProductCategoryID
__.


1. Set the Text to 
__Product Category
__.


1. Set the Type of the parameter to 
__Integer
__.


1. Set the 
__Visible
__ property to True.


1. Expand the AvailableValues.


1. Start the 
__Data Source Wizard
__ and set the DataSource for 
			the parameter to the following query:
		        


	
````SQL
SELECT
              ProductCategoryID,
              Name AS CategoryName
FROM
              Production.ProductCategory
				
````




1. Click 
__Next
__ and 
__Finish
__ the Data Source Wizard.


1. Set the DisplayMember to 
__= Fields.CategoryName
__ column.


1. Set the ValueMember to 
__= Fields.ProductCategoryID
__.


1. It is not compulsory to set the DataMember property when the data source contains only one table.


1. Click 
__OK
__ to close the Report Parameter Editor.


1. Click 
__Next
__ and 
__Finish
__ the Data Source Wizard for the ProductCategoryID parameter.


1. Select the 
__Report Parameter Editor
__ 
			for the 
__ProductSubcategoryID
__ parameter.


1. Set the 
__DisplayMember
__ to 
__= Fields.SubcategoryName
__ column


1. Set the 
__ValueMember
__ to 
__= Fields.ProductSubcategoryID
__.


1. It is not compulsory to set the DataMember property when the data source contains only one table.


1. Click 
__OK
__ to close the 
__Report Parameter Editor
__.


1. Click 
__Next
__ and 
__Finish
__ the 
__Data Source Wizard
__ for the 
__ProductSubcategoryID
__ parameter.


1. Preview the report. Use the Product Category and Product Subcategory parameters to filter the list of products shown in the report.


# See Also

