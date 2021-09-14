---
title: How to Add report viewer to a WPF .NET Core project
page_title: How to Add report viewer to a WPF .NET Core project | for Telerik Reporting Documentation
description: How to Add report viewer to a WPF .NET Core project
slug: telerikreporting/using-reports-in-applications/display-reports-in-applications/wpf-application/how-to-add-report-viewer-to-a-wpf-dotnet-core-project
tags: how,to,add,report,viewer,to,a,wpf,.net,core,project
published: True
position: 2
---

# How to Add report viewer to a WPF .NET Core project



This article explains the steps needed to integrate the WPF report viewer to a .NET Core project.       

## Prerequisites:

* Visual Studio 2019 or newer

* .NET Core SDK 3 Preview 4 or newer

* WPF App (.NET Core) project

## 

###Steps to add report viewer to a WPF .NET Core project

1. Add the following assembly references (available in Telerik Reporting installation Bin directory)                   or NuGet package references (available in [Telerik private NuGet repository]({%slug telerikreporting/using-reports-in-applications/how-to-add-the-telerik-private-nuget-feed-to-visual-studio%})):                 
   + Telerik.Reporting (located in Bin\netstandard2.0)

   + Telerik.ReportViewer.Wpf (located in Bin\netcoreapp3.1)

   + Telerik.ReportViewer.Wpf.Themes (located in Bin\netcoreapp3.1)

   + Telerik.Windows.Controls (located in Bin\WpfViewerDependencies\Core)

   + Telerik.Windows.Controls.Input (located in Bin\WpfViewerDependencies\Core)

   + Telerik.Windows.Controls.Navigation (located in Bin\WpfViewerDependencies\Core)

   + Telerik.Windows.Data (located in Bin\WpfViewerDependencies\Core)
    In case Telerik UI for WPF is used only for the report viewer, reference the                   Telerik UI for WPF assemblies available with Telerik Reporting.                   They are internally unlocked for the WPF Report Viewer but can only be used                   with the report viewer. The Telerik UI for WPF assemblies are located in                   %programfiles(x86)%\Progress\Telerik Reporting {{site.suiteversion}}\Examples\CSharp\WpfDemo\bin).                     The WPF ReportViewer is build with the latest official release of Telerik UI for WPF.                   In this way we provide trouble free upgrade for most of the users.                   This means that you can use the latest version of Telerik UI for WPF in your project                   and report viewer.                     It is possible that the Telerik UI for WPF assemblies have a greater version                   (service pack or internal build) than the one with which the WPF report viewer                   control targets. In this case assembly binding                   redirects are required (see [Binding Redirects](e34dad8d-92f7-491e-903d-53cc2654d61c#BindingRedirects) topic below).                 

1. Merge the required theme resources to the application in the App.xaml:                 

{{source=CodeSnippets\CS\API\Telerik\ReportViewer\Wpf\App.xaml}}
````XML
	<Application x:Class="WpfApplication1.App"
	         xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
	         xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
	         StartupUri="MainWindow.xaml">
	    <Application.Resources>
	        <ResourceDictionary>
	            <ResourceDictionary.MergedDictionaries>
	                <ResourceDictionary Source="/Telerik.ReportViewer.Wpf.Themes;component/Themes/Fluent/System.Windows.xaml" />
	                <ResourceDictionary Source="/Telerik.ReportViewer.Wpf.Themes;component/Themes/Fluent/Telerik.Windows.Controls.xaml" />
	                <ResourceDictionary Source="/Telerik.ReportViewer.Wpf.Themes;component/Themes/Fluent/Telerik.Windows.Controls.Input.xaml" />
	                <ResourceDictionary Source="/Telerik.ReportViewer.Wpf.Themes;component/Themes/Fluent/Telerik.Windows.Controls.Navigation.xaml" />
	                <ResourceDictionary Source="/Telerik.ReportViewer.Wpf.Themes;component/Themes/Fluent/Telerik.ReportViewer.Wpf.xaml" />
	            </ResourceDictionary.MergedDictionaries>
	        </ResourceDictionary>
	    </Application.Resources>
	</Application>
````



1. Add the following namespaces to the target Window declaration:                 

	
    ````XML
              xmlns:tr="http://schemas.telerik.com/wpf"
              xmlns:telerikControls="clr-namespace:Telerik.Windows.Controls;assembly=Telerik.Windows.Controls"
              xmlns:telerikReporting="clr-namespace:Telerik.Reporting;assembly=Telerik.Reporting"
````



1. Add the WPF Report Viewer declaration to the target Window and set the proper UriReportSource.Uri relative path:                 

	
    ````XML
        <tr:ReportViewer Grid.Row="1" x:Name="ReportViewer1" HorizontalAlignment="Stretch"> 
            <tr:ReportViewer.ReportSource> 
                <telerikReporting:UriReportSource Uri="..\..\..\..\..\..\Report Designer\Examples\Report Catalog.trdp" /> 
            </tr:ReportViewer.ReportSource> 
        </tr:ReportViewer>
````



# See Also


 * [.NET Core Support]({%slug telerikreporting/using-reports-in-applications/dotnet-core-support%})

 * [Report Viewer Localization]({%slug telerikreporting/using-reports-in-applications/display-reports-in-applications/wpf-application/report-viewer-localization%})
