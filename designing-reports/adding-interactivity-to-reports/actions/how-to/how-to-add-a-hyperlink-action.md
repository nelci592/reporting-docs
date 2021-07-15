---
title: How to Add a Hyperlink Action
page_title: How to Add a Hyperlink Action | for Telerik Reporting Documentation
description: How to Add a Hyperlink Action
slug: telerikreporting/designing-reports/adding-interactivity-to-reports/actions/how-to/how-to-add-a-hyperlink-action
tags: how,to,add,a,hyperlink,action
published: True
position: 2
---

# How to Add a Hyperlink Action



Add a hyperlink to a URL when you want users to be able to click a link in a report and open a browser
    	to the URL you specify. You must ensure that the user has access to the URL that you provide i.e. it allows anonymous access or does not require credentials. 
    	You can add a hyperlink to a URL to any item that has an Action property.


## Adding a Hyperlink action using Report Designer

1. In Design view, right-click a report item to which you want to add a link and then click __Properties__.

1. In the Properties dialog box, click __Action__.

1. Select __Navigate to URL__. An additional section appears in the dialog box for this option.

1. In __Target URL__ TextBox, type a URL or an expression that evaluates to a URL.

1. Click __OK__.

1. To test the link, run the report and click the report item with the applied __Action__. For TextBoxes, it is
	helpful to change the color and effect of the text to indicate that the text is a link. For example, change the color to blue and
	the effect to underline by setting the corresponding __Font__ properties of the TextBox.


## Adding a Hyperlink action programatically

{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````C#
	
	            Telerik.Reporting.NavigateToUrlAction UrlAction1 = new Telerik.Reporting.NavigateToUrlAction();
	            UrlAction1.Url = "http://demos.telerik.com/reporting";
	            textBox1.Action = UrlAction1;
	
````



{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````VB
	
	        Dim UrlAction1 As New Telerik.Reporting.NavigateToUrlAction()
	        UrlAction1.Url = "http://demos.telerik.com/reporting"
	        textBox1.Action = UrlAction1
	
	        '#End Region
	
	        Assert.AreEqual("http://demos.telerik.com/reporting", UrlAction1.Url)
	    End Sub
	
	    <TestMethod()> _
	    Public Sub Toggle_Visibility_Snippet()
	        Dim textBox1 As New Telerik.Reporting.TextBox()
	        Dim textBox2 As New Telerik.Reporting.TextBox()
	
	        '#Region "AddNewToggleVisibilitySnippet"
	
	        Dim toggleVisibilityAction1 As New Telerik.Reporting.ToggleVisibilityAction()
	        textBox1.Action = toggleVisibilityAction1
	        toggleVisibilityAction1.DisplayExpandedMark = False
	        toggleVisibilityAction1.Targets.AddRange(New Telerik.Reporting.IToggleVisibilityTarget() {textBox2})
	
	        '#End Region
	
	    End Sub
	
	    <TestMethod()> _
	    Public Sub CustomAction_Snippet()
	        Dim textBox1 As New Telerik.Reporting.TextBox()
	
	        '#Region "AddNewCustomActionSnippet"
	
	        Dim customAction As New Telerik.Reporting.CustomAction()
	        customAction.Parameters.Add("param1", "=Fields.Name")
	        customAction.Parameters.Add("param2", "=Now()")
	        textBox1.Action = customAction
	
	        '#End Region
	
	    End Sub
	
	End Class



# See Also

 * [How to: Add a Drillthrough Report Action]({%slug telerikreporting/designing-reports/adding-interactivity-to-reports/actions/how-to/how-to-add-a-drillthrough/navigate-to-report-action%})

 * [How to: Add a Bookmark Action]({%slug telerikreporting/designing-reports/adding-interactivity-to-reports/actions/how-to/how-to-add-a-bookmark-action%})

 * [Expressions]({%slug telerikreporting/designing-reports/connecting-to-data/expressions/overview%})

 * [Data Items]({%slug telerikreporting/designing-reports/connecting-to-data/data-items/overview%})
