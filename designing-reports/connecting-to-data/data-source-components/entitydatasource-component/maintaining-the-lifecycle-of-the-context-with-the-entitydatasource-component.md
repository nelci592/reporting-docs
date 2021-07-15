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



This section discusses how to maintain the lifecycle of the __ObjectContext/DbContext__ when using the 
    	__EntityDataSource__ component. The provided examples and code snippets assume an existing __Entity Data Model__ 
    	of the __Adventure Works__ sample database with the following structure:

  
  ![](images/DataSources/EntityDataSourceAdventureWorksEntityModel.png)

## 

One possible approach to connect to an __Entity Data Model__ without using the __EntityDataSource__ component 
      	is to create a custom business object with a method that retrieves the necessary entities for the report. 
      	The sample code below defines a method that retrieves information about all products:
      	

{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````C#
	
	        public class SampleBusinessObject
	        {
	            public System.Collections.Generic.List<Product> GetProducts()
	            {
	                using (AdventureWorksEntities context = new AdventureWorksEntities())
	                {
	                    return context.Products.ToList();
	                }
	            }
	        }
	
````



{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````VB
	
	    Public Class SampleBusinessObject
	        Public Function GetProducts() As System.Collections.Generic.List(Of Product)
	            Using context As AdventureWorksEntities = New AdventureWorksEntities()
	                Return context.Products.ToList()
	            End Using
	        End Function
	    End Class
	
	    '#End Region
	
	    '#Region SampleMethodSnippet
	
	    Partial Class AdventureWorksEntities
	        Public Function GetProducts(ByVal color As String, ByVal price As Decimal) As System.Collections.Generic.List(Of Product)
	            Return Me.Products.Where(Function(product) product.Color = color And product.ListPrice <= price).ToList()
	        End Function
	    End Class
	
	    '#End Region
	
	    '#Region LinqQuerySnippet
	
	    Public Class ReportData
	        Public Property CategoryName As String
	        Public Property SubcategoryName As String
	        Public Property ProductName As String
	        Public Property ListPrice As Decimal
	    End Class
	
	    Partial Class AdventureWorksEntities
	        Public Function GetProducts(ByVal category As String, ByVal subcategory As String) As System.Collections.Generic.List(Of ReportData)
	            Dim result = From productCategory In Me.ProductCategories
	                         Where productCategory.Name.StartsWith(category)
	                         From productSubcategory In productCategory.ProductSubcategories
	                         Where productCategory.Name.StartsWith(subcategory)
	                         From product In productSubcategory.Products
	                         Select New ReportData With
	                         {
	                             .CategoryName = productCategory.Name,
	                             .SubcategoryName = productSubcategory.Name,
	                             .ProductName = product.Name,
	                             .ListPrice = product.ListPrice
	                         }
	
	            Return result.ToList()
	        End Function
	    End Class
	
	    '#End Region
	
	    Partial Public Class AdventureWorksEntities
	        Implements System.IDisposable
	
	        Public ReadOnly Property ProductCategories As System.Collections.Generic.List(Of ProductCategory)
	            Get
	                Return New System.Collections.Generic.List(Of ProductCategory)
	            End Get
	        End Property
	
	        Public ReadOnly Property ProductSubcategories As System.Collections.Generic.List(Of ProductSubcategory)
	            Get
	                Return New System.Collections.Generic.List(Of ProductSubcategory)
	            End Get
	        End Property
	
	        Public ReadOnly Property ProductModels As System.Collections.Generic.List(Of ProductModel)
	            Get
	                Return New System.Collections.Generic.List(Of ProductModel)
	            End Get
	        End Property
	
	        Public ReadOnly Property Products As System.Collections.Generic.List(Of Product)
	            Get
	                Return New System.Collections.Generic.List(Of Product)
	            End Get
	        End Property
	
	        Public Sub Dispose() Implements IDisposable.Dispose
	        End Sub
	    End Class
	
	    Public Class ProductCategory
	        Public ReadOnly Property Name As String
	            Get
	                Return String.Empty
	            End Get
	        End Property
	
	        Public ReadOnly Property ProductSubcategories As System.Collections.Generic.List(Of ProductSubcategory)
	            Get
	                Return New System.Collections.Generic.List(Of ProductSubcategory)
	            End Get
	        End Property
	    End Class
	
	    Public Class ProductSubcategory
	        Public ReadOnly Property Name As String
	            Get
	                Return String.Empty
	            End Get
	        End Property
	
	        Public ReadOnly Property ProductCategory As ProductCategory
	            Get
	                Return New ProductCategory()
	            End Get
	        End Property
	
	        Public ReadOnly Property Products As System.Collections.Generic.List(Of Product)
	            Get
	                Return New System.Collections.Generic.List(Of Product)
	            End Get
	        End Property
	    End Class
	
	    Public Class ProductModel
	        Public ReadOnly Property Name As String
	            Get
	                Return String.Empty
	            End Get
	        End Property
	
	        Public ReadOnly Property Products As System.Collections.Generic.List(Of Product)
	            Get
	                Return New System.Collections.Generic.List(Of Product)
	            End Get
	        End Property
	    End Class
	
	    Public Class Product
	        Public ReadOnly Property Name As String
	            Get
	                Return String.Empty
	            End Get
	        End Property
	
	        Public ReadOnly Property Color As String
	            Get
	                Return String.Empty
	            End Get
	        End Property
	
	        Public ReadOnly Property ListPrice As Decimal
	            Get
	                Return Decimal.Zero
	            End Get
	        End Property
	
	        Public ReadOnly Property ProductSubcategory As ProductSubcategory
	            Get
	                Return New ProductSubcategory()
	            End Get
	        End Property
	
	        Public ReadOnly Property ProductModel As ProductModel
	            Get
	                Return New ProductModel()
	            End Get
	        End Property
	    End Class
	End Class



Then you can use __ObjectDataSource__ to connect to that business object, as shown in the following code snippet:
      	

{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````C#
	
	            var objectDataSource = new Telerik.Reporting.ObjectDataSource();
	
	            objectDataSource.DataSource = typeof(SampleBusinessObject);
	            objectDataSource.DataMember = "GetProducts";
	
	            var report = new Report1();
	
	            report.DataSource = objectDataSource;
	
````



{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````VB
	
	        Dim objectDataSource As Telerik.Reporting.ObjectDataSource = New Telerik.Reporting.ObjectDataSource()
	
	        objectDataSource.DataSource = GetType(SampleBusinessObject)
	        objectDataSource.DataMember = "GetProducts"
	
	        Dim report As New Report1()
	
	        report.DataSource = objectDataSource
	
	        '#End Region
	    End Sub
	
	    <Microsoft.VisualStudio.TestTools.UnitTesting.TestMethod()>
	    Public Sub ConnectionStringSnippet()
	        '#Region ConnectionStringSnippet
	
	        Dim entityDataSource As Telerik.Reporting.EntityDataSource = New Telerik.Reporting.EntityDataSource()
	
	        entityDataSource.ConnectionString = "AdventureWorksConnection"
	        entityDataSource.Context = GetType(AdventureWorksEntities)
	        entityDataSource.ContextMember = "Products"
	
	        Dim report As New Report1()
	
	        report.DataSource = entityDataSource
	
	        '#End Region
	    End Sub
	
	    <Microsoft.VisualStudio.TestTools.UnitTesting.TestMethod()>
	    Public Sub PropertyBindingSnippet()
	        '#Region PropertyBindingSnippet
	
	        Dim entityDataSource As New Telerik.Reporting.EntityDataSource()
	
	        entityDataSource.Context = GetType(AdventureWorksEntities)
	        entityDataSource.ContextMember = "Products"
	
	        Dim report As New Report1()
	
	        report.DataSource = entityDataSource
	
	        '#End Region
	    End Sub
	
	    <Microsoft.VisualStudio.TestTools.UnitTesting.TestMethod()>
	    Public Sub InstanceBindingSnippet()
	        '#Region InstanceBindingSnippet
	
	        Dim entityDataSource As New Telerik.Reporting.EntityDataSource()
	        Dim context As New AdventureWorksEntities()
	
	        entityDataSource.Context = context
	        entityDataSource.ContextMember = "Products"
	
	        Dim report As New Report1()
	
	        report.DataSource = entityDataSource
	
	        ' You have to dispose the context explicitly when done with the report.
	        context.Dispose()
	
	        '#End Region
	    End Sub
	
	    <Microsoft.VisualStudio.TestTools.UnitTesting.TestMethod()>
	    Public Sub MethodBindingSnippet()
	        '#Region MethodBindingSnippet
	
	        Dim entityDataSource As New Telerik.Reporting.EntityDataSource()
	
	        entityDataSource.Context = GetType(AdventureWorksEntities)
	        entityDataSource.ContextMember = "GetProducts"
	        entityDataSource.Parameters.Add("color", GetType(String), "Black")
	        entityDataSource.Parameters.Add("price", GetType(Decimal), 100)
	
	        Dim report As New Report1()
	
	        report.DataSource = entityDataSource
	
	        '#End Region
	    End Sub
	
	    <Microsoft.VisualStudio.TestTools.UnitTesting.TestMethod()>
	    Public Sub ParameterBindingSnippet()
	        '#Region ParameterBindingSnippet
	
	        Dim entityDataSource As New Telerik.Reporting.EntityDataSource()
	
	        entityDataSource.Context = GetType(AdventureWorksEntities)
	        entityDataSource.ContextMember = "GetProducts"
	        entityDataSource.Parameters.Add("color", GetType(String), "=Parameters.Color.Value")
	        entityDataSource.Parameters.Add("price", GetType(Decimal), "=Parameters.Price.Value")
	
	        Dim report As New Report1()
	
	        report.DataSource = entityDataSource
	        report.ReportParameters.Add("Color", Telerik.Reporting.ReportParameterType.String, "Black")
	        report.ReportParameters.Add("Price", Telerik.Reporting.ReportParameterType.Float, 100)
	
	        '#End Region
	    End Sub
	
	    <Microsoft.VisualStudio.TestTools.UnitTesting.TestMethod()>
	    Public Sub LinqBindingSnippet()
	        '#Region LinqBindingSnippet
	
	        Dim entityDataSource As New Telerik.Reporting.EntityDataSource()
	
	        entityDataSource.Context = GetType(AdventureWorksEntities)
	        entityDataSource.ContextMember = "GetProducts"
	        entityDataSource.Parameters.Add("category", GetType(String), "Bike")
	        entityDataSource.Parameters.Add("subcategory", GetType(String), "Road")
	
	        Dim report As New Report1()
	
	        report.DataSource = entityDataSource
	
	        '#End Region
	    End Sub
	
	    '#Region SampleObjectSnippet
	
	    Public Class SampleBusinessObject
	        Public Function GetProducts() As System.Collections.Generic.List(Of Product)
	            Using context As AdventureWorksEntities = New AdventureWorksEntities()
	                Return context.Products.ToList()
	            End Using
	        End Function
	    End Class
	
	    '#End Region
	
	    '#Region SampleMethodSnippet
	
	    Partial Class AdventureWorksEntities
	        Public Function GetProducts(ByVal color As String, ByVal price As Decimal) As System.Collections.Generic.List(Of Product)
	            Return Me.Products.Where(Function(product) product.Color = color And product.ListPrice <= price).ToList()
	        End Function
	    End Class
	
	    '#End Region
	
	    '#Region LinqQuerySnippet
	
	    Public Class ReportData
	        Public Property CategoryName As String
	        Public Property SubcategoryName As String
	        Public Property ProductName As String
	        Public Property ListPrice As Decimal
	    End Class
	
	    Partial Class AdventureWorksEntities
	        Public Function GetProducts(ByVal category As String, ByVal subcategory As String) As System.Collections.Generic.List(Of ReportData)
	            Dim result = From productCategory In Me.ProductCategories
	                         Where productCategory.Name.StartsWith(category)
	                         From productSubcategory In productCategory.ProductSubcategories
	                         Where productCategory.Name.StartsWith(subcategory)
	                         From product In productSubcategory.Products
	                         Select New ReportData With
	                         {
	                             .CategoryName = productCategory.Name,
	                             .SubcategoryName = productSubcategory.Name,
	                             .ProductName = product.Name,
	                             .ListPrice = product.ListPrice
	                         }
	
	            Return result.ToList()
	        End Function
	    End Class
	
	    '#End Region
	
	    Partial Public Class AdventureWorksEntities
	        Implements System.IDisposable
	
	        Public ReadOnly Property ProductCategories As System.Collections.Generic.List(Of ProductCategory)
	            Get
	                Return New System.Collections.Generic.List(Of ProductCategory)
	            End Get
	        End Property
	
	        Public ReadOnly Property ProductSubcategories As System.Collections.Generic.List(Of ProductSubcategory)
	            Get
	                Return New System.Collections.Generic.List(Of ProductSubcategory)
	            End Get
	        End Property
	
	        Public ReadOnly Property ProductModels As System.Collections.Generic.List(Of ProductModel)
	            Get
	                Return New System.Collections.Generic.List(Of ProductModel)
	            End Get
	        End Property
	
	        Public ReadOnly Property Products As System.Collections.Generic.List(Of Product)
	            Get
	                Return New System.Collections.Generic.List(Of Product)
	            End Get
	        End Property
	
	        Public Sub Dispose() Implements IDisposable.Dispose
	        End Sub
	    End Class
	
	    Public Class ProductCategory
	        Public ReadOnly Property Name As String
	            Get
	                Return String.Empty
	            End Get
	        End Property
	
	        Public ReadOnly Property ProductSubcategories As System.Collections.Generic.List(Of ProductSubcategory)
	            Get
	                Return New System.Collections.Generic.List(Of ProductSubcategory)
	            End Get
	        End Property
	    End Class
	
	    Public Class ProductSubcategory
	        Public ReadOnly Property Name As String
	            Get
	                Return String.Empty
	            End Get
	        End Property
	
	        Public ReadOnly Property ProductCategory As ProductCategory
	            Get
	                Return New ProductCategory()
	            End Get
	        End Property
	
	        Public ReadOnly Property Products As System.Collections.Generic.List(Of Product)
	            Get
	                Return New System.Collections.Generic.List(Of Product)
	            End Get
	        End Property
	    End Class
	
	    Public Class ProductModel
	        Public ReadOnly Property Name As String
	            Get
	                Return String.Empty
	            End Get
	        End Property
	
	        Public ReadOnly Property Products As System.Collections.Generic.List(Of Product)
	            Get
	                Return New System.Collections.Generic.List(Of Product)
	            End Get
	        End Property
	    End Class
	
	    Public Class Product
	        Public ReadOnly Property Name As String
	            Get
	                Return String.Empty
	            End Get
	        End Property
	
	        Public ReadOnly Property Color As String
	            Get
	                Return String.Empty
	            End Get
	        End Property
	
	        Public ReadOnly Property ListPrice As Decimal
	            Get
	                Return Decimal.Zero
	            End Get
	        End Property
	
	        Public ReadOnly Property ProductSubcategory As ProductSubcategory
	            Get
	                Return New ProductSubcategory()
	            End Get
	        End Property
	
	        Public ReadOnly Property ProductModel As ProductModel
	            Get
	                Return New ProductModel()
	            End Get
	        End Property
	    End Class
	End Class



The problem with this approach is that it is not guaranteed to work in all possible scenarios. Simple expressions 
      	accessing primitive properties of the __Product__ entity might work as expected:
      	

=Fields.Name

However, let us consider the following expression that is intended to obtain the category of a given product:

=Fields.ProductSubcategory.ProductCategory.Name

The above expression relies upon the lazy loading mechanism of the [ADO.NET Entity Framework](http://msdn.microsoft.com/en-us/library/aa697427%28VS.80%29.aspx) to 
      	obtain the __ProductSubcategory__ entity for the current __Product__ entity via the corresponding relation property, 
      	and then the __ProductCategory__ entity for the current __ProductSubcategory__ entity. This is not guaranteed to work 
      	because the __ObjectContext/DbContext__ is already destroyed when evaluating the expression, so lazy loading is no longer 
      	possible. One of the greatest advantages of the __EntityDataSource__ component is that it can maintain the 
      	lifecycle of the __ObjectContext/DbContext__ automatically, so scenarios like the previous one are guaranteed to work as 
      	expected. When specifying a __Type__ for the __Context__ property, __EntityDataSource__ creates internally a new 
      	instance of the __ObjectContext/DbContext__ with the given type, keeps it alive for the duration of the report generation 
      	process, and then destroys it automatically when it is no longer needed by the reporting engine. The following 
      	code snippet accomplishes the previous task with the help of the __EntityDataSource__ component:
      	

{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````C#
	
	            var entityDataSource = new Telerik.Reporting.EntityDataSource();
	
	            entityDataSource.Context = typeof(AdventureWorksEntities);
	            entityDataSource.ContextMember = "Products";
	
	            var report = new Report1();
	
	            report.DataSource = entityDataSource;
	
````



{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````VB
	
	        Dim entityDataSource As New Telerik.Reporting.EntityDataSource()
	
	        entityDataSource.Context = GetType(AdventureWorksEntities)
	        entityDataSource.ContextMember = "Products"
	
	        Dim report As New Report1()
	
	        report.DataSource = entityDataSource
	
	        '#End Region
	    End Sub
	
	    <Microsoft.VisualStudio.TestTools.UnitTesting.TestMethod()>
	    Public Sub InstanceBindingSnippet()
	        '#Region InstanceBindingSnippet
	
	        Dim entityDataSource As New Telerik.Reporting.EntityDataSource()
	        Dim context As New AdventureWorksEntities()
	
	        entityDataSource.Context = context
	        entityDataSource.ContextMember = "Products"
	
	        Dim report As New Report1()
	
	        report.DataSource = entityDataSource
	
	        ' You have to dispose the context explicitly when done with the report.
	        context.Dispose()
	
	        '#End Region
	    End Sub
	
	    <Microsoft.VisualStudio.TestTools.UnitTesting.TestMethod()>
	    Public Sub MethodBindingSnippet()
	        '#Region MethodBindingSnippet
	
	        Dim entityDataSource As New Telerik.Reporting.EntityDataSource()
	
	        entityDataSource.Context = GetType(AdventureWorksEntities)
	        entityDataSource.ContextMember = "GetProducts"
	        entityDataSource.Parameters.Add("color", GetType(String), "Black")
	        entityDataSource.Parameters.Add("price", GetType(Decimal), 100)
	
	        Dim report As New Report1()
	
	        report.DataSource = entityDataSource
	
	        '#End Region
	    End Sub
	
	    <Microsoft.VisualStudio.TestTools.UnitTesting.TestMethod()>
	    Public Sub ParameterBindingSnippet()
	        '#Region ParameterBindingSnippet
	
	        Dim entityDataSource As New Telerik.Reporting.EntityDataSource()
	
	        entityDataSource.Context = GetType(AdventureWorksEntities)
	        entityDataSource.ContextMember = "GetProducts"
	        entityDataSource.Parameters.Add("color", GetType(String), "=Parameters.Color.Value")
	        entityDataSource.Parameters.Add("price", GetType(Decimal), "=Parameters.Price.Value")
	
	        Dim report As New Report1()
	
	        report.DataSource = entityDataSource
	        report.ReportParameters.Add("Color", Telerik.Reporting.ReportParameterType.String, "Black")
	        report.ReportParameters.Add("Price", Telerik.Reporting.ReportParameterType.Float, 100)
	
	        '#End Region
	    End Sub
	
	    <Microsoft.VisualStudio.TestTools.UnitTesting.TestMethod()>
	    Public Sub LinqBindingSnippet()
	        '#Region LinqBindingSnippet
	
	        Dim entityDataSource As New Telerik.Reporting.EntityDataSource()
	
	        entityDataSource.Context = GetType(AdventureWorksEntities)
	        entityDataSource.ContextMember = "GetProducts"
	        entityDataSource.Parameters.Add("category", GetType(String), "Bike")
	        entityDataSource.Parameters.Add("subcategory", GetType(String), "Road")
	
	        Dim report As New Report1()
	
	        report.DataSource = entityDataSource
	
	        '#End Region
	    End Sub
	
	    '#Region SampleObjectSnippet
	
	    Public Class SampleBusinessObject
	        Public Function GetProducts() As System.Collections.Generic.List(Of Product)
	            Using context As AdventureWorksEntities = New AdventureWorksEntities()
	                Return context.Products.ToList()
	            End Using
	        End Function
	    End Class
	
	    '#End Region
	
	    '#Region SampleMethodSnippet
	
	    Partial Class AdventureWorksEntities
	        Public Function GetProducts(ByVal color As String, ByVal price As Decimal) As System.Collections.Generic.List(Of Product)
	            Return Me.Products.Where(Function(product) product.Color = color And product.ListPrice <= price).ToList()
	        End Function
	    End Class
	
	    '#End Region
	
	    '#Region LinqQuerySnippet
	
	    Public Class ReportData
	        Public Property CategoryName As String
	        Public Property SubcategoryName As String
	        Public Property ProductName As String
	        Public Property ListPrice As Decimal
	    End Class
	
	    Partial Class AdventureWorksEntities
	        Public Function GetProducts(ByVal category As String, ByVal subcategory As String) As System.Collections.Generic.List(Of ReportData)
	            Dim result = From productCategory In Me.ProductCategories
	                         Where productCategory.Name.StartsWith(category)
	                         From productSubcategory In productCategory.ProductSubcategories
	                         Where productCategory.Name.StartsWith(subcategory)
	                         From product In productSubcategory.Products
	                         Select New ReportData With
	                         {
	                             .CategoryName = productCategory.Name,
	                             .SubcategoryName = productSubcategory.Name,
	                             .ProductName = product.Name,
	                             .ListPrice = product.ListPrice
	                         }
	
	            Return result.ToList()
	        End Function
	    End Class
	
	    '#End Region
	
	    Partial Public Class AdventureWorksEntities
	        Implements System.IDisposable
	
	        Public ReadOnly Property ProductCategories As System.Collections.Generic.List(Of ProductCategory)
	            Get
	                Return New System.Collections.Generic.List(Of ProductCategory)
	            End Get
	        End Property
	
	        Public ReadOnly Property ProductSubcategories As System.Collections.Generic.List(Of ProductSubcategory)
	            Get
	                Return New System.Collections.Generic.List(Of ProductSubcategory)
	            End Get
	        End Property
	
	        Public ReadOnly Property ProductModels As System.Collections.Generic.List(Of ProductModel)
	            Get
	                Return New System.Collections.Generic.List(Of ProductModel)
	            End Get
	        End Property
	
	        Public ReadOnly Property Products As System.Collections.Generic.List(Of Product)
	            Get
	                Return New System.Collections.Generic.List(Of Product)
	            End Get
	        End Property
	
	        Public Sub Dispose() Implements IDisposable.Dispose
	        End Sub
	    End Class
	
	    Public Class ProductCategory
	        Public ReadOnly Property Name As String
	            Get
	                Return String.Empty
	            End Get
	        End Property
	
	        Public ReadOnly Property ProductSubcategories As System.Collections.Generic.List(Of ProductSubcategory)
	            Get
	                Return New System.Collections.Generic.List(Of ProductSubcategory)
	            End Get
	        End Property
	    End Class
	
	    Public Class ProductSubcategory
	        Public ReadOnly Property Name As String
	            Get
	                Return String.Empty
	            End Get
	        End Property
	
	        Public ReadOnly Property ProductCategory As ProductCategory
	            Get
	                Return New ProductCategory()
	            End Get
	        End Property
	
	        Public ReadOnly Property Products As System.Collections.Generic.List(Of Product)
	            Get
	                Return New System.Collections.Generic.List(Of Product)
	            End Get
	        End Property
	    End Class
	
	    Public Class ProductModel
	        Public ReadOnly Property Name As String
	            Get
	                Return String.Empty
	            End Get
	        End Property
	
	        Public ReadOnly Property Products As System.Collections.Generic.List(Of Product)
	            Get
	                Return New System.Collections.Generic.List(Of Product)
	            End Get
	        End Property
	    End Class
	
	    Public Class Product
	        Public ReadOnly Property Name As String
	            Get
	                Return String.Empty
	            End Get
	        End Property
	
	        Public ReadOnly Property Color As String
	            Get
	                Return String.Empty
	            End Get
	        End Property
	
	        Public ReadOnly Property ListPrice As Decimal
	            Get
	                Return Decimal.Zero
	            End Get
	        End Property
	
	        Public ReadOnly Property ProductSubcategory As ProductSubcategory
	            Get
	                Return New ProductSubcategory()
	            End Get
	        End Property
	
	        Public ReadOnly Property ProductModel As ProductModel
	            Get
	                Return New ProductModel()
	            End Get
	        End Property
	    End Class
	End Class



If you have already implemented your own mechanism for maintaining the lifecycle of the __ObjectContext/DbContext__ 
      	you can continue using the __EntityDataSource__ component. In this case however you need to specify a live instance 
      	of your __ObjectContext/DbContext__ to the __Context__ property as demonstrated here:
    	

{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````C#
	
	            var entityDataSource = new Telerik.Reporting.EntityDataSource();
	            var context = new AdventureWorksEntities();
	
	            entityDataSource.Context = context;
	            entityDataSource.ContextMember = "Products";
	
	            var report = new Report1();
	
	            report.DataSource = entityDataSource;
	
	            // You have to dispose the Context explicitly when done with the report.
	            context.Dispose();
	
````



{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````VB
	
	        Dim entityDataSource As New Telerik.Reporting.EntityDataSource()
	        Dim context As New AdventureWorksEntities()
	
	        entityDataSource.Context = context
	        entityDataSource.ContextMember = "Products"
	
	        Dim report As New Report1()
	
	        report.DataSource = entityDataSource
	
	        ' You have to dispose the context explicitly when done with the report.
	        context.Dispose()
	
	        '#End Region
	    End Sub
	
	    <Microsoft.VisualStudio.TestTools.UnitTesting.TestMethod()>
	    Public Sub MethodBindingSnippet()
	        '#Region MethodBindingSnippet
	
	        Dim entityDataSource As New Telerik.Reporting.EntityDataSource()
	
	        entityDataSource.Context = GetType(AdventureWorksEntities)
	        entityDataSource.ContextMember = "GetProducts"
	        entityDataSource.Parameters.Add("color", GetType(String), "Black")
	        entityDataSource.Parameters.Add("price", GetType(Decimal), 100)
	
	        Dim report As New Report1()
	
	        report.DataSource = entityDataSource
	
	        '#End Region
	    End Sub
	
	    <Microsoft.VisualStudio.TestTools.UnitTesting.TestMethod()>
	    Public Sub ParameterBindingSnippet()
	        '#Region ParameterBindingSnippet
	
	        Dim entityDataSource As New Telerik.Reporting.EntityDataSource()
	
	        entityDataSource.Context = GetType(AdventureWorksEntities)
	        entityDataSource.ContextMember = "GetProducts"
	        entityDataSource.Parameters.Add("color", GetType(String), "=Parameters.Color.Value")
	        entityDataSource.Parameters.Add("price", GetType(Decimal), "=Parameters.Price.Value")
	
	        Dim report As New Report1()
	
	        report.DataSource = entityDataSource
	        report.ReportParameters.Add("Color", Telerik.Reporting.ReportParameterType.String, "Black")
	        report.ReportParameters.Add("Price", Telerik.Reporting.ReportParameterType.Float, 100)
	
	        '#End Region
	    End Sub
	
	    <Microsoft.VisualStudio.TestTools.UnitTesting.TestMethod()>
	    Public Sub LinqBindingSnippet()
	        '#Region LinqBindingSnippet
	
	        Dim entityDataSource As New Telerik.Reporting.EntityDataSource()
	
	        entityDataSource.Context = GetType(AdventureWorksEntities)
	        entityDataSource.ContextMember = "GetProducts"
	        entityDataSource.Parameters.Add("category", GetType(String), "Bike")
	        entityDataSource.Parameters.Add("subcategory", GetType(String), "Road")
	
	        Dim report As New Report1()
	
	        report.DataSource = entityDataSource
	
	        '#End Region
	    End Sub
	
	    '#Region SampleObjectSnippet
	
	    Public Class SampleBusinessObject
	        Public Function GetProducts() As System.Collections.Generic.List(Of Product)
	            Using context As AdventureWorksEntities = New AdventureWorksEntities()
	                Return context.Products.ToList()
	            End Using
	        End Function
	    End Class
	
	    '#End Region
	
	    '#Region SampleMethodSnippet
	
	    Partial Class AdventureWorksEntities
	        Public Function GetProducts(ByVal color As String, ByVal price As Decimal) As System.Collections.Generic.List(Of Product)
	            Return Me.Products.Where(Function(product) product.Color = color And product.ListPrice <= price).ToList()
	        End Function
	    End Class
	
	    '#End Region
	
	    '#Region LinqQuerySnippet
	
	    Public Class ReportData
	        Public Property CategoryName As String
	        Public Property SubcategoryName As String
	        Public Property ProductName As String
	        Public Property ListPrice As Decimal
	    End Class
	
	    Partial Class AdventureWorksEntities
	        Public Function GetProducts(ByVal category As String, ByVal subcategory As String) As System.Collections.Generic.List(Of ReportData)
	            Dim result = From productCategory In Me.ProductCategories
	                         Where productCategory.Name.StartsWith(category)
	                         From productSubcategory In productCategory.ProductSubcategories
	                         Where productCategory.Name.StartsWith(subcategory)
	                         From product In productSubcategory.Products
	                         Select New ReportData With
	                         {
	                             .CategoryName = productCategory.Name,
	                             .SubcategoryName = productSubcategory.Name,
	                             .ProductName = product.Name,
	                             .ListPrice = product.ListPrice
	                         }
	
	            Return result.ToList()
	        End Function
	    End Class
	
	    '#End Region
	
	    Partial Public Class AdventureWorksEntities
	        Implements System.IDisposable
	
	        Public ReadOnly Property ProductCategories As System.Collections.Generic.List(Of ProductCategory)
	            Get
	                Return New System.Collections.Generic.List(Of ProductCategory)
	            End Get
	        End Property
	
	        Public ReadOnly Property ProductSubcategories As System.Collections.Generic.List(Of ProductSubcategory)
	            Get
	                Return New System.Collections.Generic.List(Of ProductSubcategory)
	            End Get
	        End Property
	
	        Public ReadOnly Property ProductModels As System.Collections.Generic.List(Of ProductModel)
	            Get
	                Return New System.Collections.Generic.List(Of ProductModel)
	            End Get
	        End Property
	
	        Public ReadOnly Property Products As System.Collections.Generic.List(Of Product)
	            Get
	                Return New System.Collections.Generic.List(Of Product)
	            End Get
	        End Property
	
	        Public Sub Dispose() Implements IDisposable.Dispose
	        End Sub
	    End Class
	
	    Public Class ProductCategory
	        Public ReadOnly Property Name As String
	            Get
	                Return String.Empty
	            End Get
	        End Property
	
	        Public ReadOnly Property ProductSubcategories As System.Collections.Generic.List(Of ProductSubcategory)
	            Get
	                Return New System.Collections.Generic.List(Of ProductSubcategory)
	            End Get
	        End Property
	    End Class
	
	    Public Class ProductSubcategory
	        Public ReadOnly Property Name As String
	            Get
	                Return String.Empty
	            End Get
	        End Property
	
	        Public ReadOnly Property ProductCategory As ProductCategory
	            Get
	                Return New ProductCategory()
	            End Get
	        End Property
	
	        Public ReadOnly Property Products As System.Collections.Generic.List(Of Product)
	            Get
	                Return New System.Collections.Generic.List(Of Product)
	            End Get
	        End Property
	    End Class
	
	    Public Class ProductModel
	        Public ReadOnly Property Name As String
	            Get
	                Return String.Empty
	            End Get
	        End Property
	
	        Public ReadOnly Property Products As System.Collections.Generic.List(Of Product)
	            Get
	                Return New System.Collections.Generic.List(Of Product)
	            End Get
	        End Property
	    End Class
	
	    Public Class Product
	        Public ReadOnly Property Name As String
	            Get
	                Return String.Empty
	            End Get
	        End Property
	
	        Public ReadOnly Property Color As String
	            Get
	                Return String.Empty
	            End Get
	        End Property
	
	        Public ReadOnly Property ListPrice As Decimal
	            Get
	                Return Decimal.Zero
	            End Get
	        End Property
	
	        Public ReadOnly Property ProductSubcategory As ProductSubcategory
	            Get
	                Return New ProductSubcategory()
	            End Get
	        End Property
	
	        Public ReadOnly Property ProductModel As ProductModel
	            Get
	                Return New ProductModel()
	            End Get
	        End Property
	    End Class
	End Class



# See Also
