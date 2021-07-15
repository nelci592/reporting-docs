---
title: Retrieving data from an Entity Data Model with the EntityDataSource component
page_title: Retrieving data from an Entity Data Model with the EntityDataSource component | for Telerik Reporting Documentation
description: Retrieving data from an Entity Data Model with the EntityDataSource component
slug: telerikreporting/designing-reports/connecting-to-data/data-source-components/entitydatasource-component/retrieving-data-from-an-entity-data-model-with-the-entitydatasource-component
tags: retrieving,data,from,an,entity,data,model,with,the,entitydatasource,component
published: True
position: 5
---

# Retrieving data from an Entity Data Model with the EntityDataSource component



This section discusses various techniques for retrieving data from an __Entity Data Model__ with the help 
    	of the __EntityDataSource__ component. The provided examples and code snippets assume an existing __Entity Data Model__ 
    	of the __Adventure Works__ sample database with the following structure:

  
  ![](images/DataSources/EntityDataSourceAdventureWorksEntityModel.png)

## 

The simplest approach to extract entities from an __Entity Data Model__ is to bind the __EntityDataSource__ component 
      	directly to an auto-generated property of the model, as shown in the sample code below:
      	

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



You can specify expressions to the data item to group, sort or filter the selected entities. The 
      	expressions are evaluated on the application level by the reporting engine after all entities are downloaded
      	from the database. Sometimes it is preferable to offload certain tasks on the database level instead. To do 
      	this you need to define a custom method in the __ObjectContext/DbContext__ class that performs the required business logic. 
      	For example, the following method uses the __Where__ extension method to filter the __Product__ entities:
      	

{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````C#
	
	        partial class AdventureWorksEntities
	        {
	            public System.Collections.Generic.List<Product> GetProducts(string color, decimal price)
	            {
	                return this.Products.Where(product => product.Color == color && product.ListPrice <= price).ToList();
	            }
	        }
	
````



{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````VB
	
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



Using a method instead of a property has the additional benefit that you can pass data source parameters to it, 
      	as illustrated in the following code snippet:
      	

{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````C#
	
	            var entityDataSource = new Telerik.Reporting.EntityDataSource();
	
	            entityDataSource.Context = typeof(AdventureWorksEntities);
	            entityDataSource.ContextMember = "GetProducts";
	            entityDataSource.Parameters.Add("color", typeof(string), "Black");
	            entityDataSource.Parameters.Add("price", typeof(decimal), 100);
	
	            var report = new Report1();
	
	            report.DataSource = entityDataSource;
	
````



{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````VB
	
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



Another common problem is related to the lazy loading feature of the [ADO.NET Entity Framework](http://msdn.microsoft.com/en-us/library/aa697427%28VS.80%29.aspx). For example, let us 
      	consider the following expression that obtains the category of a given product

=Fields.ProductSubcategory.ProductCategory.Name

The above expression relies upon the built-in lazy loading mechanism to obtain the __ProductSubcategory__ 
      	entity for the current __Product__ entity via the corresponding relation property, and then the __ProductCategory__ 
      	entity for the current __ProductSubcategory__ entity. While convenient, lazy loading requires additional round-trips
      	to the database for the entities that are not present in memory. If this happens frequently it might significantly 
      	impact the performance of the report. To overcome this you can try performing eager loading of the entities instead. 
      	For example, the following statement uses the Include method to preload the __ProductSubcategory__ and the __ProductCategory__ 
      	entities while retrieving the __Product__ entities:
      	


	
this.Products.Include("ProductSubcategory").Include("ProductSubcategory.ProductCategory").ToList()




	
Me.Products.Include("ProductSubcategory").Include("ProductSubcategory.ProductCategory").ToList()




However in certain scenarios eager loading might be costly too. Given the previous example, we 
      	materialize all __ProductSubcategory__ and __ProductCategory__ entities only to show the category name of each 
      	product. This means a lot of unnecessary data is downloaded from database just to be discarded later.
The most flexible and efficient method for retrieving data from the __Entity Data Model__ is to execute a custom query 
      	against the entities. The following sample method uses a __LINQ__ query to obtain only the necessary data for 
      	the report and then packs it into a collection of __POCOs:__

{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````C#
	
	        public class ReportData
	        {
	            public string CategoryName { get; set; }
	            public string SubcategoryName { get; set; }
	            public string ProductName { get; set; }
	            public decimal ListPrice { get; set; }
	        }
	
	        partial class AdventureWorksEntities
	        {
	            public System.Collections.Generic.List<ReportData> GetProducts(string category, string subcategory)
	            {
	                var result = from productCategory in this.ProductCategories
	                             where productCategory.Name.StartsWith(category)
	                             from productSubcategory in productCategory.ProductSubcategories
	                             where productSubcategory.Name.StartsWith(subcategory)
	                             from product in productSubcategory.Products
	                             select new ReportData
	                             {
	                                 CategoryName = productCategory.Name,
	                                 SubcategoryName = productSubcategory.Name,
	                                 ProductName = product.Name,
	                                 ListPrice = product.ListPrice
	                             };
	
	                return result.ToList();
	            }
	        }
	
````



{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````VB
	
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



The sample code that binds the EntityDataSource component to that method is shown here:
      	

{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````C#
	
	            var entityDataSource = new Telerik.Reporting.EntityDataSource();
	
	            entityDataSource.Context = typeof(AdventureWorksEntities);
	            entityDataSource.ContextMember = "GetProducts";
	            entityDataSource.Parameters.Add("category", typeof(string), "Bike");
	            entityDataSource.Parameters.Add("subcategory", typeof(string), "Road");
	
	            var report = new Report1();
	
	            report.DataSource = entityDataSource;
	
````



{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````VB
	
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
