---
title: How to Add a Bookmark Action
page_title: How to Add a Bookmark Action | for Telerik Reporting Documentation
description: How to Add a Bookmark Action
slug: telerikreporting/designing-reports/adding-interactivity-to-reports/actions/how-to/how-to-add-a-bookmark-action
tags: how,to,add,a,bookmark,action
published: True
position: 1
---

# How to Add a Bookmark Action



## Adding a bookmark action using the Report Designer

1. In Design view, right-click the report item to which you want to add a link and then click __Properties__. 


1. In The Properties dialog box for that report item, click __Action__.

1. Select __Navigate to bookmark__. An additional section appears in the dialog box for this option.

1. In the __Target bookmark by Value__ textbox, type a bookmark or an expression that 
	evaluates to a bookmark.

1. Click __OK__

1. To test the link, run the report and click the report item with the applied Action. For TextBox items, it is
	helpful to change the style of the text to indicate to the user that the text is a link. For example, 
	change the color to blue and the effect to underline by setting the corresponding Font properties of the TextBox.


## Adding a bookmark action programatically

{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````C#
	
	            Telerik.Reporting.NavigateToBookmarkAction bookmarkAction1 = new Telerik.Reporting.NavigateToBookmarkAction();
	            textBox2.DocumentMapText = "MyBookMark";
	            bookmarkAction1.TargetBookmarkId = "MyBookMark";
	            textBox1.Action = bookmarkAction1;
	
````



{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````VB
	
	        Dim bookmarkAction1 As New Telerik.Reporting.NavigateToBookmarkAction()
	        textBox2.DocumentMapText = "MyBookMark"
	        bookmarkAction1.TargetBookmarkId = "MyBookMark"
	        textBox1.Action = bookmarkAction1
	
	        '#End Region
	
	        Assert.AreEqual("MyBookMark", bookmarkAction1.TargetBookmarkId)
	        Assert.AreEqual("MyBookMark", textBox2.DocumentMapText)
	    End Sub
	
	    <TestMethod()> _
	    Public Sub Navigate_To_Url()
	        Dim textBox1 As New Telerik.Reporting.TextBox()
	
	        '#Region "AddNewNavigateToUrlSnippet"
	
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

 * [How to: Add a Hyperlink Action]({%slug telerikreporting/designing-reports/adding-interactivity-to-reports/actions/how-to/how-to-add-a-hyperlink-action%})

 * [Expressions]({%slug telerikreporting/designing-reports/connecting-to-data/expressions/overview%})

 * [Data Items]({%slug telerikreporting/designing-reports/connecting-to-data/data-items/overview%})
