---
title: XHTML Validation
page_title: XHTML Validation | for Telerik Reporting Documentation
description: XHTML Validation
slug: telerikreporting/designing-reports/report-structure/htmltextbox/xhtml-validation
tags: xhtml,validation
published: True
position: 1
---

# XHTML Validation



The __HtmlTextBox__ requires valid __XHTML__ and you should make sure you provide such otherwise the HtmlTextBox would throw exception. 
    	To handle this exception or just check whether the __HtmlTextBox__ would be able to handle the content 
    	you set as value, you should use the IsValidXhtml expressions function or 
      	M:Telerik.Reporting.Processing.XhtmlValidator.IsValidXhtml(System.String)
      	static method. Three possible
    	approaches are listed below:

## Validate Xhtml Using IsValidXhtml in Expression

Use the __IsValidXhtml__ inside the HtmlTextBox __Expression__:

{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````C#
	
	            const string validXhtml = "<b>valid xhtml</b>.";
	            const string systemXhtml = "Provided html is not acceptable.";
	
	            Telerik.Reporting.HtmlTextBox txt = new Telerik.Reporting.HtmlTextBox();
	            txt.Value = string.Format("=Iif(IsValidXhtml('{0}'), '{0}', '{1}')", validXhtml, systemXhtml);
	
````



{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````VB
	
	        Const validXhtml As String = "<b>valid xhtml</b>."
	        Const systemXhtml As String = "Provided html is not acceptable."
	
	        Dim txt As New Telerik.Reporting.HtmlTextBox()
	        txt.Value = String.Format("=Iif(IsValidXhtml('{0}'), '{0}', '{1}')", validXhtml, systemXhtml)
	
	        '#End Region
	    End Sub
	
	    Public Sub Validate_Xhtml_Using_Event_And_ValueError_Snippet()
	        '#Region Validate_Xhtml_Using_Event_And_ValueError_Snippet
	
	        Dim txt As New Telerik.Reporting.HtmlTextBox()
	        AddHandler txt.ItemDataBinding, AddressOf ValueErrorHandler
	        '#End Region
	    End Sub
	
	    '#Region Validate_Xhtml_Using_Event_And_ValueError1_Snippet
	    Const invalidXhtml As String = "<b>invalid xhtml."
	    Const defaultXhtml As String = "Provided html is not acceptable."
	
	    Private Sub ValueErrorHandler(ByVal sender As Object, ByVal e As EventArgs)
	        Dim procTxt As Telerik.Reporting.Processing.HtmlTextBox = DirectCast(sender, Telerik.Reporting.Processing.HtmlTextBox)
	        Try
	            ' html that will not be accepted
	            procTxt.Value = invalidXhtml
	        Catch generatedExceptionName As Exception
	            procTxt.Value = defaultXhtml
	        End Try
	    End Sub
	    '#End Region
	End Class



## Validate Xhtml Using Event And IsValidXhtml

Use the __IsValidXhtml__ inside the HtmlTextBox __ItemDataBinding__ handler:

{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````C#
	
	            const string validXhtml = "<b>valid xhtml</b>.";
	            const string systemXhtml = "Provided html is not acceptable.";
	
	            Telerik.Reporting.HtmlTextBox txt = new Telerik.Reporting.HtmlTextBox();
	            txt.ItemDataBinding += delegate(object sender, EventArgs args)
	                {
	                    Telerik.Reporting.Processing.HtmlTextBox procTxt = (Telerik.Reporting.Processing.HtmlTextBox)sender;
	                    if (Telerik.Reporting.Processing.XhtmlValidator.IsValidXhtml(validXhtml))
	                    {
	                        procTxt.Value = validXhtml;
	                    }
	                    else
	                    {
	                        procTxt.Value = systemXhtml;
	                    }
	                };
````



	{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````
	        Dim txt As New Telerik.Reporting.HtmlTextBox()
	        AddHandler txt.ItemDataBinding, AddressOf MyEventHandler
	        '#End Region
	
	    End Sub
	    '#Region Validate_Xhtml_Using_Event_And_IsValidXhtml1_Snippet
	    Const validXhtml As String = "<b>valid xhtml</b>."
	    Const systemXhtml As String = "Provided html is not acceptable."
	
	    Private Sub MyEventHandler(ByVal sender As Object, ByVal e As EventArgs)
	        Dim procTxt As Telerik.Reporting.Processing.HtmlTextBox = DirectCast(sender, Telerik.Reporting.Processing.HtmlTextBox)
	        If Telerik.Reporting.Processing.XhtmlValidator.IsValidXhtml(validXhtml) Then
	            procTxt.Value = validXhtml
	        Else
	            procTxt.Value = systemXhtml
	        End If
	    End Sub
	    '#End Region
	
	    Public Sub Validate_Xhtml_Using_IsValidXhtml_InExpression_Snippet()
	        '#Region Validate_Xhtml_Using_IsValidXhtml_InExpression_Snippet
	
	        Const validXhtml As String = "<b>valid xhtml</b>."
	        Const systemXhtml As String = "Provided html is not acceptable."
	
	        Dim txt As New Telerik.Reporting.HtmlTextBox()
	        txt.Value = String.Format("=Iif(IsValidXhtml('{0}'), '{0}', '{1}')", validXhtml, systemXhtml)
	
	        '#End Region
	    End Sub
	
	    Public Sub Validate_Xhtml_Using_Event_And_ValueError_Snippet()
	        '#Region Validate_Xhtml_Using_Event_And_ValueError_Snippet
	
	        Dim txt As New Telerik.Reporting.HtmlTextBox()
	        AddHandler txt.ItemDataBinding, AddressOf ValueErrorHandler
	        '#End Region
	    End Sub
	
	    '#Region Validate_Xhtml_Using_Event_And_ValueError1_Snippet
	    Const invalidXhtml As String = "<b>invalid xhtml."
	    Const defaultXhtml As String = "Provided html is not acceptable."
	
	    Private Sub ValueErrorHandler(ByVal sender As Object, ByVal e As EventArgs)
	        Dim procTxt As Telerik.Reporting.Processing.HtmlTextBox = DirectCast(sender, Telerik.Reporting.Processing.HtmlTextBox)
	        Try
	            ' html that will not be accepted
	            procTxt.Value = invalidXhtml
	        Catch generatedExceptionName As Exception
	            procTxt.Value = defaultXhtml
	        End Try
	    End Sub
	    '#End Region
	End Class



## Validate Xhtml Using Event And ValueError

Use a __try-catch block__ to handle the exception:

{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````C#
	
	            const string invalidXhtml = "<b>invalid xhtml.";
	            const string systemXhtml = "Provided html is not acceptable.";
	
	            Telerik.Reporting.HtmlTextBox txt = new Telerik.Reporting.HtmlTextBox();
	            txt.ItemDataBinding += delegate(object sender, EventArgs args)
	                {
	                    Telerik.Reporting.Processing.HtmlTextBox procTxt = (Telerik.Reporting.Processing.HtmlTextBox)sender;
	                    try
	                    {
	                        procTxt.Value = invalidXhtml;
	                        // html that will not be accepted
	                    }
	                    catch (Exception)
	                    {
	                        procTxt.Value = systemXhtml;
	                    }
	                };
````



	{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````VB
	
	        Dim txt As New Telerik.Reporting.HtmlTextBox()
	        AddHandler txt.ItemDataBinding, AddressOf ValueErrorHandler
	        '#End Region
	    End Sub
	
	    '#Region Validate_Xhtml_Using_Event_And_ValueError1_Snippet
	    Const invalidXhtml As String = "<b>invalid xhtml."
	    Const defaultXhtml As String = "Provided html is not acceptable."
	
	    Private Sub ValueErrorHandler(ByVal sender As Object, ByVal e As EventArgs)
	        Dim procTxt As Telerik.Reporting.Processing.HtmlTextBox = DirectCast(sender, Telerik.Reporting.Processing.HtmlTextBox)
	        Try
	            ' html that will not be accepted
	            procTxt.Value = invalidXhtml
	        Catch generatedExceptionName As Exception
	            procTxt.Value = defaultXhtml
	        End Try
	    End Sub
	    '#End Region
	End Class



# See Also
