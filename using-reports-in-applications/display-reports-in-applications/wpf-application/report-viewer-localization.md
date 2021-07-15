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



In the WPF Report Viewer, localized resources are stored in separate __RESX__ resource files and loaded according to the current UI culture settings. To understand how localized resources are loaded, it is useful to think of them as being organized in a hierarchical manner.
      

## Types of Resources in the Hierarchy

* 
            At the top of the hierarchy sit the fallback resources for the default UI culture, which is English ("en") by default. These are the only resources that do not have their own file. They are stored directly in the assembly of the __*Report Viewer*__.
          

* Below the fallback resources are the resources for any neutral cultures. A neutral culture is associated with a language but not a region. For example, French ("fr") is a neutral culture. Note that the fallback resources are also for a neutral culture, but a special one.

* Below those are the resources for any specific cultures. A specific culture is associated with a language and a region. For example, French Canadian ("fr-CA") is a specific culture.

When the __*Report Viewer*__ tries to load any localized resource and does not find it it will travel up the hierarchy until it finds a resource file containing the requested resource.
        

The best way to store your resources is to generalize them as much as possible. That means to store localized strings in resource files for neutral cultures rather than specific cultures whenever possible. For instance, if you have resources for the French Belgian ("fr-BE") culture and the resources immediately above are the fallback resources in English, a problem may result when someone uses your application on a system configured for the French Canadian culture. The __*Report Viewer*__ will look for a __RESX__ file named "fr-CA", it will not find it and will load the fallback resource, which is English, instead of loading the French resources. The following picture shows this undesirable scenario.
        

  
  ![](images/localization1.png)

If you follow the recommended practice of placing as many resources as possible in a neutral resource file for the "fr" culture, the French Canadian user would not see resources marked for the "fr-BE" culture, but he or she would still see strings in French. The following situation demonstrates this preferred scenario.

  
  ![](images/localization2.png)

## Naming Conventions for the Localization Resources

__The Report Viewer__ uses the following naming convention when searching for localized __RESX__ resource files in the main application folder:
        

* The names of the __RESX__ localization resource files should have the following format:
            *

Telerik.ReportViewer.WPF.TextResources.__[culture]__.resx
              *Here “__[culture]__” is the name of the culture for the specified localization resource. For example, to provide a localization resource
              for the French Belgian culture, the corresponding resource file should be named as follows:
            *

Telerik.ReportViewer.WPF.TextResources.__fr-BE__.resx
              *

* Respectively, to provide a localization resource for the French neutral culture, the corresponding resource file should
              be named as follows:
            *

Telerik.ReportViewer.WPF.TextResources.__fr__.resx
              *

* It is possible to override the default resources for the language neutral culture, which are stored in the assembly of the
              __*Report Viewer*__. In that case the resource file should be named as follows:
            *

Telerik.ReportViewer.WPF.TextResources.resx*

As described above, if for example the current UI culture is set to French Belgian, the __*Report Viewer*__ will search for localized __RESX__ resource files inside the main application folder in the following order:
        

1. 
            Telerik.ReportViewer.WPF.TextResources.__fr-BE__.resx
          

1. 
            Telerik.ReportViewer.WPF.TextResources.__fr__.resx
          

1. Telerik.ReportViewer.WPF.TextResources.resx

  
  ![](images/localization3.png)

The above diagram illustrates a simple view of the resource fallback for a UI culture set to "fr-BE". The __*Report Viewer*__ handles the case probing the "fr-BE" __RESX__ resource file for the requested key first, and subsequently falls back to the neutral French culture "fr", ultimately looking in the default assembly resources for a value if a value has still not been found.
        

## Adding Localization Resources for the Report Viewer

1. 
            Add a new __RESX__ resource file to the main project of the application. Name the newly-created __RESX__ file according to the naming convention described above.
          

1. 
            In the __*Property Inspector*__ specify the following properties for the resource file:
            

1. __*Build Action:*__ "*None*"
              

1. __*Copy to Output Directory:*__ "*Copy if newer*" or "*Copy always*"
              

1. 
            Open the __RESX__ resource file in the __*Visual Studio Resource Editor*__. Enter the required
            resource strings (T:Telerik.ReportViewer.Wpf.TextResources)
            to translate the __*Report Viewer*__ to the desired language.
          

1. 
            Repeat steps from 1 to 3 for each desired translation of the __*Report Viewer*__.
          

1. 
            Compile and run the project. When viewing a __*Telerik Report*__, the __*Report Viewer*__ should be translated according to the current UI culture.
          

## Distributing an Application with a Localized Report Viewer

In order to distribute an application that uses __*Telerik Reporting*__
          with a localized __*Report Viewer*__, one should distribute all of the required
          localization __RESX__ resource files, in addition to the main application assemblies.
          For __*WPF Applications*__ the __RESX__
          files should be placed in the same directory, where the application is installed.
        

## Localization Using the ITextResources interface

The other way to localize the WPF __*Report Viewer*__ in a more flexible manner is to create a class that implements the
          ITextResources interface and to implement all its properties, which represent all tooltips and messages in the Report Viewer. After you implement ITextResources you have to pass an instance of your custom class to the TextResources property ot the report viewer. The logic is pretty
          simple, the property just has to return the correct translation for each resource key, as it is shown below:
        

	{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````
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
````



	{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````
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
	        '#End Region
	
	        Public ReadOnly Property CancelButtonText As String Implements ReportViewer.Wpf.ITextResources.CancelButtonText
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property LabelOf As String Implements ReportViewer.Wpf.ITextResources.LabelOf
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property ReportParametersNullText As String Implements ReportViewer.Wpf.ITextResources.ReportParametersNullText
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property PreviewButtonText As String Implements ReportViewer.Wpf.ITextResources.PreviewButtonText
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property DocumentMapToolTip As String Implements ReportViewer.Wpf.ITextResources.DocumentMapToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property ExportError As String Implements ReportViewer.Wpf.ITextResources.ExportError
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property ExportingMessage As String Implements ReportViewer.Wpf.ITextResources.ExportingMessage
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property ExportToolTip As String Implements ReportViewer.Wpf.ITextResources.ExportToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property FirstPageToolTip As String Implements ReportViewer.Wpf.ITextResources.FirstPageToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property ForwardToolTip As String Implements ReportViewer.Wpf.ITextResources.ForwardToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property LastPageToolTip As String Implements ReportViewer.Wpf.ITextResources.LastPageToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property LoadingPageMessage As String Implements ReportViewer.Wpf.ITextResources.LoadingPageMessage
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property NextPageToolTip As String Implements ReportViewer.Wpf.ITextResources.NextPageToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property NoReportError As String Implements ReportViewer.Wpf.ITextResources.NoReportError
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property PageNumberGreaterThanRangeError As String Implements ReportViewer.Wpf.ITextResources.PageNumberGreaterThanRangeError
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property PageNumberLessThanRangeError As String Implements ReportViewer.Wpf.ITextResources.PageNumberLessThanRangeError
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property PageSetupToolTip() As String Implements ReportViewer.Wpf.ITextResources.PageSetupToolTip
	            Get
	                Return "Página de configuración"
	            End Get
	        End Property
	
	        Public ReadOnly Property ParametersToolTip As String Implements ReportViewer.Wpf.ITextResources.ParametersToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property PreviousPageToolTip As String Implements ReportViewer.Wpf.ITextResources.PreviousPageToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property PrintPreviewToolTip As String Implements ReportViewer.Wpf.ITextResources.PrintPreviewToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property PrintToolTip As String Implements ReportViewer.Wpf.ITextResources.PrintToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property ProcessingReportMessage As String Implements ReportViewer.Wpf.ITextResources.ProcessingReportMessage
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property RefreshToolTip As String Implements ReportViewer.Wpf.ITextResources.RefreshToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property ReportParametersAreaValidationError As String Implements ReportViewer.Wpf.ITextResources.ReportParametersAreaValidationError
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property ReportParametersSelectAllText As String Implements ReportViewer.Wpf.ITextResources.ReportParametersSelectAllText
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property InvalidValueForParameter As String Implements ReportViewer.Wpf.ITextResources.InvalidValueForParameter
	            Get
	                Return "Valor no válido para el parámetro"
	            End Get
	        End Property
	
	        Public ReadOnly Property ReportParametersValidationError As String Implements ReportViewer.Wpf.ITextResources.ReportParametersValidationError
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property StopToolTip() As String Implements ReportViewer.Wpf.ITextResources.StopToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property TotalPagesToolTip As String Implements ReportViewer.Wpf.ITextResources.TotalPagesToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property UpdatingParametersMessage As String Implements ReportViewer.Wpf.ITextResources.UpdatingParametersMessage
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property ZoomToolTip As String Implements ReportViewer.Wpf.ITextResources.ZoomToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property ZoomToPageWidth As String Implements ReportViewer.Wpf.ITextResources.ZoomToPageWidth
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property ZoomToWholePage As String Implements ReportViewer.Wpf.ITextResources.ZoomToWholePage
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property NoPageToDisplay As String Implements ReportViewer.Wpf.ITextResources.NoPageToDisplay
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property SessionExpired As String Implements ReportViewer.Wpf.ITextResources.SessionExpired
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityReportContentsArea As String Implements ITextResources.AccessibilityReportContentsArea
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityDocumentMapArea As String Implements ITextResources.AccessibilityDocumentMapArea
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityParametersArea As String Implements ITextResources.AccessibilityParametersArea
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityParameter As String Implements ITextResources.AccessibilityParameter
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityParameterText As String Implements ITextResources.AccessibilityParameterText
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityParameterBoolean As String Implements ITextResources.AccessibilityParameterBoolean
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityParameterDateTime As String Implements ITextResources.AccessibilityParameterDateTime
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityParameterNumerical As String Implements ITextResources.AccessibilityParameterNumerical
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityParameterMultiSelect As String Implements ITextResources.AccessibilityParameterMultiSelect
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityParameterMultiValue As String Implements ITextResources.AccessibilityParameterMultiValue
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityParameterErrorMessage As String Implements ITextResources.AccessibilityParameterErrorMessage
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityPageNumberEditor As String Implements ITextResources.AccessibilityPageNumberEditor
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityPageNumberSelector As String Implements ITextResources.AccessibilityPageNumberSelector
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityReportViewerToolbar As String Implements ITextResources.AccessibilityReportViewerToolbar
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityStatus As String Implements ITextResources.AccessibilityStatus
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityStatusEnabled As String Implements ITextResources.AccessibilityStatusEnabled
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityStatusDisabled As String Implements ITextResources.AccessibilityStatusDisabled
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityToolbarButtonToggleParameters As String Implements ITextResources.AccessibilityToolbarButtonToggleParameters
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityToolbarButtonToggleDocumentMap As String Implements ITextResources.AccessibilityToolbarButtonToggleDocumentMap
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityStateChecked As String Implements ITextResources.AccessibilityStateChecked
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityStateUnchecked As String Implements ITextResources.AccessibilityStateUnchecked
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property SearchCaptionLabel As String Implements ITextResources.SearchCaptionLabel
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property SearchToolTip As String Implements ITextResources.SearchToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property SearchStopToolTip As String Implements ITextResources.SearchStopToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property SearchMatchCaseToolTip As String Implements ITextResources.SearchMatchCaseToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property SearchMatchWholeWordToolTip As String Implements ITextResources.SearchMatchWholeWordToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property SearchUseRegexToolTip As String Implements ITextResources.SearchUseRegexToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property SearchNoMetadata As String Implements ITextResources.SearchNoMetadata
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property SearchNoResults As String Implements ITextResources.SearchNoResults
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property SearchResultsFormatString As String Implements ITextResources.SearchResultsFormatString
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	        '#Region "InterfaceLocalizationSnippetEnd"
	    End Class
	    '#End Region
	
	
	    '#Region "InterfaceLocalizationUsingMethodsSnippetStart"
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
	        '#End Region
	
	        Public ReadOnly Property CancelButtonText As String Implements ReportViewer.Wpf.ITextResources.CancelButtonText
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property LabelOf As String Implements ReportViewer.Wpf.ITextResources.LabelOf
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property ReportParametersNullText As String Implements ReportViewer.Wpf.ITextResources.ReportParametersNullText
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property PreviewButtonText As String Implements ReportViewer.Wpf.ITextResources.PreviewButtonText
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property DocumentMapToolTip As String Implements ReportViewer.Wpf.ITextResources.DocumentMapToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property ExportError As String Implements ReportViewer.Wpf.ITextResources.ExportError
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property ExportingMessage As String Implements ReportViewer.Wpf.ITextResources.ExportingMessage
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property ExportToolTip As String Implements ReportViewer.Wpf.ITextResources.ExportToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property FirstPageToolTip As String Implements ReportViewer.Wpf.ITextResources.FirstPageToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property ForwardToolTip As String Implements ReportViewer.Wpf.ITextResources.ForwardToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property LastPageToolTip As String Implements ReportViewer.Wpf.ITextResources.LastPageToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property LoadingPageMessage As String Implements ReportViewer.Wpf.ITextResources.LoadingPageMessage
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property NextPageToolTip As String Implements ReportViewer.Wpf.ITextResources.NextPageToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property NoReportError As String Implements ReportViewer.Wpf.ITextResources.NoReportError
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property PageNumberGreaterThanRangeError As String Implements ReportViewer.Wpf.ITextResources.PageNumberGreaterThanRangeError
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property PageNumberLessThanRangeError As String Implements ReportViewer.Wpf.ITextResources.PageNumberLessThanRangeError
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property PageSetupToolTip() As String Implements ReportViewer.Wpf.ITextResources.PageSetupToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property ParametersToolTip As String Implements ReportViewer.Wpf.ITextResources.ParametersToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property PreviousPageToolTip As String Implements ReportViewer.Wpf.ITextResources.PreviousPageToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property PrintPreviewToolTip As String Implements ReportViewer.Wpf.ITextResources.PrintPreviewToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property PrintToolTip As String Implements ReportViewer.Wpf.ITextResources.PrintToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property ProcessingReportMessage As String Implements ReportViewer.Wpf.ITextResources.ProcessingReportMessage
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property RefreshToolTip As String Implements ReportViewer.Wpf.ITextResources.RefreshToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property ReportParametersAreaValidationError As String Implements ReportViewer.Wpf.ITextResources.ReportParametersAreaValidationError
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property ReportParametersSelectAllText As String Implements ReportViewer.Wpf.ITextResources.ReportParametersSelectAllText
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property InvalidValueForParameter As String Implements ReportViewer.Wpf.ITextResources.InvalidValueForParameter
	            Get
	                Return "Valor no válido para el parámetro"
	            End Get
	        End Property
	
	        Public ReadOnly Property ReportParametersValidationError As String Implements ReportViewer.Wpf.ITextResources.ReportParametersValidationError
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property StopToolTip() As String Implements ReportViewer.Wpf.ITextResources.StopToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property TotalPagesToolTip As String Implements ReportViewer.Wpf.ITextResources.TotalPagesToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property UpdatingParametersMessage As String Implements ReportViewer.Wpf.ITextResources.UpdatingParametersMessage
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property ZoomToolTip As String Implements ReportViewer.Wpf.ITextResources.ZoomToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property ZoomToPageWidth As String Implements ReportViewer.Wpf.ITextResources.ZoomToPageWidth
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property ZoomToWholePage As String Implements ReportViewer.Wpf.ITextResources.ZoomToWholePage
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property NoPageToDisplay As String Implements ReportViewer.Wpf.ITextResources.NoPageToDisplay
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property SessionExpired As String Implements ReportViewer.Wpf.ITextResources.SessionExpired
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityReportContentsArea As String Implements ITextResources.AccessibilityReportContentsArea
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityDocumentMapArea As String Implements ITextResources.AccessibilityDocumentMapArea
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityParametersArea As String Implements ITextResources.AccessibilityParametersArea
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityParameter As String Implements ITextResources.AccessibilityParameter
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityParameterText As String Implements ITextResources.AccessibilityParameterText
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityParameterBoolean As String Implements ITextResources.AccessibilityParameterBoolean
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityParameterDateTime As String Implements ITextResources.AccessibilityParameterDateTime
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityParameterNumerical As String Implements ITextResources.AccessibilityParameterNumerical
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityParameterMultiSelect As String Implements ITextResources.AccessibilityParameterMultiSelect
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityParameterMultiValue As String Implements ITextResources.AccessibilityParameterMultiValue
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityParameterErrorMessage As String Implements ITextResources.AccessibilityParameterErrorMessage
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityPageNumberEditor As String Implements ITextResources.AccessibilityPageNumberEditor
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityPageNumberSelector As String Implements ITextResources.AccessibilityPageNumberSelector
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityReportViewerToolbar As String Implements ITextResources.AccessibilityReportViewerToolbar
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityStatus As String Implements ITextResources.AccessibilityStatus
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityStatusEnabled As String Implements ITextResources.AccessibilityStatusEnabled
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityStatusDisabled As String Implements ITextResources.AccessibilityStatusDisabled
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityToolbarButtonToggleParameters As String Implements ITextResources.AccessibilityToolbarButtonToggleParameters
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityToolbarButtonToggleDocumentMap As String Implements ITextResources.AccessibilityToolbarButtonToggleDocumentMap
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityStateChecked As String Implements ITextResources.AccessibilityStateChecked
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityStateUnchecked As String Implements ITextResources.AccessibilityStateUnchecked
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property SearchCaptionLabel As String Implements ITextResources.SearchCaptionLabel
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property SearchToolTip As String Implements ITextResources.SearchToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property SearchStopToolTip As String Implements ITextResources.SearchStopToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property SearchMatchCaseToolTip As String Implements ITextResources.SearchMatchCaseToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property SearchMatchWholeWordToolTip As String Implements ITextResources.SearchMatchWholeWordToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property SearchUseRegexToolTip As String Implements ITextResources.SearchUseRegexToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property SearchNoMetadata As String Implements ITextResources.SearchNoMetadata
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property SearchNoResults As String Implements ITextResources.SearchNoResults
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property SearchResultsFormatString As String Implements ITextResources.SearchResultsFormatString
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	        '#Region "InterfaceLocalizationUsingMethodsSnippetEnd"
	    End Class
	    '#End Region
	
	    <TestMethod()>
	    Public Sub TestMethod1()
	    End Sub
	
	End Class



Instead of a hard-coded string the property can be set in a method/contructor or to be created a method that returns string and implements a cutsom logic,
          for example retreives the resource key from a database.
        

	{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````
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
````



	{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````
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
	        '#End Region
	
	        Public ReadOnly Property CancelButtonText As String Implements ReportViewer.Wpf.ITextResources.CancelButtonText
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property LabelOf As String Implements ReportViewer.Wpf.ITextResources.LabelOf
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property ReportParametersNullText As String Implements ReportViewer.Wpf.ITextResources.ReportParametersNullText
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property PreviewButtonText As String Implements ReportViewer.Wpf.ITextResources.PreviewButtonText
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property DocumentMapToolTip As String Implements ReportViewer.Wpf.ITextResources.DocumentMapToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property ExportError As String Implements ReportViewer.Wpf.ITextResources.ExportError
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property ExportingMessage As String Implements ReportViewer.Wpf.ITextResources.ExportingMessage
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property ExportToolTip As String Implements ReportViewer.Wpf.ITextResources.ExportToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property FirstPageToolTip As String Implements ReportViewer.Wpf.ITextResources.FirstPageToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property ForwardToolTip As String Implements ReportViewer.Wpf.ITextResources.ForwardToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property LastPageToolTip As String Implements ReportViewer.Wpf.ITextResources.LastPageToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property LoadingPageMessage As String Implements ReportViewer.Wpf.ITextResources.LoadingPageMessage
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property NextPageToolTip As String Implements ReportViewer.Wpf.ITextResources.NextPageToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property NoReportError As String Implements ReportViewer.Wpf.ITextResources.NoReportError
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property PageNumberGreaterThanRangeError As String Implements ReportViewer.Wpf.ITextResources.PageNumberGreaterThanRangeError
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property PageNumberLessThanRangeError As String Implements ReportViewer.Wpf.ITextResources.PageNumberLessThanRangeError
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property PageSetupToolTip() As String Implements ReportViewer.Wpf.ITextResources.PageSetupToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property ParametersToolTip As String Implements ReportViewer.Wpf.ITextResources.ParametersToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property PreviousPageToolTip As String Implements ReportViewer.Wpf.ITextResources.PreviousPageToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property PrintPreviewToolTip As String Implements ReportViewer.Wpf.ITextResources.PrintPreviewToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property PrintToolTip As String Implements ReportViewer.Wpf.ITextResources.PrintToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property ProcessingReportMessage As String Implements ReportViewer.Wpf.ITextResources.ProcessingReportMessage
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property RefreshToolTip As String Implements ReportViewer.Wpf.ITextResources.RefreshToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property ReportParametersAreaValidationError As String Implements ReportViewer.Wpf.ITextResources.ReportParametersAreaValidationError
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property ReportParametersSelectAllText As String Implements ReportViewer.Wpf.ITextResources.ReportParametersSelectAllText
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property InvalidValueForParameter As String Implements ReportViewer.Wpf.ITextResources.InvalidValueForParameter
	            Get
	                Return "Valor no válido para el parámetro"
	            End Get
	        End Property
	
	        Public ReadOnly Property ReportParametersValidationError As String Implements ReportViewer.Wpf.ITextResources.ReportParametersValidationError
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property StopToolTip() As String Implements ReportViewer.Wpf.ITextResources.StopToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property TotalPagesToolTip As String Implements ReportViewer.Wpf.ITextResources.TotalPagesToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property UpdatingParametersMessage As String Implements ReportViewer.Wpf.ITextResources.UpdatingParametersMessage
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property ZoomToolTip As String Implements ReportViewer.Wpf.ITextResources.ZoomToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property ZoomToPageWidth As String Implements ReportViewer.Wpf.ITextResources.ZoomToPageWidth
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property ZoomToWholePage As String Implements ReportViewer.Wpf.ITextResources.ZoomToWholePage
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property NoPageToDisplay As String Implements ReportViewer.Wpf.ITextResources.NoPageToDisplay
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property SessionExpired As String Implements ReportViewer.Wpf.ITextResources.SessionExpired
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityReportContentsArea As String Implements ITextResources.AccessibilityReportContentsArea
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityDocumentMapArea As String Implements ITextResources.AccessibilityDocumentMapArea
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityParametersArea As String Implements ITextResources.AccessibilityParametersArea
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityParameter As String Implements ITextResources.AccessibilityParameter
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityParameterText As String Implements ITextResources.AccessibilityParameterText
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityParameterBoolean As String Implements ITextResources.AccessibilityParameterBoolean
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityParameterDateTime As String Implements ITextResources.AccessibilityParameterDateTime
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityParameterNumerical As String Implements ITextResources.AccessibilityParameterNumerical
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityParameterMultiSelect As String Implements ITextResources.AccessibilityParameterMultiSelect
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityParameterMultiValue As String Implements ITextResources.AccessibilityParameterMultiValue
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityParameterErrorMessage As String Implements ITextResources.AccessibilityParameterErrorMessage
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityPageNumberEditor As String Implements ITextResources.AccessibilityPageNumberEditor
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityPageNumberSelector As String Implements ITextResources.AccessibilityPageNumberSelector
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityReportViewerToolbar As String Implements ITextResources.AccessibilityReportViewerToolbar
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityStatus As String Implements ITextResources.AccessibilityStatus
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityStatusEnabled As String Implements ITextResources.AccessibilityStatusEnabled
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityStatusDisabled As String Implements ITextResources.AccessibilityStatusDisabled
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityToolbarButtonToggleParameters As String Implements ITextResources.AccessibilityToolbarButtonToggleParameters
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityToolbarButtonToggleDocumentMap As String Implements ITextResources.AccessibilityToolbarButtonToggleDocumentMap
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityStateChecked As String Implements ITextResources.AccessibilityStateChecked
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property AccessibilityStateUnchecked As String Implements ITextResources.AccessibilityStateUnchecked
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property SearchCaptionLabel As String Implements ITextResources.SearchCaptionLabel
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property SearchToolTip As String Implements ITextResources.SearchToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property SearchStopToolTip As String Implements ITextResources.SearchStopToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property SearchMatchCaseToolTip As String Implements ITextResources.SearchMatchCaseToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property SearchMatchWholeWordToolTip As String Implements ITextResources.SearchMatchWholeWordToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property SearchUseRegexToolTip As String Implements ITextResources.SearchUseRegexToolTip
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property SearchNoMetadata As String Implements ITextResources.SearchNoMetadata
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property SearchNoResults As String Implements ITextResources.SearchNoResults
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	
	        Public ReadOnly Property SearchResultsFormatString As String Implements ITextResources.SearchResultsFormatString
	            Get
	                Return "Página corriente"
	            End Get
	        End Property
	        '#Region "InterfaceLocalizationUsingMethodsSnippetEnd"
	    End Class
	    '#End Region
	
	    <TestMethod()>
	    Public Sub TestMethod1()
	    End Sub
	
	End Class



## Related articles

T:Telerik.ReportViewer.Wpf.TextResources

[WPF Application]({%slug telerikreporting/using-reports-in-applications/display-reports-in-applications/wpf-application/overview%})

[How to Add report viewer to a WPF .NET Framework project]({%slug telerikreporting/using-reports-in-applications/display-reports-in-applications/wpf-application/how-to-add-report-viewer-to-a-wpf-.net-framework-project%})

[Setting a Theme (Using Implicit Styles)]({%slug telerikreporting/using-reports-in-applications/display-reports-in-applications/wpf-application/setting-a-theme-(using-implicit-styles)%})

# See Also

 * [Hierarchical Organization of Resources for Localization](http://msdn2.microsoft.com/en-us/library/756hydy4(VS.71).aspx)

 * [WPF Globalization and Localization Overview](http://msdn.microsoft.com/en-us/library/ms788718(v=VS.85).aspx)

 * [Security and Localized Satellite Assemblies](http://msdn2.microsoft.com/en-us/library/ff8dk041(VS.71).aspx)
