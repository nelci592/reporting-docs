---
title: Report Viewer Localization
page_title: Report Viewer Localization | for Telerik Reporting Documentation
description: Report Viewer Localization
slug: telerikreporting/using-reports-in-applications/display-reports-in-applications/wpf-application/report-viewer-localization
tags: report,viewer,localization
published: True
position: 6
---

# Report Viewer Localization



In the WPF Report Viewer, localized resources are stored in separate __RESX__  resource files and loaded according to the current UI culture settings. To understand how localized resources are loaded, it is useful to think of them as being organized in a hierarchical manner.       

## Types of Resources in the Hierarchy

* At the top of the hierarchy sit the fallback resources for the default UI culture, which is English ("en") by default. These are the only resources that do not have their own file. They are stored directly in the assembly of the __Report Viewer__  .

* Below the fallback resources are the resources for any neutral cultures. A neutral culture is associated with a language but not a region. For example, French ("fr") is a neutral culture. Note that the fallback resources are also for a neutral culture, but a special one.

* Below those are the resources for any specific cultures. A specific culture is associated with a language and a region. For example, French Canadian ("fr-CA") is a specific culture.

When the __Report Viewer__  tries to load any localized resource and does not find it it will travel up the hierarchy until it finds a resource file containing the requested resource.         

The best way to store your resources is to generalize them as much as possible. That means to store localized strings in resource files for neutral cultures rather than specific cultures whenever possible. For instance, if you have resources for the French Belgian ("fr-BE") culture and the resources immediately above are the fallback resources in English, a problem may result when someone uses your application on a system configured for the French Canadian culture. The __Report Viewer__  will look for a __RESX__  file named "fr-CA", it will not find it and will load the fallback resource, which is English, instead of loading the French resources. The following picture shows this undesirable scenario.         

  

  ![](images/localization1.png)

If you follow the recommended practice of placing as many resources as possible in a neutral resource file for the "fr" culture, the French Canadian user would not see resources marked for the "fr-BE" culture, but he or she would still see strings in French. The following situation demonstrates this preferred scenario.

  

  ![](images/localization2.png)

## Naming Conventions for the Localization Resources

__The Report Viewer__  uses the following naming convention when searching for localized __RESX__  resource files in the main application folder:         

* The names of the __RESX__  localization resource files should have the following format:             *Telerik.ReportViewer.WPF.TextResources.[culture].resx* Here “__[culture]__ ” is the name of the culture for the specified localization resource. For example, to provide a localization resource               for the French Belgian culture, the corresponding resource file should be named as follows:             *Telerik.ReportViewer.WPF.TextResources.fr-BE.resx* 

* Respectively, to provide a localization resource for the French neutral culture, the corresponding resource file should               be named as follows:             *Telerik.ReportViewer.WPF.TextResources.fr.resx* 

* It is possible to override the default resources for the language neutral culture, which are stored in the assembly of the               __Report Viewer__ . In that case the resource file should be named as follows:             *Telerik.ReportViewer.WPF.TextResources.resx* 

As described above, if for example the current UI culture is set to French Belgian, the __Report Viewer__  will search for localized __RESX__  resource files inside the main application folder in the following order:         

1. Telerik.ReportViewer.WPF.TextResources. __fr-BE__  .resx

1. Telerik.ReportViewer.WPF.TextResources. __fr__  .resx

1. Telerik.ReportViewer.WPF.TextResources.resx

  

  ![](images/localization3.png)

The above diagram illustrates a simple view of the resource fallback for a UI culture set to "fr-BE". The __Report Viewer__  handles the case probing the "fr-BE" __RESX__  resource file for the requested key first, and subsequently falls back to the neutral French culture "fr", ultimately looking in the default assembly resources for a value if a value has still not been found.         

## Adding Localization Resources for the Report Viewer

1. Add a new __RESX__  resource file to the main project of the application. Name the newly-created __RESX__  file according to the naming convention described above.

1. In the __Property Inspector__  specify the following properties for the resource file:

   1. __Build Action:__  "*None* "
              

   1. __Copy to Output Directory:__  "*Copy if newer* " or "*Copy always* "
              

1. Open the __RESX__  resource file in the __Visual Studio Resource Editor__  . Enter the required
            resource strings ([TextResources](/reporting/api/Telerik.ReportViewer.Wpf.TextResources))
            to translate the __Report Viewer__  to the desired language.

1. Repeat steps from 1 to 3 for each desired translation of the __Report Viewer__  .

1. Compile and run the project. When viewing a __Telerik Report__  , the __Report Viewer__  should be translated according to the current UI culture.

## Distributing an Application with a Localized Report Viewer

In order to distribute an application that uses __Telerik Reporting__            with a localized __Report Viewer__ , one should distribute all of the required           localization __RESX__  resource files, in addition to the main application assemblies.           For __WPF Applications__  the __RESX__            files should be placed in the same directory, where the application is installed.         

## Localization Using the ITextResources interface

The other way to localize the WPF __Report Viewer__  in a more flexible manner is to create a class that implements the           ITextResources interface and to implement all its properties, which represent all tooltips and messages in the Report Viewer. After you implement ITextResources you have to pass an instance of your custom class to the TextResources property ot the report viewer. The logic is pretty           simple, the property just has to return the correct translation for each resource key, as it is shown below:         

{{source=CodeSnippets\CS\API\Telerik\ReportViewer\Wpf\InterfaceLocalizationSnippets.cs region=InterfaceLocalizationSnippetStart}}
````C#
	        class CustomResources : Telerik.ReportViewer.Wpf.ITextResources
	        {
	            public string AllFiles
	            {
	                get
	                {
	                    return "Todos Archivos";
	                }
	            }
	            public string BackToolTip
	            {
	                get
	                {
	                    return "Navega hacia atrás";
	                }
	            }
	            public string CurrentPageToolTip
	            {
	                get
	                {
	                    return "Página corriente";
	                }
	            }
	
	
	            //...... Implement the rest of the properties ...... 
	            public string PageSetupToolTip
	            {
	                get
	                {
	                    return "Página de configuración";
	                }
	            }
	
	            public string LabelOf
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string CancelButtonText
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string ReportParametersNullText
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string PreviewButtonText
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string DocumentMapToolTip
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string ExportError
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string ExportingMessage
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string ExportToolTip
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string FirstPageToolTip
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string ForwardToolTip
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string LastPageToolTip
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string LoadingPageMessage
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string NextPageToolTip
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string NoReportError
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string PageNumberGreaterThanRangeError
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string PageNumberLessThanRangeError
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string ParametersToolTip
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string PreviousPageToolTip
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string PrintPreviewToolTip
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string PrintToolTip
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string ProcessingReportMessage
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string RefreshToolTip
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string ReportParametersAreaValidationError
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string ReportParametersSelectAllText
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string ReportParametersValidationError
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string InvalidValueForParameter
	            {
	                get
	                {
	                    return "Valor no válido para el parámetro";
	                }
	            }
	            public string StopToolTip
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string TotalPagesToolTip
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string UpdatingParametersMessage
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string ZoomToolTip
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string ZoomToPageWidth
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string ZoomToWholePage
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string NoPageToDisplay
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string SessionExpired
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string AccessibilityReportContentsArea
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string AccessibilityDocumentMapArea
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string AccessibilityParametersArea
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string AccessibilityParameter
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string AccessibilityParameterText
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string AccessibilityParameterBoolean
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string AccessibilityParameterDateTime
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string AccessibilityParameterNumerical
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string AccessibilityParameterMultiSelect
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string AccessibilityParameterMultiValue
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string AccessibilityParameterErrorMessage
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string AccessibilityPageNumberEditor
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string AccessibilityPageNumberSelector
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string AccessibilityReportViewerToolbar
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string AccessibilityStatus
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string AccessibilityStatusEnabled
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string AccessibilityStatusDisabled
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string AccessibilityToolbarButtonToggleParameters
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string AccessibilityToolbarButtonToggleDocumentMap
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string AccessibilityStateChecked
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string AccessibilityStateUnchecked
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string SearchCaptionLabel
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string SearchToolTip
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string SearchStopToolTip
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string SearchMatchCaseToolTip
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string SearchMatchWholeWordToolTip
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string SearchUseRegexToolTip
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string SearchNoMetadata
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string SearchNoResults
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string SearchResultsFormatString
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	        }
````
{{source=CodeSnippets\VB\API\Telerik\ReportViewer\Wpf\InterfaceLocalizationSnippets.vb region=InterfaceLocalizationSnippetStart}}
````VB.NET
	    Class CustomResources
	        Implements Telerik.ReportViewer.Wpf.ITextResources
	
	        Public ReadOnly Property AllFiles() As String Implements ReportViewer.Wpf.ITextResources.AllFiles
	            Get
	                Return "Todos Archivos"
	            End Get
	        End Property
	
	        Public ReadOnly Property BackToolTip() As String Implements ReportViewer.Wpf.ITextResources.BackToolTip
	            Get
	                Return "Navega hacia atrás"
	            End Get
	        End Property
	
	        Public ReadOnly Property CurrentPageToolTip() As String Implements ReportViewer.Wpf.ITextResources.CurrentPageToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        '...... Implement the rest of the properties ......
	        Public ReadOnly Property CancelButtonText As String Implements ReportViewer.Wpf.ITextResources.CancelButtonText
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property LabelOf As String Implements ReportViewer.Wpf.ITextResources.LabelOf
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property ReportParametersNullText As String Implements ReportViewer.Wpf.ITextResources.ReportParametersNullText
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property PreviewButtonText As String Implements ReportViewer.Wpf.ITextResources.PreviewButtonText
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property DocumentMapToolTip As String Implements ReportViewer.Wpf.ITextResources.DocumentMapToolTip
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property ExportError As String Implements ReportViewer.Wpf.ITextResources.ExportError
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property ExportingMessage As String Implements ReportViewer.Wpf.ITextResources.ExportingMessage
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property ExportToolTip As String Implements ReportViewer.Wpf.ITextResources.ExportToolTip
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property FirstPageToolTip As String Implements ReportViewer.Wpf.ITextResources.FirstPageToolTip
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property ForwardToolTip As String Implements ReportViewer.Wpf.ITextResources.ForwardToolTip
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property LastPageToolTip As String Implements ReportViewer.Wpf.ITextResources.LastPageToolTip
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property LoadingPageMessage As String Implements ReportViewer.Wpf.ITextResources.LoadingPageMessage
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property NextPageToolTip As String Implements ReportViewer.Wpf.ITextResources.NextPageToolTip
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property NoReportError As String Implements ReportViewer.Wpf.ITextResources.NoReportError
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property PageNumberGreaterThanRangeError As String Implements ReportViewer.Wpf.ITextResources.PageNumberGreaterThanRangeError
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property PageNumberLessThanRangeError As String Implements ReportViewer.Wpf.ITextResources.PageNumberLessThanRangeError
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property PageSetupToolTip() As String Implements ReportViewer.Wpf.ITextResources.PageSetupToolTip
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property ParametersToolTip As String Implements ReportViewer.Wpf.ITextResources.ParametersToolTip
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property PreviousPageToolTip As String Implements ReportViewer.Wpf.ITextResources.PreviousPageToolTip
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property PrintPreviewToolTip As String Implements ReportViewer.Wpf.ITextResources.PrintPreviewToolTip
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property PrintToolTip As String Implements ReportViewer.Wpf.ITextResources.PrintToolTip
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property ProcessingReportMessage As String Implements ReportViewer.Wpf.ITextResources.ProcessingReportMessage
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property RefreshToolTip As String Implements ReportViewer.Wpf.ITextResources.RefreshToolTip
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property ReportParametersAreaValidationError As String Implements ReportViewer.Wpf.ITextResources.ReportParametersAreaValidationError
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property ReportParametersSelectAllText As String Implements ReportViewer.Wpf.ITextResources.ReportParametersSelectAllText
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property InvalidValueForParameter As String Implements ReportViewer.Wpf.ITextResources.InvalidValueForParameter
	            Get
	                Return "Valor no válido para el parámetro"
	            End Get
	        End Property
	
	        Public ReadOnly Property ReportParametersValidationError As String Implements ReportViewer.Wpf.ITextResources.ReportParametersValidationError
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property StopToolTip() As String Implements ReportViewer.Wpf.ITextResources.StopToolTip
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property TotalPagesToolTip As String Implements ReportViewer.Wpf.ITextResources.TotalPagesToolTip
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property UpdatingParametersMessage As String Implements ReportViewer.Wpf.ITextResources.UpdatingParametersMessage
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property ZoomToolTip As String Implements ReportViewer.Wpf.ITextResources.ZoomToolTip
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property ZoomToPageWidth As String Implements ReportViewer.Wpf.ITextResources.ZoomToPageWidth
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property ZoomToWholePage As String Implements ReportViewer.Wpf.ITextResources.ZoomToWholePage
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property NoPageToDisplay As String Implements ReportViewer.Wpf.ITextResources.NoPageToDisplay
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property SessionExpired As String Implements ReportViewer.Wpf.ITextResources.SessionExpired
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityReportContentsArea As String Implements ITextResources.AccessibilityReportContentsArea
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityDocumentMapArea As String Implements ITextResources.AccessibilityDocumentMapArea
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityParametersArea As String Implements ITextResources.AccessibilityParametersArea
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityParameter As String Implements ITextResources.AccessibilityParameter
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityParameterText As String Implements ITextResources.AccessibilityParameterText
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityParameterBoolean As String Implements ITextResources.AccessibilityParameterBoolean
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityParameterDateTime As String Implements ITextResources.AccessibilityParameterDateTime
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityParameterNumerical As String Implements ITextResources.AccessibilityParameterNumerical
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityParameterMultiSelect As String Implements ITextResources.AccessibilityParameterMultiSelect
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityParameterMultiValue As String Implements ITextResources.AccessibilityParameterMultiValue
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityParameterErrorMessage As String Implements ITextResources.AccessibilityParameterErrorMessage
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityPageNumberEditor As String Implements ITextResources.AccessibilityPageNumberEditor
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityPageNumberSelector As String Implements ITextResources.AccessibilityPageNumberSelector
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityReportViewerToolbar As String Implements ITextResources.AccessibilityReportViewerToolbar
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityStatus As String Implements ITextResources.AccessibilityStatus
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityStatusEnabled As String Implements ITextResources.AccessibilityStatusEnabled
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityStatusDisabled As String Implements ITextResources.AccessibilityStatusDisabled
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityToolbarButtonToggleParameters As String Implements ITextResources.AccessibilityToolbarButtonToggleParameters
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityToolbarButtonToggleDocumentMap As String Implements ITextResources.AccessibilityToolbarButtonToggleDocumentMap
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityStateChecked As String Implements ITextResources.AccessibilityStateChecked
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityStateUnchecked As String Implements ITextResources.AccessibilityStateUnchecked
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property SearchCaptionLabel As String Implements ITextResources.SearchCaptionLabel
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property SearchToolTip As String Implements ITextResources.SearchToolTip
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property SearchStopToolTip As String Implements ITextResources.SearchStopToolTip
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property SearchMatchCaseToolTip As String Implements ITextResources.SearchMatchCaseToolTip
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property SearchMatchWholeWordToolTip As String Implements ITextResources.SearchMatchWholeWordToolTip
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property SearchUseRegexToolTip As String Implements ITextResources.SearchUseRegexToolTip
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property SearchNoMetadata As String Implements ITextResources.SearchNoMetadata
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property SearchNoResults As String Implements ITextResources.SearchNoResults
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property SearchResultsFormatString As String Implements ITextResources.SearchResultsFormatString
	            Get
	                Return "..."
	            End Get
	        End Property
	    End Class
````



Instead of a hard-coded string the property can be set in a method/contructor or to be created a method that returns string and implements a cutsom logic,           for example retreives the resource key from a database.         

{{source=CodeSnippets\CS\API\Telerik\ReportViewer\Wpf\InterfaceLocalizationSnippets.cs region=InterfaceLocalizationUsingMethodsSnippetStart}}
````C#
	        class CustomTextResources : Telerik.ReportViewer.Wpf.ITextResources
	        {
	
	            public string AllFiles
	            {
	                get
	                {
	                    return SqlHelper.GetViewerKeyFromDb(TextResourcesEnum.AllFiles);
	                }
	            }
	
	            public string BackToolTip
	            {
	                get
	                {
	                    return SqlHelper.GetViewerKeyFromDb(TextResourcesEnum.BackToolTip);
	                }
	            }
	
	            public string CurrentPageToolTip
	            {
	                get
	                {
	                    return SqlHelper.GetViewerKeyFromDb(TextResourcesEnum.CurrentPageToolTip);
	                }
	            }
	
	            //...... Implement the rest of the properties ......
	            public string CancelButtonText
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string LabelOf
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string ReportParametersNullText
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string PreviewButtonText
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string DocumentMapToolTip
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string ExportError
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string ExportingMessage
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string ExportToolTip
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string FirstPageToolTip
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string ForwardToolTip
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string LastPageToolTip
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string LoadingPageMessage
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string NextPageToolTip
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string NoReportError
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string PageNumberGreaterThanRangeError
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string PageNumberLessThanRangeError
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string PageSetupToolTip
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string ParametersToolTip
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string PreviousPageToolTip
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string PrintPreviewToolTip
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string PrintToolTip
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string ProcessingReportMessage
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string RefreshToolTip
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string ReportParametersAreaValidationError
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string ReportParametersSelectAllText
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string ReportParametersValidationError
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string InvalidValueForParameter
	            {
	                get
	                {
	                    return "Valor no válido para el parámetro";
	                }
	            }
	            public string StopToolTip
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string TotalPagesToolTip
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string UpdatingParametersMessage
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string ZoomToolTip
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string ZoomToPageWidth
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string ZoomToWholePage
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string NoPageToDisplay
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	            public string SessionExpired
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string AccessibilityReportContentsArea
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string AccessibilityDocumentMapArea
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string AccessibilityParametersArea
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string AccessibilityParameter
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string AccessibilityParameterText
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string AccessibilityParameterBoolean
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string AccessibilityParameterDateTime
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string AccessibilityParameterNumerical
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string AccessibilityParameterMultiSelect
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string AccessibilityParameterMultiValue
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string AccessibilityParameterErrorMessage
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string AccessibilityPageNumberEditor
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string AccessibilityPageNumberSelector
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string AccessibilityReportViewerToolbar
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string AccessibilityStatus
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string AccessibilityStatusEnabled
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string AccessibilityStatusDisabled
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string AccessibilityToolbarButtonToggleParameters
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string AccessibilityToolbarButtonToggleDocumentMap
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string AccessibilityStateChecked
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string AccessibilityStateUnchecked
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string SearchCaptionLabel
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string SearchToolTip
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string SearchStopToolTip
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string SearchMatchCaseToolTip
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string SearchMatchWholeWordToolTip
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string SearchUseRegexToolTip
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string SearchNoMetadata
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string SearchNoResults
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	
	            public string SearchResultsFormatString
	            {
	                get
	                {
	                    return "...";
	                }
	            }
	        }
````
{{source=CodeSnippets\VB\API\Telerik\ReportViewer\Wpf\InterfaceLocalizationSnippets.vb region=InterfaceLocalizationUsingMethodsSnippetStart}}
````VB.NET
	    Class CustomTextResources
	        Implements Telerik.ReportViewer.Wpf.ITextResources
	
	        Public ReadOnly Property AllFiles() As String Implements ReportViewer.Wpf.ITextResources.AllFiles
	            Get
	                Return SqlHelper.GetViewerKeyFromDb(TextResourcesEnum.AllFiles)
	            End Get
	        End Property
	
	        Public ReadOnly Property BackToolTip() As String Implements ReportViewer.Wpf.ITextResources.BackToolTip
	            Get
	                Return SqlHelper.GetViewerKeyFromDb(TextResourcesEnum.BackToolTip)
	            End Get
	        End Property
	
	        Public ReadOnly Property CurrentPageToolTip() As String Implements ReportViewer.Wpf.ITextResources.CurrentPageToolTip
	            Get
	                Return SqlHelper.GetViewerKeyFromDb(TextResourcesEnum.CurrentPageToolTip)
	            End Get
	        End Property
	
	        '...... Implement the rest of the properties ......
	        Public ReadOnly Property CancelButtonText As String Implements ReportViewer.Wpf.ITextResources.CancelButtonText
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property LabelOf As String Implements ReportViewer.Wpf.ITextResources.LabelOf
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property ReportParametersNullText As String Implements ReportViewer.Wpf.ITextResources.ReportParametersNullText
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property PreviewButtonText As String Implements ReportViewer.Wpf.ITextResources.PreviewButtonText
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property DocumentMapToolTip As String Implements ReportViewer.Wpf.ITextResources.DocumentMapToolTip
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property ExportError As String Implements ReportViewer.Wpf.ITextResources.ExportError
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property ExportingMessage As String Implements ReportViewer.Wpf.ITextResources.ExportingMessage
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property ExportToolTip As String Implements ReportViewer.Wpf.ITextResources.ExportToolTip
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property FirstPageToolTip As String Implements ReportViewer.Wpf.ITextResources.FirstPageToolTip
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property ForwardToolTip As String Implements ReportViewer.Wpf.ITextResources.ForwardToolTip
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property LastPageToolTip As String Implements ReportViewer.Wpf.ITextResources.LastPageToolTip
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property LoadingPageMessage As String Implements ReportViewer.Wpf.ITextResources.LoadingPageMessage
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property NextPageToolTip As String Implements ReportViewer.Wpf.ITextResources.NextPageToolTip
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property NoReportError As String Implements ReportViewer.Wpf.ITextResources.NoReportError
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property PageNumberGreaterThanRangeError As String Implements ReportViewer.Wpf.ITextResources.PageNumberGreaterThanRangeError
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property PageNumberLessThanRangeError As String Implements ReportViewer.Wpf.ITextResources.PageNumberLessThanRangeError
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property PageSetupToolTip() As String Implements ReportViewer.Wpf.ITextResources.PageSetupToolTip
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property ParametersToolTip As String Implements ReportViewer.Wpf.ITextResources.ParametersToolTip
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property PreviousPageToolTip As String Implements ReportViewer.Wpf.ITextResources.PreviousPageToolTip
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property PrintPreviewToolTip As String Implements ReportViewer.Wpf.ITextResources.PrintPreviewToolTip
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property PrintToolTip As String Implements ReportViewer.Wpf.ITextResources.PrintToolTip
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property ProcessingReportMessage As String Implements ReportViewer.Wpf.ITextResources.ProcessingReportMessage
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property RefreshToolTip As String Implements ReportViewer.Wpf.ITextResources.RefreshToolTip
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property ReportParametersAreaValidationError As String Implements ReportViewer.Wpf.ITextResources.ReportParametersAreaValidationError
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property ReportParametersSelectAllText As String Implements ReportViewer.Wpf.ITextResources.ReportParametersSelectAllText
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property InvalidValueForParameter As String Implements ReportViewer.Wpf.ITextResources.InvalidValueForParameter
	            Get
	                Return "Valor no válido para el parámetro"
	            End Get
	        End Property
	
	        Public ReadOnly Property ReportParametersValidationError As String Implements ReportViewer.Wpf.ITextResources.ReportParametersValidationError
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property StopToolTip() As String Implements ReportViewer.Wpf.ITextResources.StopToolTip
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property TotalPagesToolTip As String Implements ReportViewer.Wpf.ITextResources.TotalPagesToolTip
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property UpdatingParametersMessage As String Implements ReportViewer.Wpf.ITextResources.UpdatingParametersMessage
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property ZoomToolTip As String Implements ReportViewer.Wpf.ITextResources.ZoomToolTip
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property ZoomToPageWidth As String Implements ReportViewer.Wpf.ITextResources.ZoomToPageWidth
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property ZoomToWholePage As String Implements ReportViewer.Wpf.ITextResources.ZoomToWholePage
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property NoPageToDisplay As String Implements ReportViewer.Wpf.ITextResources.NoPageToDisplay
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property SessionExpired As String Implements ReportViewer.Wpf.ITextResources.SessionExpired
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityReportContentsArea As String Implements ITextResources.AccessibilityReportContentsArea
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityDocumentMapArea As String Implements ITextResources.AccessibilityDocumentMapArea
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityParametersArea As String Implements ITextResources.AccessibilityParametersArea
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityParameter As String Implements ITextResources.AccessibilityParameter
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityParameterText As String Implements ITextResources.AccessibilityParameterText
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityParameterBoolean As String Implements ITextResources.AccessibilityParameterBoolean
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityParameterDateTime As String Implements ITextResources.AccessibilityParameterDateTime
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityParameterNumerical As String Implements ITextResources.AccessibilityParameterNumerical
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityParameterMultiSelect As String Implements ITextResources.AccessibilityParameterMultiSelect
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityParameterMultiValue As String Implements ITextResources.AccessibilityParameterMultiValue
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityParameterErrorMessage As String Implements ITextResources.AccessibilityParameterErrorMessage
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityPageNumberEditor As String Implements ITextResources.AccessibilityPageNumberEditor
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityPageNumberSelector As String Implements ITextResources.AccessibilityPageNumberSelector
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityReportViewerToolbar As String Implements ITextResources.AccessibilityReportViewerToolbar
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityStatus As String Implements ITextResources.AccessibilityStatus
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityStatusEnabled As String Implements ITextResources.AccessibilityStatusEnabled
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityStatusDisabled As String Implements ITextResources.AccessibilityStatusDisabled
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityToolbarButtonToggleParameters As String Implements ITextResources.AccessibilityToolbarButtonToggleParameters
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityToolbarButtonToggleDocumentMap As String Implements ITextResources.AccessibilityToolbarButtonToggleDocumentMap
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityStateChecked As String Implements ITextResources.AccessibilityStateChecked
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityStateUnchecked As String Implements ITextResources.AccessibilityStateUnchecked
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property SearchCaptionLabel As String Implements ITextResources.SearchCaptionLabel
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property SearchToolTip As String Implements ITextResources.SearchToolTip
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property SearchStopToolTip As String Implements ITextResources.SearchStopToolTip
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property SearchMatchCaseToolTip As String Implements ITextResources.SearchMatchCaseToolTip
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property SearchMatchWholeWordToolTip As String Implements ITextResources.SearchMatchWholeWordToolTip
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property SearchUseRegexToolTip As String Implements ITextResources.SearchUseRegexToolTip
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property SearchNoMetadata As String Implements ITextResources.SearchNoMetadata
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property SearchNoResults As String Implements ITextResources.SearchNoResults
	            Get
	                Return "..."
	            End Get
	        End Property
	
	        Public ReadOnly Property SearchResultsFormatString As String Implements ITextResources.SearchResultsFormatString
	            Get
	                Return "..."
	            End Get
	        End Property
	    End Class
````



## Related articles

[TextResources](/reporting/api/Telerik.ReportViewer.Wpf.TextResources)

[WPF Application]({%slug telerikreporting/using-reports-in-applications/display-reports-in-applications/wpf-application/overview%})

[How to Add report viewer to a WPF .NET Framework project]({%slug telerikreporting/using-reports-in-applications/display-reports-in-applications/wpf-application/how-to-add-report-viewer-to-a-wpf-dotnet-framework-project%})

[Setting a Theme (Using Implicit Styles)]({%slug telerikreporting/using-reports-in-applications/display-reports-in-applications/wpf-application/setting-a-theme-(using-implicit-styles)%})

# See Also


 * [Hierarchical Organization of Resources for Localization](http://msdn2.microsoft.com/en-us/library/756hydy4(VS.71).aspx)

 * [WPF Globalization and Localization Overview](http://msdn.microsoft.com/en-us/library/ms788718(v=VS.85).aspx)

 * [Security and Localized Satellite Assemblies](http://msdn2.microsoft.com/en-us/library/ff8dk041(VS.71).aspx)
