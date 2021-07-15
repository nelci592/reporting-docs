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
      

	



	



# See Also

 * [Overview]({%slug telerikreporting/designing-reports/adding-interactivity-to-reports/actions/overview%})

 * [Interactive Action Events]({%slug telerikreporting/designing-reports/adding-interactivity-to-reports/actions/interactive-action-events%})

 * [How to Add a Custom Action]({%slug telerikreporting/designing-reports/adding-interactivity-to-reports/actions/how-to/how-to-add-a-custom-action%})
