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


Remaining:

how to pass the real tokes to _config.yml