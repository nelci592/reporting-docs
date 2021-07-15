---
title: Implement Send Mail Message
page_title: Implement Send Mail Message | for Telerik Reporting Documentation
description: Implement Send Mail Message
slug: telerikreporting/using-reports-in-applications/host-the-report-engine-remotely/telerik-reporting-rest-services/implement-send-mail-message
tags: implement,send,mail,message
published: True
position: 7
---

# Implement Send Mail Message



This tutorial elaborates how to implement the SendMailMessage method of the [ReportsController]({%slug telerikreporting/using-reports-in-applications/host-the-report-engine-remotely/telerik-reporting-rest-services/asp.net-web-api-implementation/how-to-implement-the-reportscontroller-in-an-application%}).
        This is required to enable the send document endpoint used for [HTML5 Report Viewer Send Mail Message]({%slug telerikreporting/using-reports-in-applications/display-reports-in-applications/web-application/send-mail-message%}) functionality.
      To send e-mail use the MailMessage with SMTP client as shown in the following code snippet:

{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````C#
	        protected override HttpStatusCode SendMailMessage(MailMessage mailMessage)
	        {
	            using (var smtpClient = new SmtpClient("smtp.companyname.com", 25))
	            {
	                smtpClient.DeliveryMethod = SmtpDeliveryMethod.Network;
	                smtpClient.EnableSsl = true;
	                smtpClient.Send(mailMessage);
	            }
	
	            return HttpStatusCode.OK;
	        }
````



{{source=System.Xml.XmlAttribute region=System.Xml.XmlAttribute}}````VB
	    Protected Overrides Function SendMailMessage(ByVal mailMessage As MailMessage) As HttpStatusCode
	        Using smtpClient = New SmtpClient("smtp.companyname.com", 25)
	            smtpClient.DeliveryMethod = SmtpDeliveryMethod.Network
	            smtpClient.EnableSsl = True
	            smtpClient.Send(mailMessage)
	        End Using
	
	        Return HttpStatusCode.OK
	    End Function
	    '#End Region
	End Class
	'#End Region
	
	'#Region "ReportsControllerOnGetDocument"
	Public Class ReportController
	    Inherits Telerik.Reporting.Services.WebApi.ReportsControllerBase
	    Protected Overrides Sub OnGetDocument(args As GetDocumentEventArgs)
	        'modify the rendered document in args.DocumentBytes 
	        If args.Extension = "PDF" Then
	        End If
	    End Sub
	End Class
	'#End Region
	
	'#Region "ReportsHostOnGetDocument"
	Public Class ReportHost
	    Inherits Telerik.Reporting.Services.ServiceStack.ReportsHostBase
	    Protected Overrides Sub OnGetDocument(args As GetDocumentEventArgs)
	        'modify the rendered document in args.DocumentBytes 
	        If args.Extension = "PDF" Then
	        End If
	    End Sub
	End Class
	'#End Region
	
	'#Region "ReportsHostOnCreateDocument"
	Public Class ReportHost2
	    Inherits Telerik.Reporting.Services.ServiceStack.ReportsHostBase
	    Protected Overrides Sub OnCreateDocument(args As CreateDocumentEventArgs)
	        If args.Extension = "PDF" Then
	            args.DeviceInfo.Add("OwnerPassword", "password1")
	            args.DeviceInfo.Add("UserPassword", "password2")
	        End If
	    End Sub
	End Class
	'#End Region



 * [Send Mail Message]({%slug telerikreporting/using-reports-in-applications/display-reports-in-applications/web-application/send-mail-message%})
