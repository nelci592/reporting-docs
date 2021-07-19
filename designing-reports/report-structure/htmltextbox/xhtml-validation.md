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

{{source=CodeSnippets\CS\API\Telerik\Reporting\Processing\HtmlTextBoxSnippets.cs region=Validate_Xhtml_Using_IsValidXhtml_InExpression_Snippet}}
````C#
	
	            const string validXhtml = "<b>valid xhtml</b>.";
	            const string systemXhtml = "Provided html is not acceptable.";
	
	            Telerik.Reporting.HtmlTextBox txt = new Telerik.Reporting.HtmlTextBox();
	            txt.Value = string.Format("=Iif(IsValidXhtml('{0}'), '{0}', '{1}')", validXhtml, systemXhtml);
	
````



{{source=CodeSnippets\VB\API\Telerik\Reporting\Processing\HtmlTextBoxSnippets.vb region=Validate_Xhtml_Using_IsValidXhtml_InExpression_Snippet}}
````VB
	
	        Const validXhtml As String = "<b>valid xhtml</b>."
	        Const systemXhtml As String = "Provided html is not acceptable."
	
	        Dim txt As New Telerik.Reporting.HtmlTextBox()
	        txt.Value = String.Format("=Iif(IsValidXhtml('{0}'), '{0}', '{1}')", validXhtml, systemXhtml)
	
````



## Validate Xhtml Using Event And IsValidXhtml

Use the __IsValidXhtml__ inside the HtmlTextBox __ItemDataBinding__ handler:

{{source=CodeSnippets\CS\API\Telerik\Reporting\Processing\HtmlTextBoxSnippets.cs region=Validate_Xhtml_Using_Event_And_IsValidXhtml_Snippet}}
````C#
	
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







## Validate Xhtml Using Event And ValueError

Use a __try-catch block__ to handle the exception:

	



	



# See Also
