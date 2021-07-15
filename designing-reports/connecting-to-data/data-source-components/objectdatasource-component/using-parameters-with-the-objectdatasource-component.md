---
title: Using Parameters with the ObjectDataSource Component
page_title: Using Parameters with the ObjectDataSource Component | for Telerik Reporting Documentation
description: Using Parameters with the ObjectDataSource Component
slug: telerikreporting/designing-reports/connecting-to-data/data-source-components/objectdatasource-component/using-parameters-with-the-objectdatasource-component
tags: using,parameters,with,the,objectdatasource,component
published: True
position: 2
---

# Using Parameters with the ObjectDataSource Component



The __ObjectDataSource__ component can call a business object method based
        on the name of the method specified in the __DataMember__ property, and based
        additionally on the argument names that make up the business object method's
        signature. When you create methods in a business object, you must ensure that
        the parameter names and types accepted by the business object method match the
        parameter names and types that the __ObjectDataSource__ component passes.
      

The __ObjectDataSource__ component accepts input parameters at run time and
        manages them in a parameter collection. You can use the __Parameters__ property
        to specify the parameters. For each parameter you can set a name and a default
        value or an expression. During the report processing the __ObjectDataSource__
        parameters’ values are used as argument values for the data method or the
        constructor of the business object. Because of this the order of the
        parameters is important and should exactly match the order of the arguments
        along with their types and names. Any discrepancy will result in a run-time
        exception.
      

>note The [ObjectDataSource Wizard]({%slug telerikreporting/designing-reports/report-designer-tools/desktop-designers/tools/data-source-wizards/objectdatasource-wizard%}) can detect parameters          of the data-retrieval method, and it will ask you to provide values for them at  __Configure Data Source Parameters__  step.        


Here is an example of programmatically setting the ObjectDataSource’s
        parameters:
      

{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````C#
	
	        public void HowToObjectDataSourceParameters()
	        {
	            Telerik.Reporting.ObjectDataSource objectDataSource1 = new Telerik.Reporting.ObjectDataSource();
	            objectDataSource1.DataMember = "GetCars";
	            objectDataSource1.DataSource = typeof(Cars);
	            objectDataSource1.Parameters.Add(new Telerik.Reporting.ObjectDataSourceParameter("year", typeof(int), 2010));
	            objectDataSource1.Parameters.Add(new Telerik.Reporting.ObjectDataSourceParameter("color", typeof(string), "=Parameters.Color"));
	        }
````



{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````VB
	    Public Sub HowToObjectDataSourceParameters()
	        Dim objectDataSource1 As New Telerik.Reporting.ObjectDataSource()
	        objectDataSource1.DataMember = "GetCars"
	        objectDataSource1.DataSource = GetType(Cars)
	        objectDataSource1.Parameters.Add(New Telerik.Reporting.ObjectDataSourceParameter("year", GetType(Integer), 2010))
	        objectDataSource1.Parameters.Add(New Telerik.Reporting.ObjectDataSourceParameter("color", GetType(String), "=Parameters.Color"))
	    End Sub
	
	    '#End Region
	
	    '#Region DataMethodSnippet
	
	    <System.ComponentModel.DataObject()>
	    Public Class Cars
	        Inherits System.Collections.Generic.List(Of Car)
	
	        <System.ComponentModel.DataObjectMethod(System.ComponentModel.DataObjectMethodType.Select)>
	        Public Function GetCarsByYear(ByVal year As Integer) As System.Collections.Generic.List(Of Car)
	            ' TODO: Implement your specific business logic here.
	            Return New System.Collections.Generic.List(Of Car)
	        End Function
	
	        <System.ComponentModel.DataObjectMethod(System.ComponentModel.DataObjectMethodType.Select)>
	        Public Function GetCarsByColor(ByVal color As String) As System.Collections.Generic.List(Of Car)
	            ' TODO: Implement your specific business logic here.
	            Return New System.Collections.Generic.List(Of Car)
	        End Function
	
	        <System.ComponentModel.DataObjectMethod(System.ComponentModel.DataObjectMethodType.Select)>
	        Public Function GetCars(ByVal year As Integer, ByVal color As String) As System.Collections.Generic.List(Of Car)
	            ' TODO: Implement your specific business logic here.
	            Return New System.Collections.Generic.List(Of Car)
	        End Function
	    End Class
	
	    '#End Region
	
	
	    Dim reportViewer1 As New Telerik.ReportViewer.WinForms.ReportViewer()
	
	    '#Region HowToBindToBusinessObjectSnippet
	
	    Class Product
	        Dim mName As String
	        Dim mProductNumber As String
	        Dim mListPrice As Decimal
	        Dim mProductModelID As Integer
	        Dim mColor As String
	
	        Public Property Name() As String
	            Get
	                Return mName
	            End Get
	            Set(ByVal value As String)
	                mName = value
	            End Set
	        End Property
	        Public Property ProductNumber() As String
	            Get
	                Return mProductNumber
	            End Get
	            Set(ByVal value As String)
	                mProductNumber = value
	            End Set
	        End Property
	        Public Property ListPrice() As Decimal
	            Get
	                Return mListPrice
	            End Get
	            Set(ByVal value As Decimal)
	                mListPrice = value
	            End Set
	        End Property
	        Public Property ProductModelID() As Integer
	            Get
	                Return mProductModelID
	            End Get
	            Set(ByVal value As Integer)
	                mProductModelID = value
	            End Set
	        End Property
	        Public Property Color() As String
	            Get
	                Return mColor
	            End Get
	            Set(ByVal value As String)
	                mColor = value
	            End Set
	        End Property
	    End Class
	
	    <DataObject()>
	    Class Products
	        Const SelectCommandText As String = "SELECT Name, ProductNumber, ListPrice, ProductModelID, Color" + "  FROM Production.Product" + "  WHERE ProductModelID is not NULL" + "    AND Color is not NULL"
	
	        Const ConnectionString As String = "Data Source=(local)\SQLEXPRESS;Initial Catalog=AdventureWorks;Integrated Security=True"
	
	        <DataObjectMethod(DataObjectMethodType.Select)>
	        Public Function GetDataTableSource() As DataTable
	            Dim dataTable = New DataTable()
	            Using dataAdapter = New SqlDataAdapter(SelectCommandText, ConnectionString)
	                dataAdapter.Fill(dataTable)
	            End Using
	            Return dataTable
	        End Function
	
	        <DataObjectMethod(DataObjectMethodType.Select)>
	        Public Function GetDataAdapterSource() As IDataAdapter
	            Return New SqlDataAdapter(SelectCommandText, ConnectionString)
	        End Function
	
	        <DataObjectMethod(DataObjectMethodType.[Select])>
	        Public Function GetDataViewSource(ByVal name As String) As DataView
	            Dim dataAdapter = New SqlDataAdapter(SelectCommandText, ConnectionString)
	            Dim dataTable = New DataTable()
	
	            dataAdapter.Fill(dataTable)
	
	            Dim dataView = dataTable.DefaultView
	            dataView.RowFilter = String.Format("Name like '%{0}%'", name)
	
	            Return dataView
	        End Function
	
	        <DataObjectMethod(DataObjectMethodType.[Select])>
	        Public Function GetArraySource() As Product()
	            Return Me.GetAllProducts().ToArray()
	        End Function
	
	        <DataObjectMethod(DataObjectMethodType.[Select])>
	        Public Function GetArrayListSource() As ArrayList
	            Dim arrayList As New ArrayList()
	            For Each product In Me.GetAllProducts()
	                arrayList.Add(product)
	            Next
	            Return arrayList
	        End Function
	
	        <DataObjectMethod(DataObjectMethodType.[Select])>
	        Public Function GetAllProducts() As List(Of Product)
	            Dim connection As New SqlConnection(ConnectionString)
	            Dim command As New SqlCommand(SelectCommandText, connection)
	            Dim reader As SqlDataReader = Nothing
	            Dim products As New List(Of Product)()
	            Try
	                connection.Open()
	                reader = command.ExecuteReader()
	                While reader.Read()
	                    Dim product As New Product()
	                    product.Name = reader.GetString(0)
	                    product.ProductNumber = reader.GetString(1)
	                    product.ListPrice = reader.GetDecimal(2)
	                    product.ProductModelID = reader.GetInt32(3)
	                    product.Color = reader.GetString(4)
	                    products.Add(product)
	                End While
	                ' Handle exception.
	            Catch ex As SqlException
	            Finally
	                If Not reader Is Nothing Then
	                    reader.Close()
	                End If
	                connection.Close()
	            End Try
	            Return products
	        End Function
	
	        ' Gets products bellow a specified max price.
	        <DataObjectMethod(DataObjectMethodType.Select)>
	        Public Function GetProducts(ByVal maxPrice As Decimal) As IList(Of Product)
	            Return Me.GetAllProducts().FindAll(Function(product) product.ListPrice <= maxPrice)
	        End Function
	
	        ' Gets products of specific model and a color.
	        <DataObjectMethod(DataObjectMethodType.Select)>
	        Public Function GetProducts(ByVal productModelID As Integer, ByVal color As String) As IList(Of Product)
	            Return Me.GetAllProducts().FindAll(Function(product) (product.ProductModelID = productModelID AndAlso product.Color = color))
	        End Function
	    End Class
	
	    Private Sub Form2_Load(ByVal sender As System.Object, ByVal e As System.EventArgs)
	
	        ' Creating and configuring the ObjectDataSource component:
	        Dim objectDataSource As New Telerik.Reporting.ObjectDataSource()
	        objectDataSource.DataSource = GetType(Products) ' Specifying the business object type
	        objectDataSource.DataMember = "GetProducts" ' Specifying the name of the method for retrieving the data
	        objectDataSource.CalculatedFields.Add(New Telerik.Reporting.CalculatedField("FullName", GetType(String), "=Fields.Name + ' ' + Fields.ProductNumber")) ' Adding a sample calculated field.
	
	
	        'Specifying the parameters, their types and values that should be passed to the method at runtime
	        objectDataSource.Parameters.Add(New Telerik.Reporting.ObjectDataSourceParameter("color", GetType(String), "Silver"))
	        objectDataSource.Parameters.Add(New Telerik.Reporting.ObjectDataSourceParameter("productModelID", GetType(Integer), 23))
	
	        'Creating a new report
	        Dim report As New Report1()
	
	        ' Assigning the ObjectDataSource component to the DataSource property of the report.
	        report.DataSource = objectDataSource
	
	        ' Use the InstanceReportSource to pass the report to the viewer for displaying.
	        Dim reportSource As New InstanceReportSource
	        reportSource.ReportDocument = report
	
	        ' Assigning the report to the report viewer.
	        reportViewer1.ReportSource = reportSource
	
	        ' Calling the RefreshReport method in case this is a WinForms application.
	        reportViewer1.RefreshReport()
	
	    End Sub
	    '#End Region
	
	    '#Region HowToBindToDataTableSnippet
	
	    Private Sub Form1_Load(ByVal sender As System.Object, ByVal e As System.EventArgs)
	
	        ' Creating and configuring the ObjectDataSource component:
	        Dim objectDataSource As New Telerik.Reporting.ObjectDataSource()
	        objectDataSource.DataSource = GetData() ' GetData returns a DataTable
	        objectDataSource.CalculatedFields.Add(New Telerik.Reporting.CalculatedField("FullName", GetType(String), "=Fields.Name + ' ' + Fields.ProductNumber")) ' Adding a sample calculated field.
	
	
	        'Creating a new report
	        Dim report As New Report1()
	
	        ' Assigning the ObjectDataSource component to the DataSource property of the report.
	        report.DataSource = objectDataSource
	
	        ' Use the InstanceReportSource to pass the report to the viewer for displaying.
	        Dim reportSource As New InstanceReportSource
	        reportSource.ReportDocument = report
	
	        ' Assigning the report to the report viewer.
	        reportViewer1.ReportSource = reportSource
	
	        ' Calling the RefreshReport method in case this is a WinForms application.
	        Me.reportViewer1.RefreshReport()
	
	    End Sub
	
	    Shared Function GetData() As DataTable
	        Const connectionString As String =
	            "Data Source=(local)\SQLEXPRESS;Initial Catalog=AdventureWorks;Integrated Security=True"
	
	        Dim selectCommandText As String =
	            "SELECT Name, ProductNumber FROM Production.Product;"
	
	        Dim dataAdapter = New SqlDataAdapter(selectCommandText, connectionString)
	        Dim dataTable As New DataTable()
	        dataAdapter.Fill(dataTable)
	
	        Return dataTable
	    End Function
	
	    '#End Region
	
	    '#Region HowToBindToDataViewSnippet
	
	    Private Sub Form3_Load(ByVal sender As System.Object, ByVal e As System.EventArgs)
	
	        ' Creating and configuring the ObjectDataSource component:
	        Dim objectDataSource As New Telerik.Reporting.ObjectDataSource()
	        objectDataSource.DataSource = GetData("Name LIKE 'Mountain%'") ' GetData returns a DataView with the specified row filter.
	        objectDataSource.CalculatedFields.Add(New Telerik.Reporting.CalculatedField("FullName", GetType(String), "=Fields.Name + ' ' + Fields.ProductNumber")) ' Adding a sample calculated field.
	
	
	        'Creating a new report
	        Dim report As New Report1()
	
	        ' Assigning the ObjectDataSource component to the DataSource property of the report.
	        report.DataSource = objectDataSource
	
	        ' Use the InstanceReportSource to pass the report to the viewer for displaying.
	        Dim reportSource As New InstanceReportSource
	        reportSource.ReportDocument = report
	
	        ' Assigning the report to the report viewer.
	        reportViewer1.ReportSource = reportSource
	
	        ' Calling the RefreshReport method in case this is a WinForms application.
	        reportViewer1.RefreshReport()
	
	    End Sub
	
	    Shared Function GetData(ByVal rowFilter As String) As DataView
	        Const connectionString As String =
	            "Data Source=(local)\SQLEXPRESS;Initial Catalog=AdventureWorks;Integrated Security=True"
	
	        Dim selectCommandText As String =
	            "SELECT Name, ProductNumber FROM Production.Product;"
	
	        Dim dataAdapter = New SqlDataAdapter(selectCommandText, connectionString)
	        Dim dataTable As New DataTable()
	        dataAdapter.Fill(dataTable)
	
	        Dim dataView = dataTable.DefaultView
	        dataView.RowFilter = rowFilter
	
	        Return dataView
	    End Function
	
	    '#End Region
	
	    '#Region HowToBindToDataAdapterSnippet
	
	    Private Sub Form4_Load(ByVal sender As System.Object, ByVal e As System.EventArgs)
	        ' Creating and configuring the ObjectDataSource component:
	        Dim objectDataSource As New Telerik.Reporting.ObjectDataSource()
	        objectDataSource.DataSource = GetMyData() ' GetData returns a SqlDataAdapter object which has a select command with three SELECT statements.
	        objectDataSource.DataMember = "Table2" ' Indicating the exact table to bind to. If the DataMember is not specified the first data table will be used.
	        objectDataSource.CalculatedFields.Add(New Telerik.Reporting.CalculatedField("FullName", GetType(String), "=Fields.Name + ' ' + Fields.ProductNumber")) ' Adding a sample calculated field.
	
	        'Creating a new report
	        Dim report As New Report1()
	
	        ' Assigning the ObjectDataSource component to the DataSource property of the report.
	        report.DataSource = objectDataSource
	
	        ' Use the InstanceReportSource to pass the report to the viewer for displaying.
	        Dim reportSource As New InstanceReportSource
	        reportSource.ReportDocument = report
	
	        ' Assigning the report to the report viewer.
	        reportViewer1.ReportSource = reportSource
	
	        ' Calling the RefreshReport method in case this is a WinForms application.
	        Me.reportViewer1.RefreshReport()
	    End Sub
	
	    Shared Function GetMyData() As IDataAdapter
	        Const connectionString As String =
	            "Data Source=(local)\SQLEXPRESS;Initial Catalog=AdventureWorks;Integrated Security=True"
	
	        Dim selectCommandText As String =
	            "SELECT Name, ProductCategoryID FROM Production.ProductCategory;" _
	            + "SELECT Name, ProductCategoryID FROM Production.ProductSubcategory;" _
	            + "SELECT Name, ProductNumber FROM Production.Product;"
	
	        Return New SqlDataAdapter(selectCommandText, connectionString)
	    End Function
	
	    '#End Region
	
	    '#Region HowToBindToDataSetSnippet
	
	    Private Sub Form5_Load(ByVal sender As System.Object, ByVal e As System.EventArgs)
	
	        ' Creating and configuring the ObjectDataSource component:
	        Dim objectDataSource As New Telerik.Reporting.ObjectDataSource()
	        objectDataSource.DataSource = GetAllData() ' GetData returns a DataSet with three tables
	        objectDataSource.DataMember = "Product" ' Indicating the exact table to bind to. If the DataMember is not specified the first data table will be used.
	        objectDataSource.CalculatedFields.Add(New Telerik.Reporting.CalculatedField("FullName", GetType(String), "=Fields.Name + ' ' + Fields.ProductNumber")) ' Adding a sample calculated field.
	
	        'Creating a new report
	        Dim report As New Report1()
	
	        ' Assigning the ObjectDataSource component to the DataSource property of the report.
	        report.DataSource = objectDataSource
	
	        ' Use the InstanceReportSource to pass the report to the viewer for displaying.
	        Dim reportSource As New InstanceReportSource
	        reportSource.ReportDocument = report
	
	        ' Assigning the report to the report viewer.
	        reportViewer1.ReportSource = reportSource
	
	        ' Calling the RefreshReport method in case this is a WinForms application.
	        reportViewer1.RefreshReport()
	
	    End Sub
	
	
	    Shared Function GetAllData() As DataSet
	        Const connectionString As String =
	            "Data Source=(local)\SQLEXPRESS;Initial Catalog=AdventureWorks;Integrated Security=True"
	
	        Dim selectCommandText As String =
	            "SELECT Name, ProductCategoryID FROM Production.ProductCategory;" _
	            + "SELECT Name, ProductCategoryID FROM Production.ProductSubcategory;" _
	            + "SELECT Name, ProductNumber FROM Production.Product;"
	
	        Dim adapter As New SqlDataAdapter(selectCommandText, connectionString)
	        Dim dataSet As New DataSet()
	
	        'The data set will be filled with three tables: ProductCategory, ProductSubcategory 
	        'and Product as the select command contains three SELECT statements.
	        adapter.Fill(dataSet)
	
	        'Giving meaningful names for the tables so that we can use them later.
	        dataSet.Tables(0).TableName = "ProductCategory"
	        dataSet.Tables(1).TableName = "ProductSubcategory"
	        dataSet.Tables(2).TableName = "Product"
	
	        Return dataSet
	    End Function
	
	    '#End Region
	End Class
	
	Class SampleDataSourceSnippets
	
	    '#Region SampleDataSource
	    Class Product
	        'properties
	    End Class
	
	    <DataObject()>
	    Class Products
	        'objects
	    End Class
	
	    '#End Region
	End Class



# See Also

 * [Using Parameters with Data Source objects]({%slug telerikreporting/designing-reports/connecting-to-data/data-source-components/using-parameters-with-data-source-objects%})
