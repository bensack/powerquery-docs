---
title: Common Data Service
description: Power Query Common Data Service connector reference
author: DougKlopfenstein
ms.service: powerquery
ms.topic: conceptual
ms.date: 08/06/2020
ms.author: v-douklo
LocalizationGroup: reference
---

# Common Data Service

## Summary

Release State: General Availability

Products: Power BI Desktop, Power BI Service (Enterprise Gateway), Dataflows in PowerBI.com (Enterprise Gateway), Dynamics 365 Customer Insights

Authentication types: Organizational account

## Prerequisites

You must have a Common Data Service environment with maker permissions to access the portal, and read permissions to access data within entities.

## Capabilities supported

* Server URL
* Advanced
   * Reorder columns
   * Add display column

## Finding your Common Data Service Environment URL

Open [Power Apps](https://make.powerapps.com/?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc). In the upper right of the Power Apps page, select the environment you're going to connect to. Select the ![Settings icon](media/common-data-service/settings-icon.png) settings icon, and then select **Advanced settings**.

In the new browser tab that opens, copy the root of the URL. This root URL is the unique URL for your environment. The URL will be in the format of https://\<*yourenvironmentid*>.crm.dynamics.com/. Make sure not to copy the rest of the URL. Keep this URL somewhere handy so you can use it later, for example, when you create Power BI reports.

![Common Data Service Environment](media/common-data-service/cds-env.png)

## Connect to Common Data Service from Power BI Desktop

>[!Note]
> The Power Query Common Data Service connector is mostly suited towards analytics workloads, not bulk data extraction. For more information, see [Alternative Common Data Service connections](#alternative-common-data-service-connections).

To connect to Common Data Service from Power BI Desktop:

1. Select **Get data** from the **Home** tab.

2. In the **Get Data** dialog box, select **Power Platform > Common Data Service**.

   ![Get data in Power BI Desktop](media/common-data-service/get-data.png)

2. Enter the server URL address of the data you want to load.

   ![Server URL selection](media/common-data-service/enter-url.png)

   When the table is loaded in the Navigator dialog box, by default the columns in the table are reordered in alphabetical order by the column names. If you don't want the columns reordered, in the advanced settings enter **false** in **Reorder columns**.

   Also when the table is loaded, by default if the table contains any picklist fields, a new column with the name of the picklist field with **_display** appended at the end of the name is added to the table. If you don't want the picklist field display column added, in the advanced settings enter **false** in **Add display column**.

   When you've finished filling in the information, select **OK**.

3. If this is the first time you're connecting to this site, select **Sign in** and input your credentials. Then select **Connect**.

   ![Sign in to this site](media/common-data-service/sign-in.png)

4. In **Navigator**, select the data you require, then either load or transform the data.

   ![Load or transform from navigator](media/common-data-service/navigator.png)

## Connect to Common Data Service from Power Query Online

To connect to Common Data Service from Power Query Online:

1. From the **Data sources** page, select **Common Data Service**.

   ![Get data from Power Query Online](media/common-data-service/get-data-online.png)

2. Enter the server URL address of the data you want to load.

   ![Enter the server URL](media/common-data-service/enter-url-online.png)

3. If necessary, enter an on-premises data gateway if you're going to be using on-premises data (for example, if you're going to combine data from Common Data Service and an on-premises SQL Server database).

4. Sign in to your organizational account.

5. When you've successfully signed in, select **Next**.

6. In the navigation page, select the data you require, and then select **Transform Data**.

## Limitations and issues

### Common Data Service OData API performance and throttling limits

For information about OData API performance and throttling limits for Common Data Service connections, see [Requests limits and allocations](https://docs.microsoft.com/power-platform/admin/api-request-limits-allocations). These limitations apply to both the Common Data Source connector (which uses the OData API as an implementation detail) and the [OData Feed](odatafeed.md) connector when accessing the same endpoint.

### Entity retrieval rate

As a guideline, most default entities will be retrieved at a rate of approximately 500 rows per second using the Common Data Service connector. Take this rate into account when deciding whether you want to connect to Common Data Service or export to data lake. If you require faster retrieval rates, consider using the Export to data lake feature or Tabular Data Stream (TDS) endpoint. For more information, see [Alternative Common Data Service connections](#alternative-common-data-service-connections).

### Alternative Common Data Service connections

There are several alternative ways of extracting and migrating data from Common Data Service:

* Use the OData connector to move data in and out of Common Data Service. For more information on how to migrate data between Common Data Service environments using the dataflows OData connector, see [Migrate data between Common Data Service environments using the dataflows OData connector](https://docs.microsoft.com/powerapps/developer/common-data-service/cds-odata-dataflows-migration).

* Use the **Export to data lake** feature in Power Apps to extract data from Common Data Service into Azure Data Lake Storage Gen2, which can then be used to run analytics. For more information about the export to data lake feature, see [Exporting CDS data to Azure Data Lake is Generally Available](https://powerapps.microsoft.com/blog/exporting-cds-data-to-azure-data-lake-preview/#:~:text=Exporting%20CDS%20data%20to%20Azure%20Data%20Lake%20is,BI%20reporting%2C%20ML%2C%20Data%20Warehousing%20and%20other%20).

* Use the Tabular Data Stream (TDS) Protocol endpoint to access read-only data in Common Data Service. For more information about this preview feature and a video on how it works, see [Tabular Data Stream (TDS) Protocol endpoint for Common Data Service (CDS)](https://powerapps.microsoft.com/blog/tabular-data-stream-tds-protocol-endpoint-for-common-data-service-cds/).

>[!Note]
> Both the Common Data Service connector and the OData APIs are meant to serve analytical scenarios where data volumes are relatively small. The recommended approach for bulk data extraction is “Export to Data Lake”. The TDS endpoint is a better option than the Common Data Service connector and OData endpoint, but is currently in Preview.

