---
title: Custom Action
page_title: Custom Action | for Telerik Reporting Documentation
description: Custom Action
slug: telerikreporting/designing-reports/adding-interactivity-to-reports/actions/custom-action
tags: custom,action
published: True
position: 7
---

# Custom Action



A custom action is an action that contains a collection of parameters, defined by the user, that will be evaluated during report processing.
        It does not affect the currently viewed report in any way - its purpose is to be used in a report viewer's interactive action event handlers:
        __InteractiveActionExecuting()__, __InteractiveActionEnter()__ and __InteractiveActionLeave()__.
      

To define a T:Telerik.Reporting.CustomAction use the [Edit Action Dialog]({%slug telerikreporting/designing-reports/report-designer-tools/desktop-designers/tools/edit-action-dialog%}) or create it programmatically in the report class body.
      

Here is an example how to get the custom action's parameters in __InteractiveActionExecuting()__ event of __WinForms Report Viewer__.
      

{{source=CodeSnippets\CS\API\Telerik\ReportViewer\WinForms\Form1.cs region=WinFormsCustomInteractiveActionExecutingEventSnippet}}
````C#
	
	        void reportViewer1_CustomInteractiveActionExecuting(object sender, Telerik.ReportViewer.Common.InteractiveActionCancelEventArgs args)
	        {
	            var strB = new System.Text.StringBuilder();
	            strB.AppendLine("ReportItem name: " + args.Action.ReportItemName);
	
	            var customAction = args.Action as Telerik.Reporting.Processing.CustomAction;
	            if (null != customAction)
	            {
	                foreach (var p in customAction.Parameters)
	                {
	                    strB.AppendLine(string.Format("Parameter \"{0}\" value: {1}", p.Key, p.Value));
	                }
	            }
	
	            strB.AppendLine(string.Format("Mouse cursor position: {0}; Item bounds: {1}", args.CursorPos, args.Bounds));
	
	            MessageBox.Show(strB.ToString());
	        }
````



{{source=CodeSnippets\VB\API\Telerik\ReportViewer\WinForms\Form1.vb region=WinFormsCustomInteractiveActionExecutingEventSnippet}}
````VB
	    ' Handles the InteractiveActionExecuting event
	    ' Do not forget to add the WithEvents clause on ReportViewer1 instantiation if needed.
	    Private Sub reportViewer1_CustomInteractiveActionExecuting(sender As Object, args As Telerik.ReportViewer.Common.InteractiveActionCancelEventArgs) Handles ReportViewer1.InteractiveActionExecuting
	
	        Dim strB = New System.Text.StringBuilder()
	        strB.AppendLine("ReportItem name: " + args.Action.ReportItemName)
	
	        Dim customAction = TryCast(args.Action, Telerik.Reporting.Processing.CustomAction)
	        If customAction IsNot Nothing Then
	            For Each p As KeyValuePair(Of String, Object) In customAction.Parameters
	                strB.AppendLine(String.Format("Parameter ""{0}"" value: {1}", p.Key, p.Value))
	            Next
	        End If
	
	        strB.AppendLine(String.Format("Mouse cursor position: {0}; Item bounds: {1}", args.CursorPos, args.Bounds))
	
	        MessageBox.Show(strB.ToString())
	    End Sub
	#End Region
	
	#Region "WinFormsCancelingInteractiveActionExecutingEventSnippet"
	    ' Handles the InteractiveActionExecuting event
	    ' Do not forget to add the WithEvents clause on ReportViewer1 instantiation if needed.
	    Private Sub reportViewer1_InteractiveActionExecuting(sender As Object, args As Telerik.ReportViewer.Common.InteractiveActionCancelEventArgs) Handles ReportViewer1.InteractiveActionExecuting
	
	        Dim navigateToUrlAction = TryCast(args.Action, Telerik.Reporting.Processing.NavigateToUrlAction)
	        If navigateToUrlAction IsNot Nothing Then
	            If Not navigateToUrlAction.Url.StartsWith("https") Then
	                args.Cancel = MessageBox.Show("You are about to navigate to a non-secure page. Continue?", "Warning", MessageBoxButtons.YesNo, MessageBoxIcon.Warning) <> System.Windows.Forms.DialogResult.Yes
	            End If
	        End If
	    End Sub
	#End Region
	
	#Region "WinFormsInteractiveActionEnterEventSnippet"
	    ' Handles the InteractiveActionEnter event
	    ' Do not forget to add the WithEvents clause on ReportViewer1 instantiation if needed.
	    Private Sub reportViewer1_InteractiveActionEnter(sender As Object, args As Telerik.ReportViewer.Common.InteractiveActionEventArgs) Handles ReportViewer1.InteractiveActionEnter
	
	        Dim strB = New System.Text.StringBuilder()
	        strB.AppendLine("You have just entered an action area.")
	        strB.AppendLine("Action type: " + args.Action.[GetType]().Name)
	        strB.AppendLine("ReportItem name: " + args.Action.ReportItemName)
	        strB.AppendLine(String.Format("Mouse cursor position: {0}; Item bounds: {1}", args.CursorPos, args.Bounds))
	
	        Console.Out.WriteLine(strB.ToString())
	    End Sub
	#End Region
	
	#Region "WinFormsInteractiveActionLeaveEventSnippet"
	    ' Handles the InteractiveActionLeave event
	    ' Do not forget to add the WithEvents clause on ReportViewer1 instantiation if needed.
	    Private Sub reportViewer1_InteractiveActionLeave(sender As Object, args As Telerik.ReportViewer.Common.InteractiveActionEventArgs) Handles ReportViewer1.InteractiveActionLeave
	
	        Dim strB = New System.Text.StringBuilder()
	        strB.AppendLine("You have just left an action area.")
	        strB.AppendLine("Action type: " + args.Action.[GetType]().Name)
	        strB.AppendLine("ReportItem name: " + args.Action.ReportItemName)
	        strB.AppendLine(String.Format("Item bounds: {0}", args.Bounds))
	
	        Console.Out.WriteLine(strB.ToString())
	    End Sub
	#End Region
	
	#Region "WinFormsViewerToolTipOpeningEventSnippet"
	    ' Handles the ViewerToolTipOpening event
	    ' Do not forget to add the WithEvents clause on ReportViewer1 instantiation if needed.
	    Private Sub reportViewer1_ViewerToolTipOpening(sender As Object, args As Telerik.ReportViewer.Common.ToolTipOpeningEventArgs) Handles ReportViewer1.ViewerToolTipOpening
	        If args.ToolTip.Title.Contains("DoNotShow") Then
	            args.Cancel = True
	        Else
	            args.ToolTip.Title = "The tooltip title is changed!"
	            args.ToolTip.Text += " (changed)"
	        End If
	    End Sub
	#End Region
	
	
	#Region "WinFormsViewerAccessibilityKeyMapSnippet"
	
	    Private Sub SetToolbarShortcutKey()
	        ' substituting the default 'M' key to access the toolbar with 'T'
	        Dim map As System.Collections.Generic.Dictionary(Of Integer, Telerik.ReportViewer.Common.Accessibility.ShortcutKeys) = Me.ReportViewer1.AccessibilityKeyMap
	        map.Remove(CType(Keys.M, Integer))
	        map(CType(Keys.T, Integer)) = Telerik.ReportViewer.Common.Accessibility.ShortcutKeys.MENU_AREA_KEY
	        Me.ReportViewer1.AccessibilityKeyMap = map
	    End Sub
	#End Region
	
	End Class



# See Also

 * [Overview]({%slug telerikreporting/designing-reports/adding-interactivity-to-reports/actions/overview%})

 * [Interactive Action Events]({%slug telerikreporting/designing-reports/adding-interactivity-to-reports/actions/interactive-action-events%})

 * [How to Add a Custom Action]({%slug telerikreporting/designing-reports/adding-interactivity-to-reports/actions/how-to/how-to-add-a-custom-action%})
