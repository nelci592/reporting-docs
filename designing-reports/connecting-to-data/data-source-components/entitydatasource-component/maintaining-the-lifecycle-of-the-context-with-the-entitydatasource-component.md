---
title: Maintaining the lifecycle of the Context with the EntityDataSource component
page_title: Maintaining the lifecycle of the Context with the EntityDataSource component | for Telerik Reporting Documentation
description: Maintaining the lifecycle of the Context with the EntityDataSource component
slug: telerikreporting/designing-reports/connecting-to-data/data-source-components/entitydatasource-component/maintaining-the-lifecycle-of-the-context-with-the-entitydatasource-component
tags: maintaining,the,lifecycle,of,the,context,with,the,entitydatasource,component
published: True
position: 4
---

# Maintaining the lifecycle of the Context with the EntityDataSource component



This section discusses how to maintain the lifecycle of the 
__ObjectContext/DbContext
__ when using the 
    	
__EntityDataSource
__ component. The provided examples and code snippets assume an existing 
__Entity Data Model
__ 
    	of the 
__Adventure Works
__ sample database with the following structure:


  
  ![](images/DataSources/EntityDataSourceAdventureWorksEntityModel.png)

## 

One possible approach to connect to an 
__Entity Data Model
__ without using the 
__EntityDataSource
__ component 
      	is to create a custom business object with a method that retrieves the necessary entities for the report. 
      	The sample code below defines a method that retrieves information about all products:
      	


{{source=CodeSnippets\CS\API\Telerik\Reporting\EntityDataSourceSnippets.cs region=SampleObjectSnippet}}
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




{{source=CodeSnippets\VB\API\Telerik\Reporting\EntityDataSourceSnippets.vb region=SampleObjectSnippet}}
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
      	


{{source=CodeSnippets\CS\API\Telerik\Reporting\EntityDataSourceSnippets.cs region=ObjectBindingSnippet}}
````C#
	
	            var objectDataSource = new Telerik.Reporting.ObjectDataSource();
	
	            objectDataSource.DataSource = typeof(SampleBusinessObject);
	            objectDataSource.DataMember = "GetProducts";
	
	            var report = new Report1();
	
	            report.DataSource = objectDataSource;
	
````




{{source=CodeSnippets\VB\API\Telerik\Reporting\EntityDataSourceSnippets.vb region=ObjectBindingSnippet}}
````VB
	
	        Dim objectDataSource As Telerik.Reporting.ObjectDataSource = New Telerik.Reporting.ObjectDataSource()
	
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


The above expression relies upon the lazy loading mechanism of the 
[ADO.NET Entity Framework
](http://msdn.microsoft.com/en-us/library/aa697427%28VS.80%29.aspx
) to 
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
__ObjectContext/DbContext
__ is already destroyed when evaluating the expression, so lazy loading is no longer 
      	possible. One of the greatest advantages of the 
__EntityDataSource
__ component is that it can maintain the 
      	lifecycle of the 
__ObjectContext/DbContext
__ automatically, so scenarios like the previous one are guaranteed to work as 
      	expected. When specifying a 
__Type
__ for the 
__Context
__ property, 
__EntityDataSource
__ creates internally a new 
      	instance of the 
__ObjectContext/DbContext
__ with the given type, keeps it alive for the duration of the report generation 
      	process, and then destroys it automatically when it is no longer needed by the reporting engine. The following 
      	code snippet accomplishes the previous task with the help of the 
__EntityDataSource
__ component:
      	


{{source=CodeSnippets\CS\API\Telerik\Reporting\EntityDataSourceSnippets.cs region=PropertyBindingSnippet}}
````C#
	
	            var entityDataSource = new Telerik.Reporting.EntityDataSource();
	
	            entityDataSource.Context = typeof(AdventureWorksEntities);
	            entityDataSource.ContextMember = "Products";
	
	            var report = new Report1();
	
	            report.DataSource = entityDataSource;
	
````




{{source=CodeSnippets\VB\API\Telerik\Reporting\EntityDataSourceSnippets.vb region=PropertyBindingSnippet}}
````VB
	
	        Dim entityDataSource As New Telerik.Reporting.EntityDataSource()
	
	        entityDataSource.Context = GetType(AdventureWorksEntities)
	        entityDataSource.ContextMember = "Products"
	
	        Dim report As New Report1()
	
	        report.DataSource = entityDataSource
	
````




If you have already implemented your own mechanism for maintaining the lifecycle of the 
__ObjectContext/DbContext
__ 
      	you can continue using the 
__EntityDataSource
__ component. In this case however you need to specify a live instance 
      	of your 
__ObjectContext/DbContext
__ to the 
__Context
__ property as demonstrated here:
    	


{{source=CodeSnippets\CS\API\Telerik\Reporting\EntityDataSourceSnippets.cs region=InstanceBindingSnippet}}
````C#
	
	            var entityDataSource = new Telerik.Reporting.EntityDataSource();
	            var context = new AdventureWorksEntities();
	
	            entityDataSource.Context = context;
	            entityDataSource.ContextMember = "Products";
	
	            var report = new Report1();
	
	            report.DataSource = entityDataSource;
	
	            // You have to dispose the Context explicitly when done with the report.
	            context.Dispose();
	
````




{{source=CodeSnippets\VB\API\Telerik\Reporting\EntityDataSourceSnippets.vb region=InstanceBindingSnippet}}
````VB
	
	        Dim entityDataSource As New Telerik.Reporting.EntityDataSource()
	        Dim context As New AdventureWorksEntities()
	
	        entityDataSource.Context = context
	        entityDataSource.ContextMember = "Products"
	
	        Dim report As New Report1()
	
	        report.DataSource = entityDataSource
	
	        ' You have to dispose the context explicitly when done with the report.
	        context.Dispose()
	
````




# See Also

