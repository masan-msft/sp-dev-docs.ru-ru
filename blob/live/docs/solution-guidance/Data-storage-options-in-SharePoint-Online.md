---
title: Data storage options in SharePoint Online
ms.date: 11/03/2017
ms.openlocfilehash: 61913916350d33a15ed753ac60fe7310182a3073
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="data-storage-options-in-sharepoint-online"></a><span data-ttu-id="4742a-102">Data storage options in SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="4742a-102">Data storage options in SharePoint Online</span></span>

<span data-ttu-id="4742a-103">When you develop SharePoint Online add-ins, you have a number of different options for data storage.</span><span class="sxs-lookup"><span data-stu-id="4742a-103">When you develop SharePoint Online add-ins, you have a number of different options for data storage.</span></span> <span data-ttu-id="4742a-104">You can use the sample described in this article to explore the differences between each option, and to learn about the advantages to using remote data storage.</span><span class="sxs-lookup"><span data-stu-id="4742a-104">You can use the sample described in this article to explore the differences between each option, and to learn about the advantages to using remote data storage.</span></span> 

<span data-ttu-id="4742a-105">_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="4742a-105">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="4742a-106">This article describes the  [Core.DataStorageModels](https://github.com/SharePoint/PnP/tree/master/Samples/Core.DataStorageModels) sample app, which shows you each of the following data storage options and the advantages and disadvantages of each:</span><span class="sxs-lookup"><span data-stu-id="4742a-106">This article describes the  [Core.DataStorageModels](https://github.com/SharePoint/PnP/tree/master/Samples/Core.DataStorageModels) sample app, which shows you each of the following data storage options and the advantages and disadvantages of each:</span></span>

- <span data-ttu-id="4742a-107">SharePoint list on the host web</span><span class="sxs-lookup"><span data-stu-id="4742a-107">SharePoint list on the host web</span></span>
    
- <span data-ttu-id="4742a-108">SharePoint list on the app web</span><span class="sxs-lookup"><span data-stu-id="4742a-108">SharePoint list on the app web</span></span>
    
- <span data-ttu-id="4742a-109">SQL Azure database</span><span class="sxs-lookup"><span data-stu-id="4742a-109">SQL Azure database</span></span>
    
- <span data-ttu-id="4742a-110">Azure queue storage</span><span class="sxs-lookup"><span data-stu-id="4742a-110">Azure queue storage</span></span>
    
- <span data-ttu-id="4742a-111">Azure table storage</span><span class="sxs-lookup"><span data-stu-id="4742a-111">Azure table storage</span></span>
    
- <span data-ttu-id="4742a-112">External web service</span><span class="sxs-lookup"><span data-stu-id="4742a-112">External web service</span></span>
    
<span data-ttu-id="4742a-113">The  [Core.DataStorageModels](https://github.com/SharePoint/PnP/tree/master/Samples/Core.DataStorageModels) sample app is a provider-hosted app written in C# and JavaScript that deploys a number of SharePoint artifacts (lists, app part, web part) to both the host web and the app web.</span><span class="sxs-lookup"><span data-stu-id="4742a-113">The  [Core.DataStorageModels](https://github.com/SharePoint/PnP/tree/master/Samples/Core.DataStorageModels) sample app is a provider-hosted app written in C# and JavaScript that deploys a number of SharePoint artifacts (lists, app part, web part) to both the host web and the app web.</span></span> <span data-ttu-id="4742a-114">It interacts with SharePoint lists on the app web and host web, and also makes calls to a SQL Azure database, an Azure queue and table storage, and a remote web service that implements OData.</span><span class="sxs-lookup"><span data-stu-id="4742a-114">It interacts with SharePoint lists on the app web and host web, and also makes calls to a SQL Azure database, an Azure queue and table storage, and a remote web service that implements OData.</span></span> <span data-ttu-id="4742a-115">This sample uses the Model-View-Controller (MVC) pattern.</span><span class="sxs-lookup"><span data-stu-id="4742a-115">This sample uses the Model-View-Controller (MVC) pattern.</span></span>
<span data-ttu-id="4742a-116">The  [Core.DataStorageModels](https://github.com/SharePoint/PnP/tree/master/Samples/Core.DataStorageModels) sample app applies each data storage option to a specific function for which the option is well suited, as described in the following table.</span><span class="sxs-lookup"><span data-stu-id="4742a-116">The  [Core.DataStorageModels](https://github.com/SharePoint/PnP/tree/master/Samples/Core.DataStorageModels) sample app applies each data storage option to a specific function for which the option is well suited, as described in the following table.</span></span>

|<span data-ttu-id="4742a-117">Sample app storage option</span><span class="sxs-lookup"><span data-stu-id="4742a-117">Sample app storage option</span></span>|<span data-ttu-id="4742a-118">Used for</span><span class="sxs-lookup"><span data-stu-id="4742a-118">Used for</span></span>|
|:--|:--|
|<span data-ttu-id="4742a-119">SharePoint list app web</span><span class="sxs-lookup"><span data-stu-id="4742a-119">SharePoint list app web</span></span>|<span data-ttu-id="4742a-120">Customer notes</span><span class="sxs-lookup"><span data-stu-id="4742a-120">Customer notes</span></span>|
|<span data-ttu-id="4742a-121">SharePoint list host web</span><span class="sxs-lookup"><span data-stu-id="4742a-121">SharePoint list host web</span></span>|<span data-ttu-id="4742a-122">Support cases</span><span class="sxs-lookup"><span data-stu-id="4742a-122">Support cases</span></span>|
|<span data-ttu-id="4742a-123">Northwind OData service</span><span class="sxs-lookup"><span data-stu-id="4742a-123">Northwind OData service</span></span>|<span data-ttu-id="4742a-124">Customers</span><span class="sxs-lookup"><span data-stu-id="4742a-124">Customers</span></span>|
|<span data-ttu-id="4742a-125">Azure table storage</span><span class="sxs-lookup"><span data-stu-id="4742a-125">Azure table storage</span></span>|<span data-ttu-id="4742a-126">CSR ratings</span><span class="sxs-lookup"><span data-stu-id="4742a-126">CSR ratings</span></span>|
|<span data-ttu-id="4742a-127">Azure queue storage</span><span class="sxs-lookup"><span data-stu-id="4742a-127">Azure queue storage</span></span>|<span data-ttu-id="4742a-128">Call queue</span><span class="sxs-lookup"><span data-stu-id="4742a-128">Call queue</span></span>|
|<span data-ttu-id="4742a-129">SQL Azure Northwind database</span><span class="sxs-lookup"><span data-stu-id="4742a-129">SQL Azure Northwind database</span></span>|<span data-ttu-id="4742a-130">Orders, order details, products</span><span class="sxs-lookup"><span data-stu-id="4742a-130">Orders, order details, products</span></span>|

<span data-ttu-id="4742a-131">The app implements a customer service dashboard and related interfaces that show recent orders, customer representative survey ratings, customer notes, support cases, and a customer representative call queue.</span><span class="sxs-lookup"><span data-stu-id="4742a-131">The app implements a customer service dashboard and related interfaces that show recent orders, customer representative survey ratings, customer notes, support cases, and a customer representative call queue.</span></span> <span data-ttu-id="4742a-132">The first two scenarios let you retrieve data by using relatively simply client object model code or REST queries, but are limited by list query thresholds.</span><span class="sxs-lookup"><span data-stu-id="4742a-132">The first two scenarios let you retrieve data by using relatively simply client object model code or REST queries, but are limited by list query thresholds.</span></span> <span data-ttu-id="4742a-133">The next four scenarios uses different types of remote storage.</span><span class="sxs-lookup"><span data-stu-id="4742a-133">The next four scenarios uses different types of remote storage.</span></span> 

<span data-ttu-id="4742a-134">**Figure 1. Data storage models start page prompts you to deploy SharePoint components**</span><span class="sxs-lookup"><span data-stu-id="4742a-134">**Figure 1. Data storage models start page prompts you to deploy SharePoint components**</span></span>

![Screenshot of app sample UI](media/bb3b58ca-b983-4ec4-b36d-18a911edb5d5.png)

## <a name="before-you-begin"></a><span data-ttu-id="4742a-136">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="4742a-136">Before you begin</span></span>
<span data-ttu-id="4742a-137"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="4742a-137"></span></span>

<span data-ttu-id="4742a-138">Before you use this sample, make sure that you have the following:</span><span class="sxs-lookup"><span data-stu-id="4742a-138">Before you use this sample, make sure that you have the following:</span></span>

- <span data-ttu-id="4742a-139">A Microsoft Azure account where you can deploy a SQL Azure database and create an Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="4742a-139">A Microsoft Azure account where you can deploy a SQL Azure database and create an Azure storage account.</span></span> 
    
- <span data-ttu-id="4742a-140">A SharePoint developer site so that you can deploy the sample from Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="4742a-140">A SharePoint developer site so that you can deploy the sample from Visual Studio 2013.</span></span>
    
<span data-ttu-id="4742a-141">Also, you need to deploy the Northwind database to Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="4742a-141">Also, you need to deploy the Northwind database to Microsoft Azure.</span></span>

### <a name="to-deploy-the-northwind-database"></a><span data-ttu-id="4742a-142">To deploy the Northwind database</span><span class="sxs-lookup"><span data-stu-id="4742a-142">To deploy the Northwind database</span></span>

1. <span data-ttu-id="4742a-143">Log on to the Azure Management Portal and choose  **SQL Databases**> **Servers**.</span><span class="sxs-lookup"><span data-stu-id="4742a-143">Log on to the Azure Management Portal and choose  **SQL Databases**> **Servers**.</span></span>
    
2. <span data-ttu-id="4742a-144">Choose  **Create a SQL Database Server**.</span><span class="sxs-lookup"><span data-stu-id="4742a-144">Choose  **Create a SQL Database Server**.</span></span>
    
3. <span data-ttu-id="4742a-145">In the  **Create Server** form, enter values for **Login Name**,  **Login Password**, and  **Region**, as shown in Figure 2.</span><span class="sxs-lookup"><span data-stu-id="4742a-145">In the  **Create Server** form, enter values for **Login Name**,  **Login Password**, and  **Region**, as shown in Figure 2.</span></span>
    
    <span data-ttu-id="4742a-146">**Figure 2. SQL database server settings**</span><span class="sxs-lookup"><span data-stu-id="4742a-146">**Figure 2. SQL database server settings**</span></span>

    ![Shows the SQL database server settings](media/7ae059fa-eecc-4446-8171-294e44acb189.png)

4. <span data-ttu-id="4742a-148">Choose the checkmark button to finish and create the server.</span><span class="sxs-lookup"><span data-stu-id="4742a-148">Choose the checkmark button to finish and create the server.</span></span>
    
5. <span data-ttu-id="4742a-149">Now that you've created the database, choose the server name that you created, as shown in Figure 3.</span><span class="sxs-lookup"><span data-stu-id="4742a-149">Now that you've created the database, choose the server name that you created, as shown in Figure 3.</span></span>
    
    <span data-ttu-id="4742a-150">**Figure 3. Server name on the Servers page**</span><span class="sxs-lookup"><span data-stu-id="4742a-150">**Figure 3. Server name on the Servers page**</span></span>

    ![Shows the list of SQL databases](media/a6b097e4-5ad2-47df-9e31-ac0d699efd76.png)

6. <span data-ttu-id="4742a-152">Choose  **CONFIGURE**, and then choose the arrow in the lower right corner to complete the configuration, and choose  **SAVE**.</span><span class="sxs-lookup"><span data-stu-id="4742a-152">Choose  **CONFIGURE**, and then choose the arrow in the lower right corner to complete the configuration, and choose  **SAVE**.</span></span>
    
7. <span data-ttu-id="4742a-153">Open SQL Server Management Studio on your local development computer and create a new database named  **NorthWind**.</span><span class="sxs-lookup"><span data-stu-id="4742a-153">Open SQL Server Management Studio on your local development computer and create a new database named  **NorthWind**.</span></span>
    
8. <span data-ttu-id="4742a-154">In the  **Object Explorer**, select the  **Northwind** database, and then choose **New Query**.</span><span class="sxs-lookup"><span data-stu-id="4742a-154">In the  **Object Explorer**, select the  **Northwind** database, and then choose **New Query**.</span></span>
    
9. <span data-ttu-id="4742a-155">In a text editor of your choice, open the northwind.sql SQL script that is provided with the  [Core.DataStorageModels](https://github.com/SharePoint/PnP/tree/master/Samples/Core.DataStorageModels) sample.</span><span class="sxs-lookup"><span data-stu-id="4742a-155">In a text editor of your choice, open the northwind.sql SQL script that is provided with the  [Core.DataStorageModels](https://github.com/SharePoint/PnP/tree/master/Samples/Core.DataStorageModels) sample.</span></span>
    
10. <span data-ttu-id="4742a-156">Copy the text in the northwind.sql file and paste it into the  **SQL Query window** in the SQL Server Management Studio, and then choose **Execute**.</span><span class="sxs-lookup"><span data-stu-id="4742a-156">Copy the text in the northwind.sql file and paste it into the  **SQL Query window** in the SQL Server Management Studio, and then choose **Execute**.</span></span>
    
11. <span data-ttu-id="4742a-157">In the  **Object Explorer**, open the shortcut menu for (right-click) the  **Northwind** database, select **Tasks**, and then select  **Deploy Database to SQL Azure**.</span><span class="sxs-lookup"><span data-stu-id="4742a-157">In the  **Object Explorer**, open the shortcut menu for (right-click) the  **Northwind** database, select **Tasks**, and then select  **Deploy Database to SQL Azure**.</span></span>
    
12. <span data-ttu-id="4742a-158">On the  **Introduction** screen, choose **Next**.</span><span class="sxs-lookup"><span data-stu-id="4742a-158">On the  **Introduction** screen, choose **Next**.</span></span>
    
13. <span data-ttu-id="4742a-159">Choose  **Connect ...** and enter the **Server name** for the SQL Azure Database Server you just created.</span><span class="sxs-lookup"><span data-stu-id="4742a-159">Choose  **Connect ...** and enter the **Server name** for the SQL Azure Database Server you just created.</span></span>
    
14. <span data-ttu-id="4742a-160">In the  **Authentication** dropdown, select **SQL Server Authentication**.</span><span class="sxs-lookup"><span data-stu-id="4742a-160">In the  **Authentication** dropdown, select **SQL Server Authentication**.</span></span>
    
15. <span data-ttu-id="4742a-161">Enter the user name and password you used when you created the SQL Azure Database server, then choose  **Connect**.</span><span class="sxs-lookup"><span data-stu-id="4742a-161">Enter the user name and password you used when you created the SQL Azure Database server, then choose  **Connect**.</span></span>
    
16. <span data-ttu-id="4742a-162">Choose  **Next**, and then choose  **Finish**, and wait until the database is created.</span><span class="sxs-lookup"><span data-stu-id="4742a-162">Choose  **Next**, and then choose  **Finish**, and wait until the database is created.</span></span> <span data-ttu-id="4742a-163">After it is created, choose  **Close** to close the wizard.</span><span class="sxs-lookup"><span data-stu-id="4742a-163">After it is created, choose  **Close** to close the wizard.</span></span>
    
17. <span data-ttu-id="4742a-164">Return to the Azure Management Portal ( [https://manage.windowsazure.com/](https://manage.windowsazure.com/)) to verify that the Northwind database was created successfully.</span><span class="sxs-lookup"><span data-stu-id="4742a-164">Return to the Azure Management Portal ( [https://manage.windowsazure.com/](https://manage.windowsazure.com/)) to verify that the Northwind database was created successfully.</span></span> <span data-ttu-id="4742a-165">You should see it listed on the sql databases screen, as shown in Figure 4.</span><span class="sxs-lookup"><span data-stu-id="4742a-165">You should see it listed on the sql databases screen, as shown in Figure 4.</span></span>
    
    <span data-ttu-id="4742a-166">**Figure 4. Listing of SQL Server databases**</span><span class="sxs-lookup"><span data-stu-id="4742a-166">**Figure 4. Listing of SQL Server databases**</span></span>

    ![Shows a list of all SQL databases, including Northwind](media/036b4252-f57b-4f39-9f60-ddaa30daf23c.png)

18. <span data-ttu-id="4742a-168">Select the Northwind database, and then select  **View SQL Database connection strings**.</span><span class="sxs-lookup"><span data-stu-id="4742a-168">Select the Northwind database, and then select  **View SQL Database connection strings**.</span></span>
    
19. <span data-ttu-id="4742a-169">Copy the connection string and paste it into a text file and save it locally.</span><span class="sxs-lookup"><span data-stu-id="4742a-169">Copy the connection string and paste it into a text file and save it locally.</span></span> <span data-ttu-id="4742a-170">You will need this connection string later.</span><span class="sxs-lookup"><span data-stu-id="4742a-170">You will need this connection string later.</span></span> <span data-ttu-id="4742a-171">Close the  **Connection Strings** dialog box.</span><span class="sxs-lookup"><span data-stu-id="4742a-171">Close the  **Connection Strings** dialog box.</span></span>
    
20. <span data-ttu-id="4742a-172">Choose the  **Set up Windows Azure firewall rules for this IP address** link and add your IP address to the firewall rules to allow you to access the database.</span><span class="sxs-lookup"><span data-stu-id="4742a-172">Choose the  **Set up Windows Azure firewall rules for this IP address** link and add your IP address to the firewall rules to allow you to access the database.</span></span>
    
21. <span data-ttu-id="4742a-173">Open the Core.DataStorageModels.sln project in Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="4742a-173">Open the Core.DataStorageModels.sln project in Visual Studio 2013.</span></span>
    
22. <span data-ttu-id="4742a-174">In the Visual Studio **Solution Explorer**, locate the Web.config file.</span><span class="sxs-lookup"><span data-stu-id="4742a-174">In the Visual Studio **Solution Explorer**, locate the Web.config file.</span></span>
    
23. <span data-ttu-id="4742a-175">In the Web.config file, locate the add  `name="NorthWindEntities"` element and replace the existing connectionString value with the connection string information that you saved locally in step 19.</span><span class="sxs-lookup"><span data-stu-id="4742a-175">In the Web.config file, locate the add  `name="NorthWindEntities"` element and replace the existing connectionString value with the connection string information that you saved locally in step 19.</span></span> 
    
    ```XML
      <add name="NorthWindEntities" connectionString="metadata=res://*/Northwind.csdl|res://*/Northwind.ssdl|res://*/Northwind.msl;provider=System.Data.SqlClient;provider connection string=&amp;quot;data source=<Your Server Here>.database.windows.net;initial catalog=NorthWind;user id=<Your Username Here>@<Your Server Here>;password=<Your Password Here>;MultipleActiveResultSets=True;App=EntityFramework&amp;quot;" providerName="System.Data.EntityClient" />
    ```
24. <span data-ttu-id="4742a-176">Save the Web.config file.</span><span class="sxs-lookup"><span data-stu-id="4742a-176">Save the Web.config file.</span></span>

## <a name="sharepoint-list-on-the-app-web-notes-scenario"></a><span data-ttu-id="4742a-177">SharePoint list on the app web (Notes scenario)</span><span class="sxs-lookup"><span data-stu-id="4742a-177">SharePoint list on the app web (Notes scenario)</span></span>
<span data-ttu-id="4742a-178"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="4742a-178"></span></span>

<span data-ttu-id="4742a-179">The Notes list scenario, which uses a SharePoint list on an app web, shows how lists perform in a SharePoint app web.</span><span class="sxs-lookup"><span data-stu-id="4742a-179">The Notes list scenario, which uses a SharePoint list on an app web, shows how lists perform in a SharePoint app web.</span></span> <span data-ttu-id="4742a-180">The Notes list is created in the app web with a title and description field.</span><span class="sxs-lookup"><span data-stu-id="4742a-180">The Notes list is created in the app web with a title and description field.</span></span> <span data-ttu-id="4742a-181">The SharePoint REST API queries the Notes list and returns all the notes based on a customer ID.</span><span class="sxs-lookup"><span data-stu-id="4742a-181">The SharePoint REST API queries the Notes list and returns all the notes based on a customer ID.</span></span>

<span data-ttu-id="4742a-182">Using lists in the app web has one important advantage over other storage solutions: you can use simple SharePoint REST API calls to query data.</span><span class="sxs-lookup"><span data-stu-id="4742a-182">Using lists in the app web has one important advantage over other storage solutions: you can use simple SharePoint REST API calls to query data.</span></span> <span data-ttu-id="4742a-183">However, there are some disadvantages:</span><span class="sxs-lookup"><span data-stu-id="4742a-183">However, there are some disadvantages:</span></span>

- <span data-ttu-id="4742a-184">To update list metadata, you must update and redeploy the app.</span><span class="sxs-lookup"><span data-stu-id="4742a-184">To update list metadata, you must update and redeploy the app.</span></span>
    
- <span data-ttu-id="4742a-185">To update the data structure, you must rewrite application logic for storing and updating data.</span><span class="sxs-lookup"><span data-stu-id="4742a-185">To update the data structure, you must rewrite application logic for storing and updating data.</span></span>
    
- <span data-ttu-id="4742a-186">Information stored in the list cannot be shared easily with other add-ins.</span><span class="sxs-lookup"><span data-stu-id="4742a-186">Information stored in the list cannot be shared easily with other add-ins.</span></span>
    
- <span data-ttu-id="4742a-187">You cannot search for data in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="4742a-187">You cannot search for data in SharePoint.</span></span>
    
- <span data-ttu-id="4742a-188">The amount of data that you can store in lists and the size of query result sets are limited.</span><span class="sxs-lookup"><span data-stu-id="4742a-188">The amount of data that you can store in lists and the size of query result sets are limited.</span></span>
    
<span data-ttu-id="4742a-189">The code that underlies the Notes section of the customer dashboard uses REST queries to retrieve data from a list that is deployed to the app web.</span><span class="sxs-lookup"><span data-stu-id="4742a-189">The code that underlies the Notes section of the customer dashboard uses REST queries to retrieve data from a list that is deployed to the app web.</span></span> <span data-ttu-id="4742a-190">This list contains fields for titles, authors, customer IDs, and descriptions.</span><span class="sxs-lookup"><span data-stu-id="4742a-190">This list contains fields for titles, authors, customer IDs, and descriptions.</span></span> <span data-ttu-id="4742a-191">You can use the app's interface to add and retrieve notes for a specified customer, as shown in Figure 5.</span><span class="sxs-lookup"><span data-stu-id="4742a-191">You can use the app's interface to add and retrieve notes for a specified customer, as shown in Figure 5.</span></span>

<span data-ttu-id="4742a-192">**Figure 5. User interface for the Notes app**</span><span class="sxs-lookup"><span data-stu-id="4742a-192">**Figure 5. User interface for the Notes app**</span></span>

![A screenshot that shows the UI for the Notes data storage model](media/d98ce2cf-5022-4f2b-ad3e-da4eea52dfb2.png)

<span data-ttu-id="4742a-194">The  **View Notes List in App Web** link provides an "out of the box" view of the list data.</span><span class="sxs-lookup"><span data-stu-id="4742a-194">The  **View Notes List in App Web** link provides an "out of the box" view of the list data.</span></span>

<span data-ttu-id="4742a-195">This app uses the Model-View-Controller (MVC) pattern.</span><span class="sxs-lookup"><span data-stu-id="4742a-195">This app uses the Model-View-Controller (MVC) pattern.</span></span> <span data-ttu-id="4742a-196">You can see the code for the notes scenario in the Views/CustomerDashboard/Notes.cshtml file.</span><span class="sxs-lookup"><span data-stu-id="4742a-196">You can see the code for the notes scenario in the Views/CustomerDashboard/Notes.cshtml file.</span></span> <span data-ttu-id="4742a-197">It uses simple REST calls to add and retrieve data.</span><span class="sxs-lookup"><span data-stu-id="4742a-197">It uses simple REST calls to add and retrieve data.</span></span> <span data-ttu-id="4742a-198">The following code retrieves notes from the Notes list for a specified customer.</span><span class="sxs-lookup"><span data-stu-id="4742a-198">The following code retrieves notes from the Notes list for a specified customer.</span></span>

```C#
function getNotesAndShow() {
    var executor = new SP.RequestExecutor(appWebUrl);
    executor.executeAsync(
       {
           url: appWebUrl + "/_api/web/lists/getByTitle('Notes')/items/" +
                "?$select=FTCAM_Description,Modified,Title,Author/ID,Author/Title" +
                "&amp;$expand=Author/ID,Author/Title" +
                "&amp;$filter=(Title eq '" + customerID + "')",
           type: "GET",
           dataType: 'json',
           headers: { "accept": "application/json;odata=verbose" },
           success: function (data) {
               var value = JSON.parse(data.body);
               showNotes(value.d.results);
           },
           error: function (error) { console.log(JSON.stringify(error)) }
       }

    );
}
```

<span data-ttu-id="4742a-199">The following code adds a note for a given customer to the notes list.</span><span class="sxs-lookup"><span data-stu-id="4742a-199">The following code adds a note for a given customer to the notes list.</span></span>

```C#
function addNoteToList(note, customerID) {
    var executor = new SP.RequestExecutor(appWebUrl);
    var bodyProps = {
        '__metadata': { 'type': 'SP.Data.NotesListItem' },
        'Title': customerID,
        'FTCAM_Description': note
    };
    executor.executeAsync({
        url: appWebUrl + "/_api/SP.AppContextSite(@target)/web/lists/getbytitle('Notes')/items?@target='" + appWebUrl + "'",
        contentType: "application/json;odata=verbose",
        method: "POST",
        headers: {
            "accept": "application/json;odata=verbose",
            "content-type": "application/json;odata=verbose",
            "X-RequestDigest": $("#__REQUESTDIGEST").val()
        },
        body: JSON.stringify(bodyProps),
        success: getNotesAndShow,
        error: addNoteFailed
    });
}
```

<span data-ttu-id="4742a-200">You can add 5000 items to the list to show that list queries that generate a result set of 5000 or more items will hit the list query threshold and fail.</span><span class="sxs-lookup"><span data-stu-id="4742a-200">You can add 5000 items to the list to show that list queries that generate a result set of 5000 or more items will hit the list query threshold and fail.</span></span> <span data-ttu-id="4742a-201">You can also add so much data to your list on the app web that you exceed the storage limit for your site collection (which depends on how much storage space you've allocated to it).</span><span class="sxs-lookup"><span data-stu-id="4742a-201">You can also add so much data to your list on the app web that you exceed the storage limit for your site collection (which depends on how much storage space you've allocated to it).</span></span> <span data-ttu-id="4742a-202">These scenarios show two of the most important limitations of this approach: list query size limits and storage space limits.</span><span class="sxs-lookup"><span data-stu-id="4742a-202">These scenarios show two of the most important limitations of this approach: list query size limits and storage space limits.</span></span> <span data-ttu-id="4742a-203">If your business needs require you to work with large data sets and query result sets, this approach won't work.</span><span class="sxs-lookup"><span data-stu-id="4742a-203">If your business needs require you to work with large data sets and query result sets, this approach won't work.</span></span>

### <a name="list-query-threshold"></a><span data-ttu-id="4742a-204">List query threshold</span><span class="sxs-lookup"><span data-stu-id="4742a-204">List query threshold</span></span>
<span data-ttu-id="4742a-205"><a name="bk_listquerythreshold"> </a></span><span class="sxs-lookup"><span data-stu-id="4742a-205"></span></span>

<span data-ttu-id="4742a-206">To load enough data to exceed the list query threshold limit:</span><span class="sxs-lookup"><span data-stu-id="4742a-206">To load enough data to exceed the list query threshold limit:</span></span>


1. <span data-ttu-id="4742a-207">In the left menu, choose  **Sample Home Page**.</span><span class="sxs-lookup"><span data-stu-id="4742a-207">In the left menu, choose  **Sample Home Page**.</span></span>
    
2. <span data-ttu-id="4742a-208">In the  **List Query Thresholds** section, choose **Add list items to the Notes list in the App Web**.</span><span class="sxs-lookup"><span data-stu-id="4742a-208">In the  **List Query Thresholds** section, choose **Add list items to the Notes list in the App Web**.</span></span>
    
3. <span data-ttu-id="4742a-209">Per the instructions that appear above the button, perform this operation 10 times.</span><span class="sxs-lookup"><span data-stu-id="4742a-209">Per the instructions that appear above the button, perform this operation 10 times.</span></span>
    
    <span data-ttu-id="4742a-210">When the Notes list is updated, a message appears at the top of the page that indicates how many list items (Notes) you added and how many are left to add.</span><span class="sxs-lookup"><span data-stu-id="4742a-210">When the Notes list is updated, a message appears at the top of the page that indicates how many list items (Notes) you added and how many are left to add.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="4742a-211">The operation takes about one minute to run each time you choose the button.</span><span class="sxs-lookup"><span data-stu-id="4742a-211">The operation takes about one minute to run each time you choose the button.</span></span> <span data-ttu-id="4742a-212">The end result of running the operation 10 times is shown in Figure 6.</span><span class="sxs-lookup"><span data-stu-id="4742a-212">The end result of running the operation 10 times is shown in Figure 6.</span></span>

4. <span data-ttu-id="4742a-213">After you've added 5,001 items to the list, choose Notes in the left menu.</span><span class="sxs-lookup"><span data-stu-id="4742a-213">After you've added 5,001 items to the list, choose Notes in the left menu.</span></span> <span data-ttu-id="4742a-214">When the page loads, you will see the error message shown in Figure 6, which comes from the SharePoint REST API.</span><span class="sxs-lookup"><span data-stu-id="4742a-214">When the page loads, you will see the error message shown in Figure 6, which comes from the SharePoint REST API.</span></span>
    
    <span data-ttu-id="4742a-215">**Figure 6. List query thresold exceeded error message**</span><span class="sxs-lookup"><span data-stu-id="4742a-215">**Figure 6. List query thresold exceeded error message**</span></span>

    ![A screenshot that shows an error message that states that the operation exceeded the list view threshol.](media/90202b64-4b14-4764-9a4c-8fb236f8d10b.png)

5. <span data-ttu-id="4742a-217">Choose  **View Notes List in App Web** and page through the list to see that it includes 500 rows.</span><span class="sxs-lookup"><span data-stu-id="4742a-217">Choose  **View Notes List in App Web** and page through the list to see that it includes 500 rows.</span></span> <span data-ttu-id="4742a-218">Note that although SharePoint list views can accommodate browsing of this many entries, the REST API fails due to the list query throttling threshold.</span><span class="sxs-lookup"><span data-stu-id="4742a-218">Note that although SharePoint list views can accommodate browsing of this many entries, the REST API fails due to the list query throttling threshold.</span></span>
    
### <a name="data-storage-limit"></a><span data-ttu-id="4742a-219">Data storage limit</span><span class="sxs-lookup"><span data-stu-id="4742a-219">Data storage limit</span></span>
<span data-ttu-id="4742a-220"><a name="bk_listquerythreshold"> </a></span><span class="sxs-lookup"><span data-stu-id="4742a-220"></span></span>

<span data-ttu-id="4742a-221">To load enough data to exceed the data storage limit:</span><span class="sxs-lookup"><span data-stu-id="4742a-221">To load enough data to exceed the data storage limit:</span></span>

1. <span data-ttu-id="4742a-222">In the left menu, choose  **Sample Home Page**.</span><span class="sxs-lookup"><span data-stu-id="4742a-222">In the left menu, choose  **Sample Home Page**.</span></span>
    
2. <span data-ttu-id="4742a-223">In the Data Threshold section, choose  **Fill the App Web Notes list with 1GB of data**.</span><span class="sxs-lookup"><span data-stu-id="4742a-223">In the Data Threshold section, choose  **Fill the App Web Notes list with 1GB of data**.</span></span>
    
3. <span data-ttu-id="4742a-224">Per the instructions that appear above the  **Fill the App Web Notes list with 1GB of data** button, perform this operation 11 times.</span><span class="sxs-lookup"><span data-stu-id="4742a-224">Per the instructions that appear above the  **Fill the App Web Notes list with 1GB of data** button, perform this operation 11 times.</span></span>
    
    <span data-ttu-id="4742a-225">When the Notes list is updated, a message appears at the top of the page that indicates how many list items (Notes) you added and how many are left to add.</span><span class="sxs-lookup"><span data-stu-id="4742a-225">When the Notes list is updated, a message appears at the top of the page that indicates how many list items (Notes) you added and how many are left to add.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="4742a-226">The operation takes about one minute to run each time you choose the button.</span><span class="sxs-lookup"><span data-stu-id="4742a-226">The operation takes about one minute to run each time you choose the button.</span></span> <span data-ttu-id="4742a-227">The end result of running the operation 11 times is shown in Figure 7.</span><span class="sxs-lookup"><span data-stu-id="4742a-227">The end result of running the operation 11 times is shown in Figure 7.</span></span>

4. <span data-ttu-id="4742a-228">After you perform the operation 11 times, an error message will occur when you choose the button, as shown in Figure 7.</span><span class="sxs-lookup"><span data-stu-id="4742a-228">After you perform the operation 11 times, an error message will occur when you choose the button, as shown in Figure 7.</span></span>
    
    <span data-ttu-id="4742a-229">**Figure 7. Data storage threshold exceeded error message**</span><span class="sxs-lookup"><span data-stu-id="4742a-229">**Figure 7. Data storage threshold exceeded error message**</span></span>

    ![A screenshot that shows the error message that occurs when the data storage limit is exceeded](media/0bc55483-0ee1-487a-ba34-e827ec47aadd.png)

5. <span data-ttu-id="4742a-231">After you exceed the data storage limit, choose the back button in the web browser, and then choose the  **Notes** link in the left menu.</span><span class="sxs-lookup"><span data-stu-id="4742a-231">After you exceed the data storage limit, choose the back button in the web browser, and then choose the  **Notes** link in the left menu.</span></span>
    
6. <span data-ttu-id="4742a-232">Choose  **View Notes List in App Web**.</span><span class="sxs-lookup"><span data-stu-id="4742a-232">Choose  **View Notes List in App Web**.</span></span>
    
    <span data-ttu-id="4742a-233">When the page loads, an error message appears at the top of the page that indicates that the site is out of storage space.</span><span class="sxs-lookup"><span data-stu-id="4742a-233">When the page loads, an error message appears at the top of the page that indicates that the site is out of storage space.</span></span>

## <a name="sharepoint-list-on-the-host-web-support-cases-scenario"></a><span data-ttu-id="4742a-234">SharePoint list on the host web (Support Cases scenario)</span><span class="sxs-lookup"><span data-stu-id="4742a-234">SharePoint list on the host web (Support Cases scenario)</span></span>
<span data-ttu-id="4742a-235"><a name="sectionSection2"> </a></span><span class="sxs-lookup"><span data-stu-id="4742a-235"></span></span>

<span data-ttu-id="4742a-236">The Support Cases scenario displays data that is stored in a SharePoint list in the host web.</span><span class="sxs-lookup"><span data-stu-id="4742a-236">The Support Cases scenario displays data that is stored in a SharePoint list in the host web.</span></span> <span data-ttu-id="4742a-237">This scenario uses two different patterns to access and interact with the data.</span><span class="sxs-lookup"><span data-stu-id="4742a-237">This scenario uses two different patterns to access and interact with the data.</span></span> <span data-ttu-id="4742a-238">The first pattern includes the SharePoint Search Service and the Content By Search Web Part with a custom Display Template applied.</span><span class="sxs-lookup"><span data-stu-id="4742a-238">The first pattern includes the SharePoint Search Service and the Content By Search Web Part with a custom Display Template applied.</span></span> <span data-ttu-id="4742a-239">The second pattern includes an App Part (Client Web Part) that displays an MVC view, which uses the  **SP.RequestExecutor** class to call the SharePoint REST API.</span><span class="sxs-lookup"><span data-stu-id="4742a-239">The second pattern includes an App Part (Client Web Part) that displays an MVC view, which uses the  **SP.RequestExecutor** class to call the SharePoint REST API.</span></span>

<span data-ttu-id="4742a-240">There are several advantages to using this approach:</span><span class="sxs-lookup"><span data-stu-id="4742a-240">There are several advantages to using this approach:</span></span>

- <span data-ttu-id="4742a-241">You can query data easily using simple REST queries or client object model code.</span><span class="sxs-lookup"><span data-stu-id="4742a-241">You can query data easily using simple REST queries or client object model code.</span></span>
    
- <span data-ttu-id="4742a-242">You can search for data in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="4742a-242">You can search for data in SharePoint.</span></span>
    
- <span data-ttu-id="4742a-243">You can update the list metadata and create new views for a list without updating and redeploying the app.</span><span class="sxs-lookup"><span data-stu-id="4742a-243">You can update the list metadata and create new views for a list without updating and redeploying the app.</span></span> <span data-ttu-id="4742a-244">These changes won't affect the behavior of your app.</span><span class="sxs-lookup"><span data-stu-id="4742a-244">These changes won't affect the behavior of your app.</span></span>
    
- <span data-ttu-id="4742a-245">Lists on the host web are not deleted when you uninstall your app, unless the app uses the  **AppUninstalled** event to remove the list and/or delete the data.</span><span class="sxs-lookup"><span data-stu-id="4742a-245">Lists on the host web are not deleted when you uninstall your app, unless the app uses the  **AppUninstalled** event to remove the list and/or delete the data.</span></span>
    
<span data-ttu-id="4742a-246">Offsetting these advantages are the following disadvantages:</span><span class="sxs-lookup"><span data-stu-id="4742a-246">Offsetting these advantages are the following disadvantages:</span></span>

- <span data-ttu-id="4742a-247">The host web limits both the amount of data you can store in lists and the size of the query results.</span><span class="sxs-lookup"><span data-stu-id="4742a-247">The host web limits both the amount of data you can store in lists and the size of the query results.</span></span> <span data-ttu-id="4742a-248">If your business needs require storing and/or querying large data sets, this is not a recommended approach.</span><span class="sxs-lookup"><span data-stu-id="4742a-248">If your business needs require storing and/or querying large data sets, this is not a recommended approach.</span></span>
    
- <span data-ttu-id="4742a-249">For complex queries, lists do not perform as well as databases.</span><span class="sxs-lookup"><span data-stu-id="4742a-249">For complex queries, lists do not perform as well as databases.</span></span>
    
- <span data-ttu-id="4742a-250">For backing up and restoring data, lists do not perform as well as databases.</span><span class="sxs-lookup"><span data-stu-id="4742a-250">For backing up and restoring data, lists do not perform as well as databases.</span></span>
    
<span data-ttu-id="4742a-251">The data for this scenario is stored in a SharePoint list deployed to the host web.</span><span class="sxs-lookup"><span data-stu-id="4742a-251">The data for this scenario is stored in a SharePoint list deployed to the host web.</span></span> <span data-ttu-id="4742a-252">Data is retrieved and displayed by means of the following:</span><span class="sxs-lookup"><span data-stu-id="4742a-252">Data is retrieved and displayed by means of the following:</span></span> 

- <span data-ttu-id="4742a-253">A  [Content Search Web Part](https://msdn.microsoft.com/en-us/library/office/jj163789%28v=office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="4742a-253">A  [Content Search Web Part](https://msdn.microsoft.com/en-us/library/office/jj163789%28v=office.15%29.aspx).</span></span>
    
- <span data-ttu-id="4742a-254">An app part that's implemented as a model-view-controller view.</span><span class="sxs-lookup"><span data-stu-id="4742a-254">An app part that's implemented as a model-view-controller view.</span></span> 
    
<span data-ttu-id="4742a-255">The code in this view uses REST queries to retrieve information from the list, while the content search web part uses the SharePoint search service to retrieve the data.</span><span class="sxs-lookup"><span data-stu-id="4742a-255">The code in this view uses REST queries to retrieve information from the list, while the content search web part uses the SharePoint search service to retrieve the data.</span></span> <span data-ttu-id="4742a-256">The two approaches demonstrate the significant advantage of this option: you can use both the search service and the REST/CSOM APIs to retrieve information from a list on the host web.</span><span class="sxs-lookup"><span data-stu-id="4742a-256">The two approaches demonstrate the significant advantage of this option: you can use both the search service and the REST/CSOM APIs to retrieve information from a list on the host web.</span></span>

<span data-ttu-id="4742a-257">When you select a customer from the support cases drop-down, you'll see the support case data for that customer displayed in both the web part and the app part (Figure 8).</span><span class="sxs-lookup"><span data-stu-id="4742a-257">When you select a customer from the support cases drop-down, you'll see the support case data for that customer displayed in both the web part and the app part (Figure 8).</span></span> <span data-ttu-id="4742a-258">The web part might not return content right away, because it can take up to 24 hours for the SharePoint search service to index the data.</span><span class="sxs-lookup"><span data-stu-id="4742a-258">The web part might not return content right away, because it can take up to 24 hours for the SharePoint search service to index the data.</span></span> <span data-ttu-id="4742a-259">You can also choose the  **View Support Cases List in Host Web** link to see a conventional view of the list data.</span><span class="sxs-lookup"><span data-stu-id="4742a-259">You can also choose the  **View Support Cases List in Host Web** link to see a conventional view of the list data.</span></span>

<span data-ttu-id="4742a-260">**Figure 8. User interface for the support case scenario**</span><span class="sxs-lookup"><span data-stu-id="4742a-260">**Figure 8. User interface for the support case scenario**</span></span>

![A screenshot that shows the UI for interacting with the support case scenario](media/eac41f5c-90b7-4fe3-b47e-0d65b79cbf1c.png)

<span data-ttu-id="4742a-262">The content search web part deployed by this app uses a custom display template.</span><span class="sxs-lookup"><span data-stu-id="4742a-262">The content search web part deployed by this app uses a custom display template.</span></span> <span data-ttu-id="4742a-263">Figure 9 shows where in the  **Assets** directory of the web project you can find the web part and the associated template.</span><span class="sxs-lookup"><span data-stu-id="4742a-263">Figure 9 shows where in the  **Assets** directory of the web project you can find the web part and the associated template.</span></span>

<span data-ttu-id="4742a-264">**Figure 9. Contents of the Assets directory of the web project**</span><span class="sxs-lookup"><span data-stu-id="4742a-264">**Figure 9. Contents of the Assets directory of the web project**</span></span>

![Screenshot of the Assets directory](media/95db9118-9e56-4e39-84b1-271e54447792.png)

<span data-ttu-id="4742a-266">The following JavaScript code that you'll find in the Views/SupportCaseAppPart\Index.cshtml file uses the cross-domain library to invoke a REST query on the SharePoint list on the host web.</span><span class="sxs-lookup"><span data-stu-id="4742a-266">The following JavaScript code that you'll find in the Views/SupportCaseAppPart\Index.cshtml file uses the cross-domain library to invoke a REST query on the SharePoint list on the host web.</span></span> 

```C#
function execCrossDomainRequest() {
var executor = new SP.RequestExecutor(appWebUrl);

executor.executeAsync(
   {
        url: appWebUrl + "/_api/SP.AppContextSite(@@target)" +
                "/web/lists/getbytitle('Support Cases')/items" +
              "?$filter=(FTCAM_CustomerID eq '" + customerID + "')" +
            "&amp;$top=30" +
                    "&amp;$select=Id,Title,FTCAM_Status,FTCAM_CSR" +
                    "&amp;@@target='" + hostWebUrl + "'",
method: "GET",
              headers: { "Accept": "application/json; odata=verbose" },
              success: successHandler,
              error: errorHandler
   }
);
}
```

<span data-ttu-id="4742a-267">You can add 5000 items to the list to show that list queries that generate a result set of 5000 or more items will hit the list query threshold and fail.</span><span class="sxs-lookup"><span data-stu-id="4742a-267">You can add 5000 items to the list to show that list queries that generate a result set of 5000 or more items will hit the list query threshold and fail.</span></span> <span data-ttu-id="4742a-268">This scenario shows one of the most important limitations of this approach: list query size limits.</span><span class="sxs-lookup"><span data-stu-id="4742a-268">This scenario shows one of the most important limitations of this approach: list query size limits.</span></span> <span data-ttu-id="4742a-269">If your business needs require you to work with large data and query result sets, this approach won't work.</span><span class="sxs-lookup"><span data-stu-id="4742a-269">If your business needs require you to work with large data and query result sets, this approach won't work.</span></span> <span data-ttu-id="4742a-270">For more information, see  [List query threshold](#bk_listquerythreshold) earlier in this article.</span><span class="sxs-lookup"><span data-stu-id="4742a-270">For more information, see  [List query threshold](#bk_listquerythreshold) earlier in this article.</span></span>

## <a name="northwind-odata-web-service-customer-dashboard-scenario"></a><span data-ttu-id="4742a-271">Northwind OData web service (Customer Dashboard scenario)</span><span class="sxs-lookup"><span data-stu-id="4742a-271">Northwind OData web service (Customer Dashboard scenario)</span></span>
<span data-ttu-id="4742a-272"><a name="sectionSection3"> </a></span><span class="sxs-lookup"><span data-stu-id="4742a-272"></span></span>

<span data-ttu-id="4742a-273">The Customer Dashboard scenario uses JQuery AJAX to invoke the NorthWind OData service to return customer information.</span><span class="sxs-lookup"><span data-stu-id="4742a-273">The Customer Dashboard scenario uses JQuery AJAX to invoke the NorthWind OData service to return customer information.</span></span> <span data-ttu-id="4742a-274">The app stores its data in a web service, then uses  [OData](http://www.odata.org/) to retrieve it.</span><span class="sxs-lookup"><span data-stu-id="4742a-274">The app stores its data in a web service, then uses  [OData](http://www.odata.org/) to retrieve it.</span></span>

<span data-ttu-id="4742a-275">The following are the advantages to using this approach:</span><span class="sxs-lookup"><span data-stu-id="4742a-275">The following are the advantages to using this approach:</span></span>

- <span data-ttu-id="4742a-276">A given web service can support multiple add-ins.</span><span class="sxs-lookup"><span data-stu-id="4742a-276">A given web service can support multiple add-ins.</span></span>
    
- <span data-ttu-id="4742a-277">You can update your web service without having to update and redeploy your app.</span><span class="sxs-lookup"><span data-stu-id="4742a-277">You can update your web service without having to update and redeploy your app.</span></span>
    
- <span data-ttu-id="4742a-278">Your SharePoint and web service installations do not affect one another.</span><span class="sxs-lookup"><span data-stu-id="4742a-278">Your SharePoint and web service installations do not affect one another.</span></span>
    
- <span data-ttu-id="4742a-279">Hosting services such as Microsoft Azure enable you to scale your web services.</span><span class="sxs-lookup"><span data-stu-id="4742a-279">Hosting services such as Microsoft Azure enable you to scale your web services.</span></span>
    
- <span data-ttu-id="4742a-280">You can back up and restore information on your web services separately from your SharePoint site.</span><span class="sxs-lookup"><span data-stu-id="4742a-280">You can back up and restore information on your web services separately from your SharePoint site.</span></span>
    
- <span data-ttu-id="4742a-281">You don't lose data when uninstalling your app, unless the app uses the  **AppUninstalled** event to delete the data.</span><span class="sxs-lookup"><span data-stu-id="4742a-281">You don't lose data when uninstalling your app, unless the app uses the  **AppUninstalled** event to delete the data.</span></span>
    
<span data-ttu-id="4742a-282">The customer dashboard scenario stores its data in a web service that implements the OData standard to retrieve data.</span><span class="sxs-lookup"><span data-stu-id="4742a-282">The customer dashboard scenario stores its data in a web service that implements the OData standard to retrieve data.</span></span> <span data-ttu-id="4742a-283">In the customer dashboard interface, you select a customer from a drop-down menu, and customer information displays in the  **Customer Info** pane.</span><span class="sxs-lookup"><span data-stu-id="4742a-283">In the customer dashboard interface, you select a customer from a drop-down menu, and customer information displays in the  **Customer Info** pane.</span></span>

<span data-ttu-id="4742a-284">This UI page is a Model-View-Controller view.</span><span class="sxs-lookup"><span data-stu-id="4742a-284">This UI page is a Model-View-Controller view.</span></span> <span data-ttu-id="4742a-285">The display is defined in the Views/CustomerDashboard\Home.cshtml file.</span><span class="sxs-lookup"><span data-stu-id="4742a-285">The display is defined in the Views/CustomerDashboard\Home.cshtml file.</span></span> <span data-ttu-id="4742a-286">The underlying code is in the Scripts/CustomerDashboard.js file.</span><span class="sxs-lookup"><span data-stu-id="4742a-286">The underlying code is in the Scripts/CustomerDashboard.js file.</span></span> <span data-ttu-id="4742a-287">The JavaScript code uses AJAX to query the Northwind web service.</span><span class="sxs-lookup"><span data-stu-id="4742a-287">The JavaScript code uses AJAX to query the Northwind web service.</span></span> <span data-ttu-id="4742a-288">Because this is an OData service, the web service query consists of query string arguments attached to a URL that points to a web service endpoint.</span><span class="sxs-lookup"><span data-stu-id="4742a-288">Because this is an OData service, the web service query consists of query string arguments attached to a URL that points to a web service endpoint.</span></span> <span data-ttu-id="4742a-289">The service returns customer information in JSON format.</span><span class="sxs-lookup"><span data-stu-id="4742a-289">The service returns customer information in JSON format.</span></span>

<span data-ttu-id="4742a-290">The following code runs when you choose the  **Customer Dashboard** link.</span><span class="sxs-lookup"><span data-stu-id="4742a-290">The following code runs when you choose the  **Customer Dashboard** link.</span></span> <span data-ttu-id="4742a-291">It retrieves all the customer names and IDs in order to populate the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="4742a-291">It retrieves all the customer names and IDs in order to populate the drop-down menu.</span></span>

```C#
var getCustomerIDsUrl = "https://odatasampleservices.azurewebsites.net/V3/Northwind/Northwind.svc/Customers?$format=json&amp;$select=CustomerID";
    $.get(getCustomerIDsUrl).done(getCustomerIDsDone)
        .error(function (jqXHR, textStatus, errorThrown) {
            $('#topErrorMessage').text('Can\'t get customers. An error occurred: ' + jqXHR.statusText);
        });
```

<span data-ttu-id="4742a-292">The following code runs when you select a customer name from the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="4742a-292">The following code runs when you select a customer name from the drop-down menu.</span></span> <span data-ttu-id="4742a-293">It uses the OData  **$filter** argument to specify the customer ID and other query string arguments to retrieve information related to this customer.</span><span class="sxs-lookup"><span data-stu-id="4742a-293">It uses the OData  **$filter** argument to specify the customer ID and other query string arguments to retrieve information related to this customer.</span></span>

```C#
var url = "https://odatasampleservices.azurewebsites.net/V3/Northwind/Northwind.svc/Customers?$format=json" +  "&amp;$select=CustomerID,CompanyName,ContactName,ContactTitle,Address,City,Country,Phone,Fax" + "&amp;$filter=CustomerID eq '" + customerID + "'";

$.get(url).done(getCustomersDone)
   .error(function (jqXHR, textStatus, errorThrown) {
          alert('Can\'t get customer ' + customerID + '. An error occurred: ' + 
                 jqXHR.statusText);
});
```

## <a name="azure-table-storage-customer-service-survey-scenario"></a><span data-ttu-id="4742a-294">Azure table storage (Customer Service Survey scenario)</span><span class="sxs-lookup"><span data-stu-id="4742a-294">Azure table storage (Customer Service Survey scenario)</span></span>
<span data-ttu-id="4742a-295"><a name="sectionSection4"> </a></span><span class="sxs-lookup"><span data-stu-id="4742a-295"></span></span>

<span data-ttu-id="4742a-296">The Customer Service Survey scenario allows a customer service representative to see their rating based on customer surveys and uses Azure table storage and the Microsoft.WindowsAzure.Storage.Table.CloudTable API to store and interact with the data.</span><span class="sxs-lookup"><span data-stu-id="4742a-296">The Customer Service Survey scenario allows a customer service representative to see their rating based on customer surveys and uses Azure table storage and the Microsoft.WindowsAzure.Storage.Table.CloudTable API to store and interact with the data.</span></span>

<span data-ttu-id="4742a-297">The following are the advantages to using this approach:</span><span class="sxs-lookup"><span data-stu-id="4742a-297">The following are the advantages to using this approach:</span></span>

- <span data-ttu-id="4742a-298">Azure storage tables support more than one app.</span><span class="sxs-lookup"><span data-stu-id="4742a-298">Azure storage tables support more than one app.</span></span>
    
- <span data-ttu-id="4742a-299">You can update Azure storage tables without having to update and redeploy your app.</span><span class="sxs-lookup"><span data-stu-id="4742a-299">You can update Azure storage tables without having to update and redeploy your app.</span></span>
    
- <span data-ttu-id="4742a-300">Your SharePoint installation and Azure storage tables have no effect on each other's performance.</span><span class="sxs-lookup"><span data-stu-id="4742a-300">Your SharePoint installation and Azure storage tables have no effect on each other's performance.</span></span>
    
- <span data-ttu-id="4742a-301">Azure storage tables scale easily.</span><span class="sxs-lookup"><span data-stu-id="4742a-301">Azure storage tables scale easily.</span></span>
    
- <span data-ttu-id="4742a-302">You can back up and restore your Azure storage tables separately from your SharePoint site.</span><span class="sxs-lookup"><span data-stu-id="4742a-302">You can back up and restore your Azure storage tables separately from your SharePoint site.</span></span>
    
- <span data-ttu-id="4742a-303">You don't lose data when you uninstall your app, unless the app uses the  **AppUninstalled** event to delete the data.</span><span class="sxs-lookup"><span data-stu-id="4742a-303">You don't lose data when you uninstall your app, unless the app uses the  **AppUninstalled** event to delete the data.</span></span>
    
<span data-ttu-id="4742a-304">The app's interface displays the current user's survey rating in the center page.</span><span class="sxs-lookup"><span data-stu-id="4742a-304">The app's interface displays the current user's survey rating in the center page.</span></span> <span data-ttu-id="4742a-305">If that Azure storage table is empty, the app will add some information to the table before it displays it.</span><span class="sxs-lookup"><span data-stu-id="4742a-305">If that Azure storage table is empty, the app will add some information to the table before it displays it.</span></span>

<span data-ttu-id="4742a-306">The following code from the CSRInfoController.cs defines the  **Home** method that retrieves the user's **nameId**.</span><span class="sxs-lookup"><span data-stu-id="4742a-306">The following code from the CSRInfoController.cs defines the  **Home** method that retrieves the user's **nameId**.</span></span>

```C#
[SharePointContextFilter]
public ActionResult Home()
{
    var context = 
        SharePointContextProvider.Current.GetSharePointContext(HttpContext);
    var sharePointService = new SharePointService(context);
    var currentUser = sharePointService.GetCurrentUser();
    ViewBag.UserName = currentUser.Title;

    var surveyRatingsService = new SurveyRatingsService();
    ViewBag.Score = surveyRatingsService.GetUserScore(currentUser.UserId.NameId);

    return View();
}
```

<span data-ttu-id="4742a-307">The following code from the SurveyRatingService.cs file defines the  **SurveyRatingsService** constructor, which sets up the connection to the Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="4742a-307">The following code from the SurveyRatingService.cs file defines the  **SurveyRatingsService** constructor, which sets up the connection to the Azure storage account.</span></span>

```C#
public SurveyRatingsService(string storageConnectionStringConfigName = 
        "StorageConnectionString")
{
    var connectionString = Util.GetConfigSetting("StorageConnectionString");
    var storageAccount = CloudStorageAccount.Parse(connectionString);

    this.tableClient = storageAccount.CreateCloudTableClient();
    this.surveyRatingsTable = this.tableClient.GetTableReference("SurveyRatings");
    this.surveyRatingsTable.CreateIfNotExists();
}
```

<span data-ttu-id="4742a-308">The following code from the same file defines the  **GetUserScore** method, which retrieves the user's survey score from the Azure storage table.</span><span class="sxs-lookup"><span data-stu-id="4742a-308">The following code from the same file defines the  **GetUserScore** method, which retrieves the user's survey score from the Azure storage table.</span></span>

```C#
public float GetUserScore(string userName)
{
    var query = new TableQuery<Models.Customer>()
    .Select(new List<string> { "Score" })
    .Where(TableQuery.GenerateFilterCondition("Name", 
    QueryComparisons.Equal, userName));

    var items = surveyRatingsTable
         .ExecuteQuery(query)
             .ToArray();

    if (items.Length == 0)           
    return AddSurveyRatings(userName);

    return (float)items.Average(c => c.Score);
}
```

<span data-ttu-id="4742a-309">If the table doesn't contain any survey data related to the current user, the  **AddSurveyRating** method randomly assigns a score for the user.</span><span class="sxs-lookup"><span data-stu-id="4742a-309">If the table doesn't contain any survey data related to the current user, the  **AddSurveyRating** method randomly assigns a score for the user.</span></span>

```C#
private float AddSurveyRatings(string userName)
{
    float sum = 0;
    int count = 4;
    var random = new Random();

    for (int i = 0; i < count; i++)
    {
    var score = random.Next(80, 100);
    var customer = new Models.Customer(Guid.NewGuid(), userName, score);

    var insertOperation = TableOperation.Insert(customer);
    surveyRatingsTable.Execute(insertOperation);

    sum += score;
    }
    return sum / count;
}
```

## <a name="azure-queue-storage-customer-call-queue-scenario"></a><span data-ttu-id="4742a-310">Azure queue storage (Customer Call Queue scenario)</span><span class="sxs-lookup"><span data-stu-id="4742a-310">Azure queue storage (Customer Call Queue scenario)</span></span>
<span data-ttu-id="4742a-311"><a name="sectionSection5"> </a></span><span class="sxs-lookup"><span data-stu-id="4742a-311"></span></span>

<span data-ttu-id="4742a-312">The Customer Call Queue scenario lists callers in the support queue and simulates taking calls.</span><span class="sxs-lookup"><span data-stu-id="4742a-312">The Customer Call Queue scenario lists callers in the support queue and simulates taking calls.</span></span> <span data-ttu-id="4742a-313">The scenario uses Azure storage queues to store data and the  **Microsoft.WindowsAzure.Storage.Queue.CloudQueue** API with Model-View-Controller.</span><span class="sxs-lookup"><span data-stu-id="4742a-313">The scenario uses Azure storage queues to store data and the  **Microsoft.WindowsAzure.Storage.Queue.CloudQueue** API with Model-View-Controller.</span></span>

<span data-ttu-id="4742a-314">The following are the advantages to using this approach:</span><span class="sxs-lookup"><span data-stu-id="4742a-314">The following are the advantages to using this approach:</span></span>

- <span data-ttu-id="4742a-315">Azure storage queues support more than one app.</span><span class="sxs-lookup"><span data-stu-id="4742a-315">Azure storage queues support more than one app.</span></span>
    
- <span data-ttu-id="4742a-316">You can update Azure storage queues without having to update and redeploy your app.</span><span class="sxs-lookup"><span data-stu-id="4742a-316">You can update Azure storage queues without having to update and redeploy your app.</span></span>
    
- <span data-ttu-id="4742a-317">Your SharePoint installation and Azure storage queues have no effect on each other's performance.</span><span class="sxs-lookup"><span data-stu-id="4742a-317">Your SharePoint installation and Azure storage queues have no effect on each other's performance.</span></span>
    
- <span data-ttu-id="4742a-318">Azure storage queues scale easily.</span><span class="sxs-lookup"><span data-stu-id="4742a-318">Azure storage queues scale easily.</span></span>
    
- <span data-ttu-id="4742a-319">You can back up and restore your Azure storage queues separately from your SharePoint site.</span><span class="sxs-lookup"><span data-stu-id="4742a-319">You can back up and restore your Azure storage queues separately from your SharePoint site.</span></span>
    
- <span data-ttu-id="4742a-320">You don't lose data when you uninstall your app, unless the app uses the  **AppUninstalled** event to delete the data.</span><span class="sxs-lookup"><span data-stu-id="4742a-320">You don't lose data when you uninstall your app, unless the app uses the  **AppUninstalled** event to delete the data.</span></span>
    
<span data-ttu-id="4742a-321">The app's interface displays a support call queue in the center pane when you choose the  **Call Queue** link.</span><span class="sxs-lookup"><span data-stu-id="4742a-321">The app's interface displays a support call queue in the center pane when you choose the  **Call Queue** link.</span></span> <span data-ttu-id="4742a-322">You can simulate receiving calls (adding a call to the queue) by choosing **Simulate Calls**, and you can simulate taking the oldest call (removing a call from the queue) by choosing the  **Take Call** action associated with a given call.</span><span class="sxs-lookup"><span data-stu-id="4742a-322">You can simulate receiving calls (adding a call to the queue) by choosing **Simulate Calls**, and you can simulate taking the oldest call (removing a call from the queue) by choosing the  **Take Call** action associated with a given call.</span></span>

<span data-ttu-id="4742a-323">This page is a Model-View-Controller view that is defined in the Views\CallQueue\Home.cshmtl file.</span><span class="sxs-lookup"><span data-stu-id="4742a-323">This page is a Model-View-Controller view that is defined in the Views\CallQueue\Home.cshmtl file.</span></span> <span data-ttu-id="4742a-324">The Controllers\CallQueueController.cs file defines the  **CallQueueController** class, which contains methods for retrieving all calls in the queue, adding a call to the queue (simulating a call), and removing a call from the queue (taking a call).</span><span class="sxs-lookup"><span data-stu-id="4742a-324">The Controllers\CallQueueController.cs file defines the  **CallQueueController** class, which contains methods for retrieving all calls in the queue, adding a call to the queue (simulating a call), and removing a call from the queue (taking a call).</span></span> <span data-ttu-id="4742a-325">Each of these methods calls methods defined in the Services\CallQueueService.cs file, which uses the Azure storage queue API to retrieve the underlying information in the storage queue.</span><span class="sxs-lookup"><span data-stu-id="4742a-325">Each of these methods calls methods defined in the Services\CallQueueService.cs file, which uses the Azure storage queue API to retrieve the underlying information in the storage queue.</span></span>

```C#
public class CallQueueController : Controller
{
    public CallQueueService CallQueueService { get; private set; }

    public CallQueueController()
    {
        CallQueueService = new CallQueueService();
    }

    // GET: CallQueue
    public ActionResult Home(UInt16 displayCount = 10)
    {
        var calls = CallQueueService.PeekCalls(displayCount);
        ViewBag.DisplayCount = displayCount;
        ViewBag.TotalCallCount = CallQueueService.GetCallCount();
        return View(calls);
    }

    [HttpPost]
    public ActionResult SimulateCalls(string spHostUrl)
    {
        int count = CallQueueService.SimulateCalls();
        TempData["Message"] = string.Format("Successfully simulated {0} calls and added them to the call queue.", count);
        return RedirectToAction("Index", new { SPHostUrl = spHostUrl });
    }

    [HttpPost]
    public ActionResult TakeCall(string spHostUrl)
    {
        CallQueueService.DequeueCall();
        TempData["Message"] = "Call taken successfully and removed from the call queue!";
        return RedirectToAction("Index", new { SPHostUrl = spHostUrl });
    }
}
```

<span data-ttu-id="4742a-326">The CallQueueService.cs file defines the  **CallQueueService** class, which establishes the connection to the Azure storage queue.</span><span class="sxs-lookup"><span data-stu-id="4742a-326">The CallQueueService.cs file defines the  **CallQueueService** class, which establishes the connection to the Azure storage queue.</span></span> <span data-ttu-id="4742a-327">That class also contains the methods for adding, removing (dequeuing), and retrieving the calls from the queue.</span><span class="sxs-lookup"><span data-stu-id="4742a-327">That class also contains the methods for adding, removing (dequeuing), and retrieving the calls from the queue.</span></span>

```C#
public class CallQueueService
{
    private CloudQueueClient queueClient;

    private CloudQueue queue;

    public CallQueueService(string storageConnectionStringConfigName = "StorageConnectionString")
    {
        var connectionString = CloudConfigurationManager.GetSetting(storageConnectionStringConfigName);
        var storageAccount = CloudStorageAccount.Parse(connectionString);

        this.queueClient = storageAccount.CreateCloudQueueClient();
        this.queue = queueClient.GetQueueReference("calls");
        this.queue.CreateIfNotExists();
        }

        public int? GetCallCount()
        {
        queue.FetchAttributes();
        return queue.ApproximateMessageCount;
    }

    public IEnumerable<Call> PeekCalls(UInt16 count)
    {
        var messages = queue.PeekMessages(count);

        var serializer = new JavaScriptSerializer();
        foreach (var message in messages)
        {
        Call call = null;
        try
        {
        call = serializer.Deserialize<Call>(message.AsString);
        }
        catch { }

        if (call != null) yield return call;
        }
    }

    public void AddCall(Call call)
    {
        var serializer = new JavaScriptSerializer();
        var content = serializer.Serialize(call);
        var message = new CloudQueueMessage(content);
        queue.AddMessage(message);
    }

    public void DequeueCall()
    {
        var message = queue.GetMessage();
        queue.DeleteMessage(message);
    }

    public int SimulateCalls()
    {
        Random random = new Random();
        int count = random.Next(1, 6);
        for (int i = 0; i < count; i++)
        {
        int phoneNumber = random.Next();
        var call = new Call
        {
        ReceivedDate = DateTime.Now,
        PhoneNumber = phoneNumber.ToString("+1-000-000-0000")
        };
        AddCall(call);

        return count;
    }
}
```

## <a name="sql-azure-database-recent-orders-scenario"></a><span data-ttu-id="4742a-328">SQL Azure database (Recent Orders scenario)</span><span class="sxs-lookup"><span data-stu-id="4742a-328">SQL Azure database (Recent Orders scenario)</span></span>
<span data-ttu-id="4742a-329"><a name="sectionSection6"> </a></span><span class="sxs-lookup"><span data-stu-id="4742a-329"></span></span>

<span data-ttu-id="4742a-330">The Recent Orders scenario uses a direct call to the Northwind SQL Azure database to return all the orders for a given customer.</span><span class="sxs-lookup"><span data-stu-id="4742a-330">The Recent Orders scenario uses a direct call to the Northwind SQL Azure database to return all the orders for a given customer.</span></span>

<span data-ttu-id="4742a-331">The following are the advantages to using this approach:</span><span class="sxs-lookup"><span data-stu-id="4742a-331">The following are the advantages to using this approach:</span></span>

- <span data-ttu-id="4742a-332">A database can support more than one app.</span><span class="sxs-lookup"><span data-stu-id="4742a-332">A database can support more than one app.</span></span>
    
- <span data-ttu-id="4742a-333">You can update your database schema without having to update and redeploy your app, as long as the schema changes don't affect the queries in your app.</span><span class="sxs-lookup"><span data-stu-id="4742a-333">You can update your database schema without having to update and redeploy your app, as long as the schema changes don't affect the queries in your app.</span></span>
    
- <span data-ttu-id="4742a-334">A relational database can support many-to-many relationships and thus support more complex business scenarios.</span><span class="sxs-lookup"><span data-stu-id="4742a-334">A relational database can support many-to-many relationships and thus support more complex business scenarios.</span></span>
    
- <span data-ttu-id="4742a-335">You can use database design tools to optimize the design of your database.</span><span class="sxs-lookup"><span data-stu-id="4742a-335">You can use database design tools to optimize the design of your database.</span></span>
    
- <span data-ttu-id="4742a-336">Relational databases provide better performance than the other options when you need to execute complex operations in your queries, such as calculations and joins.</span><span class="sxs-lookup"><span data-stu-id="4742a-336">Relational databases provide better performance than the other options when you need to execute complex operations in your queries, such as calculations and joins.</span></span>
    
- <span data-ttu-id="4742a-337">A SQL Azure database allows you to import and export data easily, so it's easier to manage and move your data.</span><span class="sxs-lookup"><span data-stu-id="4742a-337">A SQL Azure database allows you to import and export data easily, so it's easier to manage and move your data.</span></span>
    
- <span data-ttu-id="4742a-338">You don't lose any data when you uninstall your app, unless the app uses the  **AppUninstalled** event to delete the data.</span><span class="sxs-lookup"><span data-stu-id="4742a-338">You don't lose any data when you uninstall your app, unless the app uses the  **AppUninstalled** event to delete the data.</span></span>
    
<span data-ttu-id="4742a-339">The recent orders interface works much like the customer dashboard interface.</span><span class="sxs-lookup"><span data-stu-id="4742a-339">The recent orders interface works much like the customer dashboard interface.</span></span> <span data-ttu-id="4742a-340">You choose on the  **Recent Orders** link in the left column, and then choose a customer from the drop-down menu at the top of the center pane.</span><span class="sxs-lookup"><span data-stu-id="4742a-340">You choose on the  **Recent Orders** link in the left column, and then choose a customer from the drop-down menu at the top of the center pane.</span></span> <span data-ttu-id="4742a-341">A list of orders from that customer will appear in the center pane.</span><span class="sxs-lookup"><span data-stu-id="4742a-341">A list of orders from that customer will appear in the center pane.</span></span>

<span data-ttu-id="4742a-342">This page is a Model-View-Controller view defined in the Views\CustomerDashboard\Orders.cshtml file.</span><span class="sxs-lookup"><span data-stu-id="4742a-342">This page is a Model-View-Controller view defined in the Views\CustomerDashboard\Orders.cshtml file.</span></span> <span data-ttu-id="4742a-343">Code in the Controllers\CustomerDashboardController.cs file uses the  [Entity Framework ](https://msdn.microsoft.com/en-us/data/ef.aspx) to query the **Orders** table in your SQL Azure database.</span><span class="sxs-lookup"><span data-stu-id="4742a-343">Code in the Controllers\CustomerDashboardController.cs file uses the  [Entity Framework ](https://msdn.microsoft.com/en-us/data/ef.aspx) to query the **Orders** table in your SQL Azure database.</span></span> <span data-ttu-id="4742a-344">The customer ID is passed by using a query string parameter in the URL that is passed when the user selects a customer from the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="4742a-344">The customer ID is passed by using a query string parameter in the URL that is passed when the user selects a customer from the drop-down menu.</span></span> <span data-ttu-id="4742a-345">The query creates a join on the **Customer**,  **Employee**, and  **Shipper** tables.</span><span class="sxs-lookup"><span data-stu-id="4742a-345">The query creates a join on the **Customer**,  **Employee**, and  **Shipper** tables.</span></span> <span data-ttu-id="4742a-346">The query result is then passed to the Model-View-Controller view that displays the results.</span><span class="sxs-lookup"><span data-stu-id="4742a-346">The query result is then passed to the Model-View-Controller view that displays the results.</span></span>

<span data-ttu-id="4742a-347">The following code from the CustomerDashboardController.cs file performs the database query and returns the data to the view.</span><span class="sxs-lookup"><span data-stu-id="4742a-347">The following code from the CustomerDashboardController.cs file performs the database query and returns the data to the view.</span></span>

```C#
public ActionResult Orders(string customerId)
{            
    Order[] orders;
    using (var db = new NorthWindEntities())
    {
            orders = db.Orders
                  .Include(o => o.Customer)
                  .Include(o => o.Employee)
                  .Include(o => o.Shipper)
                  .Where(c => c.CustomerID == customerId)
                  .ToArray();
    }

    ViewBag.SharePointContext = 
        SharePointContextProvider.Current.GetSharePointContext(HttpContext);

    return View(orders);
}
```

## <a name="see-also"></a><span data-ttu-id="4742a-348">См. также</span><span class="sxs-lookup"><span data-stu-id="4742a-348">See also</span></span>
<span data-ttu-id="4742a-349"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="4742a-349"></span></span>

-  [<span data-ttu-id="4742a-350">Composite business add-ins for SharePoint 2013 and SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="4742a-350">Composite business add-ins for SharePoint 2013 and SharePoint Online</span></span>](Composite-buisness-apps-for-SharePoint.md)
    
-  [<span data-ttu-id="4742a-351">Шаблоны и рекомендации по разработке решений для Office 365 на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="4742a-351">Office 365 Development Patterns and Practices on GitHub</span></span>](https://github.com/SharePoint/PnP)
