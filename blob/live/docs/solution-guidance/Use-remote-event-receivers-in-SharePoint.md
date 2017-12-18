---
title: Use remote event receivers in SharePoint
ms.date: 11/03/2017
ms.openlocfilehash: 73ad90bdcf96c2ca31e94e76d9c22bb196b69712
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="use-remote-event-receivers-in-sharepoint"></a><span data-ttu-id="433b0-102">Use remote event receivers in SharePoint</span><span class="sxs-lookup"><span data-stu-id="433b0-102">Use remote event receivers in SharePoint</span></span>

<span data-ttu-id="433b0-103">Use remote event receivers to handle events in the SharePoint add-in model.</span><span class="sxs-lookup"><span data-stu-id="433b0-103">Use remote event receivers to handle events in the SharePoint add-in model.</span></span> <span data-ttu-id="433b0-104">Use AppInstalled and AppUninstalling events to set up or remove SharePoint objects and other event receivers your add-in needs.</span><span class="sxs-lookup"><span data-stu-id="433b0-104">Use AppInstalled and AppUninstalling events to set up or remove SharePoint objects and other event receivers your add-in needs.</span></span>

<span data-ttu-id="433b0-105">_**Applies to:** add-ins for SharePoint | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="433b0-105">_**Applies to:** add-ins for SharePoint | SharePoint 2013 | SharePoint Online_</span></span>

><span data-ttu-id="433b0-106">**Important** As of January 2017 SharePoint Online does support list webhooks which you can use instead of "-ed" remote event receivers.</span><span class="sxs-lookup"><span data-stu-id="433b0-106">**Important** As of January 2017 SharePoint Online does support list webhooks which you can use instead of "-ed" remote event receivers.</span></span> <span data-ttu-id="433b0-107">Checkout [Overview of SharePoint webhooks](https://dev.office.com/sharepoint/docs/apis/webhooks/overview-sharepoint-webhooks) to learn more about webhooks.</span><span class="sxs-lookup"><span data-stu-id="433b0-107">Checkout [Overview of SharePoint webhooks](https://dev.office.com/sharepoint/docs/apis/webhooks/overview-sharepoint-webhooks) to learn more about webhooks.</span></span> <span data-ttu-id="433b0-108">Also note that several webhook samples are available from the [sp-dev-samples](https://github.com/SharePoint/sp-dev-samples/tree/master/Samples) GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="433b0-108">Also note that several webhook samples are available from the [sp-dev-samples](https://github.com/SharePoint/sp-dev-samples/tree/master/Samples) GitHub repository.</span></span>

<span data-ttu-id="433b0-109">The  [Core.EventReceivers](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EventReceivers) sample shows how to use a provider-hosted add-in with a remote event receiver to handle the AppInstalled and AppUninstalling events.</span><span class="sxs-lookup"><span data-stu-id="433b0-109">The  [Core.EventReceivers](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EventReceivers) sample shows how to use a provider-hosted add-in with a remote event receiver to handle the AppInstalled and AppUninstalling events.</span></span> <span data-ttu-id="433b0-110">The AppInstalled and AppUninstalling events set up and remove SharePoint objects that the add-in uses when it runs.</span><span class="sxs-lookup"><span data-stu-id="433b0-110">The AppInstalled and AppUninstalling events set up and remove SharePoint objects that the add-in uses when it runs.</span></span> <span data-ttu-id="433b0-111">Additionally, the AppInstalled event handler adds the ItemAdded event handler to a list.</span><span class="sxs-lookup"><span data-stu-id="433b0-111">Additionally, the AppInstalled event handler adds the ItemAdded event handler to a list.</span></span> <span data-ttu-id="433b0-112">Use this solution if you want to:</span><span class="sxs-lookup"><span data-stu-id="433b0-112">Use this solution if you want to:</span></span>

- <span data-ttu-id="433b0-113">Configure your add-in on first run using the AppInstalled event to set up various SharePoint objects or additional event receivers that your add-in works with.</span><span class="sxs-lookup"><span data-stu-id="433b0-113">Configure your add-in on first run using the AppInstalled event to set up various SharePoint objects or additional event receivers that your add-in works with.</span></span>
    
- <span data-ttu-id="433b0-114">Replace event receivers implemented using fully trusted code solutions.</span><span class="sxs-lookup"><span data-stu-id="433b0-114">Replace event receivers implemented using fully trusted code solutions.</span></span> <span data-ttu-id="433b0-115">In fully trusted code solutions, you can run event receivers on the SharePoint server.</span><span class="sxs-lookup"><span data-stu-id="433b0-115">In fully trusted code solutions, you can run event receivers on the SharePoint server.</span></span> <span data-ttu-id="433b0-116">In the new SharePoint add-in model, because you cannot run the event receiver on the SharePoint server, you need to implement a remote event receiver on a web server.</span><span class="sxs-lookup"><span data-stu-id="433b0-116">In the new SharePoint add-in model, because you cannot run the event receiver on the SharePoint server, you need to implement a remote event receiver on a web server.</span></span>
    
- <span data-ttu-id="433b0-117">Receive notifications of changes occuring in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="433b0-117">Receive notifications of changes occuring in SharePoint.</span></span> <span data-ttu-id="433b0-118">For example, when a new item is added to a list, you want to perform a task.</span><span class="sxs-lookup"><span data-stu-id="433b0-118">For example, when a new item is added to a list, you want to perform a task.</span></span>

- <span data-ttu-id="433b0-119">Complement your change log solution.</span><span class="sxs-lookup"><span data-stu-id="433b0-119">Complement your change log solution.</span></span> <span data-ttu-id="433b0-120">Using the remote event receiver pattern with a change log pattern provides a more reliable architecture for handling all changes made to SharePoint content databases, site collections, sites, or lists.</span><span class="sxs-lookup"><span data-stu-id="433b0-120">Using the remote event receiver pattern with a change log pattern provides a more reliable architecture for handling all changes made to SharePoint content databases, site collections, sites, or lists.</span></span> <span data-ttu-id="433b0-121">Remote event receivers run immediately, but because they run on a remote server, you might encounter a communication failure.</span><span class="sxs-lookup"><span data-stu-id="433b0-121">Remote event receivers run immediately, but because they run on a remote server, you might encounter a communication failure.</span></span> <span data-ttu-id="433b0-122">The change log pattern ensures that all changes are available for processing, but the application processing the changes usually runs on a schedule (for example, a timer job).</span><span class="sxs-lookup"><span data-stu-id="433b0-122">The change log pattern ensures that all changes are available for processing, but the application processing the changes usually runs on a schedule (for example, a timer job).</span></span> <span data-ttu-id="433b0-123">This means that changes are not processed immediately.</span><span class="sxs-lookup"><span data-stu-id="433b0-123">This means that changes are not processed immediately.</span></span> <span data-ttu-id="433b0-124">If you use these two patterns together, ensure you use a mechanism to prevent processing the same change twice.</span><span class="sxs-lookup"><span data-stu-id="433b0-124">If you use these two patterns together, ensure you use a mechanism to prevent processing the same change twice.</span></span> <span data-ttu-id="433b0-125">For more information, see [Query SharePoint change log with ChangeQuery and ChangeToken](query-sharepoint-change-log-with-changequery-and-changeToken.md).</span><span class="sxs-lookup"><span data-stu-id="433b0-125">For more information, see [Query SharePoint change log with ChangeQuery and ChangeToken](query-sharepoint-change-log-with-changequery-and-changeToken.md).</span></span>

> [!NOTE] 
> <span data-ttu-id="433b0-126">SharePoint-hosted add-ins do not support remote event receivers.</span><span class="sxs-lookup"><span data-stu-id="433b0-126">SharePoint-hosted add-ins do not support remote event receivers.</span></span> <span data-ttu-id="433b0-127">To use remote event receivers, you need to use a provider-hosted add-in.</span><span class="sxs-lookup"><span data-stu-id="433b0-127">To use remote event receivers, you need to use a provider-hosted add-in.</span></span> <span data-ttu-id="433b0-128">You should not use remote event receivers for synchronization scenarios, or for long running processes.</span><span class="sxs-lookup"><span data-stu-id="433b0-128">You should not use remote event receivers for synchronization scenarios, or for long running processes.</span></span> <span data-ttu-id="433b0-129">For more information, see  [How to: Create an add-in event receiver](https://msdn.microsoft.com/library/office/jj220052.aspx).</span><span class="sxs-lookup"><span data-stu-id="433b0-129">For more information, see  [How to: Create an add-in event receiver](https://msdn.microsoft.com/library/office/jj220052.aspx).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="433b0-130">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="433b0-130">Before you begin</span></span>
<span data-ttu-id="433b0-131"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="433b0-131"></span></span>

<span data-ttu-id="433b0-132">To get started, download the  [Core.EventReceivers](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EventReceivers) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span><span class="sxs-lookup"><span data-stu-id="433b0-132">To get started, download the  [Core.EventReceivers](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EventReceivers) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

<span data-ttu-id="433b0-133">Before you run this add-in, do the following:</span><span class="sxs-lookup"><span data-stu-id="433b0-133">Before you run this add-in, do the following:</span></span>

1. <span data-ttu-id="433b0-134">In the properties on the Core.EventReceivers project, verify that  **Handle App Installed** and **Handle App Uninstalling** is set to **True**.</span><span class="sxs-lookup"><span data-stu-id="433b0-134">In the properties on the Core.EventReceivers project, verify that  **Handle App Installed** and **Handle App Uninstalling** is set to **True**.</span></span> <span data-ttu-id="433b0-135">Setting  **Handle App Installed** and **Handle App Uninstalling** to **True** creates a WCF service that defines the event handler for the **AppInstalled** and **AppUninstalling** event.</span><span class="sxs-lookup"><span data-stu-id="433b0-135">Setting  **Handle App Installed** and **Handle App Uninstalling** to **True** creates a WCF service that defines the event handler for the **AppInstalled** and **AppUninstalling** event.</span></span> <span data-ttu-id="433b0-136">In Core.EventReceivers, open the shortcut menu (right-click) on AppManifest.xml, and choose **Properties**.</span><span class="sxs-lookup"><span data-stu-id="433b0-136">In Core.EventReceivers, open the shortcut menu (right-click) on AppManifest.xml, and choose **Properties**.</span></span> <span data-ttu-id="433b0-137">The  **InstalledEventEndpoint** and **UninstallingEventEndpoint** point to the remote event receiver that handles the **AppInstalled** and **AppUninstalling** events.</span><span class="sxs-lookup"><span data-stu-id="433b0-137">The  **InstalledEventEndpoint** and **UninstallingEventEndpoint** point to the remote event receiver that handles the **AppInstalled** and **AppUninstalling** events.</span></span>
    
2. <span data-ttu-id="433b0-138">Attaching a remote event receiver to an object in the host web usually requires  **Manage** permission for that object only.</span><span class="sxs-lookup"><span data-stu-id="433b0-138">Attaching a remote event receiver to an object in the host web usually requires  **Manage** permission for that object only.</span></span> <span data-ttu-id="433b0-139">For example, when attaching an event receiver to an existing list, the add-in requires **Manage** permission on the **List** only.</span><span class="sxs-lookup"><span data-stu-id="433b0-139">For example, when attaching an event receiver to an existing list, the add-in requires **Manage** permission on the **List** only.</span></span> <span data-ttu-id="433b0-140">This code sample requires **Manage** permissions on the **Web** because it adds a list and activates a feature on the host web.</span><span class="sxs-lookup"><span data-stu-id="433b0-140">This code sample requires **Manage** permissions on the **Web** because it adds a list and activates a feature on the host web.</span></span> <span data-ttu-id="433b0-141">To set manage permissions on the web:</span><span class="sxs-lookup"><span data-stu-id="433b0-141">To set manage permissions on the web:</span></span>
    
    1. <span data-ttu-id="433b0-142">Double click Core.EventReceivers\AppManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="433b0-142">Double click Core.EventReceivers\AppManifest.xml.</span></span>
    
    2. <span data-ttu-id="433b0-143">Choose  **Permissions**.</span><span class="sxs-lookup"><span data-stu-id="433b0-143">Choose  **Permissions**.</span></span>
    
    3. <span data-ttu-id="433b0-144">Verify that  **Scope** is set to **Web**, and  **Permission** is set to **Manage**.</span><span class="sxs-lookup"><span data-stu-id="433b0-144">Verify that  **Scope** is set to **Web**, and  **Permission** is set to **Manage**.</span></span>
    
3. <span data-ttu-id="433b0-145">To run this code sample, you need an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="433b0-145">To run this code sample, you need an Azure subscription.</span></span> <span data-ttu-id="433b0-146">To sign up for a trial, see  [Free one-month trial](http://azure.microsoft.com/en-us/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="433b0-146">To sign up for a trial, see  [Free one-month trial](http://azure.microsoft.com/en-us/pricing/free-trial/).</span></span>
    
4. <span data-ttu-id="433b0-147">Create an Azure Service Bus Namespace with ACS Support.</span><span class="sxs-lookup"><span data-stu-id="433b0-147">Create an Azure Service Bus Namespace with ACS Support.</span></span>
    
    1. <span data-ttu-id="433b0-148">Install Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="433b0-148">Install Azure PowerShell.</span></span> <span data-ttu-id="433b0-149">For more information, see  [How to: Install Azure PowerShell](http://azure.microsoft.com/en-us/documentation/articles/powershell-install-configure/#Install).</span><span class="sxs-lookup"><span data-stu-id="433b0-149">For more information, see  [How to: Install Azure PowerShell](http://azure.microsoft.com/en-us/documentation/articles/powershell-install-configure/#Install).</span></span>
    
    2. <span data-ttu-id="433b0-150">Start  **Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="433b0-150">Start  **Azure PowerShell**.</span></span>
    
    3. <span data-ttu-id="433b0-151">Enter  **Add-AzureAccount**.</span><span class="sxs-lookup"><span data-stu-id="433b0-151">Enter  **Add-AzureAccount**.</span></span>
    
    4. <span data-ttu-id="433b0-152">Enter your email address in the  **Sign in to Windows Azure** dialog, and then choose **Continue**.</span><span class="sxs-lookup"><span data-stu-id="433b0-152">Enter your email address in the  **Sign in to Windows Azure** dialog, and then choose **Continue**.</span></span>
    
    5. <span data-ttu-id="433b0-153">Enter your password, and then choose  **Sign in**.</span><span class="sxs-lookup"><span data-stu-id="433b0-153">Enter your password, and then choose  **Sign in**.</span></span>
    
    6. <span data-ttu-id="433b0-154">Create a new service bus namespace using the following PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="433b0-154">Create a new service bus namespace using the following PowerShell cmdlet.</span></span>
    
        ```powershell
        New-AzureSBNamespace NamespaceNameRegion -CreateACSNamespace $true -NamespaceType Messaging
        
        ```
    
       <span data-ttu-id="433b0-155">Где:</span><span class="sxs-lookup"><span data-stu-id="433b0-155">Where:</span></span>
    
       -  <span data-ttu-id="433b0-156">_NamespaceName_ is the name of your Azure Service Bus namespace.</span><span class="sxs-lookup"><span data-stu-id="433b0-156">_NamespaceName_ is the name of your Azure Service Bus namespace.</span></span>
    
       -  <span data-ttu-id="433b0-157">_Region_ is the region closest to you.</span><span class="sxs-lookup"><span data-stu-id="433b0-157">_Region_ is the region closest to you.</span></span> <span data-ttu-id="433b0-158">For example, you may enter **"West US"**.</span><span class="sxs-lookup"><span data-stu-id="433b0-158">For example, you may enter **"West US"**.</span></span> <span data-ttu-id="433b0-159">You must include the region name in double quotes.</span><span class="sxs-lookup"><span data-stu-id="433b0-159">You must include the region name in double quotes.</span></span>
    
    7. <span data-ttu-id="433b0-160">Return to your Azure Management Portal.</span><span class="sxs-lookup"><span data-stu-id="433b0-160">Return to your Azure Management Portal.</span></span> <span data-ttu-id="433b0-161">Choose  **SERVICE BUS**, and then choose the namespace name you entered.</span><span class="sxs-lookup"><span data-stu-id="433b0-161">Choose  **SERVICE BUS**, and then choose the namespace name you entered.</span></span>
    
    8. <span data-ttu-id="433b0-162">Choose  **Manage Connection Strings**, and then in  **ACS CONNECTION STRING**, choose the copy button.</span><span class="sxs-lookup"><span data-stu-id="433b0-162">Choose  **Manage Connection Strings**, and then in  **ACS CONNECTION STRING**, choose the copy button.</span></span>
    
    9. <span data-ttu-id="433b0-163">Return to Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="433b0-163">Return to Visual Studio.</span></span>
    
    10. <span data-ttu-id="433b0-164">Right-click Core.EventReceivers >  **Properties** > **SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="433b0-164">Right-click Core.EventReceivers >  **Properties** > **SharePoint**.</span></span>
    
    11. <span data-ttu-id="433b0-165">Select  **Enable debugging via Microsoft Azure Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="433b0-165">Select  **Enable debugging via Microsoft Azure Service Bus**.</span></span>
    
    12. <span data-ttu-id="433b0-166">In  **Microsoft Azure Service Bus connection string**, paste the ACS Connection String.</span><span class="sxs-lookup"><span data-stu-id="433b0-166">In  **Microsoft Azure Service Bus connection string**, paste the ACS Connection String.</span></span>
    
    13. <span data-ttu-id="433b0-167">Choose  **Save**.</span><span class="sxs-lookup"><span data-stu-id="433b0-167">Choose  **Save**.</span></span>
    
5. <span data-ttu-id="433b0-168">Run the code sample, and perform the following additional steps:</span><span class="sxs-lookup"><span data-stu-id="433b0-168">Run the code sample, and perform the following additional steps:</span></span>
    
    - <span data-ttu-id="433b0-169">Click  **Trust It** in the **Grant permissions to the app** window.</span><span class="sxs-lookup"><span data-stu-id="433b0-169">Click  **Trust It** in the **Grant permissions to the app** window.</span></span>
    
    - <span data-ttu-id="433b0-170">Close the  **Grant permissions to the app** window.</span><span class="sxs-lookup"><span data-stu-id="433b0-170">Close the  **Grant permissions to the app** window.</span></span>
    
    - <span data-ttu-id="433b0-171">When installation of the add-in and WCF service is completed, your browser will open.</span><span class="sxs-lookup"><span data-stu-id="433b0-171">When installation of the add-in and WCF service is completed, your browser will open.</span></span>
    
    - <span data-ttu-id="433b0-172">Sign in to your Office 365 site.</span><span class="sxs-lookup"><span data-stu-id="433b0-172">Sign in to your Office 365 site.</span></span> <span data-ttu-id="433b0-173">The start page of the Core.EventReceivers add-in is displayed.</span><span class="sxs-lookup"><span data-stu-id="433b0-173">The start page of the Core.EventReceivers add-in is displayed.</span></span>

## <a name="use-the-coreeventreceivers-add-in"></a><span data-ttu-id="433b0-174">Use the Core.EventReceivers add-in</span><span class="sxs-lookup"><span data-stu-id="433b0-174">Use the Core.EventReceivers add-in</span></span>
<span data-ttu-id="433b0-175"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="433b0-175"></span></span>

<span data-ttu-id="433b0-176">To see a demo of the Core.EventReceivers code sample:</span><span class="sxs-lookup"><span data-stu-id="433b0-176">To see a demo of the Core.EventReceivers code sample:</span></span>

1. <span data-ttu-id="433b0-177">Run the sample, and on the start page, choose  **Back to Site**.</span><span class="sxs-lookup"><span data-stu-id="433b0-177">Run the sample, and on the start page, choose  **Back to Site**.</span></span>
    
2. <span data-ttu-id="433b0-178">Choose  **Site Contents**.</span><span class="sxs-lookup"><span data-stu-id="433b0-178">Choose  **Site Contents**.</span></span>
    
3. <span data-ttu-id="433b0-179">Choose  **Remote Event Receiver Jobs**.</span><span class="sxs-lookup"><span data-stu-id="433b0-179">Choose  **Remote Event Receiver Jobs**.</span></span>
    
4. <span data-ttu-id="433b0-180">Choose  **new item**.</span><span class="sxs-lookup"><span data-stu-id="433b0-180">Choose  **new item**.</span></span>
    
5. <span data-ttu-id="433b0-181">In  **Title**, enter  **Contoso**, and in  **Description** enter **Contoso test**.</span><span class="sxs-lookup"><span data-stu-id="433b0-181">In  **Title**, enter  **Contoso**, and in  **Description** enter **Contoso test**.</span></span>
    
6. <span data-ttu-id="433b0-182">Return to the list and refresh the page.</span><span class="sxs-lookup"><span data-stu-id="433b0-182">Return to the list and refresh the page.</span></span>
    
7. <span data-ttu-id="433b0-183">Verify that the description of the newly added item was updated to  **Contoso test Updated by ReR 192336**, where  **192336** is a timestamp.</span><span class="sxs-lookup"><span data-stu-id="433b0-183">Verify that the description of the newly added item was updated to  **Contoso test Updated by ReR 192336**, where  **192336** is a timestamp.</span></span>
    
<span data-ttu-id="433b0-184">In Services/AppEventReceiver.cs,  **AppEventReceiver** implements the **IRemoteEventService** interface.</span><span class="sxs-lookup"><span data-stu-id="433b0-184">In Services/AppEventReceiver.cs,  **AppEventReceiver** implements the **IRemoteEventService** interface.</span></span> <span data-ttu-id="433b0-185">This code sample provides an implementation for the **ProcessEvent** method because it uses synchronous events.</span><span class="sxs-lookup"><span data-stu-id="433b0-185">This code sample provides an implementation for the **ProcessEvent** method because it uses synchronous events.</span></span> <span data-ttu-id="433b0-186">If you use asynchronous events, you need to provide an implementation for the **ProcessOneWayEvent** method.</span><span class="sxs-lookup"><span data-stu-id="433b0-186">If you use asynchronous events, you need to provide an implementation for the **ProcessOneWayEvent** method.</span></span>

<span data-ttu-id="433b0-187">The  **ProcessEvent** handles the following **SPRemoteEventType** remote events:</span><span class="sxs-lookup"><span data-stu-id="433b0-187">The  **ProcessEvent** handles the following **SPRemoteEventType** remote events:</span></span>

-  <span data-ttu-id="433b0-188">**AppInstalled** events when installing the add-in.</span><span class="sxs-lookup"><span data-stu-id="433b0-188">**AppInstalled** events when installing the add-in.</span></span> <span data-ttu-id="433b0-189">When an **AppInstalled** event occurs, **ProcessEvent** calls **HandleAppInstalled**.</span><span class="sxs-lookup"><span data-stu-id="433b0-189">When an **AppInstalled** event occurs, **ProcessEvent** calls **HandleAppInstalled**.</span></span>
    
-  <span data-ttu-id="433b0-190">**AppUninstalling** events when uninstalling the add-in.</span><span class="sxs-lookup"><span data-stu-id="433b0-190">**AppUninstalling** events when uninstalling the add-in.</span></span> <span data-ttu-id="433b0-191">When an **AppUninstalling** event occurs, **ProcessEvent** calls **HandleAppUninstalling**.</span><span class="sxs-lookup"><span data-stu-id="433b0-191">When an **AppUninstalling** event occurs, **ProcessEvent** calls **HandleAppUninstalling**.</span></span> <span data-ttu-id="433b0-192">The  **AppUninstalling** event only runs when a user completely removes the add-in either by deleting the add-in from the site recycle bin (for end users) or by removing the add-in from the **Apps in testing** list (for developers).</span><span class="sxs-lookup"><span data-stu-id="433b0-192">The  **AppUninstalling** event only runs when a user completely removes the add-in either by deleting the add-in from the site recycle bin (for end users) or by removing the add-in from the **Apps in testing** list (for developers).</span></span>
    
-  <span data-ttu-id="433b0-193">**ItemAdded** events when an item is added to a list.</span><span class="sxs-lookup"><span data-stu-id="433b0-193">**ItemAdded** events when an item is added to a list.</span></span> <span data-ttu-id="433b0-194">When an **ItemAdded** event occurs, **ProcessEvent** calls **HandleItemAdded**.</span><span class="sxs-lookup"><span data-stu-id="433b0-194">When an **ItemAdded** event occurs, **ProcessEvent** calls **HandleItemAdded**.</span></span>

> [!NOTE] 
> <span data-ttu-id="433b0-195">In the Core.EventReceiver project properties, only  **Handle App Installed** and **Handle App Uninstalling** properties are available.</span><span class="sxs-lookup"><span data-stu-id="433b0-195">In the Core.EventReceiver project properties, only  **Handle App Installed** and **Handle App Uninstalling** properties are available.</span></span> <span data-ttu-id="433b0-196">This code sample shows how you can add the **ItemAdded** event handler to a list on the host web by using the **AppInstalled** event during add-in installation.</span><span class="sxs-lookup"><span data-stu-id="433b0-196">This code sample shows how you can add the **ItemAdded** event handler to a list on the host web by using the **AppInstalled** event during add-in installation.</span></span>

> [!NOTE] 
> <span data-ttu-id="433b0-197">The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span><span class="sxs-lookup"><span data-stu-id="433b0-197">The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```C#
public SPRemoteEventResult ProcessEvent(SPRemoteEventProperties properties)
        {

            SPRemoteEventResult result = new SPRemoteEventResult();

            switch (properties.EventType)
            {
                case SPRemoteEventType.AppInstalled:
                    HandleAppInstalled(properties);
                    break;
                case SPRemoteEventType.AppUninstalling:
                    HandleAppUninstalling(properties);
                    break;
                case SPRemoteEventType.ItemAdded:
                    HandleItemAdded(properties);
                    break;
            }


            return result;
        }
```

<span data-ttu-id="433b0-198">**HandleAppInstalled** calls **RemoteEventReceiverManager.AssociateRemoteEventsToHostWeb** in RemoteEventReceiverManager.cs.</span><span class="sxs-lookup"><span data-stu-id="433b0-198">**HandleAppInstalled** calls **RemoteEventReceiverManager.AssociateRemoteEventsToHostWeb** in RemoteEventReceiverManager.cs.</span></span>

```C#
 private void HandleAppInstalled(SPRemoteEventProperties properties)
        {
            using (ClientContext clientContext =
                TokenHelper.CreateAppEventClientContext(properties, false))
            {
                if (clientContext != null)
                {
                    new RemoteEventReceiverManager().AssociateRemoteEventsToHostWeb(clientContext);
                }
            }
        }
```

<span data-ttu-id="433b0-199">**AssociateRemoteEventsToHostWeb** creates or enables various SharePoint objects that the Core.EventReceivers add-in uses.</span><span class="sxs-lookup"><span data-stu-id="433b0-199">**AssociateRemoteEventsToHostWeb** creates or enables various SharePoint objects that the Core.EventReceivers add-in uses.</span></span> <span data-ttu-id="433b0-200">Your requirements might differ.</span><span class="sxs-lookup"><span data-stu-id="433b0-200">Your requirements might differ.</span></span> <span data-ttu-id="433b0-201">**AssociateRemoteEventsToHostWeb** does the following:</span><span class="sxs-lookup"><span data-stu-id="433b0-201">**AssociateRemoteEventsToHostWeb** does the following:</span></span>

- <span data-ttu-id="433b0-202">Enables the Push Notification feature by using  **Web.Features.Add**.</span><span class="sxs-lookup"><span data-stu-id="433b0-202">Enables the Push Notification feature by using  **Web.Features.Add**.</span></span>
    
- <span data-ttu-id="433b0-203">Uses the  **clientContext** object to search for a list.</span><span class="sxs-lookup"><span data-stu-id="433b0-203">Uses the  **clientContext** object to search for a list.</span></span> <span data-ttu-id="433b0-204">If the list does not exist, **CreateJobsList** creates the list.</span><span class="sxs-lookup"><span data-stu-id="433b0-204">If the list does not exist, **CreateJobsList** creates the list.</span></span> <span data-ttu-id="433b0-205">If the list exists, **List.EventReceivers** is used to search for an existing event receiver whose name is **ItemAddedEvent**.</span><span class="sxs-lookup"><span data-stu-id="433b0-205">If the list exists, **List.EventReceivers** is used to search for an existing event receiver whose name is **ItemAddedEvent**.</span></span>
    
- <span data-ttu-id="433b0-206">If the  **ItemAddedEvent** event receiver does not exist:</span><span class="sxs-lookup"><span data-stu-id="433b0-206">If the  **ItemAddedEvent** event receiver does not exist:</span></span>
    
    - <span data-ttu-id="433b0-207">Instantiates a new  **EventReceiverDefinitionCreationInformation** object to create the new remote event receiver.</span><span class="sxs-lookup"><span data-stu-id="433b0-207">Instantiates a new  **EventReceiverDefinitionCreationInformation** object to create the new remote event receiver.</span></span> <span data-ttu-id="433b0-208">The **ItemAdded** event receiver type is added to **EventReceiverDefinitionCreationInformation.EventType**.</span><span class="sxs-lookup"><span data-stu-id="433b0-208">The **ItemAdded** event receiver type is added to **EventReceiverDefinitionCreationInformation.EventType**.</span></span>
    
    - <span data-ttu-id="433b0-209">Sets the  **EventReceiverDefinitionCreationInformation.ReceiverURL** to the URL of the **AppInstalled** remote event receiver.</span><span class="sxs-lookup"><span data-stu-id="433b0-209">Sets the  **EventReceiverDefinitionCreationInformation.ReceiverURL** to the URL of the **AppInstalled** remote event receiver.</span></span>
    
    - <span data-ttu-id="433b0-210">Adds a new event receiver to the list using  **List.EventReceivers.Add**.</span><span class="sxs-lookup"><span data-stu-id="433b0-210">Adds a new event receiver to the list using  **List.EventReceivers.Add**.</span></span>

```C#
public void AssociateRemoteEventsToHostWeb(ClientContext clientContext)
        {
            // Add Push Notification feature to host web.
            // Not required but it is included here to show you
            // how to activate features.
            clientContext.Web.Features.Add(
                     new Guid("41e1d4bf-b1a2-47f7-ab80-d5d6cbba3092"),
                     true, FeatureDefinitionScope.None);


            // Get the Title and EventReceivers lists.
            clientContext.Load(clientContext.Web.Lists,
                lists => lists.Include(
                    list => list.Title,
                    list => list.EventReceivers).Where
                        (list => list.Title == LIST_TITLE));

            clientContext.ExecuteQuery();

            List jobsList = clientContext.Web.Lists.FirstOrDefault();

            bool rerExists = false;
            if (null == jobsList)
            {
                // List does not exist, create it. 
                jobsList = CreateJobsList(clientContext);

            }
            else
            {
                foreach (var rer in jobsList.EventReceivers)
                {
                    if (rer.ReceiverName == RECEIVER_NAME)
                    {
                        rerExists = true;
                        System.Diagnostics.Trace.WriteLine("Found existing ItemAdded receiver at "
                            + rer.ReceiverUrl);
                    }
                }
            }

            if (!rerExists)
            {
                EventReceiverDefinitionCreationInformation receiver =
                    new EventReceiverDefinitionCreationInformation();
                receiver.EventType = EventReceiverType.ItemAdded;
                
                // Get WCF URL where this message was handled.
                OperationContext op = OperationContext.Current;
                Message msg = op.RequestContext.RequestMessage;
                receiver.ReceiverUrl = msg.Headers.To.ToString();

                receiver.ReceiverName = RECEIVER_NAME;
                receiver.Synchronization = EventReceiverSynchronization.Synchronous;

                // Add the new event receiver to a list in the host web.
                jobsList.EventReceivers.Add(receiver);
                clientContext.ExecuteQuery();

                System.Diagnostics.Trace.WriteLine("Added ItemAdded receiver at " + receiver.ReceiverUrl);
            }
        }
```

<span data-ttu-id="433b0-211">When an item is added to the  **Remote Event Receiver Jobs** list, **ProcessEvent** in AppEventReceiver.svc.cs handles the **ItemAdded** event, and then calls **HandleItemAdded**.</span><span class="sxs-lookup"><span data-stu-id="433b0-211">When an item is added to the  **Remote Event Receiver Jobs** list, **ProcessEvent** in AppEventReceiver.svc.cs handles the **ItemAdded** event, and then calls **HandleItemAdded**.</span></span>  <span data-ttu-id="433b0-212">**HandleItemAdded** calls **RemoteEventReceiverManager.ItemAddedToListEventHandler**.</span><span class="sxs-lookup"><span data-stu-id="433b0-212">**HandleItemAdded** calls **RemoteEventReceiverManager.ItemAddedToListEventHandler**.</span></span>  <span data-ttu-id="433b0-213">**ItemAddedToListEventHandler** fetches the list item that was added, and adds the string **Updated by ReR** to the list item's description.</span><span class="sxs-lookup"><span data-stu-id="433b0-213">**ItemAddedToListEventHandler** fetches the list item that was added, and adds the string **Updated by ReR** to the list item's description.</span></span>

```C#
 public void ItemAddedToListEventHandler(ClientContext clientContext, Guid listId, int listItemId)
        {
            try
            {
                List photos = clientContext.Web.Lists.GetById(listId);
                ListItem item = photos.GetItemById(listItemId);
                clientContext.Load(item);
                clientContext.ExecuteQuery();

                item["Description"] += "\nUpdated by RER " +
                    System.DateTime.Now.ToLongTimeString();
                item.Update();
                clientContext.ExecuteQuery();
            }
            catch (Exception oops)
            {
                System.Diagnostics.Trace.WriteLine(oops.Message);
            }

        }
```

## <a name="see-also"></a><span data-ttu-id="433b0-214">См. также</span><span class="sxs-lookup"><span data-stu-id="433b0-214">See also</span></span>
<span data-ttu-id="433b0-215"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="433b0-215"></span></span>

-  [<span data-ttu-id="433b0-216">Office 365 development patterns and practices solution guidance</span><span class="sxs-lookup"><span data-stu-id="433b0-216">Office 365 development patterns and practices solution guidance</span></span>](Office-365-development-patterns-and-practices-solution-guidance.md)
    
-  [<span data-ttu-id="433b0-217">Core.AppEvents.HandlerDelegation </span><span class="sxs-lookup"><span data-stu-id="433b0-217">Core.AppEvents.HandlerDelegation </span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.AppEvents.HandlerDelegation)
    
