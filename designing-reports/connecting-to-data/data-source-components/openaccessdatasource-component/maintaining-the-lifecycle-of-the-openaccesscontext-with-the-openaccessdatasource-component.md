---
title: Maintaining the lifecycle of the OpenAccessContext with the OpenAccessDataSource component
page_title: Maintaining the lifecycle of the OpenAccessContext with the OpenAccessDataSource component | for Telerik Reporting Documentation
description: Maintaining the lifecycle of the OpenAccessContext with the OpenAccessDataSource component
slug: telerikreporting/designing-reports/connecting-to-data/data-source-components/openaccessdatasource-component/maintaining-the-lifecycle-of-the-openaccesscontext-with-the-openaccessdatasource-component
tags: maintaining,the,lifecycle,of,the,openaccesscontext,with,the,openaccessdatasource,component
published: True
position: 4
---

# Maintaining the lifecycle of the OpenAccessContext with the OpenAccessDataSource component



This section discusses how to maintain the lifecycle of the 
__OpenAccessContext
__ when using the 
    	
__OpenAccessDataSource
__ component. The provided examples and code snippets assume an existing 
__Telerik Data Access Model
__ 
    	of the 
__Adventure Works
__ sample database with the following structure:


  
  ![](images/DataSources/OpenAccessDataSourceAdventureWorksEntityModel.png)

## 

One possible approach to connect to a 
__Telerik Data Access Model
__ without using the 
__OpenAccessDataSource
__ component 
      	is to create a custom business object with a method that retrieves the necessary entities for the report. 
      	The sample code below defines a method that retrieves information about all products:
      	


{{source=CodeSnippets\CS\API\Telerik\Reporting\OpenAccessDataSourceSnippets.cs region=SampleObjectSnippet}}
````C#
	
	        public class SampleBusinessObject
	        {
	            public System.Collections.Generic.List```<Product>``` GetProducts()
	            {
	                using (AdventureWorksEntities context = new AdventureWorksEntities())
	                {
	                    return context.Products.ToList();
	                }
	            }
	        }
	
````




{{source=CodeSnippets\VB\API\Telerik\Reporting\OpenAccessDataSourceSnippets.vb region=SampleObjectSnippet}}
````VB
	
	    Public Class SampleBusinessObject
	        Public Function GetProducts() As System.Collections.Generic.List(Of Product)
	            Using context As AdventureWorksEntities = New AdventureWorksEntities()
	                Return context.Products.ToList()
	            End Using
	        End Function
	    End Class
	
````




Then you can use 
__ObjectDataSource
__ to connect to that business object, as shown in the following code snippet:
      	


{{source=CodeSnippets\CS\API\Telerik\Reporting\OpenAccessDataSourceSnippets.cs region=ObjectBindingSnippet}}
````C#
	
	            var objectDataSource = new Telerik.Reporting.ObjectDataSource();
	
	            objectDataSource.DataSource = typeof(SampleBusinessObject);
	            objectDataSource.DataMember = "GetProducts";
	
	            var report = new Report1();
	
	            report.DataSource = objectDataSource;
	
````




{{source=CodeSnippets\VB\API\Telerik\Reporting\OpenAccessDataSourceSnippets.vb region=ObjectBindingSnippet}}
````VB
	
	        Dim objectDataSource As New Telerik.Reporting.ObjectDataSource()
	
	        objectDataSource.DataSource = GetType(SampleBusinessObject)
	        objectDataSource.DataMember = "GetProducts"
	
	        Dim report As New Report1()
	
	        report.DataSource = objectDataSource
	
````




The problem with this approach is that it is not guaranteed to work in all possible scenarios. Simple expressions 
      	accessing primitive properties of the 
__Product
__ entity might work as expected:
      	


=Fields.Name


However, let us consider the following expression that is intended to obtain the category of a given product:


=Fields.ProductSubcategory.ProductCategory.Name


The above expression relies upon the lazy loading mechanism of 
__Telerik Data Access
__ to 
      	obtain the 
__ProductSubcategory
__ entity for the current 
__Product
__ entity via the corresponding relation property, 
      	and then the 
__ProductCategory
__ entity for the current 
__ProductSubcategory
__ entity. This is not guaranteed to work 
      	because the 
__OpenAccessContext
__ is already destroyed when evaluating the expression, so lazy loading is no longer 
      	possible. One of the greatest advantages of the 
__OpenAccessDataSource
__ component is that it can maintain the 
      	lifecycle of the 
__OpenAccessContext
__ automatically, so scenarios like the previous one are guaranteed to work as 
      	expected. When specifying a 
__Type
__ for the 
__OpenAccessContext
__ property, 
__OpenAccessDataSource
__ creates internally a new 
      	instance of the 
__OpenAccessContext
__ with the given type, keeps it alive for the duration of the report generation 
      	process, and then destroys it automatically when it is no longer needed by the reporting engine. The following 
      	code snippet accomplishes the previous task with the help of the 
__OpenAccessDataSource
__ component:
      	


{{source=CodeSnippets\CS\API\Telerik\Reporting\OpenAccessDataSourceSnippets.cs region=PropertyBindingSnippet}}
````C#
	
	            var openAccessDataSource = new Telerik.Reporting.OpenAccessDataSource();
	
	            openAccessDataSource.ObjectContext = typeof(AdventureWorksEntities);
	            openAccessDataSource.ObjectContextMember = "Products";
	
	            var report = new Report1();
	
	            report.DataSource = openAccessDataSource;
	
````




{{source=CodeSnippets\VB\API\Telerik\Reporting\OpenAccessDataSourceSnippets.vb region=PropertyBindingSnippet}}
````VB
	
	        Dim openAccessDataSource As New Telerik.Reporting.OpenAccessDataSource()
	
	        openAccessDataSource.ObjectContext = GetType(AdventureWorksEntities)
	        openAccessDataSource.ObjectContextMember = "Products"
	
	        Dim report As New Report1()
	
	        report.DataSource = openAccessDataSource
	
````




If you have already implemented your own mechanism for maintaining the lifecycle of the 
__OpenAccessContext
__ 
      	you can continue using the 
__OpenAccessDataSource
__ component. In this case however you need to specify a live instance 
      	of your 
__OpenAccessContext
__ to the 
__ObjectContext
__ property as demonstrated here:
    	


{{source=CodeSnippets\CS\API\Telerik\Reporting\OpenAccessDataSourceSnippets.cs region=InstanceBindingSnippet}}
````C#
	
	            var openAccessDataSource = new Telerik.Reporting.OpenAccessDataSource();
	            var openAccessContext = new AdventureWorksEntities();
	
	            openAccessDataSource.ObjectContext = openAccessContext;
	            openAccessDataSource.ObjectContextMember = "Products";
	
	            var report = new Report1();
	
	            report.DataSource = openAccessDataSource;
	
	            // You have to dispose the OpenAccessContext explicitly when done with the report.
	            openAccessContext.Dispose();
	
````




{{source=CodeSnippets\VB\API\Telerik\Reporting\OpenAccessDataSourceSnippets.vb region=InstanceBindingSnippet}}
````VB
	
	        Dim openAccessDataSource As Telerik.Reporting.OpenAccessDataSource = New Telerik.Reporting.OpenAccessDataSource()
	        Dim openAccessContext As AdventureWorksEntities = New AdventureWorksEntities()
	
	        openAccessDataSource.ObjectContext = openAccessContext
	        openAccessDataSource.ObjectContextMember = "Products"
	
	        Dim report As New Report1()
	
	        report.DataSource = openAccessDataSource
	
	        ' You have to dispose the OpenAccessContext explicitly when done with the report.
	        openAccessContext.Dispose()
	
````




# See Also

