---
title: "Ограничение разрешений на управление доступом для кода пользовательских функций"
ms.date: 09/25/2017
keywords: cas,how to,howdoi,howto,UDF list
f1_keywords:
- cas,how to,howdoi,howto,UDF list
ms.prod: sharepoint
ms.assetid: 4f022e0d-1fe3-4fab-b41f-82a0d628f77c
ms.openlocfilehash: 6a562afe83302a01be3f9a349b61f0e3b6944acc
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="restrict-udf-code-access-security-permissions"></a><span data-ttu-id="ae640-103">Ограничение разрешений на управление доступом для кода пользовательских функций</span><span class="sxs-lookup"><span data-stu-id="ae640-103">Restrict UDF code access security permissions</span></span>

<span data-ttu-id="ae640-p101">If you do not want a particular user-defined function (UDF) assembly to run with full trust, you must explicitly restrict code access security permissions for it. You can configure code groups and restrict permissions by using the .NET Framework 2.0 Configuration tool.</span><span class="sxs-lookup"><span data-stu-id="ae640-p101">If you do not want a particular user-defined function (UDF) assembly to run with full trust, you must explicitly restrict code access security permissions for it. You can configure code groups and restrict permissions by using the .NET Framework 2.0 Configuration tool.</span></span> 
  
    
    

<span data-ttu-id="ae640-p102">For example, imagine a scenario where you have a UDF assembly that contains multiple methods. One of the UDF methods performs a custom calculation, and another UDF method in the same assembly calls a Web service to obtain stock quotes. Because your users only use Excel workbooks that call the first (calculation) method, you might want to disable the assembly from having Web access, for increased security. You have the UDF assembly installed in a folder on the server at C:\\UdfAssemblies\\CalcAndWebAccessUdf.dll. Because the assembly is on the same computer as Microsoft SharePoint Server 2010, when Службы вычислений Excel loads the UDF assembly, it is loaded in the MyComputer zone. By default, the MyComputer zone is fully trusted. This means that the UDF assembly is granted full trust permission.</span><span class="sxs-lookup"><span data-stu-id="ae640-p102">For example, imagine a scenario where you have a UDF assembly that contains multiple methods. One of the UDF methods performs a custom calculation, and another UDF method in the same assembly calls a Web service to obtain stock quotes. Because your users only use Excel workbooks that call the first (calculation) method, you might want to disable the assembly from having Web access, for increased security. You have the UDF assembly installed in a folder on the server at C:\\UdfAssemblies\\CalcAndWebAccessUdf.dll. Because the assembly is on the same computer as Microsoft SharePoint Server 2010, when Excel Calculation Services loads the UDF assembly, it is loaded in the MyComputer zone. By default, the MyComputer zone is fully trusted. This means that the UDF assembly is granted full trust permission.</span></span> 
  
    
    

<span data-ttu-id="ae640-113">To lock down the UDF assembly so that it cannot have Web access, you must explicitly restrict the permission set that it is granted by following these steps:</span><span class="sxs-lookup"><span data-stu-id="ae640-113">To lock down the UDF assembly so that it cannot have Web access, you must explicitly restrict the permission set that it is granted by following these steps:</span></span>
1. <span data-ttu-id="ae640-p103">Create a new URL-based code group under My_Computer_Zone at the Machine level. Scope the code group to that specific assembly and create a custom permission set.</span><span class="sxs-lookup"><span data-stu-id="ae640-p103">Create a new URL-based code group under My_Computer_Zone at the Machine level. Scope the code group to that specific assembly and create a custom permission set.</span></span>
    
  
2. <span data-ttu-id="ae640-p104">Configure the custom code group properties so that your policy level has only the permissions from the permission set that is associated with the custom code group. When Службы вычислений Excel loads a UDF assembly that resides on the same computer, the assembly is loaded in the MyComputer zone. This means that by default, the UDF assembly is granted full trust. When the custom permission set intersects with the full trust permission set, the result is full trust. To make it so that the a policy has only the permission from the permission set that is associated with your custom code group, you must enable the **This policy level will only have the permissions from the permission set associated with this code group** property.</span><span class="sxs-lookup"><span data-stu-id="ae640-p104">Configure the custom code group properties so that your policy level has only the permissions from the permission set that is associated with the custom code group. When Excel Calculation Services loads a UDF assembly that resides on the same computer, the assembly is loaded in the MyComputer zone. This means that by default, the UDF assembly is granted full trust. When the custom permission set intersects with the full trust permission set, the result is full trust. To make it so that the a policy has only the permission from the permission set that is associated with your custom code group, you must enable the **This policy level will only have the permissions from the permission set associated with this code group** property.</span></span>
    
  
<span data-ttu-id="ae640-121">For more information about configuring code groups, see the following articles on MSDN:</span><span class="sxs-lookup"><span data-stu-id="ae640-121">For more information about configuring code groups, see the following articles on MSDN:</span></span>
-  <span data-ttu-id="ae640-122">[Configuring Code Groups Using the .NET Framework Configuration Tool](http://msdn.microsoft.com/library/default.asp?url=/library/en-us/cpguide/html/cpconUsingNETConfigurationToolToWorkWithCodeGroups.asp?frame=true) (http://msdn.microsoft.com/library/default.asp?url=/library/en-us/cpguide/html/cpconUsingNETConfigurationToolToWorkWithCodeGroups.asp?frame=true)</span><span class="sxs-lookup"><span data-stu-id="ae640-122">[Configuring Code Groups Using the .NET Framework Configuration Tool](http://msdn.microsoft.com/library/default.asp?url=/library/en-us/cpguide/html/cpconUsingNETConfigurationToolToWorkWithCodeGroups.asp?frame=true) (http://msdn.microsoft.com/library/default.asp?url=/library/en-us/cpguide/html/cpconUsingNETConfigurationToolToWorkWithCodeGroups.asp?frame=true)</span></span>
    
  
-  <span data-ttu-id="ae640-123">[Code Access Security in Practice](http://msdn.microsoft.com/library/default.asp?url=/library/en-us/dnnetsec/html/thcmch08.asp) (http://msdn.microsoft.com/library/default.asp?url=/library/en-us/dnnetsec/html/thcmch08.asp)</span><span class="sxs-lookup"><span data-stu-id="ae640-123">[Code Access Security in Practice](http://msdn.microsoft.com/library/default.asp?url=/library/en-us/dnnetsec/html/thcmch08.asp) (http://msdn.microsoft.com/library/default.asp?url=/library/en-us/dnnetsec/html/thcmch08.asp)</span></span>
    
  

### <a name="to-create-a-new-code-group"></a><span data-ttu-id="ae640-124">To create a new code group</span><span class="sxs-lookup"><span data-stu-id="ae640-124">To create a new code group</span></span>


1. <span data-ttu-id="ae640-125">Click **Start**, point to **All Programs**, point to **Administrative Tools**, and then click **Microsoft .NET Framework 2.0 Configuration**.</span><span class="sxs-lookup"><span data-stu-id="ae640-125">Click **Start**, point to **All Programs**, point to **Administrative Tools**, and then click **Microsoft .NET Framework 2.0 Configuration**.</span></span> 
    
    <span data-ttu-id="ae640-126">This starts the **.NET 2.0 Framework Configuration** tool.</span><span class="sxs-lookup"><span data-stu-id="ae640-126">This starts the **.NET 2.0 Framework Configuration** tool.</span></span>
    
  
2. <span data-ttu-id="ae640-127">In the left pane, expand the **My Computer** node, and then expand the **Runtime Security Policy** node.</span><span class="sxs-lookup"><span data-stu-id="ae640-127">In the left pane, expand the **My Computer** node, and then expand the **Runtime Security Policy** node.</span></span>
    
  
3. <span data-ttu-id="ae640-128">Expand the **Machine** node.</span><span class="sxs-lookup"><span data-stu-id="ae640-128">Expand the **Machine** node.</span></span>
    
  
4. <span data-ttu-id="ae640-129">Expand the **Code Groups** node.</span><span class="sxs-lookup"><span data-stu-id="ae640-129">Expand the **Code Groups** node.</span></span>
    
  
5. <span data-ttu-id="ae640-130">Expand the **All_Code** node.</span><span class="sxs-lookup"><span data-stu-id="ae640-130">Expand the **All_Code** node.</span></span>
    
  
6. <span data-ttu-id="ae640-131">Expand the **My_Computer_Zone** node.Right-click **My_Computer_Zone** and then select **New** to display the **Identify the new Code Group** dialog box.</span><span class="sxs-lookup"><span data-stu-id="ae640-131">Expand the **My_Computer_Zone** node.Right-click **My_Computer_Zone** and then select **New** to display the **Identify the new Code Group** dialog box.</span></span>
    
  
7. <span data-ttu-id="ae640-132">Select **Create a new code group**.</span><span class="sxs-lookup"><span data-stu-id="ae640-132">Select **Create a new code group**.</span></span>
    
  
8. <span data-ttu-id="ae640-133">In the **Name** field, type a name for the new code group, for example,RestrictWebAccessUdf.</span><span class="sxs-lookup"><span data-stu-id="ae640-133">In the **Name** field, type a name for the new code group, for example,RestrictWebAccessUdf.</span></span>
    
  
9. <span data-ttu-id="ae640-134">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ae640-134">Click **Next**.</span></span>
    
  
10. <span data-ttu-id="ae640-135">To scope the code group to your specific UDF assembly, select **URL** from the **Choose the condition type for this code group**.</span><span class="sxs-lookup"><span data-stu-id="ae640-135">To scope the code group to your specific UDF assembly, select **URL** from the **Choose the condition type for this code group**.</span></span> 
    
    <span data-ttu-id="ae640-136">This displays the **URL** field.</span><span class="sxs-lookup"><span data-stu-id="ae640-136">This displays the **URL** field.</span></span>
    
  
11. <span data-ttu-id="ae640-137">In the **URL** field, type the path to the UDF assembly for which you want to restrict access to the Web, for example,C:\\UdfAssemblies\\CalcAndWebAccessUdf.dll.</span><span class="sxs-lookup"><span data-stu-id="ae640-137">In the **URL** field, type the path to the UDF assembly for which you want to restrict access to the Web, for example,C:\\UdfAssemblies\\CalcAndWebAccessUdf.dll.</span></span>
    
  
12. <span data-ttu-id="ae640-138">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ae640-138">Click **Next**.</span></span>
    
  
13. <span data-ttu-id="ae640-139">Select **Create a new permission set**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ae640-139">Select **Create a new permission set**, and then click **Next**.</span></span>
    
  
14. <span data-ttu-id="ae640-140">In the **Name** field, type a name for your permission set, for example,AssemblyExecutionCustomPermissionSet.</span><span class="sxs-lookup"><span data-stu-id="ae640-140">In the **Name** field, type a name for your permission set, for example,AssemblyExecutionCustomPermissionSet.</span></span>
    
  
15. <span data-ttu-id="ae640-141">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ae640-141">Click **Next**.</span></span>
    
  
16. <span data-ttu-id="ae640-142">To give your UDF assembly "assembly execution" permission, select **Security** from the **Assembly Permissions** list, and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="ae640-142">To give your UDF assembly "assembly execution" permission, select **Security** from the **Assembly Permissions** list, and then click **Add**.</span></span> 
    
    <span data-ttu-id="ae640-143">This displays the **Permission Settings** dialog box.</span><span class="sxs-lookup"><span data-stu-id="ae640-143">This displays the **Permission Settings** dialog box.</span></span>
    
  
17. <span data-ttu-id="ae640-144">Выберите пункт **Предоставить сборкам следующие разрешения безопасности**.</span><span class="sxs-lookup"><span data-stu-id="ae640-144">Select **assemblies the following security permissions**.</span></span>
    
  
18. <span data-ttu-id="ae640-145">Select **Enable assembly execution**.</span><span class="sxs-lookup"><span data-stu-id="ae640-145">Select **Enable assembly execution**.</span></span>
    
  
19. <span data-ttu-id="ae640-146">Click **OK**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ae640-146">Click **OK**, and then click **Next**.</span></span>
    
  
20. <span data-ttu-id="ae640-147">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="ae640-147">Click **Finish**.</span></span> 
    
    <span data-ttu-id="ae640-148">You should see your new custom code group under the **My_Computer_Zone** node (in this example, **RestrictWebAccessUdf**).</span><span class="sxs-lookup"><span data-stu-id="ae640-148">You should see your new custom code group under the **My_Computer_Zone** node (in this example, **RestrictWebAccessUdf**).</span></span>
    
  

### <a name="to-make-sure-that-the-permission-sets-are-executed"></a><span data-ttu-id="ae640-149">To make sure that the permission sets are executed</span><span class="sxs-lookup"><span data-stu-id="ae640-149">To make sure that the permission sets are executed</span></span>


1. <span data-ttu-id="ae640-150">Under the **My_Computer_Zone** node, right-click the new custom code group (in this example, **RestrictWebAccessUdf**), and then select **Properties**.</span><span class="sxs-lookup"><span data-stu-id="ae640-150">Under the **My_Computer_Zone** node, right-click the new custom code group (in this example, **RestrictWebAccessUdf**), and then select **Properties**.</span></span> 
    
  
2. <span data-ttu-id="ae640-151">On the **General** tab, select the **This policy level will only have the permissions from the permission set associated with this code group** check box.</span><span class="sxs-lookup"><span data-stu-id="ae640-151">On the **General** tab, select the **This policy level will only have the permissions from the permission set associated with this code group** check box.</span></span>
    
  
3. <span data-ttu-id="ae640-152">Click **Apply**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="ae640-152">Click **Apply**, and then click **OK**.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="ae640-p105">[!Примечание] If the UDF method throws an exception because it cannot make the Web service call, you should receive a **#VALUE!** error in the Excel formula that called the UDF.</span><span class="sxs-lookup"><span data-stu-id="ae640-p105">If the UDF method throws an exception because it cannot make the Web service call, you should receive a **#VALUE!** error in the Excel formula that called the UDF.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ae640-p106">[!Примечание] If you want to enable Web access for your UDF assembly for testing, you must add the appropriate permission to your custom permission set. To do this, in Step 11 of the "To create a new code group" procedure, select **Web Access**.</span><span class="sxs-lookup"><span data-stu-id="ae640-p106">If you want to enable Web access for your UDF assembly for testing, you must add the appropriate permission to your custom permission set. To do this, in Step 11 of the "To create a new code group" procedure, select **Web Access**.</span></span> 

## <a name="see-also"></a><span data-ttu-id="ae640-157">См. также</span><span class="sxs-lookup"><span data-stu-id="ae640-157">See also</span></span>

- [<span data-ttu-id="ae640-158">How to: Create a UDF That Calls a Web Service</span><span class="sxs-lookup"><span data-stu-id="ae640-158">How to: Create a UDF That Calls a Web Service</span></span>](how-to-create-a-udf-that-calls-a-web-service.md)
- [<span data-ttu-id="ae640-159">How to: Enable UDFs</span><span class="sxs-lookup"><span data-stu-id="ae640-159">How to: Enable UDFs</span></span>](how-to-enable-udfs.md)
- [<span data-ttu-id="ae640-160">How to: Access an External Data Source from a UDF</span><span class="sxs-lookup"><span data-stu-id="ae640-160">How to: Access an External Data Source from a UDF</span></span>](how-to-access-an-external-data-source-from-a-udf.md)
- [<span data-ttu-id="ae640-161">How to: Deploy UDFs Using SharePoint Foundation Solutions</span><span class="sxs-lookup"><span data-stu-id="ae640-161">How to: Deploy UDFs Using SharePoint Foundation Solutions</span></span>](how-to-deploy-udfs-using-sharepoint-foundation-solutions.md)
- [<span data-ttu-id="ae640-162">Walkthrough: Developing a Managed-Code UDF</span><span class="sxs-lookup"><span data-stu-id="ae640-162">Walkthrough: Developing a Managed-Code UDF</span></span>](walkthrough-developing-a-managed-code-udf.md)
- [<span data-ttu-id="ae640-163">Frequently Asked Questions About Excel Services UDFs</span><span class="sxs-lookup"><span data-stu-id="ae640-163">Frequently Asked Questions About Excel Services UDFs</span></span>](frequently-asked-questions-about-excel-services-udfs.md)
- [<span data-ttu-id="ae640-164">Understanding Excel Services UDFs</span><span class="sxs-lookup"><span data-stu-id="ae640-164">Understanding Excel Services UDFs</span></span>](understanding-excel-services-udfs.md)
