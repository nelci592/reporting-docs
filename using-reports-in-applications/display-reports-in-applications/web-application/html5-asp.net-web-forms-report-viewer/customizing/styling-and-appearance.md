---
title: Styling and Appearance
page_title: Styling and Appearance | for Telerik Reporting Documentation
description: Styling and Appearance
slug: telerikreporting/using-reports-in-applications/display-reports-in-applications/web-application/html5-asp.net-web-forms-report-viewer/customizing/styling-and-appearance
tags: styling,and,appearance
published: True
position: 1
---

# Styling and Appearance



The article elaborates on the styles used by the WebForms wrapper of the HTML5 Report Viewer, and how they can be loaded manually in order to be modified.

The required stylesheets are provided automatically through a HTTPHandler via request to the Reporting REST service. If you want to customize the
        viewer styling you can stop the HTTPHandler from providing report viewer required Kendo CSS and JavaScripts by manually registering the
        Kendo JavaScript and CSS in the page head. The same approach should be used also when it is required to change the default
        theme of the viewer. Here is an example:
      

	
            <head>
            ....
              <!--kendo.all.min.js can be used as well instead of kendo.web.min.js, kendo.mobile.min.js or telerikReportViewer-kendo-->
              <script src="https://kendo.cdn.telerik.com/



The HTML5 Web Forms Report Viewer is using the default viewer template. In order to use your own viewer template you have to provide
        path to your customized one to the P:Telerik.ReportViewer.Html5.WebForms.ReportViewer.TemplateUrl

For more information on the used stylesheets and report viewer templates check out the following HTML5 Report Viewer articles:
      

# See Also
