---
title: How to Restrict UDF Code Access Security Permissions
ms.date: 09/25/2017
keywords: cas,how to,howdoi,howto,UDF list
f1_keywords: cas,how to,howdoi,howto,UDF list
ms.prod: sharepoint
ms.assetid: 4f022e0d-1fe3-4fab-b41f-82a0d628f77c
ms.openlocfilehash: 4332b90022de9b7219aa397e9fbaa3334b38a300
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-restrict-udf-code-access-security-permissions"></a>How to: Restrict UDF Code Access Security Permissions

If you do not want a particular user-defined function (UDF) assembly to run with full trust, you must explicitly restrict code access security permissions for it. You can configure code groups and restrict permissions by using the .NET Framework 2.0 Configuration tool. 
  
    
    

For example, imagine a scenario where you have a UDF assembly that contains multiple methods. One of the UDF methods performs a custom calculation, and another UDF method in the same assembly calls a Web service to obtain stock quotes. Because your users only use Excel workbooks that call the first (calculation) method, you might want to disable the assembly from having Web access, for increased security. You have the UDF assembly installed in a folder on the server at C:\\UdfAssemblies\\CalcAndWebAccessUdf.dll. Because the assembly is on the same computer as Microsoft SharePoint Server 2010, when Службы вычислений Excel loads the UDF assembly, it is loaded in the MyComputer zone. By default, the MyComputer zone is fully trusted. This means that the UDF assembly is granted full trust permission. 
  
    
    

To lock down the UDF assembly so that it cannot have Web access, you must explicitly restrict the permission set that it is granted by following these steps:
1. Create a new URL-based code group under My_Computer_Zone at the Machine level. Scope the code group to that specific assembly and create a custom permission set.
    
  
2. Configure the custom code group properties so that your policy level has only the permissions from the permission set that is associated with the custom code group. When Службы вычислений Excel loads a UDF assembly that resides on the same computer, the assembly is loaded in the MyComputer zone. This means that by default, the UDF assembly is granted full trust. When the custom permission set intersects with the full trust permission set, the result is full trust. To make it so that the a policy has only the permission from the permission set that is associated with your custom code group, you must enable the **This policy level will only have the permissions from the permission set associated with this code group** property.
    
  
For more information about configuring code groups, see the following articles on MSDN:
-  [Configuring Code Groups Using the .NET Framework Configuration Tool](http://msdn.microsoft.com/library/default.asp?url=/library/en-us/cpguide/html/cpconUsingNETConfigurationToolToWorkWithCodeGroups.asp?frame=true) (http://msdn.microsoft.com/library/default.asp?url=/library/en-us/cpguide/html/cpconUsingNETConfigurationToolToWorkWithCodeGroups.asp?frame=true)
    
  
-  [Code Access Security in Practice](http://msdn.microsoft.com/library/default.asp?url=/library/en-us/dnnetsec/html/thcmch08.asp) (http://msdn.microsoft.com/library/default.asp?url=/library/en-us/dnnetsec/html/thcmch08.asp)
    
  

### <a name="to-create-a-new-code-group"></a>To create a new code group


1. Click **Start**, point to **All Programs**, point to **Administrative Tools**, and then click **Microsoft .NET Framework 2.0 Configuration**. 
    
    This starts the **.NET 2.0 Framework Configuration** tool.
    
  
2. In the left pane, expand the **My Computer** node, and then expand the **Runtime Security Policy** node.
    
  
3. Expand the **Machine** node.
    
  
4. Expand the **Code Groups** node.
    
  
5. Expand the **All_Code** node.
    
  
6. Expand the **My_Computer_Zone** node.Right-click **My_Computer_Zone** and then select **New** to display the **Identify the new Code Group** dialog box.
    
  
7. Select **Create a new code group**.
    
  
8. In the **Name** field, type a name for the new code group, for example,RestrictWebAccessUdf.
    
  
9. Click **Next**.
    
  
10. To scope the code group to your specific UDF assembly, select **URL** from the **Choose the condition type for this code group**. 
    
    This displays the **URL** field.
    
  
11. In the **URL** field, type the path to the UDF assembly for which you want to restrict access to the Web, for example,C:\\UdfAssemblies\\CalcAndWebAccessUdf.dll.
    
  
12. Click **Next**.
    
  
13. Select **Create a new permission set**, and then click **Next**.
    
  
14. In the **Name** field, type a name for your permission set, for example,AssemblyExecutionCustomPermissionSet.
    
  
15. Click **Next**.
    
  
16. To give your UDF assembly "assembly execution" permission, select **Security** from the **Assembly Permissions** list, and then click **Add**. 
    
    This displays the **Permission Settings** dialog box.
    
  
17. Выберите пункт **Предоставить сборкам следующие разрешения безопасности**.
    
  
18. Select **Enable assembly execution**.
    
  
19. Click **OK**, and then click **Next**.
    
  
20. Click **Finish**. 
    
    You should see your new custom code group under the **My_Computer_Zone** node (in this example, **RestrictWebAccessUdf**).
    
  

### <a name="to-make-sure-that-the-permission-sets-are-executed"></a>To make sure that the permission sets are executed


1. Under the **My_Computer_Zone** node, right-click the new custom code group (in this example, **RestrictWebAccessUdf**), and then select **Properties**. 
    
  
2. On the **General** tab, select the **This policy level will only have the permissions from the permission set associated with this code group** check box.
    
  
3. Click **Apply**, and then click **OK**.
    
    > **Примечание:** Если возникает исключение метода UDF за невозможности вызова веб-службы, вы должны получить **#VALUE!** Ошибка в формуле Excel, вызвавшей пользовательскую Функцию.

    > **Примечание:** Если вы хотите включить веб-доступ для сборки пользовательских Функций для тестирования, необходимо добавить соответствующие разрешения в набор разрешений. Для этого в шаг 11 в процедуре «Чтобы создать новую группу кода» выберите **Веб-клиента**. 

## <a name="see-also"></a>См. также


#### <a name="tasks"></a>Задачи


  
    
    
 [How to: Create a UDF That Calls a Web Service](how-to-create-a-udf-that-calls-a-web-service.md)
  
    
    
 [How to: Enable UDFs](how-to-enable-udfs.md)
  
    
    
 [How to: Access an External Data Source from a UDF](how-to-access-an-external-data-source-from-a-udf.md)
  
    
    
 [How to: Deploy UDFs Using SharePoint Foundation Solutions](how-to-deploy-udfs-using-sharepoint-foundation-solutions.md)
#### <a name="concepts"></a>Основные понятия


  
    
    
 [Walkthrough: Developing a Managed-Code UDF](walkthrough-developing-a-managed-code-udf.md)
  
    
    
 [Frequently Asked Questions About Excel Services UDFs](frequently-asked-questions-about-excel-services-udfs.md)
  
    
    
 [Understanding Excel Services UDFs](understanding-excel-services-udfs.md)
