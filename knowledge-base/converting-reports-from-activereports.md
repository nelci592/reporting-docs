---
title: Converting reports from ActiveReports.
description: Transforming ActiveReports into Telerik Reports.
type: how-to
page_title: Converting reports from ActiveReports to Telerik Reports.
slug: converting-reports-from-activereports
res_type: kb
---

## Environment

<table>
	<tr>
		<td>Product</td>
		<td>Progress® Telerik® Reporting</td>
	</tr>
   	<tr>
		<td>Report Designer</td>
		<td>Visul Studio Report Designer</td>
	</tr>
</table>

   
## Description 

The Telerik converter from ActiveReports is built against ActiveReports 3 (build **5.2.1013.2**). If you're using a **newer** version of ActiveReports, you will need to add an assembly **binding redirect** statement to your Visual Studio configuration file.  
   
> Currently, the converter only works with ActiveReports 3.  

## Solution  
   
- Examine the **Global Assembly Cache** (C:\WINDOWS\assembly) to check which version of ActiveReports you have installed.

- Depending on the version you use, modify the following statements accordingly and insert them in your configuration file, usually located at:   
 
 **C:\Program Files\Microsoft Visual Studio 10.0\Common7\IDE\devenv.exe.Config** 

```xml
<configuration>    
  <runtime>    
    <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">     
      <dependentAssembly>    
        <assemblyIdentity      
name="ActiveReports3"      
publicKeyToken="cc4967777c49a3ff"      
culture="neutral" />    
        <bindingRedirect newVersion="x.x.x.x" oldVersion="x.x.x.x" />    
      </dependentAssembly>    
      <dependentAssembly>    
        <assemblyIdentity      
name="ActiveReports.Viewer3"      
publicKeyToken="cc4967777c49a3ff"      
culture="neutral" />    
        <bindingRedirect newVersion="x.x.x.x" oldVersion="x.x.x.x" />    
      </dependentAssembly>    
    </assemblyBinding>    
  </runtime>    
</configuration>    
```

where the first *x.x.x.x* is the version of **ActiveReports** that you are using and the second *x.x.x.x* is the version mentioned in the **"New Report Wizard"**.

- Restart Visual Studio.

- **Add new Telerik Report** to your project and start the Report Wizard. On its second step, select **"Convert from existing report"**.

   
> "ActiveReports" is a trademark of Data Dynamics.** 


