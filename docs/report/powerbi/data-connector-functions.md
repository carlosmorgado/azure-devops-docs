---
title: Connect using Power Query & Azure DevOps functions
titleSuffix: Azure DevOps 
description: Describes the available functions that the Power BI Data Connector and Analytics support for Azure DevOps 
ms.assetid: EC735BA2-24C9-4BA3-B35E-2CE9D2F1D7F1
ms.technology: devops-analytics
ms.topic: conceptual
ms.reviewer: stansw
ms.author: kaelli
author: KathrynEE
monikerRange: '>= azure-devops-2019'
ms.date: 8/1/2019
---

# Connect using Power Query and Azure DevOps functions 

[!INCLUDE [temp](../includes/version-azure-devops.md)]

The Data Connector for Azure DevOps includes Power Query M functions which query authors can use. These functions can handle Azure DevOps specific requirements, such as authentication for you. This article describes the arguments for the functions and how to use them to connect to Analytics. 

The VSTS.AccountContents function is a replacement for Power Query M function [Web.Contents](/powerquery-m/web-contents). Intended for more advanced scenarios, VSTS.AccountContents returns the contents downloaded from the URL for Analytics as a binary value. You can use it to call [AzureDevOps REST APIs](/rest/api/azure/devops).

> [!IMPORTANT]  
> - Use VSTS.AccountContents only to access data that isn't [available in Analytics](data-available-in-analytics.md). It pulls data directly from Azure DevOps and, to protect other Azure DevOps users, it's susceptible to throttling. For information about other approaches, see the [Power BI integration overview](overview.md). 
> - VSTS.AccountContents supports only Azure Boards data (work items). The data connector doesn't support other data types, such as pipelines. Currently, we have no plans to update the connector to support other data types.
>

## VSTS.AccountContents

Advanced function which returns the contents downloaded from the URL for Analytics as a binary value.

The `VSTS.AccountContents` function has the same arguments, options and return value format as `Web.Contents`. For more information please refer to: [Power Query (M) Formula Reference - Web.Contents](/powerquery-m/web-contents).

If you are already using `Web.Contents` to access data from Analytics (REST API or OData), you can replace it with `VSTS.AccountContents` to leverage Data Connector authentication.
This will also inform Power BI that these requests are referencing the same data source and you'll be able to combine the data without violating the single data source constraints in Power BI Service.

'VSTS.AccountContents' provides a subset of the Arguments and Options available through 'OData.Contents'. The specific limitations are outlined in the table below:

### Arguments for VSTS.Contents

<table width="100%">
    <tr>
        <th width="20%">Argument</th>
        <th width="80%">Description</th>
    </tr>
    <tr>
        <td><code>url</code></td>
        <td>URL to one of the VSTS service endpoints.</td>
    </tr>
    <tr>
        <td><code>options</code></td>
        <td>An options record to control the behavior of this function.</td>
    </tr>
</table>

### Options fields for VSTS.Contents

<table width="100%">
    <tr>
        <th width="20%">Field</th>
        <th width="80%">Description</th>
    </tr>
    <tr>
        <td><code>IsRetry</code></td>
        <td>Specifying this logical value as true will ignore any existing response in the cache when fetching data.</td>
    </tr>
    <tr>
        <td><code>ManualStatusHandling	</code></td>
        <td>Specifying this value as a list will prevent any builtin handling for HTTP requests whose response has one of these status codes.</td>
    </tr>
    <tr>
        <td><code>MaxSize</code></td>
        <td>
            Controls the max size of the table the client is interested in.
            If request exceeds this limit then server can fail the request immediately.
            Default value is zero, which tells the servers server to use its default value.
        </td>
    </tr>
    <tr>
        <td><code>Query</code></td>
        <td>Programmatically add query parameters to the URL.</td>
    </tr>
    <tr>
        <td><code>RelativePath	</code></td>
        <td>Specifying this value as text appends it to the base URL before making the request.</td>
    </tr>
    <tr>
        <td><code>Timeout</code></td>
        <td>Specifying this value as a duration will change the timeout for an HTTP request. The default value is 600 seconds.</td>
    </tr>
    <tr>
        <td><code>Version</code></td>
        <td>Version of the data model. This option is primary for diagnostics.</td>
    </tr>
</table>

## Related articles

* [Power Query (M) Formula Reference](/previous-versions/mt270235(v=msdn.10))
* [Power Query (M) Formula Reference - Accessing data functions](/powerquery-m/accessing-data-functions)
