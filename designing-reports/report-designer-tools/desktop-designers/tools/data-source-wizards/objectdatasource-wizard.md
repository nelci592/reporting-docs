---
title: ObjectDataSource Wizard
page_title: ObjectDataSource Wizard | for Telerik Reporting Documentation
description: ObjectDataSource Wizard
slug: telerikreporting/designing-reports/report-designer-tools/desktop-designers/tools/data-source-wizards/objectdatasource-wizard
tags: objectdatasource,wizard
published: True
position: 5
---

# ObjectDataSource Wizard



After the __ObjectDataSource__ wizard appears you have to perform the following steps:
      

## 

1. Select a Business Object.In this step you have to specify the business object to use for your data source. The available
              business objects are organized in two tabs for easier navigation:
            

* __Available data source types__This tab lists all available types that can be used with the __ObjectDataSource__ component. That
                  includes all public, non-abstract, non-generic classes and structures from the current project and
                  from all other referenced projects. The types are organized in a hierarchical manner grouped by namespace:
                

>note If the desired type does not appear in the list, make sure the current project is built and all                    necessary project references are added. If you use the [Visual Studio Report Designer]({%slug telerikreporting/designing-reports/report-designer-tools/desktop-designers/visual-studio-report-designer/overview%})                    have in mind that Visual Studio is a 32-bit application, so the designer is                    restricted to x86 mode even on x64 platforms, which prevents the ObjectDataSource Wizard from discovering any types from                    x64 assemblies. The solution is to use different platform configurations: for " __Debug__ "                    builds it is best to use " __Any CPU__ ", while for " __Release__ "                    builds you can use " __x64__ " instead.                  


>note When the  __"Show data components only"__  check box is checked, only the types marked with the DataObjectAttribute                    are listed. This is useful for distinguishing the types appropriate for data binding from the regular ones.                  
#_C#_

	
        [System.ComponentModel.DataObject()]
        public class Cars : List<Car>;
        {
        ....
        }


#_VB.NET_

	
        <System.ComponentModel.DataObject> _
        Public Class Cars
        Inherits List(Of Car)
        ....
        End Class




* __Existing data source components__This tab lists all existing components in the current report that can be used with the __ObjectDataSource__
                  component. That includes all components from the component tray in the designer that are not data source
                  components themselves.
                

>note When the  __"Show data components only"__  check box is checked, only the components marked with the  __DataObjectAttribute__  are listed. This is                    useful for distinguishing the components appropriate for data binding from the regular ones.                  


1. __Choose a data member__In this step you have to specify a member from the chosen business object that is responsible
              for data retrieval.
            

* __No data source member__ – selecting this option specifies that there is no specific member responsible
                  for retrieving data. In this case the chosen business object itself serves as a data source for the report.
                  If you have specified a type in the previous step, the default constructor of the chosen type is used to create
                  a new instance of the business object.
                

* __Choose a data source member__ – selecting this option allows you to specify a member of the business object
                  that is responsible for data retrieval. The list of displayed members is contextual and depends on the selection
                  from the previous step:
                

* __When a business object type is chosen__, the list of available
                      members is the following:
                    

* All public instance constructors
                        

* All public instance properties
                        

* All public static (shared in VB.NET) properties
                        

* All public instance methods
                        

* All public static (shared in VB.NET) methods
                        

* __When a business object component is chosen__, the list of available members
                      is the following:
                    

* All public instance properties
                        

* All public instance methods
                        

* __When the "Show data components only" check box is checked__, only the methods that are marked
                      with the __DataObjectMethodAttribute__ attribute are listed, and only if the specified type of the data method
                      is __DataObjectMethodType.Select__.
                    Here are some sample Cars class methods:

{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````C#
	
	        [System.ComponentModel.DataObject]
	        public class Cars : System.Collections.Generic.List<Car>
	        {
	            [System.ComponentModel.DataObjectMethod(System.ComponentModel.DataObjectMethodType.Select)]
	            public System.Collections.Generic.List<Car> GetCarsByYear(int year)
	            {
	                // TODO: Implement your specific business logic here.
	                return new System.Collections.Generic.List<Car>();
	            }
	
	            [System.ComponentModel.DataObjectMethod(System.ComponentModel.DataObjectMethodType.Select)]
	            public System.Collections.Generic.List<Car> GetCarsByColor(string color)
	            {
	                // TODO: Implement your specific business logic here.
	                return new System.Collections.Generic.List<Car>();
	            }
	
	            [System.ComponentModel.DataObjectMethod(System.ComponentModel.DataObjectMethodType.Select)]
	            public System.Collections.Generic.List<Car> GetCars(int year, string color)
	            {
	                // TODO: Implement your specific business logic here.
	                return new System.Collections.Generic.List<Car>();
	            }
	        }
	
````



{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````VB
	
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

When the __"Show data components only"__ check box from the previous step is not checked, all public members of the Cars business object type
                  are listed. When the check box is checked, only the methods with the
                  __DataObjectMethodAttribute__ attribute appear in the list. This is especially useful for filtering only the methods
                  that are appropriate for data binding.
                

>note If the chosen member does not have any parameters, this is the last step of the wizard. However, if the specified member has parameters,                    the next step allows you to configure those parameters.                  


1. __Configure Data Source Parameters__:
            Each argument of the selected method corresponds to a data source parameter. This step allows you to specify for each
              parameter a constant value, an expression, or create a new __ReportParameter__ and the expression will be set automatically
              to it.
            

>note The names and types of the defined parameters should match exactly the arguments of the selected method. In case this requirement is not                fulfilled the  __ObjectDataSource__  component will not be able to resolve or call correctly the method and will raise an                exception at runtime.              
This is the last step of the wizard. After pressing the __Finish__
              button the wizard will create the __ObjectDataSource__ component with the
              specified settings. In case you are using
              [Visual Studio Report Designer]({%slug telerikreporting/designing-reports/report-designer-tools/desktop-designers/visual-studio-report-designer/overview%}), the wizard will automatically add the necessary 
              [AssemblyReferences]({%slug telerikreporting/using-reports-in-applications/export-and-configure/configure-the-report-engine/assemblyreferences-element%}) element in report's project configuration file. If the configuration file
              does not exist, it will be created prior to populating and added to the current project. If the configuration file is under source control, it will be checked out.
              After finishing the above operations, the wizard will close and return the user to the designer.
            

# See Also

 * [Overview]({%slug telerikreporting/designing-reports/connecting-to-data/data-source-components/objectdatasource-component/overview%})

 * [assemblyReferences Element]({%slug telerikreporting/using-reports-in-applications/export-and-configure/configure-the-report-engine/assemblyreferences-element%})

 * [Data Source Components Problems]({%slug telerikreporting/designing-reports/connecting-to-data/troubleshooting/data-source-components-problems%})
