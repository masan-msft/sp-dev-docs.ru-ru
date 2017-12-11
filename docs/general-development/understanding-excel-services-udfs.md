---
title: Understanding Excel Services UDFs
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: a1567278-fac4-4b3b-a814-56f2376c1217
ms.openlocfilehash: a0cac568ed46e0b2230b302d514ba8f271ee636d
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="understanding-excel-services-udfs"></a><span data-ttu-id="8915e-102">Understanding Excel Services UDFs</span><span class="sxs-lookup"><span data-stu-id="8915e-102">Understanding Excel Services UDFs</span></span>

<span data-ttu-id="8915e-p101">User-defined functions (UDFs) are custom functions that extend the calculation and data-import capabilities of Excel. Developers create custom calculation packages to provide:</span><span class="sxs-lookup"><span data-stu-id="8915e-p101">User-defined functions (UDFs) are custom functions that extend the calculation and data-import capabilities of Excel. Developers create custom calculation packages to provide:</span></span>
  
    
    


- <span data-ttu-id="8915e-105">Functions that are not built into Excel.</span><span class="sxs-lookup"><span data-stu-id="8915e-105">Functions that are not built into Excel.</span></span>
    
  
- <span data-ttu-id="8915e-106">Custom implementations to built-in functions.</span><span class="sxs-lookup"><span data-stu-id="8915e-106">Custom implementations to built-in functions.</span></span>
    
  
- <span data-ttu-id="8915e-107">Custom data feeds for legacy or unsupported data sources, and application-specific data flows.</span><span class="sxs-lookup"><span data-stu-id="8915e-107">Custom data feeds for legacy or unsupported data sources, and application-specific data flows.</span></span>
    
  

<span data-ttu-id="8915e-108">Users who create workbooks can call UDFs from a cell through formulasfor example, "=MyUdf(A1*3.42)"just like they call built-in functions.</span><span class="sxs-lookup"><span data-stu-id="8915e-108">Users who create workbooks can call UDFs from a cell through formulas—for example, "=MyUdf(A1*3.42)"—just like they call built-in functions.</span></span>
  
    
    

<span data-ttu-id="8915e-p102">Службы Excel UDFs give you the ability to use formulas in cells to call custom functions written in managed code and deployed to Microsoft SharePoint Server 2010. You can create UDFs to:</span><span class="sxs-lookup"><span data-stu-id="8915e-p102">Excel Services UDFs give you the ability to use formulas in cells to call custom functions written in managed code and deployed to Microsoft SharePoint Server 2010. You can create UDFs to:</span></span>
- <span data-ttu-id="8915e-111">Call custom mathematical functions.</span><span class="sxs-lookup"><span data-stu-id="8915e-111">Call custom mathematical functions.</span></span>
    
  
- <span data-ttu-id="8915e-112">Get data from custom data sources into worksheets.</span><span class="sxs-lookup"><span data-stu-id="8915e-112">Get data from custom data sources into worksheets.</span></span>
    
  
- <span data-ttu-id="8915e-113">Call Web services from the UDFs.</span><span class="sxs-lookup"><span data-stu-id="8915e-113">Call Web services from the UDFs.</span></span>
    
  

## <a name="creating-managed-code-udfs"></a><span data-ttu-id="8915e-114">Creating Managed-Code UDFs</span><span class="sxs-lookup"><span data-stu-id="8915e-114">Creating Managed-Code UDFs</span></span>

<span data-ttu-id="8915e-p103">An easy way to create an Службы Excel managed-code UDF is to use the Microsoft Visual Studio 2005 class library template. You will need to reference the Службы Excel UDF dynamic link library (DLL), named Microsoft.Office.Excel.Server.Udf.dll, in your managed-code UDF project.</span><span class="sxs-lookup"><span data-stu-id="8915e-p103">An easy way to create an Excel Services managed-code UDF is to use the Microsoft Visual Studio 2005 class library template. You will need to reference the Excel Services UDF dynamic link library (DLL), named Microsoft.Office.Excel.Server.Udf.dll, in your managed-code UDF project.</span></span> 
  
    
    
<span data-ttu-id="8915e-p104">Microsoft.Office.Excel.Server.Udf.dll has been compiled using Microsoft .NET Framework 2.0. If you use Visual Studio 2003 to create your managed-code UDF, you will not be able to reference Microsoft.Office.Excel.Server.Udf.dll. It is not possible for an assembly created with an older version of the .NET Framework to reference an assembly created with .NET Framework 2.0.</span><span class="sxs-lookup"><span data-stu-id="8915e-p104">Microsoft.Office.Excel.Server.Udf.dll has been compiled using Microsoft .NET Framework 2.0. If you use Visual Studio 2003 to create your managed-code UDF, you will not be able to reference Microsoft.Office.Excel.Server.Udf.dll. It is not possible for an assembly created with an older version of the .NET Framework to reference an assembly created with .NET Framework 2.0.</span></span>
  
    
    

### <a name="required-attributes"></a><span data-ttu-id="8915e-120">Required Attributes</span><span class="sxs-lookup"><span data-stu-id="8915e-120">Required Attributes</span></span>

<span data-ttu-id="8915e-p105">To use custom functions in a class as an Службы Excel UDF class, you must mark your UDF class with the **Microsoft.Office.Excel.Server.Udf.UdfClass** attribute. Any classes that are not marked with this attribute in the UDF assembly will be ignored by Службы вычислений Excel. They are not considered to be Службы Excel UDF classes.</span><span class="sxs-lookup"><span data-stu-id="8915e-p105">To use custom functions in a class as an Excel Services UDF class, you must mark your UDF class with the **Microsoft.Office.Excel.Server.Udf.UdfClass** attribute. Any classes that are not marked with this attribute in the UDF assembly will be ignored by Excel Calculation Services. They are not considered to be Excel Services UDF classes.</span></span>
  
    
    
<span data-ttu-id="8915e-p106">To use custom functions in a class as Службы Excel UDF methods, you must mark your UDF methods with the **Microsoft.Office.Excel.Server.Udf.UdfMethod** attribute. Any methods that are not marked with this attribute in the UDF assembly will be ignored because they are not considered to be Службы Excel UDF methods.</span><span class="sxs-lookup"><span data-stu-id="8915e-p106">To use custom functions in a class as Excel Services UDF methods, you must mark your UDF methods with the **Microsoft.Office.Excel.Server.Udf.UdfMethod** attribute. Any methods that are not marked with this attribute in the UDF assembly will be ignored because they are not considered to be Excel Services UDF methods.</span></span>
  
    
    
<span data-ttu-id="8915e-p107">The **Microsoft.Office.Excel.Server.Udf.UdfMethod**attribute has an **IsVolatile** property. You use the **IsVolatile** property to specify a UDF method as volatile or nonvolatile. The **IsVolatile** property takes a Boolean value. The default value is **false**, which means that particular UDF method is nonvolatile.</span><span class="sxs-lookup"><span data-stu-id="8915e-p107">The **Microsoft.Office.Excel.Server.Udf.UdfMethod**attribute has an **IsVolatile** property. You use the **IsVolatile** property to specify a UDF method as volatile or nonvolatile. The **IsVolatile** property takes a Boolean value. The default value is **false**, which means that particular UDF method is nonvolatile.</span></span>
  
    
    

### <a name="location-of-microsoftofficeexcelserverudfdll"></a><span data-ttu-id="8915e-130">Location of Microsoft.Office.Excel.Server.Udf.dll</span><span class="sxs-lookup"><span data-stu-id="8915e-130">Location of Microsoft.Office.Excel.Server.Udf.dll</span></span>

<span data-ttu-id="8915e-131">On the computer where you have installed SharePoint Server 2010, you can find a copy of Microsoft.Office.Excel.Server.Udf.dll at:</span><span class="sxs-lookup"><span data-stu-id="8915e-131">On the computer where you have installed SharePoint Server 2010, you can find a copy of Microsoft.Office.Excel.Server.Udf.dll at:</span></span>
  
    
    
 `[drive:]\\Program Files\\Common Files\\Microsoft Shared\\web server extensions\\14\\ISAPI`
  
    
    

## <a name="deployment-and-security"></a><span data-ttu-id="8915e-132">Deployment and Security</span><span class="sxs-lookup"><span data-stu-id="8915e-132">Deployment and Security</span></span>


### <a name="deployment-location-type"></a><span data-ttu-id="8915e-133">Deployment Location Type</span><span class="sxs-lookup"><span data-stu-id="8915e-133">Deployment Location Type</span></span>

<span data-ttu-id="8915e-p108">UDF assemblies can reside in a local directory, global assembly cache, or network share. In a farm scenario, the local directory path must be identical across the farm.</span><span class="sxs-lookup"><span data-stu-id="8915e-p108">UDF assemblies can reside in a local directory, global assembly cache, or network share. In a farm scenario, the local directory path must be identical across the farm.</span></span>
  
    
    

### <a name="identification-of-udf-assemblies"></a><span data-ttu-id="8915e-136">Identification of UDF Assemblies</span><span class="sxs-lookup"><span data-stu-id="8915e-136">Identification of UDF Assemblies</span></span>

<span data-ttu-id="8915e-137">You can expose the identity of a UDF assembly by using the full path or strong name of the assembly for Службы вычислений Excel to call.</span><span class="sxs-lookup"><span data-stu-id="8915e-137">You can expose the identity of a UDF assembly by using the full path or strong name of the assembly for Excel Calculation Services to call.</span></span> 
  
    
    
<span data-ttu-id="8915e-138">For example, you can use:</span><span class="sxs-lookup"><span data-stu-id="8915e-138">For example, you can use:</span></span>
  
    
    

- <span data-ttu-id="8915e-139">C:\\UDFs\\MySampleUdf.dll</span><span class="sxs-lookup"><span data-stu-id="8915e-139">C:\\UDFs\\MySampleUdf.dll</span></span> 
    
  
- <span data-ttu-id="8915e-140">\\\\MyNetworkServer\\UDFs\\MySampleUdf.dll</span><span class="sxs-lookup"><span data-stu-id="8915e-140">\\\\MyNetworkServer\\UDFs\\MySampleUdf.dll</span></span>
    
  
- <span data-ttu-id="8915e-141">CompanyName.Hierarchichal.MyUdfNamespace.MyUdfClassName.dll, Version=1.1.0.0, Culture=en, PublicKeyToken=e8123117d7ba9ae38</span><span class="sxs-lookup"><span data-stu-id="8915e-141">CompanyName.Hierarchichal.MyUdfNamespace.MyUdfClassName.dll, Version=1.1.0.0, Culture=en, PublicKeyToken=e8123117d7ba9ae38</span></span>
    
  

### <a name="enabling-udf-assemblies"></a><span data-ttu-id="8915e-142">Enabling UDF Assemblies</span><span class="sxs-lookup"><span data-stu-id="8915e-142">Enabling UDF Assemblies</span></span>

<span data-ttu-id="8915e-143">UDF assemblies are disabled by default.</span><span class="sxs-lookup"><span data-stu-id="8915e-143">UDF assemblies are disabled by default.</span></span> 
  
    
    
<span data-ttu-id="8915e-144">Each Службы Excel trusted location has an **AllowUdfs** flag.</span><span class="sxs-lookup"><span data-stu-id="8915e-144">Each Excel Services trusted location has an **AllowUdfs** flag.</span></span>
  
> [!NOTE] 
> <span data-ttu-id="8915e-p109">[!Примечание] The **AllowUdfs** flag is denoted by the **User-defined functions allowed** option on the Службы Excel Trusted File Locations page. To learn how to navigate to the Trusted File Locations page, see [Step 3: Deploying and Enabling UDFs](step-3-deploying-and-enabling-udfs.md).</span><span class="sxs-lookup"><span data-stu-id="8915e-p109">The **AllowUdfs** flag is denoted by the **User-defined functions allowed** option on the Excel Services Trusted File Locations page. To learn how to navigate to the Trusted File Locations page, see [Step 3: Deploying and Enabling UDFs](step-3-deploying-and-enabling-udfs.md).</span></span> 
  
    
    

<span data-ttu-id="8915e-p110">The default **AllowUdfs** value is **false**. If the **AllowUdfs** value is set to **false** in a particular trusted location, the workbooks in that trusted location are not allowed to call UDFs.</span><span class="sxs-lookup"><span data-stu-id="8915e-p110">The default **AllowUdfs** value is **false**. If the **AllowUdfs** value is set to **false** in a particular trusted location, the workbooks in that trusted location are not allowed to call UDFs.</span></span>
  
    
    
<span data-ttu-id="8915e-149">In order to allow UDFs to be called from a specific trusted location, you set the **AllowUdfs** value to **true**.</span><span class="sxs-lookup"><span data-stu-id="8915e-149">In order to allow UDFs to be called from a specific trusted location, you set the **AllowUdfs** value to **true**.</span></span>
  
    
    
<span data-ttu-id="8915e-p111">If the **AllowUdfs** value is **false** when a session is started on a workbook that has UDF calls in this trusted location, the UDF calls will fail. If you change the **AllowUdfs** value to **true** after a session has started, the UDF calls will also fail. This is because changes in the **AllowUdfs** flag take effect on the next session, after the configuration database has been updated.</span><span class="sxs-lookup"><span data-stu-id="8915e-p111">If the **AllowUdfs** value is **false** when a session is started on a workbook that has UDF calls in this trusted location, the UDF calls will fail. If you change the **AllowUdfs** value to **true** after a session has started, the UDF calls will also fail. This is because changes in the **AllowUdfs** flag take effect on the next session, after the configuration database has been updated.</span></span>
  
    
    

### <a name="allowing-udf-assemblies-to-run"></a><span data-ttu-id="8915e-153">Allowing UDF Assemblies to Run</span><span class="sxs-lookup"><span data-stu-id="8915e-153">Allowing UDF Assemblies to Run</span></span>

<span data-ttu-id="8915e-154">If administrators want to allow UDF assemblies to run, they have to register all UDF assemblies, and enable workbooks to call UDFs by setting the **AllowUdfs** flag to **true** in the trusted locations.</span><span class="sxs-lookup"><span data-stu-id="8915e-154">If administrators want to allow UDF assemblies to run, they have to register all UDF assemblies, and enable workbooks to call UDFs by setting the **AllowUdfs** flag to **true** in the trusted locations.</span></span>
  
    
    

### <a name="reloading-a-udf-assembly"></a><span data-ttu-id="8915e-155">Reloading a UDF Assembly</span><span class="sxs-lookup"><span data-stu-id="8915e-155">Reloading a UDF Assembly</span></span>

<span data-ttu-id="8915e-156">To reload a UDF assembly, you can run **iisreset** or restart the Службы вычислений Excel application domain.</span><span class="sxs-lookup"><span data-stu-id="8915e-156">To reload a UDF assembly, you can run **iisreset** or restart the Excel Calculation Services application domain.</span></span>
  
    
    

> <span data-ttu-id="8915e-157">**Осторожность:** Перезапуск IIS приведет к сбросу всех текущих сеансов.</span><span class="sxs-lookup"><span data-stu-id="8915e-157">**Caution:** Resetting IIS will end all current sessions.</span></span> <span data-ttu-id="8915e-158">> Для получения дополнительных сведений см [как: включение пользовательских функций](how-to-enable-udfs.md).</span><span class="sxs-lookup"><span data-stu-id="8915e-158">> For more information, see  [How to: Enable UDFs](how-to-enable-udfs.md).</span></span> 
  
    
    

<span data-ttu-id="8915e-159">For more information, see  [Unloading an Application from Memory](http://go.microsoft.com/fwlink/?LinkId=65706) (http://msdn.microsoft.com/library/default.asp?url=/library/en-us/csvr2002/htm/cs_mmc_administering_myhj.asp).</span><span class="sxs-lookup"><span data-stu-id="8915e-159">For more information, see  [Unloading an Application from Memory](http://go.microsoft.com/fwlink/?LinkId=65706) (http://msdn.microsoft.com/library/default.asp?url=/library/en-us/csvr2002/htm/cs_mmc_administering_myhj.asp).</span></span>
  
    
    

### <a name="default-code-access-security-permission-for-udf-assemblies"></a><span data-ttu-id="8915e-160">Default Code Access Security Permission for UDF Assemblies</span><span class="sxs-lookup"><span data-stu-id="8915e-160">Default Code Access Security Permission for UDF Assemblies</span></span>

<span data-ttu-id="8915e-161">By default, UDF assemblies run with full trust.</span><span class="sxs-lookup"><span data-stu-id="8915e-161">By default, UDF assemblies run with full trust.</span></span> 
  
    
    

### <a name="restricting-code-access-security-permission-for-udf-assemblies"></a><span data-ttu-id="8915e-162">Restricting Code Access Security Permission for UDF Assemblies</span><span class="sxs-lookup"><span data-stu-id="8915e-162">Restricting Code Access Security Permission for UDF Assemblies</span></span>

<span data-ttu-id="8915e-p113">If you do not want a particular UDF assembly to run with full trust, you must explicitly restrict code access security permission for that UDF assembly. You can configure the code groups and restrict permission by using the .NET Framework 2.0 Configuration tool.</span><span class="sxs-lookup"><span data-stu-id="8915e-p113">If you do not want a particular UDF assembly to run with full trust, you must explicitly restrict code access security permission for that UDF assembly. You can configure the code groups and restrict permission by using the .NET Framework 2.0 Configuration tool.</span></span> 
  
    
    
<span data-ttu-id="8915e-165">Developers can also use the **RequestMinimum** and **RequestOptional** methods in their code to ensure that their UDF assemblies don't get more permission than they require.</span><span class="sxs-lookup"><span data-stu-id="8915e-165">Developers can also use the **RequestMinimum** and **RequestOptional** methods in their code to ensure that their UDF assemblies don't get more permission than they require.</span></span>
  
    
    
<span data-ttu-id="8915e-166">For more information about configuring code groups, as well as the **RequestMinimum** and **RequestOptional** methods, see the following articles on MSDN:</span><span class="sxs-lookup"><span data-stu-id="8915e-166">For more information about configuring code groups, as well as the **RequestMinimum** and **RequestOptional** methods, see the following articles on MSDN:</span></span>
  
    
    

-  <span data-ttu-id="8915e-167">[Configuring Code Groups Using the .NET Framework Configuration Tool](http://msdn.microsoft.com/library/default.asp?url=/library/en-us/cpguide/html/cpconUsingNETConfigurationToolToWorkWithCodeGroups.asp?frame=true) (http://msdn.microsoft.com/library/default.asp?url=/library/en-us/cpguide/html/cpconUsingNETConfigurationToolToWorkWithCodeGroups.asp?frame=true)</span><span class="sxs-lookup"><span data-stu-id="8915e-167">[Configuring Code Groups Using the .NET Framework Configuration Tool](http://msdn.microsoft.com/library/default.asp?url=/library/en-us/cpguide/html/cpconUsingNETConfigurationToolToWorkWithCodeGroups.asp?frame=true) (http://msdn.microsoft.com/library/default.asp?url=/library/en-us/cpguide/html/cpconUsingNETConfigurationToolToWorkWithCodeGroups.asp?frame=true)</span></span>
    
  
-  <span data-ttu-id="8915e-168">[Code Access Security in Practice](http://go.microsoft.com/fwlink/?LinkId=65465) (http://msdn.microsoft.com/library/default.asp?url=/library/en-us/dnnetsec/html/thcmch08.asp)</span><span class="sxs-lookup"><span data-stu-id="8915e-168">[Code Access Security in Practice](http://go.microsoft.com/fwlink/?LinkId=65465) (http://msdn.microsoft.com/library/default.asp?url=/library/en-us/dnnetsec/html/thcmch08.asp)</span></span>
    
  

## <a name="see-also"></a><span data-ttu-id="8915e-169">См. также</span><span class="sxs-lookup"><span data-stu-id="8915e-169">See also</span></span>


#### <a name="tasks"></a><span data-ttu-id="8915e-170">Задачи</span><span class="sxs-lookup"><span data-stu-id="8915e-170">Tasks</span></span>


  
    
    
 [<span data-ttu-id="8915e-171">How to: Create a UDF That Calls a Web Service</span><span class="sxs-lookup"><span data-stu-id="8915e-171">How to: Create a UDF That Calls a Web Service</span></span>](how-to-create-a-udf-that-calls-a-web-service.md)
  
    
    
 [<span data-ttu-id="8915e-172">How to: Trust a Location</span><span class="sxs-lookup"><span data-stu-id="8915e-172">How to: Trust a Location</span></span>](how-to-trust-a-location.md)
  
    
    
 [<span data-ttu-id="8915e-173">How to: Catch Exceptions</span><span class="sxs-lookup"><span data-stu-id="8915e-173">How to: Catch Exceptions</span></span>](how-to-catch-exceptions.md)
  
    
    
 [<span data-ttu-id="8915e-174">How to: Enable UDFs</span><span class="sxs-lookup"><span data-stu-id="8915e-174">How to: Enable UDFs</span></span>](how-to-enable-udfs.md)
#### <a name="concepts"></a><span data-ttu-id="8915e-175">Основные понятия</span><span class="sxs-lookup"><span data-stu-id="8915e-175">Concepts</span></span>


  
    
    
 [<span data-ttu-id="8915e-176">Walkthrough: Developing a Managed-Code UDF</span><span class="sxs-lookup"><span data-stu-id="8915e-176">Walkthrough: Developing a Managed-Code UDF</span></span>](walkthrough-developing-a-managed-code-udf.md)
  
    
    
 [<span data-ttu-id="8915e-177">Frequently Asked Questions About Excel Services UDFs</span><span class="sxs-lookup"><span data-stu-id="8915e-177">Frequently Asked Questions About Excel Services UDFs</span></span>](frequently-asked-questions-about-excel-services-udfs.md)
  
    
    
 [<span data-ttu-id="8915e-178">Архитектура служб Excel</span><span class="sxs-lookup"><span data-stu-id="8915e-178">Excel Services Architecture</span></span>](excel-services-architecture.md)
  
    
    
 [<span data-ttu-id="8915e-179">Excel Services Alerts</span><span class="sxs-lookup"><span data-stu-id="8915e-179">Excel Services Alerts</span></span>](excel-services-alerts.md)
  
    
    
 [<span data-ttu-id="8915e-180">Excel Services Known Issues and Tips</span><span class="sxs-lookup"><span data-stu-id="8915e-180">Excel Services Known Issues and Tips</span></span>](excel-services-known-issues-and-tips.md)
  
    
    
 [<span data-ttu-id="8915e-181">Excel Services Best Practices</span><span class="sxs-lookup"><span data-stu-id="8915e-181">Excel Services Best Practices</span></span>](excel-services-best-practices.md)
