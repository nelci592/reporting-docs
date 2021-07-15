---
title: How to Construct a string to connect to Report Engine
page_title: How to Construct a string to connect to Report Engine | for Telerik Reporting Documentation
description: How to Construct a string to connect to Report Engine
slug: telerikreporting/using-reports-in-applications/display-reports-in-applications/how-to-construct-a-string-to-connect-to-report-engine
tags: how,to,construct,a,string,to,connect,to,report,engine
published: True
position: 5
---

# How to Construct a string to connect to Report Engine



When using WinForms or WPF Report Viewer, its connection to a Report Server or REST service instance should be additionally set.
        This topic lists the supported keywords for each report engine type and explains how to construct a connection string with or without using helper classes.
      

All the keywords and their values are case insensitive where applicable.
      

## Embedded Report Engine


| Keyword | Value |
| ------ | ------ |
|`Engine`|Embedde|




__Example: __`engine=embedded`

You can use a T:Telerik.ReportViewer.Common.EmbeddedConnectionInfo instance to help you create the connection string or
          leave it empty - the viewer will use the embedded report engine by default.
        

{{source=CodeSnippets\CS\API\Telerik\ReportViewer\WinForms\Form1.cs region=WinFormsEmbeddedReportEngineConnectionSnippet}}
````C#
	        private void SetEmbeddedReportEngineConnection(object sender, System.EventArgs e)
	        {
	            this.reportViewer1.ReportEngineConnection = new Telerik.ReportViewer.Common.EmbeddedConnectionInfo().ConnectionString;
	            //if the ReportEngineConnection property is set to null or empty string, it will use the EmbeddedConnectionInfo by default. 
	        }
````



{{source=CodeSnippets\VB\API\Telerik\ReportViewer\WinForms\Form1.vb region=WinFormsEmbeddedReportEngineConnectionSnippet}}
````VB
	    Private Sub SetEmbeddedReportEngineConnection(sender As Object, e As System.EventArgs)
	        Me.ReportViewer1.ReportEngineConnection = New Telerik.ReportViewer.Common.EmbeddedConnectionInfo().ConnectionString
	        'if the ReportEngineConnection property is set to null or empty string, it will use the EmbeddedReportEngineConnectionInfo by default.
	    End Sub
	#End Region
	
	#Region "WinFormsReportServerReportEngineConnectionSnippet"
	    Private Sub SetReportServerReportEngineConnection(sender As Object, e As System.EventArgs)
	        Me.ReportViewer1.ReportEngineConnection = New Telerik.ReportViewer.Common.ReportServerConnectionInfo("http://reportserver:83", "user", "pass", 20).ConnectionString
	    End Sub
	#End Region
	
	#Region "WinFormsRestServiceReportEngineConnectionSnippet"
	    Private Sub SetRestServiceReportEngineConnection(sender As Object, e As System.EventArgs)
	        Me.ReportViewer1.ReportEngineConnection = New Telerik.ReportViewer.Common.RestServiceConnectionInfo("http://servicehost:83/api/reports", "authToken", 20).ConnectionString
	    End Sub
	#End Region
	
	#Region "WinFormsCustomInteractiveActionExecutingEventSnippet"
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



## Report Server Engine


| Keyword | Value |
| ------ | ------ |
|`Engine`|ReportServer|
|`Uri`| *required* ; The URI of the Report Server instance|
|`Username`| *optional* ; The user name used to connect to Report Server. If omitted, the __Guest__ account will be used, if it is enabled.|
|`Password`| *optional* ; The password associated with the user name.|
|`Timeout`| *optional* ; The timeout for rendering a document measured in seconds. The default value is 100 seconds. Value of 0 indicates no expiration.|
|`KeepClientAlive`| *optional True/False* . Sets whether the client will be kept alive. When set to true expiration of the client will<br/>                be prevented by continually sending a request to the server, determined by the Reporting REST service's __ClientSessionTimeout__ . The default value is True|




__Example: __`engine=ReportServer;uri=http://localhost:83;username=admin;password=pass;timeout=30;keepClientAlive=true`

You can use a T:Telerik.ReportViewer.Common.ReportServerConnectionInfo instance to help you create the connection string.
        

{{source=CodeSnippets\CS\API\Telerik\ReportViewer\WinForms\Form1.cs region=WinFormsReportServerReportEngineConnectionSnippet}}
````C#
	        private void SetReportServerReportEngineConnection(object sender, System.EventArgs e)
	        {
	            this.reportViewer1.ReportEngineConnection = new Telerik.ReportViewer.Common.ReportServerConnectionInfo("http://reportserver:83", "user", "pass", 20).ConnectionString;
	        }
````



{{source=CodeSnippets\VB\API\Telerik\ReportViewer\WinForms\Form1.vb region=WinFormsReportServerReportEngineConnectionSnippet}}
````VB
	    Private Sub SetReportServerReportEngineConnection(sender As Object, e As System.EventArgs)
	        Me.ReportViewer1.ReportEngineConnection = New Telerik.ReportViewer.Common.ReportServerConnectionInfo("http://reportserver:83", "user", "pass", 20).ConnectionString
	    End Sub
	#End Region
	
	#Region "WinFormsRestServiceReportEngineConnectionSnippet"
	    Private Sub SetRestServiceReportEngineConnection(sender As Object, e As System.EventArgs)
	        Me.ReportViewer1.ReportEngineConnection = New Telerik.ReportViewer.Common.RestServiceConnectionInfo("http://servicehost:83/api/reports", "authToken", 20).ConnectionString
	    End Sub
	#End Region
	
	#Region "WinFormsCustomInteractiveActionExecutingEventSnippet"
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



## REST Service Engine


| Keyword | Value |
| ------ | ------ |
|`Engine`|RestService|
|`Uri`| *required* ; The URI of the REST Service instance.|
|`Token`| *optional* ; If provided, a *Bearer* token will be set in the *Authorization* header for every request to the REST service.|
|`UseDefaultCredentials`| *optional, True/False* ; If provided, the client will send the default credentials with its requests. The default value is *False* .|
|`Timeout`| *optional* ; The timeout for rendering a document measured in seconds. The default value is 100 seconds. Value of 0 indicates no expiration.|
|`KeepClientAlive`| *optional True/False* . Sets whether the client will be kept alive. When set to true expiration of the client will<br/>                be prevented by continually sending a request to the server, determined by the Reporting REST service's __ClientSessionTimeout__ . The default value is True|




__Example: __`engine=RestService;uri=http://localhost:18103/api/reports;token=authToken;useDefaultCredentials=true;timeout=30;keepClientAlive=true`

You can use a T:Telerik.ReportViewer.Common.RestServiceConnectionInfo instance to help you create the connection string.
        

{{source=CodeSnippets\CS\API\Telerik\ReportViewer\WinForms\Form1.cs region=WinFormsRestServiceReportEngineConnectionSnippet}}
````C#
	        private void SetRestServiceReportEngineConnection(object sender, System.EventArgs e)
	        {
	            this.reportViewer1.ReportEngineConnection = new Telerik.ReportViewer.Common.RestServiceConnectionInfo("http://servicehost:83/api/reports", "authToken", 20).ConnectionString;
	        }
````



{{source=CodeSnippets\VB\API\Telerik\ReportViewer\WinForms\Form1.vb region=WinFormsRestServiceReportEngineConnectionSnippet}}
````VB
	    Private Sub SetRestServiceReportEngineConnection(sender As Object, e As System.EventArgs)
	        Me.ReportViewer1.ReportEngineConnection = New Telerik.ReportViewer.Common.RestServiceConnectionInfo("http://servicehost:83/api/reports", "authToken", 20).ConnectionString
	    End Sub
	#End Region
	
	#Region "WinFormsCustomInteractiveActionExecutingEventSnippet"
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



# See AlsoT:Telerik.ReportViewer.Common.EmbeddedConnectionInfoT:Telerik.ReportViewer.Common.ReportServerConnectionInfoT:Telerik.ReportViewer.Common.RestServiceConnectionInfo
