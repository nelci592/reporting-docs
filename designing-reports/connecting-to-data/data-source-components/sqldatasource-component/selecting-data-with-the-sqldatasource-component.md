---
title: Selecting Data with the SqlDataSource component
page_title: Selecting Data with the SqlDataSource component | for Telerik Reporting Documentation
description: Selecting Data with the SqlDataSource component
slug: telerikreporting/designing-reports/connecting-to-data/data-source-components/sqldatasource-component/selecting-data-with-the-sqldatasource-component
tags: selecting,data,with,the,sqldatasource,component
published: True
position: 2
---

# Selecting Data with the SqlDataSource component



## 

You can specify a SQL query for the __SqlDataSource__ component to execute by setting its
          __SelectCommand__ property.
        

>note If the SQL query returns more than one result sets, only the first set will be used.


The following example demonstrates a SQL query that retrieves
          a result set consisting of the names of all the persons in the __Contact__ table from the
          __AdventureWorks__ sample database:
        

	
          SELECT FirstName, LastName FROM Person.Contact
        



The following code example shows how to set the __ConnectionString__ and __
            SelectCommand
          __ properties of a __SqlDataSource__ component to retrieve the
          data from the above SQL query:
        



{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````C#
	            Telerik.Reporting.SqlDataSource sqlDataSource = new Telerik.Reporting.SqlDataSource();
	            sqlDataSource.ConnectionString = "MyAdventureWorksDB";
	            sqlDataSource.SelectCommand = "SELECT FirstName, LastName FROM Person.Contact";
````



{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````VB
	        Dim sqlDataSource As Telerik.Reporting.SqlDataSource = New Telerik.Reporting.SqlDataSource()
	        sqlDataSource.ConnectionString = "MyAdventureWorksDB"
	        sqlDataSource.SelectCommand = "SELECT FirstName, LastName FROM Person.Contact"
	        '#End Region
	    End Sub
	
	    <Microsoft.VisualStudio.TestTools.UnitTesting.TestMethod()>
	    Public Sub StoredProcedureSnippet()
	        '#Region StoredProcedureSnippet
	        Dim sqlDataSource As Telerik.Reporting.SqlDataSource = New Telerik.Reporting.SqlDataSource()
	        sqlDataSource.ConnectionString = "MyAdventureWorksDB"
	        sqlDataSource.SelectCommand = "GetAllContacts"
	        sqlDataSource.SelectCommandType = SqlDataSourceCommandType.StoredProcedure
	        '#End Region
	    End Sub
	
	    <Microsoft.VisualStudio.TestTools.UnitTesting.TestMethod()>
	    Public Sub NamedParametersSnippet()
	        '#Region NamedParametersSnippet
	        Dim sqlDataSource As Telerik.Reporting.SqlDataSource = New Telerik.Reporting.SqlDataSource()
	        sqlDataSource.ConnectionString = "MyAdventureWorksDB"
	        sqlDataSource.SelectCommand = "SELECT * FROM Person.Contact WHERE FirstName = @FirstName AND LastName = @LastName"
	        sqlDataSource.Parameters.Add("@FirstName", System.Data.DbType.String, "John")
	        sqlDataSource.Parameters.Add("@LastName", System.Data.DbType.String, "Smith")
	        '#End Region
	    End Sub
	
	    <Microsoft.VisualStudio.TestTools.UnitTesting.TestMethod()>
	    Public Sub PositionalParametersSnippet()
	        '#Region PositionalParametersSnippet
	        Dim sqlDataSource As Telerik.Reporting.SqlDataSource = New Telerik.Reporting.SqlDataSource()
	        sqlDataSource.ProviderName = "System.Data.OleDb"
	        sqlDataSource.ConnectionString = "Provider=SQLOLEDB;Data Source=(local)\SQLEXPRESS;Initial Catalog=AdventureWorks;Integrated Security=SSPI"
	        sqlDataSource.SelectCommand = "SELECT * FROM Person.Contact WHERE FirstName = ? AND LastName = ?"
	        sqlDataSource.Parameters.Add("FirstName", System.Data.DbType.String, "John")
	        sqlDataSource.Parameters.Add("LastName", System.Data.DbType.String, "Smith")
	        '#End Region
	    End Sub
	
	    <Microsoft.VisualStudio.TestTools.UnitTesting.TestMethod()>
	    Public Sub BindingExpressionSnippet()
	        '#Region BindingExpressionSnippet
	        Dim report As Telerik.Reporting.Report = New Telerik.Reporting.Report()
	        report.ReportParameters.Add("FirstName", ReportParameterType.String, "John")
	        report.ReportParameters.Add("LastName", ReportParameterType.String, "Smith")
	        Dim sqlDataSource As Telerik.Reporting.SqlDataSource = New Telerik.Reporting.SqlDataSource()
	        sqlDataSource.ConnectionString = "MyAdventureWorksDB"
	        sqlDataSource.SelectCommand = "SELECT * FROM Person.Contact WHERE FirstName = @FirstName AND LastName = @LastName"
	        sqlDataSource.Parameters.Add("@FirstName", System.Data.DbType.String, "=Parameters.FirstName")
	        sqlDataSource.Parameters.Add("@LastName", System.Data.DbType.String, "=Parameters.LastName")
	        report.DataSource = sqlDataSource
	        '#End Region
	    End Sub
	End Class



If the database you are working with supports stored procedures, you can set the __
            SelectCommand
          __ property to the name of an existing stored procedure and the __
            SelectCommandType
          __ property to __StoredProcedure__ to indicate that the __
            SelectCommand
          __ property refers to a stored procedure. The following example demonstrates a simple
          stored procedure that you can create in SQL Server:
        

	
          CREATE PROCEDURE GetAllContacts AS
          SELECT FirstName, LastName FROM Person.Contact;
          GO
        



To configure the __SqlDataSource__ component to use this stored procedure, set the
          __SelectCommand__ text to *"GetAllContacts"* and the
          __SelectCommandType__ property to __StoredProcedure__:
        



{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````C#
	            Telerik.Reporting.SqlDataSource sqlDataSource = new Telerik.Reporting.SqlDataSource();
	            sqlDataSource.ConnectionString = "MyAdventureWorksDB";
	            sqlDataSource.SelectCommand = "GetAllContacts";
	            sqlDataSource.SelectCommandType = SqlDataSourceCommandType.StoredProcedure;
````



{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````VB
	        Dim sqlDataSource As Telerik.Reporting.SqlDataSource = New Telerik.Reporting.SqlDataSource()
	        sqlDataSource.ConnectionString = "MyAdventureWorksDB"
	        sqlDataSource.SelectCommand = "GetAllContacts"
	        sqlDataSource.SelectCommandType = SqlDataSourceCommandType.StoredProcedure
	        '#End Region
	    End Sub
	
	    <Microsoft.VisualStudio.TestTools.UnitTesting.TestMethod()>
	    Public Sub NamedParametersSnippet()
	        '#Region NamedParametersSnippet
	        Dim sqlDataSource As Telerik.Reporting.SqlDataSource = New Telerik.Reporting.SqlDataSource()
	        sqlDataSource.ConnectionString = "MyAdventureWorksDB"
	        sqlDataSource.SelectCommand = "SELECT * FROM Person.Contact WHERE FirstName = @FirstName AND LastName = @LastName"
	        sqlDataSource.Parameters.Add("@FirstName", System.Data.DbType.String, "John")
	        sqlDataSource.Parameters.Add("@LastName", System.Data.DbType.String, "Smith")
	        '#End Region
	    End Sub
	
	    <Microsoft.VisualStudio.TestTools.UnitTesting.TestMethod()>
	    Public Sub PositionalParametersSnippet()
	        '#Region PositionalParametersSnippet
	        Dim sqlDataSource As Telerik.Reporting.SqlDataSource = New Telerik.Reporting.SqlDataSource()
	        sqlDataSource.ProviderName = "System.Data.OleDb"
	        sqlDataSource.ConnectionString = "Provider=SQLOLEDB;Data Source=(local)\SQLEXPRESS;Initial Catalog=AdventureWorks;Integrated Security=SSPI"
	        sqlDataSource.SelectCommand = "SELECT * FROM Person.Contact WHERE FirstName = ? AND LastName = ?"
	        sqlDataSource.Parameters.Add("FirstName", System.Data.DbType.String, "John")
	        sqlDataSource.Parameters.Add("LastName", System.Data.DbType.String, "Smith")
	        '#End Region
	    End Sub
	
	    <Microsoft.VisualStudio.TestTools.UnitTesting.TestMethod()>
	    Public Sub BindingExpressionSnippet()
	        '#Region BindingExpressionSnippet
	        Dim report As Telerik.Reporting.Report = New Telerik.Reporting.Report()
	        report.ReportParameters.Add("FirstName", ReportParameterType.String, "John")
	        report.ReportParameters.Add("LastName", ReportParameterType.String, "Smith")
	        Dim sqlDataSource As Telerik.Reporting.SqlDataSource = New Telerik.Reporting.SqlDataSource()
	        sqlDataSource.ConnectionString = "MyAdventureWorksDB"
	        sqlDataSource.SelectCommand = "SELECT * FROM Person.Contact WHERE FirstName = @FirstName AND LastName = @LastName"
	        sqlDataSource.Parameters.Add("@FirstName", System.Data.DbType.String, "=Parameters.FirstName")
	        sqlDataSource.Parameters.Add("@LastName", System.Data.DbType.String, "=Parameters.LastName")
	        report.DataSource = sqlDataSource
	        '#End Region
	    End Sub
	End Class



At run time, the __SqlDataSource__ component submits the text in the __
            SelectCommand
          __ property to the database, and the database returns the result of the SQL query or stored procedure
          back to the __SqlDataSource__ component. Any data items that are bound to the data source
          component display the result set on your report.
        
