---
title: Introducing the API for Bulk Updating Custom User Profile Properties for SharePoint Online
ms.date: 11/03/2017
ms.openlocfilehash: f758e3aea35bf83519cf48059f33f9846ebc5cd9
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="introducing-the-api-for-bulk-updating-custom-user-profile-properties-for-sharepoint-online"></a><span data-ttu-id="abacd-102">Introducing the API for Bulk Updating Custom User Profile Properties for SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="abacd-102">Introducing the API for Bulk Updating Custom User Profile Properties for SharePoint Online</span></span>


<span data-ttu-id="abacd-103">_**Applies to:** SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="abacd-103">_**Applies to:** SharePoint Online_</span></span>

<span data-ttu-id="abacd-104">As part of the new Client Side Object Model (CSOM) version (4622.1208 or newer), SharePoint has the ability to bulk import custom user profile properties.</span><span class="sxs-lookup"><span data-stu-id="abacd-104">As part of the new Client Side Object Model (CSOM) version (4622.1208 or newer), SharePoint has the ability to bulk import custom user profile properties.</span></span> <span data-ttu-id="abacd-105">Prior to this release, your only option was to take advantage of the user profile CSOM operations for updating specific properties for individual user profiles.</span><span class="sxs-lookup"><span data-stu-id="abacd-105">Prior to this release, your only option was to take advantage of the user profile CSOM operations for updating specific properties for individual user profiles.</span></span> <span data-ttu-id="abacd-106">However, this approach is inefficient and too time consuming (especially when dealing with thousands of profiles).</span><span class="sxs-lookup"><span data-stu-id="abacd-106">However, this approach is inefficient and too time consuming (especially when dealing with thousands of profiles).</span></span>

<span data-ttu-id="abacd-107">Many enterprises need to replicate custom attributes to the SharePoint user profile service and so a more performant user profile bulk API has been released.</span><span class="sxs-lookup"><span data-stu-id="abacd-107">Many enterprises need to replicate custom attributes to the SharePoint user profile service and so a more performant user profile bulk API has been released.</span></span>

## <a name="an-overview-of-the-bulk-user-profile-update-process"></a><span data-ttu-id="abacd-108">An Overview of the Bulk User Profile Update Process</span><span class="sxs-lookup"><span data-stu-id="abacd-108">An Overview of the Bulk User Profile Update Process</span></span>
<span data-ttu-id="abacd-109"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="abacd-109"></span></span>

![Bulk UPA update flow](media/bulkuserprofileupdateapi/UserProfileBulkAPIProcess.png)

1. <span data-ttu-id="abacd-111">User attributes are synchronized from the corporate Active Directory to the Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="abacd-111">User attributes are synchronized from the corporate Active Directory to the Azure Active Directory.</span></span> <span data-ttu-id="abacd-112">You can select which attributes are replicated across on-premises and Azure.</span><span class="sxs-lookup"><span data-stu-id="abacd-112">You can select which attributes are replicated across on-premises and Azure.</span></span>
2. <span data-ttu-id="abacd-113">A standardized set of attributes are replicated from Azure Active Directory to the SharePoint Online User Profile Store within Office 365.</span><span class="sxs-lookup"><span data-stu-id="abacd-113">A standardized set of attributes are replicated from Azure Active Directory to the SharePoint Online User Profile Store within Office 365.</span></span> <span data-ttu-id="abacd-114">Unlke on-premises SharePoint, these attributes cannot be customized.</span><span class="sxs-lookup"><span data-stu-id="abacd-114">Unlke on-premises SharePoint, these attributes cannot be customized.</span></span>
3. <span data-ttu-id="abacd-115">A custom synchronization tool taking advantage of the new bulk update APIs.</span><span class="sxs-lookup"><span data-stu-id="abacd-115">A custom synchronization tool taking advantage of the new bulk update APIs.</span></span> <span data-ttu-id="abacd-116">This tool uploads a JSON file to the Office 365 tenant and queues the import process.</span><span class="sxs-lookup"><span data-stu-id="abacd-116">This tool uploads a JSON file to the Office 365 tenant and queues the import process.</span></span> <span data-ttu-id="abacd-117">This tool can be implemented using managed code (.NET) or as a PowerShell script using the new CSOM APIs.</span><span class="sxs-lookup"><span data-stu-id="abacd-117">This tool can be implemented using managed code (.NET) or as a PowerShell script using the new CSOM APIs.</span></span>
4. <span data-ttu-id="abacd-118">A Line of Business (LOB) system, or any external system, which is the source of the information in the JSON file.</span><span class="sxs-lookup"><span data-stu-id="abacd-118">A Line of Business (LOB) system, or any external system, which is the source of the information in the JSON file.</span></span> <span data-ttu-id="abacd-119">This could also be a combination of data from Active Directory and any external system.</span><span class="sxs-lookup"><span data-stu-id="abacd-119">This could also be a combination of data from Active Directory and any external system.</span></span> <span data-ttu-id="abacd-120">Notice that from an API perspective, the LOB system could even be an on-premises SharePoint 2013 or 2016 farm.</span><span class="sxs-lookup"><span data-stu-id="abacd-120">Notice that from an API perspective, the LOB system could even be an on-premises SharePoint 2013 or 2016 farm.</span></span>
5. <span data-ttu-id="abacd-121">An out of the box server side timer job running in SharePoint online which checks for queued import requests and will perform the actual import operation based on the API calls and the information within the provided JSON file.</span><span class="sxs-lookup"><span data-stu-id="abacd-121">An out of the box server side timer job running in SharePoint online which checks for queued import requests and will perform the actual import operation based on the API calls and the information within the provided JSON file.</span></span>
6. <span data-ttu-id="abacd-122">Extended user profile information is available within user profiles and can be used for any out of the box or custom functionality in SharePoint online.</span><span class="sxs-lookup"><span data-stu-id="abacd-122">Extended user profile information is available within user profiles and can be used for any out of the box or custom functionality in SharePoint online.</span></span>

> [!NOTE] 
> <span data-ttu-id="abacd-123">The import only works for user profile properties which have **not** been set to be editable by end users.</span><span class="sxs-lookup"><span data-stu-id="abacd-123">The import only works for user profile properties which have **not** been set to be editable by end users.</span></span> <span data-ttu-id="abacd-124">This is to prevent the user profile import process from overriding any information which an end user has already updated.</span><span class="sxs-lookup"><span data-stu-id="abacd-124">This is to prevent the user profile import process from overriding any information which an end user has already updated.</span></span> <span data-ttu-id="abacd-125">Additionally, the import only allows custom properties that are not active directory core properties.</span><span class="sxs-lookup"><span data-stu-id="abacd-125">Additionally, the import only allows custom properties that are not active directory core properties.</span></span> <span data-ttu-id="abacd-126">These must be synchronized to Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="abacd-126">These must be synchronized to Azure Active Directory.</span></span> <span data-ttu-id="abacd-127">For the list of these core directory properties, see the table listed in the FAQ section below.</span><span class="sxs-lookup"><span data-stu-id="abacd-127">For the list of these core directory properties, see the table listed in the FAQ section below.</span></span>

<span data-ttu-id="abacd-128">Below is a brief video that demonstrates using the new CSOM API from both managed code (.NET) and from PowerShell.</span><span class="sxs-lookup"><span data-stu-id="abacd-128">Below is a brief video that demonstrates using the new CSOM API from both managed code (.NET) and from PowerShell.</span></span> <span data-ttu-id="abacd-129">You can find the sample code used, including the sample PowerShell script, in the [Office Dev PnP Code Gallery](http://dev.office.com/patterns-and-practices-detail/7202).</span><span class="sxs-lookup"><span data-stu-id="abacd-129">You can find the sample code used, including the sample PowerShell script, in the [Office Dev PnP Code Gallery](http://dev.office.com/patterns-and-practices-detail/7202).</span></span>

<iframe id="ytplayer" type="text/html" width="640" height="390" src="https://www.youtube.com/embed/-X_2T0SRUBk?autoplay=0&origin=https://msdn.microsoft.com" frameborder="0"></iframe>

## <a name="import-file-format"></a><span data-ttu-id="abacd-130">Import File Format</span><span class="sxs-lookup"><span data-stu-id="abacd-130">Import File Format</span></span>
<span data-ttu-id="abacd-131"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="abacd-131"></span></span>

<span data-ttu-id="abacd-132">The import process uses a JSON file containing the properties and their values.</span><span class="sxs-lookup"><span data-stu-id="abacd-132">The import process uses a JSON file containing the properties and their values.</span></span> <span data-ttu-id="abacd-133">Below is the expected structure of that file:</span><span class="sxs-lookup"><span data-stu-id="abacd-133">Below is the expected structure of that file:</span></span>   

```JSON
{
   "value": [
     {
       "<IdName>": "<UserIdValue_1>",
       "<AttributeName_1>": "<User1_AttributeValue_1>",
       "<AttributeName_2>": "<User1_AttributeValue_2>",
     },
     {
       "<IdName>": "<UserIdValue_2>",
       "<AttributeName_1>": "<User2_AttributeValue_1>",
       "<AttributeName_2>": "<User2_AttributeValue_2>",
     },
     {
       "<IdName>": "<UserIdValue_n>",
       "<AttributeName_1>": "<Usern_AttributeValue_1>",
       "<AttributeName_2>": "<Usern_AttributeValue_2>",
     }
   ]
}
```

<span data-ttu-id="abacd-134">Below is a simple example file using the format above:</span><span class="sxs-lookup"><span data-stu-id="abacd-134">Below is a simple example file using the format above:</span></span>

```JSON
{
  "value": [
    {
      "IdName": "vesaj@contoso.com",
      "City": "Helsinki",
      "Office": "Viper"
    },
    {
      "IdName": "bjansen@contoso.com",
      "City": "Brussels",
      "Office": "Beetle"
    },
    {
      "IdName": "unknowperson@contoso.com",
      "City": "None",
      "Office": ""
    },
    {
      "IdName": "erwin@contoso.com",
      "City": "Stockholm",
      "Office": "Elite"
    }
  ]
}
```

<span data-ttu-id="abacd-135">In the example above, identity resolution is based on the `IdName` property and there are two properties which are being updated called `City` and `Office`.</span><span class="sxs-lookup"><span data-stu-id="abacd-135">In the example above, identity resolution is based on the `IdName` property and there are two properties which are being updated called `City` and `Office`.</span></span> <span data-ttu-id="abacd-136">The file contains information for four different accounts within the tenant.</span><span class="sxs-lookup"><span data-stu-id="abacd-136">The file contains information for four different accounts within the tenant.</span></span> <span data-ttu-id="abacd-137">Property names used in this source file are not necessarily the same as the names used within the SharePoint Online User Profile Service since we will provide correct property mapping within our code.</span><span class="sxs-lookup"><span data-stu-id="abacd-137">Property names used in this source file are not necessarily the same as the names used within the SharePoint Online User Profile Service since we will provide correct property mapping within our code.</span></span> 

### <a name="source-data-file-restrictions"></a><span data-ttu-id="abacd-138">Source Data File Restrictions</span><span class="sxs-lookup"><span data-stu-id="abacd-138">Source Data File Restrictions</span></span>
<span data-ttu-id="abacd-139">There are few restrictions on individual source data files:</span><span class="sxs-lookup"><span data-stu-id="abacd-139">There are few restrictions on individual source data files:</span></span>
- <span data-ttu-id="abacd-140">Maximum file size: 2GB</span><span class="sxs-lookup"><span data-stu-id="abacd-140">Maximum file size: 2GB</span></span>
- <span data-ttu-id="abacd-141">Maximum number of properties: 500,000</span><span class="sxs-lookup"><span data-stu-id="abacd-141">Maximum number of properties: 500,000</span></span>
- <span data-ttu-id="abacd-142">The source file must be uploaded to the same SharePoint Online tenant where the process is started</span><span class="sxs-lookup"><span data-stu-id="abacd-142">The source file must be uploaded to the same SharePoint Online tenant where the process is started</span></span>


## <a name="user-profile-property-import-process"></a><span data-ttu-id="abacd-143">User Profile Property Import Process</span><span class="sxs-lookup"><span data-stu-id="abacd-143">User Profile Property Import Process</span></span>
<span data-ttu-id="abacd-144"><a name="sectionSection2"> </a></span><span class="sxs-lookup"><span data-stu-id="abacd-144"></span></span>

<span data-ttu-id="abacd-145">Here’s the full process:</span><span class="sxs-lookup"><span data-stu-id="abacd-145">Here’s the full process:</span></span>

1. <span data-ttu-id="abacd-146">Create or synchronize users in an Office 365 tenant or to the Azure AD associated to it</span><span class="sxs-lookup"><span data-stu-id="abacd-146">Create or synchronize users in an Office 365 tenant or to the Azure AD associated to it</span></span>
     - <span data-ttu-id="abacd-147">When users are synchronized to Azure AD, it will also synchronize a standardized set of attributes to the SharePoint Online User Profile Service.</span><span class="sxs-lookup"><span data-stu-id="abacd-147">When users are synchronized to Azure AD, it will also synchronize a standardized set of attributes to the SharePoint Online User Profile Service.</span></span>
2. <span data-ttu-id="abacd-148">Create any needed custom properties within the User Profile Service</span><span class="sxs-lookup"><span data-stu-id="abacd-148">Create any needed custom properties within the User Profile Service</span></span>
     - <span data-ttu-id="abacd-149">Since there’s no remote APIs for creating custom properties in the User Profile Service, this step must be performed manually for each of the tenants where custom user profile properties are needed (this only needs to be done once per tenant).</span><span class="sxs-lookup"><span data-stu-id="abacd-149">Since there’s no remote APIs for creating custom properties in the User Profile Service, this step must be performed manually for each of the tenants where custom user profile properties are needed (this only needs to be done once per tenant).</span></span>
     - <span data-ttu-id="abacd-150">Only user profile properties which are not “allowed to be edited by end users” can be imported.</span><span class="sxs-lookup"><span data-stu-id="abacd-150">Only user profile properties which are not “allowed to be edited by end users” can be imported.</span></span> <span data-ttu-id="abacd-151">Trying to import a JSON object property to a user profile property which is marked as “editable by end users” will result in an exception when the CSOM API is called.</span><span class="sxs-lookup"><span data-stu-id="abacd-151">Trying to import a JSON object property to a user profile property which is marked as “editable by end users” will result in an exception when the CSOM API is called.</span></span>
3. <span data-ttu-id="abacd-152">Create and upload the JSON file to the Office 365 tenant</span><span class="sxs-lookup"><span data-stu-id="abacd-152">Create and upload the JSON file to the Office 365 tenant</span></span>
     - <span data-ttu-id="abacd-153">You’ll need to upload the JSON data file containing the information to be updated to the Office 365 tenant.</span><span class="sxs-lookup"><span data-stu-id="abacd-153">You’ll need to upload the JSON data file containing the information to be updated to the Office 365 tenant.</span></span>
     - <span data-ttu-id="abacd-154">In the case of any exception during the import process, SharePoint will provide additional logging information saved in the same document library where the file existed within a new sub folder.</span><span class="sxs-lookup"><span data-stu-id="abacd-154">In the case of any exception during the import process, SharePoint will provide additional logging information saved in the same document library where the file existed within a new sub folder.</span></span>
     - <span data-ttu-id="abacd-155">Cleaning of the log files and JSON files are not done automatically and is the responsibility of the custom solution using the API.</span><span class="sxs-lookup"><span data-stu-id="abacd-155">Cleaning of the log files and JSON files are not done automatically and is the responsibility of the custom solution using the API.</span></span> <span data-ttu-id="abacd-156">You should consider the life cycle of these files within your implementation.</span><span class="sxs-lookup"><span data-stu-id="abacd-156">You should consider the life cycle of these files within your implementation.</span></span> <span data-ttu-id="abacd-157">These files are stored in document libraries so they will be consuming a portion of the assigned storage for the site collection.</span><span class="sxs-lookup"><span data-stu-id="abacd-157">These files are stored in document libraries so they will be consuming a portion of the assigned storage for the site collection.</span></span>
4. <span data-ttu-id="abacd-158">Call the bulk UPA Import API for queuing the import job</span><span class="sxs-lookup"><span data-stu-id="abacd-158">Call the bulk UPA Import API for queuing the import job</span></span>
     - <span data-ttu-id="abacd-159">Use the CSOM API to queue the import process.</span><span class="sxs-lookup"><span data-stu-id="abacd-159">Use the CSOM API to queue the import process.</span></span> <span data-ttu-id="abacd-160">This can be achieved by executing CSOM code using either managed code (.NET) or PowerShell.</span><span class="sxs-lookup"><span data-stu-id="abacd-160">This can be achieved by executing CSOM code using either managed code (.NET) or PowerShell.</span></span>
     - <span data-ttu-id="abacd-161">The method to queue the job requires property mapping information and the location of the data file.</span><span class="sxs-lookup"><span data-stu-id="abacd-161">The method to queue the job requires property mapping information and the location of the data file.</span></span> <span data-ttu-id="abacd-162">This method will quickly execute because it just queues the actual import process, which will later be executed as part of a back end process in SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="abacd-162">This method will quickly execute because it just queues the actual import process, which will later be executed as part of a back end process in SharePoint Online.</span></span>
5. <span data-ttu-id="abacd-163">Check the status of the import job</span><span class="sxs-lookup"><span data-stu-id="abacd-163">Check the status of the import job</span></span>
     - <span data-ttu-id="abacd-164">You can also use remote APIs to check the status of a specific import job or all of the recent import jobs.</span><span class="sxs-lookup"><span data-stu-id="abacd-164">You can also use remote APIs to check the status of a specific import job or all of the recent import jobs.</span></span> <span data-ttu-id="abacd-165">To be able to check the status of a specific call, you should store the unique job identifier received as a return value when the job is queued.</span><span class="sxs-lookup"><span data-stu-id="abacd-165">To be able to check the status of a specific call, you should store the unique job identifier received as a return value when the job is queued.</span></span>


## <a name="csom-api-for-the-bulk-import-process"></a><span data-ttu-id="abacd-166">CSOM API for the Bulk Import Process</span><span class="sxs-lookup"><span data-stu-id="abacd-166">CSOM API for the Bulk Import Process</span></span>
<span data-ttu-id="abacd-167"><a name="sectionSection3"> </a></span><span class="sxs-lookup"><span data-stu-id="abacd-167"></span></span>

### <a name="queue-import"></a><span data-ttu-id="abacd-168">Queue Import</span><span class="sxs-lookup"><span data-stu-id="abacd-168">Queue Import</span></span>
<span data-ttu-id="abacd-169">You can queue the import process by calling the [`QueueImportProfileProperties`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.queueimportprofileproperties.aspx) method located in the [`Office365Tenant`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.aspx) object.</span><span class="sxs-lookup"><span data-stu-id="abacd-169">You can queue the import process by calling the [`QueueImportProfileProperties`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.queueimportprofileproperties.aspx) method located in the [`Office365Tenant`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.aspx) object.</span></span> <span data-ttu-id="abacd-170">This is an asynchronous call in that it doesn’t download the source data or perform the import, it simply adds a work item to the queue for doing this later.</span><span class="sxs-lookup"><span data-stu-id="abacd-170">This is an asynchronous call in that it doesn’t download the source data or perform the import, it simply adds a work item to the queue for doing this later.</span></span> <span data-ttu-id="abacd-171">Here’s the full signature of the method:</span><span class="sxs-lookup"><span data-stu-id="abacd-171">Here’s the full signature of the method:</span></span>

```c#
public ClientResult<Guid> QueueImportProfileProperties(
                          ImportProfilePropertiesUserIdType idType, 
                          string sourceDataIdProperty, 
                          IDictionary<string, string> propertyMap, 
                          string sourceUri);
```

#### <a name="parameters"></a><span data-ttu-id="abacd-172">Параметры</span><span class="sxs-lookup"><span data-stu-id="abacd-172">Parameters</span></span>

<span data-ttu-id="abacd-173">**Тип_идентификатора**:_[`ImportProfilePropertiesUserIdType`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesuseridtype.aspx)_</span><span class="sxs-lookup"><span data-stu-id="abacd-173">**idType**: _[`ImportProfilePropertiesUserIdType`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesuseridtype.aspx)_</span></span>

<span data-ttu-id="abacd-174">The type of id to use when looking up the user profile.</span><span class="sxs-lookup"><span data-stu-id="abacd-174">The type of id to use when looking up the user profile.</span></span> <span data-ttu-id="abacd-175">Possible values are `Email`, `CloudId`, and `PrincipalName`.</span><span class="sxs-lookup"><span data-stu-id="abacd-175">Possible values are `Email`, `CloudId`, and `PrincipalName`.</span></span> <span data-ttu-id="abacd-176">Note that regardless of the type, the user must already exist in the User Profile Service for the import to work.</span><span class="sxs-lookup"><span data-stu-id="abacd-176">Note that regardless of the type, the user must already exist in the User Profile Service for the import to work.</span></span> <span data-ttu-id="abacd-177">It’s recommended to use the `CloudId` to ensure uniqueness.</span><span class="sxs-lookup"><span data-stu-id="abacd-177">It’s recommended to use the `CloudId` to ensure uniqueness.</span></span>

<span data-ttu-id="abacd-178">Property mapping between ID Type and Azure AD property:</span><span class="sxs-lookup"><span data-stu-id="abacd-178">Property mapping between ID Type and Azure AD property:</span></span>

<span data-ttu-id="abacd-179">UPA Bulk Import ID Type</span><span class="sxs-lookup"><span data-stu-id="abacd-179">UPA Bulk Import ID Type</span></span> | <span data-ttu-id="abacd-180">Azure Directory Attribute</span><span class="sxs-lookup"><span data-stu-id="abacd-180">Azure Directory Attribute</span></span>
--- | ---
<span data-ttu-id="abacd-181">CloudId</span><span class="sxs-lookup"><span data-stu-id="abacd-181">CloudId</span></span> | <span data-ttu-id="abacd-182">ObjectID</span><span class="sxs-lookup"><span data-stu-id="abacd-182">ObjectID</span></span>
<span data-ttu-id="abacd-183">PrincipalName</span><span class="sxs-lookup"><span data-stu-id="abacd-183">PrincipalName</span></span> | <span data-ttu-id="abacd-184">userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="abacd-184">userPrincipalName</span></span>
<span data-ttu-id="abacd-185">Email</span><span class="sxs-lookup"><span data-stu-id="abacd-185">Email</span></span> | <span data-ttu-id="abacd-186">mail</span><span class="sxs-lookup"><span data-stu-id="abacd-186">mail</span></span>

<span data-ttu-id="abacd-187">**sourceDataIdProperty**: _`System.String`_</span><span class="sxs-lookup"><span data-stu-id="abacd-187">**sourceDataIdProperty**: _`System.String`_</span></span>

<span data-ttu-id="abacd-188">The name of the id property in the source data.</span><span class="sxs-lookup"><span data-stu-id="abacd-188">The name of the id property in the source data.</span></span> <span data-ttu-id="abacd-189">The value of the property from the source data will be used to lookup the user.</span><span class="sxs-lookup"><span data-stu-id="abacd-189">The value of the property from the source data will be used to lookup the user.</span></span> <span data-ttu-id="abacd-190">The User Profile Service property used for the lookup depends on the value of `idType`.</span><span class="sxs-lookup"><span data-stu-id="abacd-190">The User Profile Service property used for the lookup depends on the value of `idType`.</span></span>

<span data-ttu-id="abacd-191">**propertyMap**: _`IDictionary<string, string>`_</span><span class="sxs-lookup"><span data-stu-id="abacd-191">**propertyMap**: _`IDictionary<string, string>`_</span></span>

<span data-ttu-id="abacd-192">A map from the source property name to the User Profile Service property name.</span><span class="sxs-lookup"><span data-stu-id="abacd-192">A map from the source property name to the User Profile Service property name.</span></span> <span data-ttu-id="abacd-193">Note that the User Profile Service properties must already exist.</span><span class="sxs-lookup"><span data-stu-id="abacd-193">Note that the User Profile Service properties must already exist.</span></span> <span data-ttu-id="abacd-194">The key is the property name used in the source file, the value is the property name used in the User Profile Service.</span><span class="sxs-lookup"><span data-stu-id="abacd-194">The key is the property name used in the source file, the value is the property name used in the User Profile Service.</span></span>

<span data-ttu-id="abacd-195">**sourceUri**: _`System.String`_</span><span class="sxs-lookup"><span data-stu-id="abacd-195">**sourceUri**: _`System.String`_</span></span>

<span data-ttu-id="abacd-196">The URI of the source data file to import.</span><span class="sxs-lookup"><span data-stu-id="abacd-196">The URI of the source data file to import.</span></span> <span data-ttu-id="abacd-197">Файл не должен перемещен или удалить сразу, так как он не могут быть загружены в течение некоторого времени.</span><span class="sxs-lookup"><span data-stu-id="abacd-197">The file should not be moved or deleted right away as it may not be downloaded for some time.</span></span>

#### <a name="return-value"></a><span data-ttu-id="abacd-198">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="abacd-198">Return value</span></span>
<span data-ttu-id="abacd-199">A Guid that identifies the import job that has been queued.</span><span class="sxs-lookup"><span data-stu-id="abacd-199">A Guid that identifies the import job that has been queued.</span></span>

#### <a name="example"></a><span data-ttu-id="abacd-200">Пример</span><span class="sxs-lookup"><span data-stu-id="abacd-200">Example</span></span>
<span data-ttu-id="abacd-201">Below is an example using C# of how to start the process using the sample input file above:</span><span class="sxs-lookup"><span data-stu-id="abacd-201">Below is an example using C# of how to start the process using the sample input file above:</span></span>

```c#
// Create an instance of the Office 365 Tenant object. Loading this object is not technically needed for this operation. 
Office365Tenant tenant = new Office365Tenant(ctx);
ctx.Load(tenant);
ctx.ExecuteQuery();

// Type of user identifier ["PrincipalName", "Email", "CloudId"] in the 
// User Profile Service. In this case, we use Email as the identifier at the UPA storage
ImportProfilePropertiesUserIdType userIdType = 
      ImportProfilePropertiesUserIdType.Email;

// Name of the user identifier property within the JSON file
var userLookupKey = "IdName";

var propertyMap = new System.Collections.Generic.Dictionary<string, string>();

// The key is the property in the JSON file, 
// The value is the user profile property Name in the User Profile Service
// Notice that we have 2 custom properties in UPA called 'City' and 'OfficeCode'
propertyMap.Add("City", "City");
propertyMap.Add("Office", "OfficeCode");

// Returns a GUID which can be used to check the status of the execution and the end results
var workItemId = tenant.QueueImportProfileProperties(
      userIdType, userLookupKey, propertyMap, fileUrl
      );

ctx.ExecuteQuery();
```

### <a name="check-the-status-of-an-import-job"></a><span data-ttu-id="abacd-202">Check the Status of an Import Job</span><span class="sxs-lookup"><span data-stu-id="abacd-202">Check the Status of an Import Job</span></span>
<span data-ttu-id="abacd-203">Вы также можете проверить состояние задания импорта службы профилей пользователей с помощью новых интерфейсов API CSOM.</span><span class="sxs-lookup"><span data-stu-id="abacd-203">You can also check the status of the User Profile Service import jobs by using the new CSOM APIs.</span></span> <span data-ttu-id="abacd-204">Существует два метода новой базы данных для объекта клиента.</span><span class="sxs-lookup"><span data-stu-id="abacd-204">There are two new methods for this in the Tenant object.</span></span>

<span data-ttu-id="abacd-205">You can check status of an individual import job by using the [`GetImportProfilePropertyJob`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.getimportprofilepropertyjob.aspx) method located in the [`Office365Tenant`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.aspx) object.</span><span class="sxs-lookup"><span data-stu-id="abacd-205">You can check status of an individual import job by using the [`GetImportProfilePropertyJob`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.getimportprofilepropertyjob.aspx) method located in the [`Office365Tenant`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.aspx) object.</span></span> <span data-ttu-id="abacd-206">You will need to have the unique identifier of a specific import job provided as a parameter to this method.</span><span class="sxs-lookup"><span data-stu-id="abacd-206">You will need to have the unique identifier of a specific import job provided as a parameter to this method.</span></span> <span data-ttu-id="abacd-207">Ниже приведен полный подпись метода.</span><span class="sxs-lookup"><span data-stu-id="abacd-207">Here’s the full signature of the method:</span></span>

```c#
public ImportProfilePropertiesJobInfo GetImportProfilePropertyJob(Guid jobId);
```

#### <a name="parameters"></a><span data-ttu-id="abacd-208">Параметры</span><span class="sxs-lookup"><span data-stu-id="abacd-208">Parameters</span></span>
<span data-ttu-id="abacd-209">**jobID**: _`System.Guid`_</span><span class="sxs-lookup"><span data-stu-id="abacd-209">**jobID**: _`System.Guid`_</span></span>

<span data-ttu-id="abacd-210">The id of the job for which to get the high-level status.</span><span class="sxs-lookup"><span data-stu-id="abacd-210">The id of the job for which to get the high-level status.</span></span>

#### <a name="return-value"></a><span data-ttu-id="abacd-211">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="abacd-211">Return value</span></span>

<span data-ttu-id="abacd-212">[`ImportProfilePropertiesJobStatus`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobinfo.aspx) Объект с высокого уровня сведений о указанного задания.</span><span class="sxs-lookup"><span data-stu-id="abacd-212">An [`ImportProfilePropertiesJobStatus`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobinfo.aspx) object with high level status information about the specified job.</span></span>

#### <a name="example"></a><span data-ttu-id="abacd-213">Пример</span><span class="sxs-lookup"><span data-stu-id="abacd-213">Example</span></span>
<span data-ttu-id="abacd-214">Ниже пример использует C# для получение сведений о состоянии с помощью сохраненных идентификатор задания определенных импорта:</span><span class="sxs-lookup"><span data-stu-id="abacd-214">Below is an example using C# of retrieving the status of a specific import job using a stored identifier:</span></span>

```c#
// Check the status of a specific request based on the job id received when we queued the job
Office365Tenant tenant = new Office365Tenant(ctx);
var job = tenant.GetImportProfilePropertyJob(workItemId);
ctx.Load(job);
ctx.ExecuteQuery();
```

<span data-ttu-id="abacd-215">Можно проверить состояние всех заданий импорта с помощью [`GetImportProfilePropertyJobs`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.getimportprofilepropertyjobs.aspx) метод находится в объекте [Office365Tenant](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.aspx) .</span><span class="sxs-lookup"><span data-stu-id="abacd-215">You can check the status of all import jobs by using the [`GetImportProfilePropertyJobs`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.getimportprofilepropertyjobs.aspx) method located in the [Office365Tenant](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.aspx) object.</span></span> <span data-ttu-id="abacd-216">Ниже приведен полный подпись метода.</span><span class="sxs-lookup"><span data-stu-id="abacd-216">Here’s the full signature of the method:</span></span>

```c#
public ImportProfilePropertiesJobStatusCollection GetImportProfilePropertyJobs(); 
```

#### <a name="return-value"></a><span data-ttu-id="abacd-217">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="abacd-217">Return value</span></span>
<span data-ttu-id="abacd-218">[`ImportProfilePropertiesJobStatusCollection`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobstatuscollection.aspx) Объект, который представляет собой коллекцию из [`ImportProfilePropertiesJobStatus`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobinfo.aspx) объекты с высокого уровня состояния сведения о каждом из заданий.</span><span class="sxs-lookup"><span data-stu-id="abacd-218">An [`ImportProfilePropertiesJobStatusCollection`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobstatuscollection.aspx) object which is a collection of [`ImportProfilePropertiesJobStatus`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobinfo.aspx) objects with high level status information about each of the jobs.</span></span>

#### <a name="example"></a><span data-ttu-id="abacd-219">Пример</span><span class="sxs-lookup"><span data-stu-id="abacd-219">Example</span></span>
<span data-ttu-id="abacd-220">Ниже пример использует C# для получения состояния всех заданий импорта, в настоящее время сохранены в клиентов.</span><span class="sxs-lookup"><span data-stu-id="abacd-220">Below is an example using C# of getting the status of all import jobs currently saved in the tenant.</span></span> <span data-ttu-id="abacd-221">Это может быть уже обработан или в очереди заданий:</span><span class="sxs-lookup"><span data-stu-id="abacd-221">These could be already processed or queued jobs:</span></span>

```c#
// Load all import jobs – old and queued ones
Office365Tenant tenant = new Office365Tenant(ctx);
var jobs = tenant.GetImportProfilePropertyJobs();
ctx.Load(jobs);
ctx.ExecuteQuery();
foreach (var item in jobs)
{
   // Check whatever properties needed
   var state = item.State;
}
```

<span data-ttu-id="abacd-222">[`ImportProfilePropertiesJobInfo`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobinfo.aspx) Объект, возвращенный с сведения о состоянии импорта имеет следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="abacd-222">An [`ImportProfilePropertiesJobInfo`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobinfo.aspx) object returned with the import status information has the following properties.</span></span> 

<span data-ttu-id="abacd-223">**JobId**:_`System.Guid`_</span><span class="sxs-lookup"><span data-stu-id="abacd-223">**JobId**: _`System.Guid`_</span></span>

<span data-ttu-id="abacd-224">Идентификатор задания импорта</span><span class="sxs-lookup"><span data-stu-id="abacd-224">The Id of the import job</span></span>

<span data-ttu-id="abacd-225">**State**: _[`ImportProfilePropertiesJobState`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobstate.aspx)_</span><span class="sxs-lookup"><span data-stu-id="abacd-225">**State**: _[`ImportProfilePropertiesJobState`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobstate.aspx)_</span></span>

<span data-ttu-id="abacd-226">Перечисление с помощью следующих значений:</span><span class="sxs-lookup"><span data-stu-id="abacd-226">An enum with following values:</span></span>
- <span data-ttu-id="abacd-227">`Unknown`-Мы не может определить состояние задания</span><span class="sxs-lookup"><span data-stu-id="abacd-227">`Unknown` - We cannot determine the state of the job</span></span>
- <span data-ttu-id="abacd-228">`Submitted`-Задания отправки в систему</span><span class="sxs-lookup"><span data-stu-id="abacd-228">`Submitted` - The job has been submitted to the system</span></span>
- <span data-ttu-id="abacd-229">`Processing`-Обрабатывается задание</span><span class="sxs-lookup"><span data-stu-id="abacd-229">`Processing` - The job is being processed</span></span>
- <span data-ttu-id="abacd-230">`Queued`-Заданием прошел проверку и в очередь для импорта для однозначного соответствия</span><span class="sxs-lookup"><span data-stu-id="abacd-230">`Queued` - The job has passed validation and queued for import to UPA</span></span>
- <span data-ttu-id="abacd-231">`Succeeded`-Задание завершена без ошибок</span><span class="sxs-lookup"><span data-stu-id="abacd-231">`Succeeded` - The job completed with no error</span></span>
- <span data-ttu-id="abacd-232">`Error`-Задание завершено с ошибкой</span><span class="sxs-lookup"><span data-stu-id="abacd-232">`Error` - The job completed with error</span></span>

<span data-ttu-id="abacd-233">**SourceUri**:_`System.String`_</span><span class="sxs-lookup"><span data-stu-id="abacd-233">**SourceUri**: _`System.String`_</span></span>

<span data-ttu-id="abacd-234">URI файл источника данных</span><span class="sxs-lookup"><span data-stu-id="abacd-234">The URI to the data source file</span></span>

<span data-ttu-id="abacd-235">**Error**: _[`ImportProfilePropertiesJobError`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjoberror.aspx)_</span><span class="sxs-lookup"><span data-stu-id="abacd-235">**Error**: _[`ImportProfilePropertiesJobError`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjoberror.aspx)_</span></span>

<span data-ttu-id="abacd-236">Перечисление, представляющее возможные ошибки:</span><span class="sxs-lookup"><span data-stu-id="abacd-236">An enum representing the possible error:</span></span>
- <span data-ttu-id="abacd-237">`NoError`-Ошибка не найден</span><span class="sxs-lookup"><span data-stu-id="abacd-237">`NoError` - No error found</span></span>
- <span data-ttu-id="abacd-238">`InternalError`-Ошибки, возникающие при сбоя в службе</span><span class="sxs-lookup"><span data-stu-id="abacd-238">`InternalError` - The error was caused by a failure in the service</span></span>
- <span data-ttu-id="abacd-239">`DataFileNotExist`-Не удалось найти файл источника данных</span><span class="sxs-lookup"><span data-stu-id="abacd-239">`DataFileNotExist` - The data source file could not be found</span></span>
- <span data-ttu-id="abacd-240">`DataFileNotInTenant`-Файл источника данных принадлежит же клиента</span><span class="sxs-lookup"><span data-stu-id="abacd-240">`DataFileNotInTenant` - The data source file did not belong to the same tenant</span></span>
- <span data-ttu-id="abacd-241">`DataFileTooBig`— Размер файла данных слишком велико</span><span class="sxs-lookup"><span data-stu-id="abacd-241">`DataFileTooBig` - The size of the data file was too big</span></span>
- <span data-ttu-id="abacd-242">`InvalidDataFile`-Файл источника данных не прошли проверку (может быть Дополнительные сведения в файле журнала)</span><span class="sxs-lookup"><span data-stu-id="abacd-242">`InvalidDataFile` - The data source file did not pass validation (There may be additional details in the log file)</span></span>
- <span data-ttu-id="abacd-243">`ImportCompleteWithError`-Импорт данных, но произошла ошибка возникала</span><span class="sxs-lookup"><span data-stu-id="abacd-243">`ImportCompleteWithError` - The data has been imported, but there was an error encountered</span></span>

<span data-ttu-id="abacd-244">**Сообщение об ошибке**:_`System.String`_</span><span class="sxs-lookup"><span data-stu-id="abacd-244">**ErrorMessage**: _`System.String`_</span></span>

<span data-ttu-id="abacd-245">The error message</span><span class="sxs-lookup"><span data-stu-id="abacd-245">The error message</span></span>

<span data-ttu-id="abacd-246">**LogFileUri**:_`System.String`_</span><span class="sxs-lookup"><span data-stu-id="abacd-246">**LogFileUri**: _`System.String`_</span></span>

<span data-ttu-id="abacd-247">Uri в папку, где были записаны журналы</span><span class="sxs-lookup"><span data-stu-id="abacd-247">The Uri to the folder where the logs have been written</span></span>

## <a name="calling-the-import-api-from-powershell"></a><span data-ttu-id="abacd-248">Вызов API импорта из PowerShell</span><span class="sxs-lookup"><span data-stu-id="abacd-248">Calling the Import API from PowerShell</span></span>
<span data-ttu-id="abacd-249"><a name="sectionSection4"> </a></span><span class="sxs-lookup"><span data-stu-id="abacd-249"></span></span>

<span data-ttu-id="abacd-250">Вы можете воспользоваться преимуществами API импорта массового службы профилей пользователей с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="abacd-250">You can take advantage of the User Profile Service bulk import API with PowerShell.</span></span> <span data-ttu-id="abacd-251">Это означает, что вы будете использовать в коде CSOM непосредственно в сценарий PowerShell, используя необходимые параметры.</span><span class="sxs-lookup"><span data-stu-id="abacd-251">This means that you’ll use the CSOM code directly in a PowerShell script using the necessary parameters.</span></span> <span data-ttu-id="abacd-252">Для этого необходимо, что обновленные распространяемый пакет CSOM был установлен на компьютере, где выполняется скрипт.</span><span class="sxs-lookup"><span data-stu-id="abacd-252">This requires that the updated CSOM redistributable package has been installed on the computer where the script is executed.</span></span>

<span data-ttu-id="abacd-253">С помощью PowerShell, нет необходимости для компиляции кода в Visual Studio, которые могут быть более подходящим модели для некоторых клиентов.</span><span class="sxs-lookup"><span data-stu-id="abacd-253">By using PowerShell, you do not need to compile your code within Visual Studio, which may be a more suitable model for some customers.</span></span>

### <a name="sample-powershell-script"></a><span data-ttu-id="abacd-254">Образец сценария PowerShell</span><span class="sxs-lookup"><span data-stu-id="abacd-254">Sample PowerShell Script</span></span>
<span data-ttu-id="abacd-255">Ниже приведен образец сценария PowerShell, который выполняет те же действия, как приведенный выше код:</span><span class="sxs-lookup"><span data-stu-id="abacd-255">Below is a sample PowerShell script which performs the same operations as the code above:</span></span> 

```Powershell
# Get needed information from the end user
$adminUrl = Read-Host -Prompt 'Enter the admin URL of your tenant'
$userName = Read-Host -Prompt 'Enter your user name'
$pwd = Read-Host -Prompt 'Enter your password' -AsSecureString
$importFileUrl = Read-Host -Prompt 'Enter the URL to the file located in your tenant'

# Get instances to the Office 365 tenant using CSOM
$uri = New-Object System.Uri -ArgumentList $adminUrl
$context = New-Object Microsoft.SharePoint.Client.ClientContext($uri)

$context.Credentials = New-Object Microsoft.SharePoint.Client.SharePointOnlineCredentials($userName, $pwd)
$o365 = New-Object Microsoft.Online.SharePoint.TenantManagement.Office365Tenant($context)
$context.Load($o365)

# Type of user identifier ["Email", "CloudId", "PrincipalName"] in the User Profile Service
$userIdType=[Microsoft.Online.SharePoint.TenantManagement.ImportProfilePropertiesUserIdType]::Email

# Name of user identifier property in the JSON
$userLookupKey="idName"

# Create property mapping between the source file property name and the O365 property name
# Notice that we have here 2 custom properties in UPA called 'City' and 'OfficeCode'
$propertyMap = New-Object -type 'System.Collections.Generic.Dictionary[String,String]'
$propertyMap.Add("City", "City")
$propertyMap.Add("Office", "OfficeCode")

# Call to queue UPA property import 
$workItemId = $o365.QueueImportProfileProperties($userIdType, $userLookupKey, $propertyMap, $importFileUrl);

# Execute the CSOM command for queuing the import job
$context.ExecuteQuery();

# Output the unique identifier of the job
Write-Host "Import job created with the following identifier:" $workItemId.Value 
```

## <a name="handling-exceptions"></a><span data-ttu-id="abacd-256">Обработка исключений</span><span class="sxs-lookup"><span data-stu-id="abacd-256">Handling Exceptions</span></span>
<span data-ttu-id="abacd-257"><a name="sectionSection5"></a> Существует два уровня проверки при использовании этот интерфейс API.</span><span class="sxs-lookup"><span data-stu-id="abacd-257"><a name="sectionSection5"> </a> There are two levels of validation when this API is used.</span></span> <span data-ttu-id="abacd-258">При запуске процесса импорта с помощью CSOM будет начальной уровень проверки указанные значения.</span><span class="sxs-lookup"><span data-stu-id="abacd-258">When you queue the import process with CSOM there will be an initial level of validation of the provided values.</span></span> <span data-ttu-id="abacd-259">Этот компонент включает подтверждения существование отмеченными сопоставление свойств в службе профилей пользователей и, что эти свойства недоступны для редактирования конечным пользователем.</span><span class="sxs-lookup"><span data-stu-id="abacd-259">This includes confirmation that the provided mapping properties exist in the User Profile Service and that these properties are not editable by the end user.</span></span> <span data-ttu-id="abacd-260">При вызове API очереди применяется только начальной уровень проверки и ее реального выполнения задания импорта выполняется последний проверка предоставлена информация.</span><span class="sxs-lookup"><span data-stu-id="abacd-260">When the queue API is called, only an initial level of validation is applied and final validation of the provided information is performed when the import job is actually executed.</span></span>

<span data-ttu-id="abacd-261">Если во время выполнения задания импорта сведения о любых исключениях, в ту же библиотеку документов, где был задан Импорт файла создается файл ведения журнала с дополнительными сведениями.</span><span class="sxs-lookup"><span data-stu-id="abacd-261">If there are any exceptions during the actual import job execution, a logging file with additional details is generated in the same document library where the import file was located.</span></span> <span data-ttu-id="abacd-262">Будут сохранены файлы журналов для задания определенных импорта sub папки с именами с помощью уникальный идентификатор задания определенных импорта.</span><span class="sxs-lookup"><span data-stu-id="abacd-262">Log files for specific import jobs are saved to sub folders named using the unique identifier of the specific import job.</span></span>

<span data-ttu-id="abacd-263">Ниже приведен пример результаты выполнения задания импорта.</span><span class="sxs-lookup"><span data-stu-id="abacd-263">Below is an example of the results of running an import job.</span></span> <span data-ttu-id="abacd-264">На рисунке ниже можно увидеть две вложенные папки для двух различных выполнений, создаваемых в библиотеке документов, где хранится файл импорта:</span><span class="sxs-lookup"><span data-stu-id="abacd-264">In the picture below, you can see two sub folders for two different executions created in the document library where the import file is stored:</span></span>

![Задание исключение вложенные папки](media/bulkuserprofileupdateapi/UserProfileBulkAPIProcess-folders.png)

<span data-ttu-id="abacd-266">Файл журнала сохраняется в папке sub и для подробного анализа, который можно загрузить из Office 365:</span><span class="sxs-lookup"><span data-stu-id="abacd-266">The actual log file is saved in the sub folder and you can download that from Office 365 for detailed analysis:</span></span>

![Задание файла журнала исключений](media/bulkuserprofileupdateapi/UserProfileBulkAPIProcess-LogFile.png)

### <a name="common-exceptions"></a><span data-ttu-id="abacd-268">Общие исключения</span><span class="sxs-lookup"><span data-stu-id="abacd-268">Common Exceptions</span></span>

<span data-ttu-id="abacd-269">Следующая таблица содержит типичные исключения, которые могут возникнуть при запуске с помощью API массового службы профилей пользователей.</span><span class="sxs-lookup"><span data-stu-id="abacd-269">Following table contains typical exceptions which you could encounter when you start using the User Profile Service bulk API.</span></span>

<span data-ttu-id="abacd-270">Пример исключений</span><span class="sxs-lookup"><span data-stu-id="abacd-270">Example Exception</span></span> | <span data-ttu-id="abacd-271">Сведения</span><span class="sxs-lookup"><span data-stu-id="abacd-271">Details</span></span>
--- | ---
<span data-ttu-id="abacd-272">_Имена свойств [AboutMe] становятся недоступны для изменения пользователем._</span><span class="sxs-lookup"><span data-stu-id="abacd-272">_Property Names [AboutMe] are editable by user._</span></span> | <span data-ttu-id="abacd-273">Это может быть создано с помощью CSOM API, при вызове `ExecuteQuery` метод при отправке задания к клиенту.</span><span class="sxs-lookup"><span data-stu-id="abacd-273">This would be thrown by the CSOM API when you call the `ExecuteQuery` method when submitting the job to your tenant.</span></span> <span data-ttu-id="abacd-274">API-Интерфейс будет проверять, что все свойства, которые в настоящий момент сопоставленные не редактируемое пользователем.</span><span class="sxs-lookup"><span data-stu-id="abacd-274">The API will validate that all properties currently being mapped are NOT user editable.</span></span> <span data-ttu-id="abacd-275">Исключение будет отметить свойство, которое не может использоваться.</span><span class="sxs-lookup"><span data-stu-id="abacd-275">The exception will point out the property which cannot be used.</span></span> <span data-ttu-id="abacd-276">В этом примере мы попытались сопоставление свойства JSON для `AboutMe` свойство в свойствах службы профилей пользователей, но это не допускается с момента `AboutMe` — это редактируемых свойств пользователя.</span><span class="sxs-lookup"><span data-stu-id="abacd-276">In this example, we have tried to map a JSON property to the `AboutMe` property in the User Profile Service properties, but this is not allowed since `AboutMe` is a user editable property.</span></span>
<span data-ttu-id="abacd-277">_InvalidProperty - vesaj@contoso.com свойство «AboutMe» не связан с любого свойства в приложение профилей пользователей._</span><span class="sxs-lookup"><span data-stu-id="abacd-277">_InvalidProperty - vesaj@contoso.com Property 'AboutMe' is not mapped to any property in the user profile application._</span></span> | <span data-ttu-id="abacd-278">Файл данных JSON содержатся свойства, которое не сопоставлен свойства службы профилей пользователей в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="abacd-278">The JSON data file contained a property which has not been mapped to the User Profile Service property in SharePoint Online.</span></span> <span data-ttu-id="abacd-279">Это означает, что файл источника данных содержит свойства, для которых не заданы сопоставления в `propertyMap` параметр.</span><span class="sxs-lookup"><span data-stu-id="abacd-279">This means that the source data file contains properties for which you have not provided a mapping in the `propertyMap` parameter.</span></span> <span data-ttu-id="abacd-280">Необходимо будет иметь определения сопоставления для каждого свойства объекта данных JSON.</span><span class="sxs-lookup"><span data-stu-id="abacd-280">You will need to have a mapping definition for each of the properties in the JSON data object.</span></span>
<span data-ttu-id="abacd-281">_MissingIdentity - идентификатор отсутствует для объекта пользователя_</span><span class="sxs-lookup"><span data-stu-id="abacd-281">_MissingIdentity - The identity is missing for the user object_</span></span> | <span data-ttu-id="abacd-282">Свойство identity не найден в объекте пользователя.</span><span class="sxs-lookup"><span data-stu-id="abacd-282">The identity property could not be found in the user object.</span></span> <span data-ttu-id="abacd-283">Возможная причина в том, что `sourceDataIdProperty` неправильно имеет атрибут `QueueImportProfileProperties` метод.</span><span class="sxs-lookup"><span data-stu-id="abacd-283">The most likely cause is that the `sourceDataIdProperty` attribute is wrongly set for the `QueueImportProfileProperties` method.</span></span> <span data-ttu-id="abacd-284">Убедитесь, имеют свойство right в исходном файле JSON и код или сценарий является назначение соответствующим образом этого атрибута.</span><span class="sxs-lookup"><span data-stu-id="abacd-284">Ensure that you have the right property in the JSON source file and that your code/script is assigning this attribute accordingly.</span></span>
<span data-ttu-id="abacd-285">_Не удалось разрешить IdentityNotResolvable unknown@contoso.com удостоверения пользователя_</span><span class="sxs-lookup"><span data-stu-id="abacd-285">_IdentityNotResolvable unknown@contoso.com User identity cannot be resolved_</span></span> | <span data-ttu-id="abacd-286">Файл данных содержится удостоверение, которое не удалось разрешить или не существует в службе профилей пользователей.</span><span class="sxs-lookup"><span data-stu-id="abacd-286">The data file contained an identity, which could not be resolved or was not present in the User Profile Service.</span></span> <span data-ttu-id="abacd-287">В этом случае профилей пользователей с помощью электронной почты из _unknown@contoso.com_ не удается найти в службе профилей пользователей.</span><span class="sxs-lookup"><span data-stu-id="abacd-287">In this case, the user profile with email of _unknown@contoso.com_ could not be located in the User Profile Service.</span></span>
<span data-ttu-id="abacd-288">_DataFileNotJson - JsonToken EndObject не является допустимым для закрытия JsonType массива. Путь «значение», строка 8, поместите 10._</span><span class="sxs-lookup"><span data-stu-id="abacd-288">_DataFileNotJson - JsonToken EndObject is not valid for closing JsonType Array. Path 'value', line 8, position 10._</span></span> | <span data-ttu-id="abacd-289">В качестве формата формат файла импорта, не является допустимым JSON и не соответствует ожидаемому формату.</span><span class="sxs-lookup"><span data-stu-id="abacd-289">Your import file format is not valid JSON and does not match the expected format.</span></span> 

## <a name="frequently-asked-questions"></a><span data-ttu-id="abacd-290">Frequently Asked Questions</span><span class="sxs-lookup"><span data-stu-id="abacd-290">Frequently Asked Questions</span></span>
<span data-ttu-id="abacd-291"><a name="sectionSection6"> </a></span><span class="sxs-lookup"><span data-stu-id="abacd-291"></span></span>

<span data-ttu-id="abacd-292">**Может выполнять код, использующий разрешения только для приложения только/надстройки**</span><span class="sxs-lookup"><span data-stu-id="abacd-292">**Can I execute the code using app-only/add-in only permissions?**</span></span>

<span data-ttu-id="abacd-293">Да, необходимо зарегистрировать идентификатор клиента и секрет должны иметь возможность выполнять интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="abacd-293">Yes, you’ll need to register the client id and secret to be able to execute the APIs.</span></span> <span data-ttu-id="abacd-294">Так как фактический импорт файла не синхронно с идентификатором вызывающего абонента, это работает без ошибок.</span><span class="sxs-lookup"><span data-stu-id="abacd-294">Since the actual import of the file does not occur synchronously with the identity of the caller, this works without any issues.</span></span>

<span data-ttu-id="abacd-295">**Этот интерфейс API обновление свойств в службе профилей пользователей, но как я создаст этих свойств в клиента?**</span><span class="sxs-lookup"><span data-stu-id="abacd-295">**This API is updating properties in the User Profile Service, but how would I create those properties in the tenant?**</span></span>

<span data-ttu-id="abacd-296">Нет удаленного интерфейса API для создания настраиваемого пользовательского свойства профиля программным способом, поэтому это вручную операция, которой следует выполнить один раз в заданном клиента.</span><span class="sxs-lookup"><span data-stu-id="abacd-296">There’s no remote API to create custom user profile properties programmatically, so this is manual operation which needs to be completed once per given tenant.</span></span> <span data-ttu-id="abacd-297">Можно найти [в этой статье](https://support.office.com/en-us/article/Add-and-edit-user-profile-properties-85091402-737F-4BB9-99A7-BC5F194502A8) представлены инструкции по созданию этих настраиваемых свойств.</span><span class="sxs-lookup"><span data-stu-id="abacd-297">You can refer to [this article](https://support.office.com/en-us/article/Add-and-edit-user-profile-properties-85091402-737F-4BB9-99A7-BC5F194502A8) for instructions on how to create these custom properties.</span></span>

<span data-ttu-id="abacd-298">**Эта возможность доступна в локальном SharePoint?**</span><span class="sxs-lookup"><span data-stu-id="abacd-298">**Is this capability available in on-premises SharePoint?**</span></span>

<span data-ttu-id="abacd-299">К сожалению эта возможность в настоящее время используется только для SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="abacd-299">Unfortunately, this capability is currently only for SharePoint Online.</span></span> <span data-ttu-id="abacd-300">В локальном SharePoint эта возможность будет полезен, но не как критические с момента его можно изменить сопоставление атрибутов в приложении-службе профилей пользователей в локальной.</span><span class="sxs-lookup"><span data-stu-id="abacd-300">In on-premises SharePoint this capability would be useful but not as critical since you can modify the attribute mapping in the on-premises User Profile Service Application.</span></span> <span data-ttu-id="abacd-301">Также можно воспользоваться преимуществами Импорт атрибутов профиля пользователя, с помощью службы Business Connectivity (BCS) в SharePoint 2013.</span><span class="sxs-lookup"><span data-stu-id="abacd-301">You can also take advantage of importing user profile attributes using the Business Connectivity Service (BCS) in SharePoint 2013.</span></span> <span data-ttu-id="abacd-302">Тем не менее этот параметр недоступен в 2016 SharePoint, которая означает, что SharePoint 2016 только параметр в настоящее время для реализации настроек, которые воспользоваться преимуществами пользователя веб-службы профилей.</span><span class="sxs-lookup"><span data-stu-id="abacd-302">However, this option is not available in SharePoint 2016, which means that for SharePoint 2016 the only option currently is to implement customizations which take advantage of the user profile web services.</span></span>

<span data-ttu-id="abacd-303">**Could I use this API for synchronizing user profile property values from my on-premises SharePoint 2013 or 2016 farm(s) to SharePoint Online?**</span><span class="sxs-lookup"><span data-stu-id="abacd-303">**Could I use this API for synchronizing user profile property values from my on-premises SharePoint 2013 or 2016 farm(s) to SharePoint Online?**</span></span>
<span data-ttu-id="abacd-304">Да, локального развертывания SharePoint можно использовать так же, как и любой другой системе источника.</span><span class="sxs-lookup"><span data-stu-id="abacd-304">Yes, on-premises SharePoint can be used just like any other source system.</span></span> <span data-ttu-id="abacd-305">Необходимо экспортировать значения профиля пользователя из локального SharePoint в формате JSON и затем процесс будет точно совпадает с Импорт значения из другой системе.</span><span class="sxs-lookup"><span data-stu-id="abacd-305">You'll need to export the user profile values from your on-premises SharePoint to the JSON file format and then the process would be exactly the same as importing values from any other system.</span></span>

<span data-ttu-id="abacd-306">**Can I import string based, multi-value properties?**</span><span class="sxs-lookup"><span data-stu-id="abacd-306">**Can I import string based, multi-value properties?**</span></span>
<span data-ttu-id="abacd-307">No, this is not currently supported with this API.</span><span class="sxs-lookup"><span data-stu-id="abacd-307">No, this is not currently supported with this API.</span></span>

<span data-ttu-id="abacd-308">**What permissions are required for executing this API??**</span><span class="sxs-lookup"><span data-stu-id="abacd-308">**What permissions are required for executing this API??**</span></span>
<span data-ttu-id="abacd-309">You will need to have Global Admin permissions currently.</span><span class="sxs-lookup"><span data-stu-id="abacd-309">You will need to have Global Admin permissions currently.</span></span> <span data-ttu-id="abacd-310">Недостаточно администрирования SharePoint.</span><span class="sxs-lookup"><span data-stu-id="abacd-310">SharePoint Admin is not sufficient.</span></span>

<span data-ttu-id="abacd-311">**Можно импортировать на основе таксономии**</span><span class="sxs-lookup"><span data-stu-id="abacd-311">**Can I import taxonomy based properties?**</span></span>
<span data-ttu-id="abacd-312">Нет, это не поддерживается в настоящее время этот интерфейс API.</span><span class="sxs-lookup"><span data-stu-id="abacd-312">No, this is not currently supported with this API.</span></span>

<span data-ttu-id="abacd-313">**What if I define a mapping in the code which is not used or have properties in the JSON file which are not mapped?**</span><span class="sxs-lookup"><span data-stu-id="abacd-313">**What if I define a mapping in the code which is not used or have properties in the JSON file which are not mapped?**</span></span>
<span data-ttu-id="abacd-314">If your code/script defines a mapping which is not used or the data file does not contain properties for that mapping, execution will continue without any exceptions and the import will be applied based on the mapped properties.</span><span class="sxs-lookup"><span data-stu-id="abacd-314">If your code/script defines a mapping which is not used or the data file does not contain properties for that mapping, execution will continue without any exceptions and the import will be applied based on the mapped properties.</span></span> <span data-ttu-id="abacd-315">If you, however, have a property in the JSON file which is not mapped, the import process will be aborted and exception details will be provided in the log file for the specific job execution.</span><span class="sxs-lookup"><span data-stu-id="abacd-315">If you, however, have a property in the JSON file which is not mapped, the import process will be aborted and exception details will be provided in the log file for the specific job execution.</span></span>

<span data-ttu-id="abacd-316">**Что делать, если я необходима для обновления настраиваемых свойств, выходящим за пределы ограничения размера этот интерфейс API массового (то есть > файл 2 ГБ или > 500 000 свойств)?**</span><span class="sxs-lookup"><span data-stu-id="abacd-316">**What if I have a need to update custom properties that are beyond the size limitations of this bulk API (i.e. >2 GB file or >500,000 properties)?**</span></span>
<span data-ttu-id="abacd-317">Необходимо пакетных заданий соответствующим образом, запуск нескольких заданий в последовательности (то есть завершения одно задание за раз с максимальное ограничение на этот интерфейс API).</span><span class="sxs-lookup"><span data-stu-id="abacd-317">You would need to batch your jobs accordingly by triggering multiple jobs in sequence (i.e. finishing one job at a time with the maximum limit on this API).</span></span> <span data-ttu-id="abacd-318">You should expect these high bandwidth imports will take a long time to complete.</span><span class="sxs-lookup"><span data-stu-id="abacd-318">You should expect these high bandwidth imports will take a long time to complete.</span></span> <span data-ttu-id="abacd-319">Also, you should optimize the import jobs only for delta changes in custom profile properties rather than importing a full set of values in all jobs.</span><span class="sxs-lookup"><span data-stu-id="abacd-319">Also, you should optimize the import jobs only for delta changes in custom profile properties rather than importing a full set of values in all jobs.</span></span>

<span data-ttu-id="abacd-320">**Which Azure Active Directory attributes are being sync’d to SharePoint Online user profile by default?**</span><span class="sxs-lookup"><span data-stu-id="abacd-320">**Which Azure Active Directory attributes are being sync’d to SharePoint Online user profile by default?**</span></span>
<span data-ttu-id="abacd-321">See the following table for the official list of synchronized attributes and their mapping between Azure Active Directory and the SharePoint Online User Profile Service.</span><span class="sxs-lookup"><span data-stu-id="abacd-321">See the following table for the official list of synchronized attributes and their mapping between Azure Active Directory and the SharePoint Online User Profile Service.</span></span>

<span data-ttu-id="abacd-322">Атрибут Azure каталога</span><span class="sxs-lookup"><span data-stu-id="abacd-322">Azure Directory Attribute</span></span>  | <span data-ttu-id="abacd-323">SharePoint Online Profile Property</span><span class="sxs-lookup"><span data-stu-id="abacd-323">SharePoint Online Profile Property</span></span>
---------|----------
<span data-ttu-id="abacd-324">ObjectSid</span><span class="sxs-lookup"><span data-stu-id="abacd-324">ObjectSid</span></span> | <span data-ttu-id="abacd-325">SPS-SavedSID</span><span class="sxs-lookup"><span data-stu-id="abacd-325">SPS-SavedSID</span></span>
<span data-ttu-id="abacd-326">msonline-UserPrincipalName</span><span class="sxs-lookup"><span data-stu-id="abacd-326">msonline-UserPrincipalName</span></span> | <span data-ttu-id="abacd-327">UserName</span><span class="sxs-lookup"><span data-stu-id="abacd-327">UserName</span></span>
<span data-ttu-id="abacd-328">msonline-UserPrincipalName</span><span class="sxs-lookup"><span data-stu-id="abacd-328">msonline-UserPrincipalName</span></span> | <span data-ttu-id="abacd-329">AccountName</span><span class="sxs-lookup"><span data-stu-id="abacd-329">AccountName</span></span>
<span data-ttu-id="abacd-330">msonline-UserPrincipalName</span><span class="sxs-lookup"><span data-stu-id="abacd-330">msonline-UserPrincipalName</span></span> | <span data-ttu-id="abacd-331">SPS-ClaimID</span><span class="sxs-lookup"><span data-stu-id="abacd-331">SPS-ClaimID</span></span>
<span data-ttu-id="abacd-332">msonline-UserPrincipalName</span><span class="sxs-lookup"><span data-stu-id="abacd-332">msonline-UserPrincipalName</span></span> | <span data-ttu-id="abacd-333">SPS-UserPrincipalName</span><span class="sxs-lookup"><span data-stu-id="abacd-333">SPS-UserPrincipalName</span></span>
<span data-ttu-id="abacd-334">GivenName</span><span class="sxs-lookup"><span data-stu-id="abacd-334">GivenName</span></span> | <span data-ttu-id="abacd-335">FirstName</span><span class="sxs-lookup"><span data-stu-id="abacd-335">FirstName</span></span>
<span data-ttu-id="abacd-336">sn</span><span class="sxs-lookup"><span data-stu-id="abacd-336">sn</span></span> | <span data-ttu-id="abacd-337">LastName</span><span class="sxs-lookup"><span data-stu-id="abacd-337">LastName</span></span>
<span data-ttu-id="abacd-338">Manager</span><span class="sxs-lookup"><span data-stu-id="abacd-338">Manager</span></span> | <span data-ttu-id="abacd-339">Manager</span><span class="sxs-lookup"><span data-stu-id="abacd-339">Manager</span></span>
<span data-ttu-id="abacd-340">DisplayName</span><span class="sxs-lookup"><span data-stu-id="abacd-340">DisplayName</span></span> | <span data-ttu-id="abacd-341">PreferredName</span><span class="sxs-lookup"><span data-stu-id="abacd-341">PreferredName</span></span>
<span data-ttu-id="abacd-342">telephoneNumber</span><span class="sxs-lookup"><span data-stu-id="abacd-342">telephoneNumber</span></span> | <span data-ttu-id="abacd-343">WorkPhone</span><span class="sxs-lookup"><span data-stu-id="abacd-343">WorkPhone</span></span>
<span data-ttu-id="abacd-344">proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="abacd-344">proxyAddresses</span></span> | <span data-ttu-id="abacd-345">WorkEmail</span><span class="sxs-lookup"><span data-stu-id="abacd-345">WorkEmail</span></span>
<span data-ttu-id="abacd-346">proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="abacd-346">proxyAddresses</span></span> | <span data-ttu-id="abacd-347">SPS-SIPAddress</span><span class="sxs-lookup"><span data-stu-id="abacd-347">SPS-SIPAddress</span></span>
<span data-ttu-id="abacd-348">PhysicalDeliveryOfficeName</span><span class="sxs-lookup"><span data-stu-id="abacd-348">PhysicalDeliveryOfficeName</span></span> | <span data-ttu-id="abacd-349">Office</span><span class="sxs-lookup"><span data-stu-id="abacd-349">Office</span></span>
<span data-ttu-id="abacd-350">Заголовок</span><span class="sxs-lookup"><span data-stu-id="abacd-350">Title</span></span> | <span data-ttu-id="abacd-351">Заголовок</span><span class="sxs-lookup"><span data-stu-id="abacd-351">Title</span></span>
<span data-ttu-id="abacd-352">Заголовок</span><span class="sxs-lookup"><span data-stu-id="abacd-352">Title</span></span> | <span data-ttu-id="abacd-353">SPS-JobTitle</span><span class="sxs-lookup"><span data-stu-id="abacd-353">SPS-JobTitle</span></span>
<span data-ttu-id="abacd-354">Department</span><span class="sxs-lookup"><span data-stu-id="abacd-354">Department</span></span> | <span data-ttu-id="abacd-355">Department</span><span class="sxs-lookup"><span data-stu-id="abacd-355">Department</span></span>
<span data-ttu-id="abacd-356">Department</span><span class="sxs-lookup"><span data-stu-id="abacd-356">Department</span></span> | <span data-ttu-id="abacd-357">SPS-Department</span><span class="sxs-lookup"><span data-stu-id="abacd-357">SPS-Department</span></span>
<span data-ttu-id="abacd-358">ObjectGuid</span><span class="sxs-lookup"><span data-stu-id="abacd-358">ObjectGuid</span></span> | <span data-ttu-id="abacd-359">ADGuid</span><span class="sxs-lookup"><span data-stu-id="abacd-359">ADGuid</span></span>
<span data-ttu-id="abacd-360">WWWHomePage</span><span class="sxs-lookup"><span data-stu-id="abacd-360">WWWHomePage</span></span> | <span data-ttu-id="abacd-361">PublicSiteRedirect</span><span class="sxs-lookup"><span data-stu-id="abacd-361">PublicSiteRedirect</span></span>
<span data-ttu-id="abacd-362">DistinguishedName</span><span class="sxs-lookup"><span data-stu-id="abacd-362">DistinguishedName</span></span> | <span data-ttu-id="abacd-363">SPS-DistinguishedName</span><span class="sxs-lookup"><span data-stu-id="abacd-363">SPS-DistinguishedName</span></span>
<span data-ttu-id="abacd-364">msOnline-ObjectId</span><span class="sxs-lookup"><span data-stu-id="abacd-364">msOnline-ObjectId</span></span> | <span data-ttu-id="abacd-365">msOnline-ObjectId</span><span class="sxs-lookup"><span data-stu-id="abacd-365">msOnline-ObjectId</span></span>
<span data-ttu-id="abacd-366">PreferredLanguage</span><span class="sxs-lookup"><span data-stu-id="abacd-366">PreferredLanguage</span></span> | <span data-ttu-id="abacd-367">SPS-MUILanguages</span><span class="sxs-lookup"><span data-stu-id="abacd-367">SPS-MUILanguages</span></span>
<span data-ttu-id="abacd-368">msExchHideFromAddressList</span><span class="sxs-lookup"><span data-stu-id="abacd-368">msExchHideFromAddressList</span></span> | <span data-ttu-id="abacd-369">SPS-HideFromAddressLists</span><span class="sxs-lookup"><span data-stu-id="abacd-369">SPS-HideFromAddressLists</span></span>
<span data-ttu-id="abacd-370">msExchRecipientTypeDetails</span><span class="sxs-lookup"><span data-stu-id="abacd-370">msExchRecipientTypeDetails</span></span> | <span data-ttu-id="abacd-371">SPS-RecipientTypeDetails</span><span class="sxs-lookup"><span data-stu-id="abacd-371">SPS-RecipientTypeDetails</span></span>
<span data-ttu-id="abacd-372">msonline-groupType</span><span class="sxs-lookup"><span data-stu-id="abacd-372">msonline-groupType</span></span> | <span data-ttu-id="abacd-373">IsUnifiedGroup</span><span class="sxs-lookup"><span data-stu-id="abacd-373">IsUnifiedGroup</span></span>
<span data-ttu-id="abacd-374">msOnline-IsPublic</span><span class="sxs-lookup"><span data-stu-id="abacd-374">msOnline-IsPublic</span></span> | <span data-ttu-id="abacd-375">IsPublic</span><span class="sxs-lookup"><span data-stu-id="abacd-375">IsPublic</span></span>
<span data-ttu-id="abacd-376">msOnline-ObjectId</span><span class="sxs-lookup"><span data-stu-id="abacd-376">msOnline-ObjectId</span></span> | <span data-ttu-id="abacd-377">msOnline-ObjectId</span><span class="sxs-lookup"><span data-stu-id="abacd-377">msOnline-ObjectId</span></span>
<span data-ttu-id="abacd-378">msOnline-UserType</span><span class="sxs-lookup"><span data-stu-id="abacd-378">msOnline-UserType</span></span> | <span data-ttu-id="abacd-379">SPS-UserType</span><span class="sxs-lookup"><span data-stu-id="abacd-379">SPS-UserType</span></span>
<span data-ttu-id="abacd-380">GroupType</span><span class="sxs-lookup"><span data-stu-id="abacd-380">GroupType</span></span> | <span data-ttu-id="abacd-381">GroupType</span><span class="sxs-lookup"><span data-stu-id="abacd-381">GroupType</span></span>
<span data-ttu-id="abacd-382">SPO-IsSharePointOnlineObject</span><span class="sxs-lookup"><span data-stu-id="abacd-382">SPO-IsSharePointOnlineObject</span></span> | <span data-ttu-id="abacd-383">SPO-IsSPO</span><span class="sxs-lookup"><span data-stu-id="abacd-383">SPO-IsSPO</span></span>

