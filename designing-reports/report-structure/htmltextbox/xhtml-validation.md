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

	



	



## Validate Xhtml Using Event And IsValidXhtml

Use the __IsValidXhtml__ inside the HtmlTextBox __ItemDataBinding__ handler:

	



	



## Validate Xhtml Using Event And ValueError

Use a __try-catch block__ to handle the exception:

	



	



# See Also
