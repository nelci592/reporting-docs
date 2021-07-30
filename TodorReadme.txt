Петър Милчев - Ajax support



Fixed:

Change _config.yml file for TOC, etc.

article names should not start with a dot '.'. Rename the article D:\Documentation migration tool-original\Help\telerikreporting\using-reports-in-applications\.net-core-support.md -> D:\Documentation migration tool-original\Help\telerikreporting\using-reports-in-applications\dotnet-core-support.md

clear '\r\n' in ALERTS

add '  \r\n' before '!['

TABLES with multiple lines in the same cell - change '\r\n' with '<br/>'.

BOLD externalLink - change XSLT schema for legacyBold 

code tag - sourceFile fixed to the local one. Need to provide correct paths to jeqyll

TOKENS for the version - make <token> tag to {{site.tokenName}} and set it value in _config.yml

For TITLES use normalize-space in XSLT

[CDATA] code handling in custom code like with CODE-with source


Change links from conceptual articles to api-ref articles like:
<codeEntityReference qualifyHint="false" autoUpgrade="true">M:Telerik.Reporting.Processing.ReportProcessor.RenderReport(System.String,Telerik.Reporting.ReportSource,System.Collections.Hashtable)</codeEntityReference>
		  
[RenderReport](/reporting/api/Telerik.Reporting.Processing.ReportProcessor.html#collapsible-Telerik_Reporting_Processing_ReportProcessor_RenderReport_System_String_Telerik_Reporting_ReportSource_System_Collections_Hashtable_)

Code and other nodes in steps - 4 spaces indent 

procedure/titles

section/titles




Remaining:

how to pass the real tokes to _config.yml


API Ref:
template:
/p:LatestBinariesPath=${LatestBinariesPath};DocsRepoName=${DocsRepoName};DocumentationBaseUrl=${DocumentationBaseUrl};DocsRepoApiAssetsFolder=${DocsRepoApiAssetsFolder}

Final - run in D:\Work
msbuild /p:LatestBinariesPath="\\telerik.com\distributions\DailyBuilds\REPORTING\2021-07-19\Reporting\R2 2021 SP1\03-48\DEV\bin";DocsRepoName=reporting-docs;DocumentationBaseUrl=https://docs.telerik.com/reporting/;DocsRepoApiAssetsFolder=_assetsApi docs-seed/_buildApi/BuildApiReference.proj

Test - run in D:\Work
msbuild /p:LatestBinariesPath="D:\Work\MdDocs\Examples\CSharp\.NET Framework\Html5IntegrationDemo\bin";DocsRepoName=reporting-docs;DocumentationBaseUrl=https://docs.telerik.com/reporting/;DocsRepoApiAssetsFolder=_assetsApi docs-seed/_buildApi/BuildApiReference.proj




Branch Development\MdDocs
Once the converter generates the mapping between SandCastle article ID and the new MD article address, the tool should update the corresponding IDs in the API Reference of our code files
OR
replace them manually - 40 in 28 files. Search by "<conceptualLink target"
Example that worked locally, from Telerik.Reporting.xml after build:
"
<member name="P:Telerik.Reporting.CheckBox.Text">
    <summary>
    Gets or sets the current text (aka label) in the check box.
    </summary>
    <value>
    A <see cref="T:System.String"/> started with "=" is interpreted as
    an expression to calculate the real data,
    otherwise - literal string. 
    
	Supports <conceptualLink target="e7d7b24c-decd-45c2-91b4-0f2b9e28271c">embedded expressions</conceptualLink> also.  -------------- OLD
	
	Supports <a href="../designing-reports/connecting-to-data/expressions/using-expressions/embedded-expressions">embedded expressions</a> also. ----------- NEW - WORKS
	
    </value>
</member>
"
Implement this change for all occurrencies above



Some article titles contain '/' that is interpreted as new subfolder and their names need to be updated manually - in the original MAML:
	D:\Work\reporting-docs\designing-reports\adding-interactivity-to-reports\actions\sorting-action\sorting-multiple-items\groups.md
	D:\Work\reporting-docs\designing-reports\adding-interactivity-to-reports\actions\how-to\how-to-add-a-drilldown\toggle-visibility-action.md
	D:\Work\reporting-docs\designing-reports\adding-interactivity-to-reports\actions\how-to\how-to-add-a-drillthrough\navigate-to-report-action.md
	D:\Work\reporting-docs\using-reports-in-applications\export-and-configure\configure-the-export-formats\wpfxaml\wpfxamlinteractive-device-information-settings.md



Merge TOC of documentation and API reference - D:\Work\reporting-docs\_assetsApi\api\index.md - change this file accordingly

