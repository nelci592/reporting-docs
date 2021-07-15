---
title: How to Add manually report viewer to a Windows Forms' .NET Framework project
page_title: How to Add manually report viewer to a Windows Forms' .NET Framework project | for Telerik Reporting Documentation
description: How to Add manually report viewer to a Windows Forms' .NET Framework project
slug: telerikreporting/using-reports-in-applications/display-reports-in-applications/windows-forms-application/how-to-add-manually-report-viewer-to-a-windows-forms'-.net-framework-project
tags: how,to,add,manually,report,viewer,to,a,windows,forms',.net,framework,project
published: True
position: 3
---

# How to Add manually report viewer to a Windows Forms' .NET Framework project



## Assign report to the viewer in design time

To use Telerik Reports in Windows Forms application, you need the Windows Forms report viewer:

1. 
            Drag the __ReportViewer__ control from the __Toolbox__
            to the form design surface.   
  ![](images/ReportViewer.png)

1. Add reference to the class library that contains your reports in the windows form application.

1. Build the application

1. 
            Set the __ReportSource__ for the report viewer. For more information, see [How to Set ReportSource for Report Viewers]({%slug telerikreporting/using-reports-in-applications/display-reports-in-applications/how-to-set-reportsource-for-report-viewers%}).
          

1. 
            To run the report in the viewer, call __ReportViewer.RefreshReport()__ from your application code__.__

## Assign report to the viewer programmatically

In the __Form_Load__ event handler you create an instance report source and set its __ReportDocument__
          property to a report instance. Next assign the instance report source to the __ReportSource__ property of the viewer.
          Finally call __ReportViewer.RefreshReport().__

{{source=CodeSnippets\CS\API\Telerik\ReportViewer\WinForms\Form1.cs region=Winviewer_SetReportSource}}
````C#
	        private void Form1_Load(object sender, EventArgs e)
	        {
	            var typeReportSource = new Telerik.Reporting.TypeReportSource();
	            typeReportSource.TypeName = "Telerik.Reporting.Examples.CSharp.ListBoundReport, CSharp.ReportLibrary";
	            this.reportViewer1.ReportSource = typeReportSource;
	            reportViewer1.RefreshReport();
	        }
````



{{source=CodeSnippets\VB\API\Telerik\ReportViewer\WinForms\Form1.vb region=Winviewer_SetReportSource}}
````VB
	    Private Sub Form1_Load(sender As Object, e As EventArgs)
	        Dim typeReportSource = New Telerik.Reporting.TypeReportSource()
	        typeReportSource.TypeName = "Telerik.Reporting.Examples.CSharp.ListBoundReport, CSharp.ReportLibrary"
	        Me.ReportViewer1.ReportSource = typeReportSource
	        ReportViewer1.RefreshReport()
	    End Sub
	#End Region
	
	    Private Sub Form1_Load2(sender As Object, e As EventArgs)
	        AddHandler Me.ReportViewer1.RenderingBegin, AddressOf reportViewer1_RenderingBegin
	        AddHandler Me.ReportViewer1.RenderingEnd, AddressOf reportViewer1_RenderingEnd
	        AddHandler Me.ReportViewer1.PrintBegin, AddressOf reportViewer1_PrintBegin
	        AddHandler Me.ReportViewer1.PrintEnd, AddressOf reportViewer1_PrintEnd
	        AddHandler Me.ReportViewer1.ExportBegin, AddressOf reportViewer1_ExportBegin
	        AddHandler Me.ReportViewer1.ExportEnd, AddressOf reportViewer1_ExportEnd
	        AddHandler Me.ReportViewer1.UpdateUI, AddressOf reportViewer1_UpdateUI
	        AddHandler Me.ReportViewer1.[Error], AddressOf reportViewer1_Error
	        AddHandler Me.ReportViewer1.InteractiveActionExecuting, AddressOf reportViewer1_CustomInteractiveActionExecuting
	        AddHandler Me.ReportViewer1.InteractiveActionExecuting, AddressOf reportViewer1_InteractiveActionExecuting
	        AddHandler Me.ReportViewer1.InteractiveActionEnter, AddressOf reportViewer1_InteractiveActionEnter
	        AddHandler Me.ReportViewer1.InteractiveActionLeave, AddressOf reportViewer1_InteractiveActionLeave
	        AddHandler Me.ReportViewer1.ViewerToolTipOpening, AddressOf reportViewer1_ViewerToolTipOpening
	    End Sub
	
	#Region "WinFormsRenderingBeginEventSnippet"
	    Private Sub reportViewer1_RenderingBegin(sender As Object, e As Telerik.ReportViewer.Common.RenderingBeginEventArgs)
	        If True Then
	            ' some logic here
	            ' Cancel is false by default
	            e.Cancel = True
	        End If
	    End Sub
	#End Region
	
	#Region "WinFormsRenderingEndEventSnippet"
	    Private Sub reportViewer1_RenderingEnd(sender As Object, e As Telerik.ReportViewer.Common.RenderingEndEventArgs)
	        ' suitable for logging and triggering other actions
	    End Sub
	#End Region
	
	#Region "WinFormsPrintBeginEventSnippet"
	    Private Sub reportViewer1_PrintBegin(sender As Object, e As Telerik.ReportViewer.Common.PrintBeginEventArgs)
	        If True Then
	            ' some logic here
	            ' Cancel is false by default
	            e.Cancel = True
	        End If
	
	        If True Then
	            e.PrinterSettings.Copies = 2
	        End If
	
	        ' To prevent the Print Dialog from appearing, you should specify valid printer settings to this method.
	        If True Then
	            ' Obtain the settings of the default printer
	            e.PrinterSettings = New System.Drawing.Printing.PrinterSettings()
	
	            ' To suppress the Print dialogs. The standard print controller comes with no UI
	            e.PrintController = New System.Drawing.Printing.StandardPrintController()
	        End If
	    End Sub
	#End Region
	
	#Region "WinFormsPrintEndEventSnippet"
	    Private Sub reportViewer1_PrintEnd(sender As Object, e As Telerik.ReportViewer.Common.PrintEndEventArgs)
	        ' suitable for logging and triggering other actions
	    End Sub
	#End Region
	
	#Region "WinFormsExportBeginEventSnippet"
	    Private Sub reportViewer1_ExportBegin(sender As Object, args As Telerik.ReportViewer.Common.ExportBeginEventArgs)
	        If True Then
	            ' some logic here
	            ' Cancel is false by default
	            args.Cancel = True
	        End If
	
	        Select Case args.Format
	            Case "Excel"
	                ' do something
	                Exit Select
	            Case "PDF"
	                ' do something
	                Exit Select
	        End Select
	    End Sub
	#End Region
	
	#Region "WinFormsExportEndEventSnippet"
	    Private Sub reportViewer1_ExportEnd(sender As Object, args As Telerik.ReportViewer.Common.ExportEndEventArgs)
	        'some logic if report processing is not successful
	        If args.Exception IsNot Nothing Then
	        Else
	            'suppress the viewer SaveFileDialog and use your own
	            args.Handled = True
	            Dim fileName = args.DocumentName
	            Dim extension = args.DocumentExtension
	            Dim filter = String.Format("{0} (*.{1})|*.{1}|All Files (*.*)|*.*", fileName, extension)
	
	            Dim saveFileDlg = New SaveFileDialog() With { _
	                .Filter = filter, _
	                .FileName = fileName + "." + extension _
	            }
	
	            If saveFileDlg.ShowDialog() = DialogResult.OK Then
	                Try
	                    Using fs = New FileStream(saveFileDlg.FileName, FileMode.Create)
	                        fs.Write(args.DocumentBytes, 0, args.DocumentBytes.Length)
	                    End Using
	
	                    'Optionally open the file
	                    If Not String.IsNullOrEmpty(saveFileDlg.FileName) Then
	                        System.Diagnostics.Process.Start(saveFileDlg.FileName)
	                    End If
	                    'Handle exception
	                Catch generatedExceptionName As Exception
	                End Try
	            End If
	        End If
	    End Sub
	#End Region
	
	#Region "WinFormsUpdateUIEventSnippet"
	    Private Sub reportViewer1_UpdateUI(sender As Object, e As System.EventArgs)
	        ' invoked whenever the viewer state is changed
	    End Sub
	#End Region
	
	#Region "WinFormsErrorEventSnippet"
	    Private Sub reportViewer1_Error(sender As Object, args As Telerik.Reporting.ErrorEventArgs)
	        If TypeOf args.Exception Is System.Exception Then
	            ' check for a specific exception
	            ' do something with the message and/or the 
	            Dim message = args.Exception.Message
	        End If
	    End Sub
	#End Region
	
	#Region "WinFormsCancelRenderingSnippet"
	    ' Stop rendering the report. 
	    Private Sub button1_Click(sender As Object, e As System.EventArgs)
	        Me.ReportViewer1.CancelRendering()
	    End Sub
	#End Region
	
	#Region "WinFormsCanMoveToPageCurrentPageSnippet"
	    ' Navigate to a desired page
	    Private Sub button2_Click(sender As Object, e As System.EventArgs)
	        Dim desiredPage = 5
	
	        ' Check if the viewer can navigate to the page since the report may have fewer pages for example
	        If Me.ReportViewer1.CanMoveToPage(desiredPage) Then
	            ' By setting the property the viewer will automatically navigate to the page in question
	            Me.ReportViewer1.CurrentPage = desiredPage
	        End If
	    End Sub
	#End Region
	
	#Region "WinFormsPrintReportSnippet"
	    ' Opens the dialog to print the report
	    Private Sub button4_Click(sender As Object, e As System.EventArgs)
	        Me.ReportViewer1.PrintReport()
	    End Sub
	#End Region
	
	#Region "WinFormsExportReportSnippet"
	    ' Opens the dialog to export the report
	    Private Sub button5_Click(sender As Object, e As System.EventArgs)
	        Me.ReportViewer1.ExportReport("PDF", Nothing)
	    End Sub
	#End Region
	
	#Region "WinFormsRefreshReportSnippet"
	    ' Refresh the report with the current parameters
	    Private Sub button6_Click(sender As Object, e As System.EventArgs)
	        Me.ReportViewer1.RefreshReport()
	    End Sub
	#End Region
	
	#Region "WinFormsNavigateBackSnippet"
	    ' Navigate to the previous report in the history if available
	    Private Sub button7_Click(sender As Object, e As System.EventArgs)
	        If Me.ReportViewer1.NavigateBackEnabled Then
	            Me.ReportViewer1.NavigateBack()
	        End If
	    End Sub
	#End Region
	
	#Region "WinFormsNavigateForwardSnippet"
	    ' Navigate to the next report in the history if available
	    Private Sub button8_Click(sender As Object, e As System.EventArgs)
	        If Me.ReportViewer1.NavigateBackEnabled Then
	            Me.ReportViewer1.NavigateBack()
	        End If
	    End Sub
	#End Region
	
	#Region "WinFormsDocumentMapSnippet"
	    ' Toggle the document map
	    Private Sub button9_Click(sender As Object, e As System.EventArgs)
	        Me.ReportViewer1.DocumentMapVisible = Not Me.ReportViewer1.DocumentMapVisible
	    End Sub
	#End Region
	
	#Region "WinFormsParametersAreaSnippet"
	    ' Toggle the parameters area
	    Private Sub button10_Click(sender As Object, e As System.EventArgs)
	        Me.ReportViewer1.ParametersAreaVisible = Not Me.ReportViewer1.ParametersAreaVisible
	    End Sub
	#End Region
	
	#Region "WinFormsTotalPagesSnippet"
	    ' Go to the middle of the report
	    Private Sub button11_Click(sender As Object, e As System.EventArgs)
	        Dim middlePage = Me.ReportViewer1.TotalPages / 2
	        Me.ReportViewer1.CurrentPage = middlePage
	    End Sub
	#End Region
	
	#Region "WinFormsViewModeSnippet"
	    ' Switch to interactive mode
	    Private Sub button12_Click(sender As Object, e As System.EventArgs)
	        Me.ReportViewer1.ViewMode = Telerik.ReportViewer.WinForms.ViewMode.Interactive
	    End Sub
	#End Region
	
	#Region "WinFormsZoomPercentSnippet"
	    ' Set the zoom percent to a specific value
	    Private Sub button13_Click(sender As Object, e As System.EventArgs)
	        Me.ReportViewer1.ZoomMode = Telerik.ReportViewer.WinForms.ZoomMode.Percent
	        Me.ReportViewer1.ZoomPercent = 140
	    End Sub
	#End Region
	
	#Region "WinFormsZoomModeSnippet"
	    ' Set the zoom mode to PageWidth
	    Private Sub button14_Click(sender As Object, e As System.EventArgs)
	        Me.ReportViewer1.ZoomMode = Telerik.ReportViewer.WinForms.ZoomMode.PageWidth
	    End Sub
	#End Region
	
	#Region "WinFormsEmbeddedReportEngineConnectionSnippet"
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



If the current application has to be declared as DPI-aware, an additional element needs to be added to the application manifest file, as explained
          [here](F25EB909-7941-4B78-B24C-4025257A26C4#dpiAware).
        

# See Also[](66CD7D60-7708-42D5-8BB4-506676E8679E)

 * [Windows Forms Application]({%slug telerikreporting/using-reports-in-applications/display-reports-in-applications/windows-forms-application/overview%})

 * [Report Viewer Localization]({%slug telerikreporting/using-reports-in-applications/display-reports-in-applications/windows-forms-application/report-viewer-localization%})
