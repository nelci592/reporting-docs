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





Remaining:

how to pass the real tokes to _config.yml


API Ref:
template:
/p:LatestBinariesPath=${LatestBinariesPath};DocsRepoName=${DocsRepoName};DocumentationBaseUrl=${DocumentationBaseUrl};DocsRepoApiAssetsFolder=${DocsRepoApiAssetsFolder}

Final - run in D:\Work
msbuild /p:LatestBinariesPath="\\telerik.com\distributions\DailyBuilds\REPORTING\2021-07-19\Reporting\R2 2021 SP1\03-48\DEV\bin";DocsRepoName=reporting-docs;DocumentationBaseUrl=https://docs.telerik.com/reporting/;DocsRepoApiAssetsFolder=_assetsApi docs-seed/_buildApi/BuildApiReference.proj

Петър Милчев - Ajax support


Once the converter generates the mapping between SandCastle article ID and the new MD article address, the tool should update the corresponding IDs in the API Reference of our code files
OR
replace them manually - 40 in 28 files. Search by "<conceptualLink target"

Merge TOC of documentation and API reference