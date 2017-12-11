---
title: "Развертывание пользовательских функций с помощью решений SharePoint Foundation"
ms.date: 09/25/2017
keywords: how to,howdoi,howto,udf list,WSS Solutions
f1_keywords: how to,howdoi,howto,udf list,WSS Solutions
ms.prod: sharepoint
ms.assetid: 97751a6c-ef73-4d95-a3c4-98014d84ba48
ms.openlocfilehash: e731eee138d97bd80cea236f78fd760cf7af2e7a
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="deploy-udfs-using-sharepoint-foundation-solutions"></a><span data-ttu-id="89003-103">Развертывание пользовательских функций с помощью решений SharePoint Foundation</span><span class="sxs-lookup"><span data-stu-id="89003-103">Deploy UDFs using SharePoint Foundation solutions</span></span>

<span data-ttu-id="89003-104">This example shows how to deploy a user-defined function (UDF) DLL by using the Microsoft SharePoint Foundation solution framework.</span><span class="sxs-lookup"><span data-stu-id="89003-104">This example shows how to deploy a user-defined function (UDF) DLL by using the Microsoft SharePoint Foundation solution framework.</span></span>
  
    
    

<span data-ttu-id="89003-p101">The SharePoint Foundation solution framework lets you bundle all the components to extend SharePoint Foundation in a new file called a solution file (a CAB-based format with a .wsp extension). A solution is a deployable, reusable package that can contain a set of features, site definitions, and assemblies that you can apply to a site, and individually enable or disable. Additionally, you can use the solution file to deploy the contents of a Web Part package, including assemblies, class resources, .dwp files, and other package components. For more information about the SharePoint Foundation solution framework, see the SharePoint Foundation node in the  [Начало работы по разработке для SharePoint Foundation](http://msdn.microsoft.com/library/ef1187aa-e007-4490-8191-db36a50b3ae4%28Office.15%29.aspx) (http://msdn.microsoft.com/en-us/library/ee539432(office.14).aspx). The procedure for creating and deploying a UDF assembly by using SharePoint Foundation solution framework is as follows:</span><span class="sxs-lookup"><span data-stu-id="89003-p101">The SharePoint Foundation solution framework lets you bundle all the components to extend SharePoint Foundation in a new file called a solution file (a CAB-based format with a .wsp extension). A solution is a deployable, reusable package that can contain a set of features, site definitions, and assemblies that you can apply to a site, and individually enable or disable. Additionally, you can use the solution file to deploy the contents of a Web Part package, including assemblies, class resources, .dwp files, and other package components. For more information about the SharePoint Foundation solution framework, see the SharePoint Foundation node in the  [Getting Started with Development for SharePoint Foundation 2010](http://msdn.microsoft.com/library/ef1187aa-e007-4490-8191-db36a50b3ae4%28Office.15%29.aspx) (http://msdn.microsoft.com/en-us/library/ee539432(office.14).aspx). The procedure for creating and deploying a UDF assembly by using SharePoint Foundation solution framework is as follows:</span></span>
  
    
    


1. <span data-ttu-id="89003-110">Create the solution manifest file, Manifest.xml.</span><span class="sxs-lookup"><span data-stu-id="89003-110">Create the solution manifest file, Manifest.xml.</span></span>
    
    <span data-ttu-id="89003-p102">The solution manifest (always called Manifest.xml) is stored at the root of a solution file. This file defines the list of features, site definitions, resource files, Web Part files, and assemblies to be processed. It does not define the file structure; if files are included in a solution but not listed in the manifest XML file, they are not processed in any way.</span><span class="sxs-lookup"><span data-stu-id="89003-p102">The solution manifest (always called Manifest.xml) is stored at the root of a solution file. This file defines the list of features, site definitions, resource files, Web Part files, and assemblies to be processed. It does not define the file structure; if files are included in a solution but not listed in the manifest XML file, they are not processed in any way.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="89003-114">[!Примечание] For more information about the structure of the manifest XML file, see the SharePoint Foundation documentation.</span><span class="sxs-lookup"><span data-stu-id="89003-114">For more information about the structure of the manifest XML file, see the SharePoint Foundation documentation.</span></span> 

2. <span data-ttu-id="89003-115">Package the UDF assembly and Manifest.xml into a CAB file.</span><span class="sxs-lookup"><span data-stu-id="89003-115">Package the UDF assembly and Manifest.xml into a CAB file.</span></span>
    
  
3. <span data-ttu-id="89003-116">Make sure that the SharePoint Foundation Administration service is running on the server.</span><span class="sxs-lookup"><span data-stu-id="89003-116">Make sure that the SharePoint Foundation Administration service is running on the server.</span></span>
    
  
4. <span data-ttu-id="89003-117">Add the solution to the server by using stsadm.exe.</span><span class="sxs-lookup"><span data-stu-id="89003-117">Add the solution to the server by using stsadm.exe.</span></span>
    
  
5. <span data-ttu-id="89003-118">Deploy the solution by using stsadm.exe.</span><span class="sxs-lookup"><span data-stu-id="89003-118">Deploy the solution by using stsadm.exe.</span></span>
    
  
<span data-ttu-id="89003-119">Each Службы Excel trusted location has an **AllowUdfs** flag.</span><span class="sxs-lookup"><span data-stu-id="89003-119">Each Excel Services trusted location has an **AllowUdfs** flag.</span></span>

> [!NOTE]
> <span data-ttu-id="89003-p103">[!Примечание] The **AllowUdfs** flag is denoted by the **User-defined functions allowed** option on the Службы Excel Trusted File Locations page. To learn how to navigate to the Trusted File Locations page, see [Step 3: Deploying and Enabling UDFs](step-3-deploying-and-enabling-udfs.md).</span><span class="sxs-lookup"><span data-stu-id="89003-p103">The **AllowUdfs** flag is denoted by the **User-defined functions allowed** option on the Excel Services Trusted File Locations page. To learn how to navigate to the Trusted File Locations page, see [Step 3: Deploying and Enabling UDFs](step-3-deploying-and-enabling-udfs.md).</span></span> 
  
    
    

<span data-ttu-id="89003-122">In order to allow UDFs to be called from a specific trusted location, you must:</span><span class="sxs-lookup"><span data-stu-id="89003-122">In order to allow UDFs to be called from a specific trusted location, you must:</span></span>
- <span data-ttu-id="89003-p104">Set the **AllowUdfs** value to **true**. The default value is **false**.</span><span class="sxs-lookup"><span data-stu-id="89003-p104">Set the **AllowUdfs** value to **true**. The default value is **false**.</span></span> 
    
  
- <span data-ttu-id="89003-125">Add the UDF assembly to the trusted UDF list to allow the UDF to be called from a workbook.</span><span class="sxs-lookup"><span data-stu-id="89003-125">Add the UDF assembly to the trusted UDF list to allow the UDF to be called from a workbook.</span></span>
    
  
<span data-ttu-id="89003-126">For more information on how to enable UDFs and add UDFs to the trusted UDF list, see  [How to: Enable UDFs](how-to-enable-udfs.md).</span><span class="sxs-lookup"><span data-stu-id="89003-126">For more information on how to enable UDFs and add UDFs to the trusted UDF list, see  [How to: Enable UDFs](how-to-enable-udfs.md).</span></span>

> [!NOTE]
> <span data-ttu-id="89003-p105">[!Примечание] To avoid name collision, give your UDF assemblies and their dependencies strong names, and name them as uniquely as possible. For more information, see  [Excel Services Best Practices](excel-services-best-practices.md) and [Excel Services Known Issues and Tips](excel-services-known-issues-and-tips.md).</span><span class="sxs-lookup"><span data-stu-id="89003-p105">To avoid name collision, give your UDF assemblies and their dependencies strong names, and name them as uniquely as possible. For more information, see  [Excel Services Best Practices](excel-services-best-practices.md) and [Excel Services Known Issues and Tips](excel-services-known-issues-and-tips.md).</span></span> 
  
    
    


## <a name="procedure"></a><span data-ttu-id="89003-129">Procedure</span><span class="sxs-lookup"><span data-stu-id="89003-129">Procedure</span></span>


### <a name="to-create-the-manifestxml-file"></a><span data-ttu-id="89003-130">To create the Manifest.xml file</span><span class="sxs-lookup"><span data-stu-id="89003-130">To create the Manifest.xml file</span></span>


1. <span data-ttu-id="89003-131">Right-click your project in **Solution Explorer**, point to **Add**, and then click **New Item**.</span><span class="sxs-lookup"><span data-stu-id="89003-131">Right-click your project in **Solution Explorer**, point to **Add**, and then click **New Item**.</span></span>
    
  
2. <span data-ttu-id="89003-132">Select **XML File**, and name the file Manifest.xml.</span><span class="sxs-lookup"><span data-stu-id="89003-132">Select **XML File**, and name the file Manifest.xml.</span></span>
    
  
3. <span data-ttu-id="89003-133">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="89003-133">Click **Add**.</span></span>
    
  
4. <span data-ttu-id="89003-134">Add the following content to the file:</span><span class="sxs-lookup"><span data-stu-id="89003-134">Add the following content to the file:</span></span>
    
```XML
  
<?xml version="1.0" encoding="utf-8" ?>
<Solution xmlns="http://schemas.microsoft.com/sharepoint/" SolutionId="{57568687-2CC0-45bf-B66A-2D50D57108CA}" DeploymentServerType="ApplicationServer">
  <Assemblies>
    <Assembly DeploymentTarget="GlobalAssemblyCache" Location="EcsUdfsCommonSet.dll"/>
  </Assemblies>
</Solution>
```


    > [!NOTE]
    > You should generate a unique GUID for each solution. For more information about **Solution** element, see the SharePoint Foundation [Solutions and Web Part Packages](http://msdn.microsoft.com/library/a145a5eb-fbb6-4328-b5b3-96bf5ce89a19%28Office.15%29.aspx) (http://msdn.microsoft.com/en-us/library/ms413687.aspx).

### <a name="to-create-a-solution-package"></a><span data-ttu-id="89003-135">To create a solution package</span><span class="sxs-lookup"><span data-stu-id="89003-135">To create a solution package</span></span>


- <span data-ttu-id="89003-136">For information about how to create the solution file, see the "Creating a Solution" topic under the "Solutions and Web Part Packages" node in the SharePoint Foundation SDK.</span><span class="sxs-lookup"><span data-stu-id="89003-136">For information about how to create the solution file, see the "Creating a Solution" topic under the "Solutions and Web Part Packages" node in the SharePoint Foundation SDK.</span></span> 
    
  

### <a name="to-verify-whether-sharepoint-foundation-administration-is-running"></a><span data-ttu-id="89003-137">To verify whether SharePoint Foundation Administration is running</span><span class="sxs-lookup"><span data-stu-id="89003-137">To verify whether SharePoint Foundation Administration is running</span></span>


1. <span data-ttu-id="89003-138">Click **Start**, point to **Administrative Tools**, and then double-click **Services**.</span><span class="sxs-lookup"><span data-stu-id="89003-138">Click **Start**, point to **Administrative Tools**, and then double-click **Services**.</span></span> 
    
    <span data-ttu-id="89003-139">The **Services** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="89003-139">The **Services** dialog box appears.</span></span>
    
  
2. <span data-ttu-id="89003-p106">Make sure that the status of SharePoint Foundation Administration service shows **Started**. If it does not, right-click SharePoint Foundation Administration, and then select **Start**.</span><span class="sxs-lookup"><span data-stu-id="89003-p106">Make sure that the status of SharePoint Foundation Administration service shows **Started**. If it does not, right-click SharePoint Foundation Administration, and then select **Start**.</span></span>
    
  

### <a name="to-add-the-solution"></a><span data-ttu-id="89003-142">To add the solution</span><span class="sxs-lookup"><span data-stu-id="89003-142">To add the solution</span></span>


1. <span data-ttu-id="89003-143">Click **Start**, click **Run**, and then typecmd.</span><span class="sxs-lookup"><span data-stu-id="89003-143">Click **Start**, click **Run**, and then typecmd.</span></span> 
    
    <span data-ttu-id="89003-144">The command prompt console appears.</span><span class="sxs-lookup"><span data-stu-id="89003-144">The command prompt console appears.</span></span>
    
  
2. <span data-ttu-id="89003-145">Run the following script to add the solution to SharePoint server:</span><span class="sxs-lookup"><span data-stu-id="89003-145">Run the following script to add the solution to SharePoint server:</span></span> 
    
    <span data-ttu-id="89003-146">stsadm.exe -o addsolution -filename <pathtoCAB></span><span class="sxs-lookup"><span data-stu-id="89003-146">stsadm.exe -o addsolution -filename <pathtoCAB></span></span>
    
    > [!NOTE]
    > <span data-ttu-id="89003-147">[!Примечание] You can find the Stsadm.exe at: > C:\\Program Files\\Common Files\\Microsoft Shared\\web server extensions\\12\\BIN.</span><span class="sxs-lookup"><span data-stu-id="89003-147">You can find the Stsadm.exe at: > C:\\Program Files\\Common Files\\Microsoft Shared\\web server extensions\\12\\BIN.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="89003-148">[!Примечание] For more information about Stsadm.exe command options, see the  [Stsadm to Windows PowerShell Mapping (SharePoint Foundation 2010)](http://technet.microsoft.com/en-us/library/ff621081.aspx) (http://technet.microsoft.com/en-us/library/ff621081.aspx).</span><span class="sxs-lookup"><span data-stu-id="89003-148">For more information about Stsadm.exe command options, see the  [Stsadm to Windows PowerShell Mapping (SharePoint Foundation 2010)](http://technet.microsoft.com/en-us/library/ff621081.aspx) (http://technet.microsoft.com/en-us/library/ff621081.aspx).</span></span>

  
    
    

### <a name="to-deploy-the-solution"></a><span data-ttu-id="89003-149">To deploy the solution</span><span class="sxs-lookup"><span data-stu-id="89003-149">To deploy the solution</span></span>


1. <span data-ttu-id="89003-150">Click **Start**, click **Run**, and then typecmd.</span><span class="sxs-lookup"><span data-stu-id="89003-150">Click **Start**, click **Run**, and then typecmd.</span></span> 
    
    <span data-ttu-id="89003-151">The command prompt console appears.</span><span class="sxs-lookup"><span data-stu-id="89003-151">The command prompt console appears.</span></span>
    
  
2. <span data-ttu-id="89003-152">Run the following script to deploy the solution to SharePoint server.</span><span class="sxs-lookup"><span data-stu-id="89003-152">Run the following script to deploy the solution to SharePoint server.</span></span> 
    
    <span data-ttu-id="89003-153">stsadm.exe -o deploysolution -name <filename of the CAB> -immediate -allowGacDeployment</span><span class="sxs-lookup"><span data-stu-id="89003-153">stsadm.exe -o deploysolution -name <filename of the CAB> -immediate -allowGacDeployment</span></span>
    
    <span data-ttu-id="89003-154">You should now see your UDF DLL in the global assembly cache.</span><span class="sxs-lookup"><span data-stu-id="89003-154">You should now see your UDF DLL in the global assembly cache.</span></span>
    
  

## <a name="see-also"></a><span data-ttu-id="89003-155">См. также</span><span class="sxs-lookup"><span data-stu-id="89003-155">See also</span></span>


#### <a name="tasks"></a><span data-ttu-id="89003-156">Задачи</span><span class="sxs-lookup"><span data-stu-id="89003-156">Tasks</span></span>


  
    
    
 [<span data-ttu-id="89003-157">How to: Create a UDF That Calls a Web Service</span><span class="sxs-lookup"><span data-stu-id="89003-157">How to: Create a UDF That Calls a Web Service</span></span>](how-to-create-a-udf-that-calls-a-web-service.md)
  
    
    
 [<span data-ttu-id="89003-158">How to: Enable UDFs</span><span class="sxs-lookup"><span data-stu-id="89003-158">How to: Enable UDFs</span></span>](how-to-enable-udfs.md)
  
    
    
 [<span data-ttu-id="89003-159">How to: Restrict UDF Code Access Security Permissions</span><span class="sxs-lookup"><span data-stu-id="89003-159">How to: Restrict UDF Code Access Security Permissions</span></span>](how-to-restrict-udf-code-access-security-permissions.md)
#### <a name="concepts"></a><span data-ttu-id="89003-160">Основные понятия</span><span class="sxs-lookup"><span data-stu-id="89003-160">Concepts</span></span>


  
    
    
 [<span data-ttu-id="89003-161">Walkthrough: Developing a Managed-Code UDF</span><span class="sxs-lookup"><span data-stu-id="89003-161">Walkthrough: Developing a Managed-Code UDF</span></span>](walkthrough-developing-a-managed-code-udf.md)
  
    
    
 [<span data-ttu-id="89003-162">Frequently Asked Questions About Excel Services UDFs</span><span class="sxs-lookup"><span data-stu-id="89003-162">Frequently Asked Questions About Excel Services UDFs</span></span>](frequently-asked-questions-about-excel-services-udfs.md)
  
    
    
 [<span data-ttu-id="89003-163">Understanding Excel Services UDFs</span><span class="sxs-lookup"><span data-stu-id="89003-163">Understanding Excel Services UDFs</span></span>](understanding-excel-services-udfs.md)
