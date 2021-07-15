---
title: Connecting the CubeDataSource component to an OLAP database
page_title: Connecting the CubeDataSource component to an OLAP database | for Telerik Reporting Documentation
description: Connecting the CubeDataSource component to an OLAP database
slug: telerikreporting/designing-reports/connecting-to-data/data-source-components/cubedatasource-component/connecting-the-cubedatasource-component-to-an-olap-database
tags: connecting,the,cubedatasource,component,to,an,olap,database
published: True
position: 2
---

# Connecting the CubeDataSource component to an OLAP database



When you configure a __CubeDataSource__ you set the __ConnectionString__
				property to a connection string that includes information required to connect to the database. Specifying an
				appropriate connection string requires at least a server name and database (catalog) name. For information on
				valid connection strings see the __ConnectionString__ property topic for the __
				AdomdConnection__ class.
			

## 

The sample code below illustrates how to connect a __CubeDataSource__ component to
					the __Adventure Works DW 2008R2__ sample database:
				

{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````c#
	            Telerik.Reporting.CubeDataSource cubeDataSource = new Telerik.Reporting.CubeDataSource();
	
	            cubeDataSource.ConnectionString = "Data Source=localhost;Initial Catalog=Adventure Works DW 2008R2";
	            cubeDataSource.SelectCommand = "select non empty { [Measures].[Sales Amount] } on columns, " +
	                                           "       non empty { [Product].[Category].[Category] } on rows " +
	                                           "from [Adventure Works]";
````



{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````vb
	        Dim cubeDataSource As Telerik.Reporting.CubeDataSource = New Telerik.Reporting.CubeDataSource()
	
	        cubeDataSource.ConnectionString = "Data Source=localhost;Initial Catalog=Adventure Works DW 2008R2"
	        cubeDataSource.SelectCommand = "select non empty { [Measures].[Sales Amount] } on columns, " & _
	                                       "       non empty { [Product].[Category].[Category] } on rows " & _
	                                       "from [Adventure Works]"
	        '#End Region
	    End Sub
	
	    <Microsoft.VisualStudio.TestTools.UnitTesting.TestMethod()>
	    Public Sub ConnectionNameSnippet()
	        '#Region ConnectionNameSnippet
	        Dim cubeDataSource As Telerik.Reporting.CubeDataSource = New Telerik.Reporting.CubeDataSource()
	
	        cubeDataSource.ConnectionString = "MyAdventureWorksDW"
	        cubeDataSource.SelectCommand = "select non empty { [Measures].[Sales Amount] } on columns, " & _
	                                       "       non empty { [Product].[Category].[Category] } on rows " & _
	                                       "from [Adventure Works]"
	        '#End Region
	    End Sub
	
	    <Microsoft.VisualStudio.TestTools.UnitTesting.TestMethod()>
	    Public Sub SelectCommandSnippet()
	        '#Region SelectCommandSnippet
	        Dim cubeDataSource As Telerik.Reporting.CubeDataSource = New Telerik.Reporting.CubeDataSource()
	
	        cubeDataSource.ConnectionString = "MyAdventureWorksDW"
	        cubeDataSource.SelectCommand = "select non empty { [Measures].[Sales Amount] } on columns, " & _
	                                       "       non empty { [Product].[Category].[Category] * " & _
	                                       "                   [Product].[Subcategory].[Subcategory] } on rows " & _
	                                       "from [Adventure Works]"
	        '#End Region
	    End Sub
	
	    <Microsoft.VisualStudio.TestTools.UnitTesting.TestMethod()>
	    Public Sub FieldMappingSnippet()
	        '#Region FieldMappingSnippet
	        Dim cubeDataSource As Telerik.Reporting.CubeDataSource = New Telerik.Reporting.CubeDataSource()
	
	        cubeDataSource.ConnectionString = "MyAdventureWorksDW"
	        cubeDataSource.SelectCommand = "select non empty { [Measures].[Sales Amount] } on columns, " & _
	                                       "       non empty { [Product].[Category].[Category] * " & _
	                                       "                   [Product].[Subcategory].[Subcategory] } on rows " & _
	                                       "from [Adventure Works]"
	        cubeDataSource.Mappings.Add("[Measures].[Sales Amount]", "Sales")
	        cubeDataSource.Mappings.Add("[Product].[Category].[Category].[MEMBER_CAPTION]", "Category")
	        cubeDataSource.Mappings.Add("[Product].[Subcategory].[Subcategory].[MEMBER_CAPTION]", "Subcategory")
	        '#End Region
	    End Sub
	
	    <Microsoft.VisualStudio.TestTools.UnitTesting.TestMethod()>
	    Public Sub SingleValueParameterSnippet()
	        '#Region SingleValueParameterSnippet
	        Dim cubeDataSource As Telerik.Reporting.CubeDataSource = New Telerik.Reporting.CubeDataSource()
	
	        cubeDataSource.ConnectionString = "MyAdventureWorksDW"
	        cubeDataSource.SelectCommand = "select non empty { [Measures].[Sales Amount] } on columns, " & _
	                                       "       non empty { [Product].[Category].[Category] * " & _
	                                       "                   [Product].[Subcategory].[Subcategory] } on rows " & _
	                                       "from [Adventure Works] " & _
	                                       "where StrToMember(@Year)"
	        cubeDataSource.Parameters.Add("Year", "[CY 2001]")
	        '#End Region
	    End Sub
	
	    <Microsoft.VisualStudio.TestTools.UnitTesting.TestMethod()>
	    Public Sub MultiValueParameterSnippet()
	        '#Region MultiValueParameterSnippet
	        Dim cubeDataSource As Telerik.Reporting.CubeDataSource = New Telerik.Reporting.CubeDataSource()
	
	        cubeDataSource.ConnectionString = "MyAdventureWorksDW"
	        cubeDataSource.SelectCommand = "select non empty { [Measures].[Sales Amount] } on columns, " & _
	                                       "       non empty { [Product].[Category].[Category] * " & _
	                                       "                   [Product].[Subcategory].[Subcategory] } on rows " & _
	                                       "from [Adventure Works] " & _
	                                       "where StrToSet(@Year)"
	        cubeDataSource.Parameters.Add("Year", New String() {"[CY 2001]", "[CY 2002]"})
	        '#End Region
	    End Sub
	
	    <Microsoft.VisualStudio.TestTools.UnitTesting.TestMethod()>
	    Public Sub ReportParameterSnippet()
	        '#Region ReportParameterSnippet
	        Dim cubeDataSource As Telerik.Reporting.CubeDataSource = New Telerik.Reporting.CubeDataSource()
	
	        cubeDataSource.ConnectionString = "MyAdventureWorksDW"
	        cubeDataSource.SelectCommand = "select non empty { [Measures].[Sales Amount] } on columns, " & _
	                                       "       non empty { [Product].[Category].[Category] * " & _
	                                       "                   [Product].[Subcategory].[Subcategory] } on rows " & _
	                                       "from [Adventure Works] " & _
	                                       "where StrToMember(@Year)"
	        cubeDataSource.Parameters.Add("Year", "=Parameters.Year.Value")
	
	        Dim report As New Report1()
	
	        report.DataSource = cubeDataSource
	        report.ReportParameters.Add("Year", ReportParameterType.String, "[CY 2001]")
	        '#End Region
	    End Sub
	End Class



Instead of setting connection strings as property settings in the __CubeDataSource__
					object, you can store them centrally as part of your application's configuration settings using the
					__connectionStrings__ configuration element. This enables you to manage connection
					strings independently of your reports, including encrypting them using __Protected Configuration
					__. The following example shows how to connect to the __Adventure Works DW 2008R2
					__ sample database using a connection string which stored in the __connectionStrings
					__ configuration element named __MyAdventureWorksDW__:
				

	
					<configuration>
						<connectionStrings>
							<add name="MyAdventureWorksDW"
								 connectionString="Data Source=localhost;Initial Catalog=Adventure Works DW 2008R2"
								 providerName="Microsoft.AnalysisServices.AdomdClient" />
						</connectionStrings>
					</configuration>
				



When the connection string is stored in the configuration file you need to specify the name of the
					configuration element as a value for the __ConnectionString__ property of the
					__CubeDataSource__ component:
				

{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````c#
	            Telerik.Reporting.CubeDataSource cubeDataSource = new Telerik.Reporting.CubeDataSource();
	
	            cubeDataSource.ConnectionString = "MyAdventureWorksDW";
	            cubeDataSource.SelectCommand = "select non empty { [Measures].[Sales Amount] } on columns, " +
	                                           "       non empty { [Product].[Category].[Category] } on rows " +
	                                           "from [Adventure Works]";
````



{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````vb
	        Dim cubeDataSource As Telerik.Reporting.CubeDataSource = New Telerik.Reporting.CubeDataSource()
	
	        cubeDataSource.ConnectionString = "MyAdventureWorksDW"
	        cubeDataSource.SelectCommand = "select non empty { [Measures].[Sales Amount] } on columns, " & _
	                                       "       non empty { [Product].[Category].[Category] } on rows " & _
	                                       "from [Adventure Works]"
	        '#End Region
	    End Sub
	
	    <Microsoft.VisualStudio.TestTools.UnitTesting.TestMethod()>
	    Public Sub SelectCommandSnippet()
	        '#Region SelectCommandSnippet
	        Dim cubeDataSource As Telerik.Reporting.CubeDataSource = New Telerik.Reporting.CubeDataSource()
	
	        cubeDataSource.ConnectionString = "MyAdventureWorksDW"
	        cubeDataSource.SelectCommand = "select non empty { [Measures].[Sales Amount] } on columns, " & _
	                                       "       non empty { [Product].[Category].[Category] * " & _
	                                       "                   [Product].[Subcategory].[Subcategory] } on rows " & _
	                                       "from [Adventure Works]"
	        '#End Region
	    End Sub
	
	    <Microsoft.VisualStudio.TestTools.UnitTesting.TestMethod()>
	    Public Sub FieldMappingSnippet()
	        '#Region FieldMappingSnippet
	        Dim cubeDataSource As Telerik.Reporting.CubeDataSource = New Telerik.Reporting.CubeDataSource()
	
	        cubeDataSource.ConnectionString = "MyAdventureWorksDW"
	        cubeDataSource.SelectCommand = "select non empty { [Measures].[Sales Amount] } on columns, " & _
	                                       "       non empty { [Product].[Category].[Category] * " & _
	                                       "                   [Product].[Subcategory].[Subcategory] } on rows " & _
	                                       "from [Adventure Works]"
	        cubeDataSource.Mappings.Add("[Measures].[Sales Amount]", "Sales")
	        cubeDataSource.Mappings.Add("[Product].[Category].[Category].[MEMBER_CAPTION]", "Category")
	        cubeDataSource.Mappings.Add("[Product].[Subcategory].[Subcategory].[MEMBER_CAPTION]", "Subcategory")
	        '#End Region
	    End Sub
	
	    <Microsoft.VisualStudio.TestTools.UnitTesting.TestMethod()>
	    Public Sub SingleValueParameterSnippet()
	        '#Region SingleValueParameterSnippet
	        Dim cubeDataSource As Telerik.Reporting.CubeDataSource = New Telerik.Reporting.CubeDataSource()
	
	        cubeDataSource.ConnectionString = "MyAdventureWorksDW"
	        cubeDataSource.SelectCommand = "select non empty { [Measures].[Sales Amount] } on columns, " & _
	                                       "       non empty { [Product].[Category].[Category] * " & _
	                                       "                   [Product].[Subcategory].[Subcategory] } on rows " & _
	                                       "from [Adventure Works] " & _
	                                       "where StrToMember(@Year)"
	        cubeDataSource.Parameters.Add("Year", "[CY 2001]")
	        '#End Region
	    End Sub
	
	    <Microsoft.VisualStudio.TestTools.UnitTesting.TestMethod()>
	    Public Sub MultiValueParameterSnippet()
	        '#Region MultiValueParameterSnippet
	        Dim cubeDataSource As Telerik.Reporting.CubeDataSource = New Telerik.Reporting.CubeDataSource()
	
	        cubeDataSource.ConnectionString = "MyAdventureWorksDW"
	        cubeDataSource.SelectCommand = "select non empty { [Measures].[Sales Amount] } on columns, " & _
	                                       "       non empty { [Product].[Category].[Category] * " & _
	                                       "                   [Product].[Subcategory].[Subcategory] } on rows " & _
	                                       "from [Adventure Works] " & _
	                                       "where StrToSet(@Year)"
	        cubeDataSource.Parameters.Add("Year", New String() {"[CY 2001]", "[CY 2002]"})
	        '#End Region
	    End Sub
	
	    <Microsoft.VisualStudio.TestTools.UnitTesting.TestMethod()>
	    Public Sub ReportParameterSnippet()
	        '#Region ReportParameterSnippet
	        Dim cubeDataSource As Telerik.Reporting.CubeDataSource = New Telerik.Reporting.CubeDataSource()
	
	        cubeDataSource.ConnectionString = "MyAdventureWorksDW"
	        cubeDataSource.SelectCommand = "select non empty { [Measures].[Sales Amount] } on columns, " & _
	                                       "       non empty { [Product].[Category].[Category] * " & _
	                                       "                   [Product].[Subcategory].[Subcategory] } on rows " & _
	                                       "from [Adventure Works] " & _
	                                       "where StrToMember(@Year)"
	        cubeDataSource.Parameters.Add("Year", "=Parameters.Year.Value")
	
	        Dim report As New Report1()
	
	        report.DataSource = cubeDataSource
	        report.ReportParameters.Add("Year", ReportParameterType.String, "[CY 2001]")
	        '#End Region
	    End Sub
	End Class


