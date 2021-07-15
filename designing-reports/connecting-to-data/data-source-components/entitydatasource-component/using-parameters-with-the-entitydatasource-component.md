---
title: Using parameters with the EntityDataSource component
page_title: Using parameters with the EntityDataSource component | for Telerik Reporting Documentation
description: Using parameters with the EntityDataSource component
slug: telerikreporting/designing-reports/connecting-to-data/data-source-components/entitydatasource-component/using-parameters-with-the-entitydatasource-component
tags: using,parameters,with,the,entitydatasource,component
published: True
position: 2
---

# Using parameters with the EntityDataSource component



This section discusses more in-depth how to pass parameters to a method of the __ObjectContext/DbContext__ with
        the __EntityDataSource__ component. The provided examples and code snippets assume an existing
        __Entity Data Model__ of the __Adventure Works__ sample database with the following structure:
        
  ![](images/DataSources/EntityDataSourceAdventureWorksEntityModel.png)

>note The [EntityDataSource Wizard]({%slug telerikreporting/designing-reports/report-designer-tools/desktop-designers/tools/data-source-wizards/entitydatasource-wizard%}) can detect parameters          of the data-retrieval method, and it will ask you to provide values for them at  __Configure Data Source Parameters__  step.        


## 

The __EntityDataSource__ component can call a method of the __ObjectContext/DbContext__ based on the name of the
          method, and additionally based on the arguments which make the signature of that method. For example,
          let us extend the __AdventureWorksEntities__ context using a partial class that defines the following method:
          

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



To call the above method specify its name to the __ContextMember__ property and define a data source parameter
          in the __Parameters__ collection for each method argument. The names and types of the data source parameters
          must match exactly the names and types of the corresponding method arguments otherwise the __EntityDataSource__
          component will raise an exception at runtime. The following code snippet illustrates how to pass parameters
          to the previous method programmatically:
          

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



When declaring a data source parameter you can specify a default value for that parameter and the
          value will be passed automatically to the corresponding method argument. Instead of supplying the
          parameter value directly, you can specify an expression to be evaluated at runtime. For example, this
          way it is possible to link the data source parameter to an existing report parameter, as shown in the
          following code snippet:
          

{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````C#
	
	            var entityDataSource = new Telerik.Reporting.EntityDataSource();
	
	            entityDataSource.Context = typeof(AdventureWorksEntities);
	            entityDataSource.ContextMember = "GetProducts";
	            entityDataSource.Parameters.Add("color", typeof(string), "=Parameters.Color.Value");
	            entityDataSource.Parameters.Add("price", typeof(decimal), "=Parameters.Price.Value");
	
	            var report = new Report1();
	
	            report.DataSource = entityDataSource;
	            report.ReportParameters.Add("Color", Telerik.Reporting.ReportParameterType.String, "Black");
	            report.ReportParameters.Add("Price", Telerik.Reporting.ReportParameterType.Float, 100);
	
````



{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````VB
	
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
