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

1. Using the[DataSource Wizard]({%slug telerikreporting/designing-reports/report-designer-tools/desktop-designers/tools/data-source-wizards/datasource-wizard%})bind the report to SqlDataSource with query:

	
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



1. Click the ellipses on the__Report.ReportParameters__property. This invokes the__ReportParameter Collection editor__.

1. Add new Report Parameter

1. __Name __it__ProductCategoryID__.

1. Set the__Type__of the parameter to__Integer__.

1. Expand the__AvailableValues.__

1. Set the__DataSource__using the__Data Source Wizard__to SqlDataSource with query:

	
    ````SQL
				SELECT
					ProductCategoryID,
					Name AS CategoryName
				FROM
					Production.ProductCategory
````



1. It is not compulsory to set the__DataMember__property when the data source contains only one table.

1. Set the__DisplayMember__to__= Fields.CategoryName__column.

1. Set the__ValueMember__to__= Fields.ProductCategoryID__.

1. Set the__Text__to__Product Category__.

1. Set the__Visible__property to__True__if needed.

1. Add new Report Parameter

1. __Name __it__ProductSubcategoryID__.

1. Set the__Type__of the parameter to__Integer__.

1. Expand the__AvailableValues.__

1. Set the__DataSource__using the__Data Source Wizard__to SqlDataSource with query:

	
    ````SQL
				SELECT
					ProductCategoryID,
					ProductSubcategoryID,
					Name AS SubcategoryName
				FROM
					Production.ProductSubcategory
````



1. It is not compulsory to set the__DataMember__property when the data source contains only one table.

1. Set the__DisplayMember__to__= Fields.SubcategoryName__column.

1. Set the__ValueMember__to__= Fields.ProductSubcategoryID__.

1. Click on the ellipsis on the__Filters__property.

1. Add new filter.

1. As__Expression__choose__=Fields.ProductCategoryID.__

1. As__Operator__choose__equals(=)__.

1. As Value choose__=Parameters.ProductCategoryID.Value__.

1. Click__OK__.

1. Set the__Multivalue__to__false__(or to__true__if you want to be able to select more than one subcategory at a time).

1. Set the__Text__to__Product Subcategory__.

1. Set the__Visible__property to__True__if needed.

1. Close the__ReportParameter Collection Editor__.

1. Click on the ellipsis on the__Filters__property of the report to open the__Edit Filters__dialog.

1. Add new filter.

1. As__Expression__choose__=Fields.ProductSubcategoryID__.

1. As__Operator__choose__equals(=)__(or to__IN__operator if you have set__ProductSubcategoryID__parameter as multivalue parameter__)__.

1. As Value choose__=Parameters.ProductSubcategoryID.Value__.

1. Click__OK__.

1. Preview the report. Use the Product Category and Product Subcategory parameters to filter the list of products shown in the report.

# See Also

