---
title: Connecting to a Telerik Data Access Model with the OpenAccessDataSource component
page_title: Connecting to a Telerik Data Access Model with the OpenAccessDataSource component | for Telerik Reporting Documentation
description: Connecting to a Telerik Data Access Model with the OpenAccessDataSource component
slug: telerikreporting/designing-reports/connecting-to-data/data-source-components/openaccessdatasource-component/connecting-to-a-telerik-data-access-model-with-the-openaccessdatasource-component
tags: connecting,to,a,telerik,data,access,model,with,the,openaccessdatasource,component
published: True
position: 1
---

# Connecting to a Telerik Data Access Model with the OpenAccessDataSource component



This section discusses how to connect the __OpenAccessDataSource__ component to a __Telerik Data Access Model__.
    	The provided examples and code snippets assume an existing __Telerik Data Access Model__ of the __Adventure Works__ 
    	sample database with the following structure:  
  ![](images/DataSources/OpenAccessDataSourceAdventureWorksEntityModel.png)

## 

The simplest way to configure __OpenAccessDataSource__ in __Report Designer__ is to use 
      	the [OpenAccessDataSource Wizard]({%slug telerikreporting/designing-reports/report-designer-tools/desktop-designers/tools/data-source-wizards/openaccessdatasource-wizard%}). That wizard is started automatically when you create a new __OpenAccessDataSource__, but you can invoke 
      	it manually at any time from the context menu associated with the data source by choosing __"Configure"__:

  
  ![](images/DataSources/OpenAccessDataSourceConfigure.png)

To configure the __OpenAccessDataSource__ component programmatically you need to specify at least an __ObjectContext__
      	and a property or a method from that __ObjectContext__ which is responsible for data retrieval. Assign the type of 
      	the __OpenAccessContext__ to the __ObjectContext__ property of __OpenAccessDataSource__ and the name of the desired member to the 
      	__ObjectContextMember__ property, as shown in the following example:
      	

{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````C#
	
	            var openAccessDataSource = new Telerik.Reporting.OpenAccessDataSource();
	
	            openAccessDataSource.ObjectContext = typeof(AdventureWorksEntities);
	            openAccessDataSource.ObjectContextMember = "Products";
	
	            var report = new Report1();
	
	            report.DataSource = openAccessDataSource;
	
````



{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````VB
	
	        Dim openAccessDataSource As New Telerik.Reporting.OpenAccessDataSource()
	
	        openAccessDataSource.ObjectContext = GetType(AdventureWorksEntities)
	        openAccessDataSource.ObjectContextMember = "Products"
	
	        Dim report As New Report1()
	
	        report.DataSource = openAccessDataSource
	
	        '#End Region
	    End Sub
	
	    <Microsoft.VisualStudio.TestTools.UnitTesting.TestMethod()>
	    Public Sub InstanceBindingSnippet()
	        '#Region InstanceBindingSnippet
	
	        Dim openAccessDataSource As Telerik.Reporting.OpenAccessDataSource = New Telerik.Reporting.OpenAccessDataSource()
	        Dim openAccessContext As AdventureWorksEntities = New AdventureWorksEntities()
	
	        openAccessDataSource.ObjectContext = openAccessContext
	        openAccessDataSource.ObjectContextMember = "Products"
	
	        Dim report As New Report1()
	
	        report.DataSource = openAccessDataSource
	
	        ' You have to dispose the OpenAccessContext explicitly when done with the report.
	        openAccessContext.Dispose()
	
	        '#End Region
	    End Sub
	
	    <Microsoft.VisualStudio.TestTools.UnitTesting.TestMethod()>
	    Public Sub MethodBindingSnippet()
	        '#Region MethodBindingSnippet
	
	        Dim openAccessDataSource As New Telerik.Reporting.OpenAccessDataSource()
	
	        openAccessDataSource.ObjectContext = GetType(AdventureWorksEntities)
	        openAccessDataSource.ObjectContextMember = "GetProducts"
	        openAccessDataSource.Parameters.Add("color", GetType(String), "Black")
	        openAccessDataSource.Parameters.Add("price", GetType(Decimal), 100)
	
	        Dim report As New Report1()
	
	        report.DataSource = openAccessDataSource
	
	        '#End Region
	    End Sub
	
	    <Microsoft.VisualStudio.TestTools.UnitTesting.TestMethod()>
	    Public Sub ParameterBindingSnippet()
	        '#Region ParameterBindingSnippet
	
	        Dim openAccessDataSource As New Telerik.Reporting.OpenAccessDataSource()
	
	        openAccessDataSource.ObjectContext = GetType(AdventureWorksEntities)
	        openAccessDataSource.ObjectContextMember = "GetProducts"
	        openAccessDataSource.Parameters.Add("color", GetType(String), "=Parameters.Color.Value")
	        openAccessDataSource.Parameters.Add("price", GetType(Decimal), "=Parameters.Price.Value")
	
	        Dim report As New Report1()
	
	        report.DataSource = openAccessDataSource
	        report.ReportParameters.Add("Color", Telerik.Reporting.ReportParameterType.String, "Black")
	        report.ReportParameters.Add("Price", Telerik.Reporting.ReportParameterType.Float, 100)
	
	        '#End Region
	    End Sub
	
	    <Microsoft.VisualStudio.TestTools.UnitTesting.TestMethod()>
	    Public Sub LinqBindingSnippet()
	        '#Region LinqBindingSnippet
	
	        Dim openAccessDataSource As New Telerik.Reporting.OpenAccessDataSource()
	
	        openAccessDataSource.ObjectContext = GetType(AdventureWorksEntities)
	        openAccessDataSource.ObjectContextMember = "GetProducts"
	        openAccessDataSource.Parameters.Add("category", GetType(String), "Bike")
	        openAccessDataSource.Parameters.Add("subcategory", GetType(String), "Road")
	
	        Dim report As New Report1()
	
	        report.DataSource = openAccessDataSource
	
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



The above code snippet connects the __OpenAccessDataSource__ component to the __AdventureWorksEntities__ 
      	context and retrieves the information for all products from the __Products__ auto-generated property.
Instead of specifying a type you can assign a live instance of the __OpenAccessContext__. In this case however it is 
      	your responsibility to destroy that __OpenAccessContext__ instance when done with the report:
      	

{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````C#
	
	            var openAccessDataSource = new Telerik.Reporting.OpenAccessDataSource();
	            var openAccessContext = new AdventureWorksEntities();
	
	            openAccessDataSource.ObjectContext = openAccessContext;
	            openAccessDataSource.ObjectContextMember = "Products";
	
	            var report = new Report1();
	
	            report.DataSource = openAccessDataSource;
	
	            // You have to dispose the OpenAccessContext explicitly when done with the report.
	            openAccessContext.Dispose();
	
````



{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````VB
	
	        Dim openAccessDataSource As Telerik.Reporting.OpenAccessDataSource = New Telerik.Reporting.OpenAccessDataSource()
	        Dim openAccessContext As AdventureWorksEntities = New AdventureWorksEntities()
	
	        openAccessDataSource.ObjectContext = openAccessContext
	        openAccessDataSource.ObjectContextMember = "Products"
	
	        Dim report As New Report1()
	
	        report.DataSource = openAccessDataSource
	
	        ' You have to dispose the OpenAccessContext explicitly when done with the report.
	        openAccessContext.Dispose()
	
	        '#End Region
	    End Sub
	
	    <Microsoft.VisualStudio.TestTools.UnitTesting.TestMethod()>
	    Public Sub MethodBindingSnippet()
	        '#Region MethodBindingSnippet
	
	        Dim openAccessDataSource As New Telerik.Reporting.OpenAccessDataSource()
	
	        openAccessDataSource.ObjectContext = GetType(AdventureWorksEntities)
	        openAccessDataSource.ObjectContextMember = "GetProducts"
	        openAccessDataSource.Parameters.Add("color", GetType(String), "Black")
	        openAccessDataSource.Parameters.Add("price", GetType(Decimal), 100)
	
	        Dim report As New Report1()
	
	        report.DataSource = openAccessDataSource
	
	        '#End Region
	    End Sub
	
	    <Microsoft.VisualStudio.TestTools.UnitTesting.TestMethod()>
	    Public Sub ParameterBindingSnippet()
	        '#Region ParameterBindingSnippet
	
	        Dim openAccessDataSource As New Telerik.Reporting.OpenAccessDataSource()
	
	        openAccessDataSource.ObjectContext = GetType(AdventureWorksEntities)
	        openAccessDataSource.ObjectContextMember = "GetProducts"
	        openAccessDataSource.Parameters.Add("color", GetType(String), "=Parameters.Color.Value")
	        openAccessDataSource.Parameters.Add("price", GetType(Decimal), "=Parameters.Price.Value")
	
	        Dim report As New Report1()
	
	        report.DataSource = openAccessDataSource
	        report.ReportParameters.Add("Color", Telerik.Reporting.ReportParameterType.String, "Black")
	        report.ReportParameters.Add("Price", Telerik.Reporting.ReportParameterType.Float, 100)
	
	        '#End Region
	    End Sub
	
	    <Microsoft.VisualStudio.TestTools.UnitTesting.TestMethod()>
	    Public Sub LinqBindingSnippet()
	        '#Region LinqBindingSnippet
	
	        Dim openAccessDataSource As New Telerik.Reporting.OpenAccessDataSource()
	
	        openAccessDataSource.ObjectContext = GetType(AdventureWorksEntities)
	        openAccessDataSource.ObjectContextMember = "GetProducts"
	        openAccessDataSource.Parameters.Add("category", GetType(String), "Bike")
	        openAccessDataSource.Parameters.Add("subcategory", GetType(String), "Road")
	
	        Dim report As New Report1()
	
	        report.DataSource = openAccessDataSource
	
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



Binding to a method is more flexible than binding to a property, because it is possible to execute some 
      	custom business logic when retrieving data for the report. If the specified method has arguments, the 
      	__OpenAccessDataSource__ component allows you to pass parameters to those arguments via the __Parameters__ collection. 
      	For example, let us extend the __AdventureWorksEntities__ context using a partial class that defines the following
      	method:
      	

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



You can bind the __OpenAccessDataSource__ component to that method with the following code snippet:
      	

{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````C#
	
	            var openAccessDataSource = new Telerik.Reporting.OpenAccessDataSource();
	
	            openAccessDataSource.ObjectContext = typeof(AdventureWorksEntities);
	            openAccessDataSource.ObjectContextMember = "GetProducts";
	            openAccessDataSource.Parameters.Add("color", typeof(string), "Black");
	            openAccessDataSource.Parameters.Add("price", typeof(decimal), 100);
	
	            var report = new Report1();
	
	            report.DataSource = openAccessDataSource;
	
````



{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````VB
	
	        Dim openAccessDataSource As New Telerik.Reporting.OpenAccessDataSource()
	
	        openAccessDataSource.ObjectContext = GetType(AdventureWorksEntities)
	        openAccessDataSource.ObjectContextMember = "GetProducts"
	        openAccessDataSource.Parameters.Add("color", GetType(String), "Black")
	        openAccessDataSource.Parameters.Add("price", GetType(Decimal), 100)
	
	        Dim report As New Report1()
	
	        report.DataSource = openAccessDataSource
	
	        '#End Region
	    End Sub
	
	    <Microsoft.VisualStudio.TestTools.UnitTesting.TestMethod()>
	    Public Sub ParameterBindingSnippet()
	        '#Region ParameterBindingSnippet
	
	        Dim openAccessDataSource As New Telerik.Reporting.OpenAccessDataSource()
	
	        openAccessDataSource.ObjectContext = GetType(AdventureWorksEntities)
	        openAccessDataSource.ObjectContextMember = "GetProducts"
	        openAccessDataSource.Parameters.Add("color", GetType(String), "=Parameters.Color.Value")
	        openAccessDataSource.Parameters.Add("price", GetType(Decimal), "=Parameters.Price.Value")
	
	        Dim report As New Report1()
	
	        report.DataSource = openAccessDataSource
	        report.ReportParameters.Add("Color", Telerik.Reporting.ReportParameterType.String, "Black")
	        report.ReportParameters.Add("Price", Telerik.Reporting.ReportParameterType.Float, 100)
	
	        '#End Region
	    End Sub
	
	    <Microsoft.VisualStudio.TestTools.UnitTesting.TestMethod()>
	    Public Sub LinqBindingSnippet()
	        '#Region LinqBindingSnippet
	
	        Dim openAccessDataSource As New Telerik.Reporting.OpenAccessDataSource()
	
	        openAccessDataSource.ObjectContext = GetType(AdventureWorksEntities)
	        openAccessDataSource.ObjectContextMember = "GetProducts"
	        openAccessDataSource.Parameters.Add("category", GetType(String), "Bike")
	        openAccessDataSource.Parameters.Add("subcategory", GetType(String), "Road")
	
	        Dim report As New Report1()
	
	        report.DataSource = openAccessDataSource
	
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



>note The names and types of the parameters in the  __Parameters__  collection should match exactly the names and 	types of the method arguments. In case this requirement is not fulfilled the  __OpenAccessDataSource__  component will 	not be able to resolve or call correctly the method and will raise an exception at runtime.


# See Also
