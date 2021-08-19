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

1. Using the[Data Source Wizard]({%slug telerikreporting/designing-reports/report-designer-tools/desktop-designers/tools/data-source-wizards/datasource-wizard%})bind the report to__SqlDataSource__with query:

	
    ````SQL
SELECT        Production.Product.ProductNumber, Production.Product.Name AS ProductName, 
              Production.ProductSubcategory.Name AS SubcategoryName
FROM          Production.Product 
              INNER JOIN Production.ProductSubcategory 
                   ON Production.Product.ProductSubcategoryID = Production.ProductSubcategory.ProductSubcategoryID
WHERE        (Production.Product.ProductSubcategoryID = @ProductSubcategoryID)
````



1. Click the__Next__button and the__"Configure Data Source Parameters"__step of the__SqlDataSource__appears. Set the__DbType__of the ProductSubcategoryID
			parameter to__Int32__and select "New Report Parameter" for the Value.

1. This invokes the__Report Parameter Editor__.

1. Name the new parameter__ProductSubcategoryID__.

1. Set the__Text__to Product SubCategory.

1. Set the__Type__of the parameter to Integer.

1. Set the__Visible__property to True.

1. Expand the__AvailableValues__.

1. Start the Data Source Wizard and set the DataSource for the parameter to the following query:

	
    ````SQL
SELECT        ProductSubcategoryID, 
              Name AS SubcategoryName
FROM          Production.ProductSubcategory
WHERE        (ProductCategoryID = @ProductCategoryID)
````



1. Click the__Next__button and the__"Configure Data Source Parameters"__step of 
			the__SqlDataSource__appears. Set the__DbType__of the__ProductCategoryID__parameter to__Int32__and select "__New Report 
			Parameter__" for the__Value__.

1. This invokes the__Report Parameter Editor__.

1. Name the new parameter__ProductCategoryID__.

1. Set the Text to__Product Category__.

1. Set the Type of the parameter to__Integer__.

1. Set the__Visible__property to True.

1. Expand the AvailableValues.

1. Start the__Data Source Wizard__and set the DataSource for 
			the parameter to the following query:

	
    ````SQL
SELECT
              ProductCategoryID,
              Name AS CategoryName
FROM
              Production.ProductCategory
````



1. Click__Next__and__Finish__the Data Source Wizard.

1. Set the DisplayMember to__= Fields.CategoryName__column.

1. Set the ValueMember to__= Fields.ProductCategoryID__.

1. It is not compulsory to set the DataMember property when the data source contains only one table.

1. Click__OK__to close the Report Parameter Editor.

1. Click__Next__and__Finish__the Data Source Wizard for the ProductCategoryID parameter.

1. Select the__Report Parameter Editor__for the__ProductSubcategoryID__parameter.

1. Set the__DisplayMember__to__= Fields.SubcategoryName__column

1. Set the__ValueMember__to__= Fields.ProductSubcategoryID__.

1. It is not compulsory to set the DataMember property when the data source contains only one table.

1. Click__OK__to close the__Report Parameter Editor__.

1. Click__Next__and__Finish__the__Data Source Wizard__for the__ProductSubcategoryID__parameter.

1. Preview the report. Use the Product Category and Product Subcategory parameters to filter the list of products shown in the report.

# See Also

