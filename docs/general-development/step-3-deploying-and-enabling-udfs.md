---
title: Step 3 Deploying and Enabling UDFs
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 1e5e2a0a-041a-481c-a18b-578562a60e24
ms.openlocfilehash: 9db2e49544445e33058734bc42ed1a33a4448b98
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="step-3-deploying-and-enabling-udfs"></a>Step 3: Deploying and Enabling UDFs

In this step, you will:
  
    
    


1. Deploy SampleUdf.dll, which you created in  [Step 2: Creating a Managed-Code UDF](step-2-creating-a-managed-code-udf.md), to a folder on a computer that has Microsoft SharePoint Server 2010 installed.
    
  
2. Allow user-defined functions (UDFs) to be called from a specific trusted location, for example, trusted Shared Documents location. 
    
  
3. Enable SampleUdf.dll.
    
  

## <a name="deploying-udfs"></a>Deploying UDFs


### <a name="to-deploy-udfs"></a>To deploy UDFs


1. Create a folder named "UDFs" on the local drive of the computer to which you want to deploy UDFs. For example, "C:\\UDFs".
    
  
2. Copy the SampleUdf.dll assembly.
    
  
3. Save SampleUdf.dll in "C:\\UDFs". 
    
  

## <a name="trusting-a-location"></a>Trusting a Location


### <a name="to-trust-a-location"></a>To trust a location


1. On the **Start** menu, click **All Programs**. 
    
  
2. Point to **Microsoft SharePoint 2010 Products** and click **SharePoint Central Administration**. 
    
  
3. Under **Application Management** click **Manage service applications**.
    
  
4. On the Manage Service Applications page, click **Excel Services Application**.
    
  
5. On the **Excel Services Application** page, click **Trusted File Locations**.
    
  
6. On the Trusted File Locations page, click **Add Trusted File Location**. 
    
  
7. On the Add Trusted File Location page, in the **Address** box, type the location where you will save your workbookfor example, _http://MyServer002/Shared%20Documents_. 
    
  
8. Under **Location type**, click the appropriate location type. In this example, select Microsoft SharePoint Foundation.
    
  
9. Under **Trust Children**, select **Children trusted** to trust child libraries or directories.
    
  
10. Under **Allow User-Defined Functions**, select **User-defined functions allowed** to allow UDFs to be called from workbooks stored in this trusted location.
    
  
11. Click **OK**.
    
  

## <a name="enabling-udfs"></a>Enabling UDFs

To do the following steps, you need a computer that has SharePoint Server 2010 installed.
  
    
    

### <a name="to-enable-udfs"></a>To enable UDFs


1. Follow steps 1 through 3 in the previous procedure ("To trust a location") to display the Shared Services home page for an SSP.
    
  
2. Under **Excel Services Settings**, click **User-defined function assemblies**. 
    
  
3. На странице "пользовательские функции служб Excel" щелкните **Добавить пользовательскую функцию** , чтобы открыть страницу "Добавить сборку пользовательских функций страницу".
    
  
4. In the **Assembly** box, type the path to the SampleUdf.dll assembly. In this example, it would be _C:\\UDFs\\SampleUdf.dll_.
    
  
5. Under **Assembly Location**, click **File path**.
    
  
6. Under **Enable Assembly**, the **Assembly enabled** check box should be selected by default.
    
  
7. Click **OK**.
    
  

## <a name="robust-programming"></a>Надежное программирование

If the **AllowUdfs** value is **false** when a session is started on a workbook that has UDF calls, the UDF calls will fail.
  
    
    

> **Примечание:** Флаг **AllowUdfs** обозначается параметр **пользовательские функции разрешены** (в разделе шаг 9 в доверие» расположение «).
  
    
    

If you change the **AllowUdfs** value to **true** after a session has started, the UDF calls will also fail. This is because changes in the **AllowUdfs** flag take effect on the next session. You can get around this by resetting Microsoft Internet Information Services (IIS). Resetting IIS will reload UDFs.
  
    
    
For more information about resetting IIS, see  [How to: Enable UDFs](how-to-enable-udfs.md).
  
    
    

## <a name="see-also"></a>См. также


#### <a name="tasks"></a>Задачи


  
    
    
 [Step 1: Creating a Project and Adding a UDF Reference](step-1-creating-a-project-and-adding-a-udf-reference.md)
  
    
    
 [Step 2: Creating a Managed-Code UDF](step-2-creating-a-managed-code-udf.md)
  
    
    
 [Step 4: Testing and Calling UDFs from Cells](step-4-testing-and-calling-udfs-from-cells.md)
  
    
    
 [How to: Enable UDFs](how-to-enable-udfs.md)
#### <a name="concepts"></a>Основные понятия


  
    
    
 [Walkthrough: Developing a Managed-Code UDF](walkthrough-developing-a-managed-code-udf.md)
  
    
    
 [Understanding Excel Services UDFs](understanding-excel-services-udfs.md)