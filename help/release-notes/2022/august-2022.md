---
title: Adobe Experience Platform Release Notes August 2022
description: The August 2022 release notes for Adobe Experience Platform.
---
# Adobe Experience Platform release notes 

**Release date: August 24, 2022**

Updates to existing features in Adobe Experience Platform:


- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai-and-ml-services)
- [[!DNL Dashboards]](#dashboards)
- [Data Prep](#data-prep)
- [Experience Data Model (XDM)](#xdm)
- [Real-time Customer Profile](#profile)
- [Segmentation Service](#segmentation)
- [Sources](#sources)

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

AI/ML services empower marketing analysts and practitioners to leverage the power of artificial intelligence and machine learning in customer experience use cases. This allows for marketing analysts to set up models specific to a company's needs using business-level configurations without the need for data science expertise.

### Attribution AI

Attribution AI is used to attribute credits to touchpoints leading to conversion events. This can be used by marketers to help quantify the marketing impact of each individual marketing touchpoint across customer journeys.

**Updated features**

| Feature | Description |
| ------- | ----------- |
| Support for Privacy | <li> Attribution AI now supports defining user roles and access policies to manage [permissions](../../help/access-control/abac/ui/permissions.md) for features and objects within a product application. </li><li>Audit log resources are recorded automatically as the activity occurs.</li> <li> Through [attribute-based access control](../../access-control/abac/overview.md), administrators can control access to specific objects and/or capabilities based on certain attributes, which can be metadata added to an object, such as labels.Administrators can also define user roles that have access to only specific fields and data that correspond to those fields.</li> <li>[Data Hygiene](../../help/hygiene/home.md) capabilities within Attribution AI allow you to only use updated data for further training and scoring. Likewise, when you request to delete data, Attribution AI refrains from using the deleted data.</li><li>Attribution AI leverages Platform datasets. To help facilitate GDPR compliance, you can use Adobe Experience Platform Privacy Service to set up protocols to honor customer requests to access and delete their data across the data lake, Identity Service, and Real-time Customer Profile. All data is encrypted in transit and at rest.</li>|

{style="table-layout:auto"}

**Note**: Attribution AI will not be available for Healthcare Shield customers until the end of Q4 2022.
 
For more information on Attribution AI, please see the [Attribution AI](../../intelligent-services/attribution-ai/overview.md) overview.

### Customer AI

Customer AI available in Real-time Customer Data Platform, is used to generate custom propensity scores such as churn and conversion for individual profiles at scale.

**Updated features**

| Feature | Description |
| ------- | ----------- |
| Support for Privacy | <li> Customer AI now supports defining user roles and access policies to manage [permissions](../../help/access-control/abac/ui/permissions.md) for features and objects within a product application. </li><li>Audit log resources are recorded automatically as the activity occurs.</li> <li> Through [attribute-based access control](../../access-control/abac/overview.md), administrators can control access to specific objects and/or capabilities based on certain attributes. These attributes can be metadata added to an object, such as labels. Administrators can also define user roles that have access to only specific fields and data that correspond to those fields.</li> <li>[Data Hygiene](../../help/hygiene/home.md) capabilities within Customer AI allow you to only use updated data for further training and scoring. Similarly, when you request to delete data, Customer AI refrains from using the deleted data.</li><li>Customer AI leverages Platform datasets. To help facilitate GDPR compliance, you can use Adobe Experience Platform Privacy Service to set up protocols to honor customer requests to access and delete their data across the data lake, Identity Service, and Real-time Customer Profile. All data is encrypted in transit and at rest.</li>|

{style="table-layout:auto"}

**Note**: Customer AI will not be available for Healthcare Shield customers until the end of Q4 2022.
 
For more information on Customer AI, please see the [Customer AI](../../intelligent-services/customer-ai/overview.md) overview.

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform provides multiple [!DNL dashboards] through which you can view important insights about your organization's data, as captured during daily snapshots.

**Updated features**

| Feature | Description |
| --- | --- |
| Scheduled activations widget | The [!UICONTROL Scheduled activations] widget provides a tabularized view of the most recently activated destinations. For each segment, it includes the name, destination platform, and activation start and end date. This widget allows you to discover at a glance where and when the audience is being activated and makes duplicate or unnecessary activations more transparent. This accumulated information also highlights where any activations have been left out. | 

For more information on [!DNL Dashboards], please see the [[!DNL Dashboards] overview](../../dashboards/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] allows data engineers to map, transform, and validate data to and from Experience Data Model (XDM).

**Updated features**

| Feature | Description | 
| --- | --- |
| Support for ingesting records with warnings | Data Prep will now localize warnings (non-critical errors) to the fields and will allow the rest of the row to be ingested. All mapper transformation errors are now reported as warnings and rows that are partially ingested are considered successful, with a warning.  Monitoring is also supported on records with warnings and diagnostic details. Partial ingestion of records with warnings is currently only available to streaming data. Review the documentation on [ingesting records with warnings](../../sources/tutorials/ui/monitor-streaming.md) for more information. |

{style="table-layout:auto"}

To learn more about [!DNL Data Prep], see the [[!DNL Data Prep] overview](../../data-prep/home.md).

## Experience Data Model (XDM) {#xdm}

XDM is an open-source specification that provides common structures and definitions (schemas) for data that is brought into Adobe Experience Platform. By adhering to XDM standards, all customer experience data can be incorporated into a common representation to deliver insights in a faster, more integrated way. You can gain valuable insights from customer actions, define customer audiences through segments, and use customer attributes for personalization purposes.

**New XDM components**

| Component type | Name | Description |
| --- | --- | --- |
| Global schema | [[!UICONTROL AJO Entity Schema]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity.schema.json) | Describes denormalized entities for Adobe Journey Optimizer. |
| Class | [[!UICONTROL AJO Execution Entities]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-execution-entity.schema.json) | Describes Adobe Journey Optimizer execution entities for use in segmentation. |
| Field group | [[!UICONTROL Workfront Work Objects]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobjects-all.schema.json) | A wrapper field group that references all the lower level object-specific field groups for Adobe Workfront.|

{style="table-layout:auto"}

**Updated XDM components**

| Component type | Name | Description |
| --- | --- | --- |
| Field group | [[!UICONTROL Journey Orchestration Step Event Common Fields]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | Two new properties have been added: `origTimeStamp` and `experienceID`. |
| Field group | [[!UICONTROL Segment Membership Details]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/segmentation.schema.json) | In addition to [!UICONTROL XDM Individual Profile], this field group can now also be used in schemas based on the XDM Business Account class. |
| Field group | (Multiple) | Several field groups related to Marketo B2B activities have been updated to stable status. See the following [pull request](https://github.com/adobe/xdm/pull/1593/files) for details. |
| Field group | (Multiple) | Several weather-related field groups have been updated to fix errors that were occurring for `uvIndex` and `sunsetTime`. See the following [pull request](https://github.com/adobe/xdm/pull/1602/files) for details. |
| Data type | [[!UICONTROL Product list item]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | A new property `productImageUrl` has been added. |
| Data type | [[!UICONTROL Qoe Data details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | A new property `framesPerSecond` has been added. |
| Data type | [[!UICONTROL Session details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | `sdkVersion` has been renamed to `appVersion`. `meta:enum` and `description` fields have also been updated. |
| Data types and field groups | (Multiple) | Several media data types and field groups have new fields and updated descriptions. See the following [pull request](https://github.com/adobe/xdm/pull/1582/files) for details. |
| (All) | (Multiple) | All schema objects that contain an `enum` field now also contain a corresponding `meta:enum` field to denote display values for each constraint. See the following [pull request](https://github.com/adobe/xdm/pull/1601/files) for details. |

{style="table-layout:auto"}

For more information on XDM in Platform, see the [XDM System overview](../../xdm/home.md).

## Real-time Customer Profile {#profile}

Adobe Experience Platform enables you to drive coordinated, consistent, and relevant experiences for your customers no matter where or when they interact with your brand. With Real-time Customer Profile, you can see a holistic view of each individual customer that combines data from multiple channels, including online, offline, CRM, and third party data. Profile allows you to consolidate customer data into a unified view offering an actionable, timestamped account of every customer interaction.

| Feature | Description |
| ------- | ----------- |
| Orphaned profile edge attribute cleanup | For all organizations, Profile Service now removes leftover edge attributes of user activity region on a daily basis to give a more accurate representation of your profiles in your system. This cleanup occurs after all the profile fragments for a given profile are deleted and should impact profiles being merged from datasets where `com_adobe_aep_profile_region_dataset` is marked as `true`. This may show a drop in the "Addressable audience" metric in the license usage dashboard and may show a drop in the "Profile count" metric in the Profile dashboard, since these metrics included leftover edge attribute fragments prior to this release. |

{style="table-layout:auto"}

To learn more about Real-time Customer Profile, including tutorials and best practices for working with profile data, please begin by reading the [Real-time Customer Profile overview](../../profile/home.md).

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] defines a particular subset of profiles by describing the criteria that distinguishes a marketable group of people within your customer base. Segments can be based on record data (such as demographic information) or time series events representing customer interactions with your brand.

**New features**

| Feature | Description |
| ------- | ----------- |
| Support for 4000 segments | All organizations with Platform can now support up to 4000 segment definitions. For more information on how this change affects the segment job APIs, please read the [segment job endpoint guide](../../segmentation/api/segment-jobs.md) |

For more information on [!DNL Segmentation Service], please see the [Segmentation overview](../../segmentation/home.md).

## Sources {#sources}

Adobe Experience Platform can ingest data from external sources while allowing you to structure, label, and enhance that data using Platform services. You can ingest data from a variety of sources such as Adobe applications, cloud-based storage, third-party software, and your CRM system.

Experience Platform provides a RESTful API and an interactive UI that lets you set up source connections for various data providers with ease. These source connections allow you to authenticate and connect to external storage systems and CRM services, set times for ingestion runs, and manage data ingestion throughput.

**New features**

| Feature | Description |
| --- | --- |
| General availability of Self-Serve Sources (Batch SDK) | Develop, test, and integrate your REST API-based data source to ingest batch data into Experience Platform using easy to configure source specifications. With Sources SDK, you can: <ul><li>Configure a new source to the Experience Platform catalog.</li><li>Define specifications for your source, including information pertaining to supported authentication types, scheduling, and how resource data is fetched.</li><li>Create user-facing documentation for your new source.</li></ul> For more information, read the documentation on [Self-Serve Sources (Batch SDK)](../../sources/sources-sdk/overview.md). |
| General availability of [!DNL Google BigQuery] source | Use the [!DNL Google BigQuery] source to ingest data from your [!DNL Google BigQuery] data warehouse to Experience Platform. For more information, read the documentation on the [[!DNL Google BigQuery] source](../../sources/connectors/databases/bigquery.md). |
| [!DNL Teradata Vantage] source (Beta) | Use the [!DNL Teradata Vantage] source to ingest data from hybrid multi-cloud environments to Experience Platform. For more information, read the documentation on the [[!DNL Teradata Vantage] source](../../sources/connectors/databases/teradata-vantage.md). |
| Cross-region support for Adobe Analytics source | You can now ingest report suites from any region (United States, United Kingdom, or Singapore). Report suites must be mapped to the same organization as the Experience Platform Sandbox instance in which the source connection is being created in. For more information, read the guide on [creating an Adobe Analytics source connection in the UI](../../sources/tutorials/ui/create/adobe-applications/analytics.md). |

{style="table-layout:auto"}

To learn more about sources, see the [sources overview](../../sources/home.md).