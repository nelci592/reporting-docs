---
title: Configuring the database connectivity with the OpenAccessDataSource component
page_title: Configuring the database connectivity with the OpenAccessDataSource component | for Telerik Reporting Documentation
description: Configuring the database connectivity with the OpenAccessDataSource component
slug: telerikreporting/designing-reports/connecting-to-data/data-source-components/openaccessdatasource-component/configuring-the-database-connectivity-with-the-openaccessdatasource-component
tags: configuring,the,database,connectivity,with,the,openaccessdatasource,component
published: True
position: 3
---

# Configuring the database connectivity with the OpenAccessDataSource component



This section discusses how to specify a database connection to the __OpenAccessDataSource__ component 
    	that can be used both at design-time and when running the report in production. The provided examples 
    	and code snippets assume an existing __Telerik Data Access Model__ of the __Adventure Works__ sample database with the 
    	following structure:

  
  ![](images/DataSources/OpenAccessDataSourceAdventureWorksEntityModel.png)

## 

Strictly speaking, it is not necessary to specify a database connection when working with the 
      	__OpenAccessDataSource__ component. Simply specifying an __OpenAccessContext__ and a member is enough to connect to 
      	the __Telerik Data Access Model__, because the __OpenAccessContext__ is already configured to access the database. The 
      	following code snippet shows the minimum code necessary to setup the __OpenAccessDataSource__ component:
      	

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



When running the report in production the above code should work just fine. However, this is not 
      	the case when generating a preview of the same report in the designer, for example. The problem is that 
      	the __OpenAccessContext__ searches its connection string in the configuration file of the current executing 
      	application or web site. When it is your application that is currently running, all that is necessary 
      	is to make sure the connection string is present in the right configuration file. On the other side, 
      	when running the report in the designer, the current executing application is __Microsoft Visual Studio__, 
      	so the connection string is no longer available. To overcome this, you can specify your connection string to the __OpenAccessDataSource__ 
    	component. Assign the connection string to the __ConnectionString__ property and the __ADO.NET__ provider to the 
    	__ProviderName__ property, as shown in the following code snippet:
      	

{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````C#
	
	            Telerik.Reporting.OpenAccessDataSource openAccessDataSource = new Telerik.Reporting.OpenAccessDataSource();
	
	            openAccessDataSource.ProviderName = "System.Data.SqlClient";
	            openAccessDataSource.ConnectionString = "Data Source=.\\SqlExpress;Initial Catalog=AdventureWorks";
	            openAccessDataSource.ObjectContext = typeof(AdventureWorksEntities);
	            openAccessDataSource.ObjectContextMember = "Products";
	
````



{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````VB
	
	        Dim openAccessDataSource As New Telerik.Reporting.OpenAccessDataSource()
	
	        openAccessDataSource.ProviderName = "System.Data.SqlClient"
	        openAccessDataSource.ConnectionString = "Data Source=.\SqlExpress;Initial Catalog=AdventureWorks"
	        openAccessDataSource.ObjectContext = GetType(AdventureWorksEntities)
	        openAccessDataSource.ObjectContextMember = "Products"
	
	        '#End Region
	    End Sub
	
	    <Microsoft.VisualStudio.TestTools.UnitTesting.TestMethod()>
	    Public Sub ConnectionNameSnippet()
	        '#Region ConnectionNameSnippet
	
	        Dim openAccessDataSource As Telerik.Reporting.OpenAccessDataSource = New Telerik.Reporting.OpenAccessDataSource()
	
	        openAccessDataSource.ConnectionString = "AdventureWorksConnection"
	        openAccessDataSource.ObjectContext = GetType(AdventureWorksEntities)
	        openAccessDataSource.ObjectContextMember = "Products"
	
	        '#End Region
	    End Sub
	
	    <Microsoft.VisualStudio.TestTools.UnitTesting.TestMethod()>
	    Public Sub PropertyBindingSnippet()
	        '#Region PropertyBindingSnippet
	
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



Instead of specifying an inline connection string you can assign the name of an existing connection string stored in 
      	the configuration file to the __ConnectionString__ property. In that case specifying an __ADO.NET__ 
      	provider to the __ProviderName__ property is no longer required, because that information is already 
      	present in the configuration. The following sample code demonstrates how to specify a named connection string from a configuration file:
      	

{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````C#
	
	            Telerik.Reporting.OpenAccessDataSource openAccessDataSource = new Telerik.Reporting.OpenAccessDataSource();
	
	            openAccessDataSource.ConnectionString = "AdventureWorksConnection";
	            openAccessDataSource.ObjectContext = typeof(AdventureWorksEntities);
	            openAccessDataSource.ObjectContextMember = "Products";
	
````



{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````VB
	
	        Dim openAccessDataSource As Telerik.Reporting.OpenAccessDataSource = New Telerik.Reporting.OpenAccessDataSource()
	
	        openAccessDataSource.ConnectionString = "AdventureWorksConnection"
	        openAccessDataSource.ObjectContext = GetType(AdventureWorksEntities)
	        openAccessDataSource.ObjectContextMember = "Products"
	
	        '#End Region
	    End Sub
	
	    <Microsoft.VisualStudio.TestTools.UnitTesting.TestMethod()>
	    Public Sub PropertyBindingSnippet()
	        '#Region PropertyBindingSnippet
	
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



>note Specifying an inline connection string directly to the  __ConnectionString__  property of the 	 __OpenAccessDataSource__  component is not recommended, because it might be difficult to maintain all your reports 	later, when that connection string changes. The recommended approach is to always specify the name of an 	existing connection string stored in the configuration file. When specifying a connection string form a 	configuration file it is important to understand which configuration file is used at design-time or when 	running the report in production. For example, let us consider the following simplified structure of a 	business application:  
  ![](images/DataSources/BusinessApplicationStructure.png)The above schema assumes that the different parts of the business application are represented as 	separate projects in the solution, each with its own configuration file. Initially, when you create the 	 __Telerik Data Access Model__  in the  __Business Logic__  project, the connection string is stored automatically in the 	configuration file of that project. Later, when creating new reports in the  __Report Library__  project, you need 	to add the connection string to the configuration file of that project, because this is where  __Report Designer__ 	searches for existing connection strings. Finally, when deploying your application or web site in production,	you need to add the connection string to the configuration file of your  __Main Application__ .


# See Also
