---
title: "Включение пользовательских функций"
ms.date: 09/25/2017
keywords: how to,howdoi,howto,UDF list
f1_keywords: how to,howdoi,howto,UDF list
ms.prod: sharepoint
ms.assetid: 8c1af2eb-bb22-45e1-82de-a2b4b53d7a26
ms.openlocfilehash: 6eb51af89ab003e507ec9acb2f81a70bf843ee99
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="enable-udfs"></a>Включение пользовательских функций

Each Службы Excel trusted location in the Shared Services Provider (SSP) has an **AllowUdfs** flag.
  
    
    


> **Примечание:** Флаг **AllowUdfs** идентификаторами с помощью параметра **пользовательские функции разрешены** на странице "Надежные расположения файлов Excel Services".
  
    
    


The default **AllowUdfs** value is **false**. If the **AllowUdfs** value is set to **false** in a particular trusted location, the workbooks in that trusted location are not allowed to call UDFs.
  
    
    

In order to allow UDFs to be called from a specific trusted location, you set the **AllowUdfs** value to **true**.If the **AllowUdfs** value is **false** when a session is started on a workbook that has UDF calls in this trusted location, the UDF calls will fail. If you change the **AllowUdfs** value to **true** after a session has started, the UDF calls will also fail. This is because changes in the **AllowUdfs** flag take effect on the next session, after the configuration database has been updated.You can get around this by restarting the sessionfor example, by selecting **Reload Workbook** in Веб-клиент Excel.
> **Осторожность:** Если вместо этого Сброс Microsoft Internet Information Services (IIS), будут завершены все текущие сеансы. 
  
    
    


## <a name="enabling-udfs"></a>Enabling UDFs

To do the following steps, you need a computer that has Microsoft SharePoint Server 2010 installed.
  
    
    

### <a name="to-enable-udfs"></a>To enable UDFs


1. On the **Start** menu, click **All Programs**. 
    
  
2. Point to **Microsoft Office Server** and click **SharePoint Central Administration**. 
    
  
3. On the Quick Launch, click your Shared Services Provider (SSP) linkfor example, "SharedServices1"to view the Shared Services home page for that particular SSP.
    
  
4. Under **Excel Services Settings**, click **User-defined functions**. 
    
  
5. On the Excel Services User-Defined Functions page, click **Add User-Defined Function** to open the Excel Services Add User-Defined Function Assembly page.
    
  
6. In the **Assembly** box, type the path to the UDF assembly. For example,C:\\MyUdfFolder\\MyUdf.dll.
    
  
7. Under **Assembly Location**, click **Local file**.
    
    > **Примечание:** Параметр **локального файла** будут заменены на **путь к файлу** в будущих выпусках служб Excel. Если отображается **путь к файлу**, выберите его. 
8. Under **Enable Assembly**, the **Assembly enabled** check box should be selected by default.
    
  
9. Click **OK**.
    
  

## <a name="allowing-udf-calls"></a>Allowing UDF Calls


### <a name="to-allow-udfs-to-be-called-from-a-workbook"></a>To allow UDFs to be called from a workbook


1. Open the Excel Services Add Trusted File Location page (if you are adding a new trusted location) or Excel Services Edit Trusted File Location page (if you are editing an existing trusted location). 
    
    > **Примечание:** Дополнительные сведения о определение надежного расположения можно [как: надежного расположения](how-to-trust-a-location.md). 
2. Under **Allow User-Defined Functions**, select **User-defined functions allowed** to allow UDFs to be called from workbooks stored in this trusted location.
    
  
3. Click **OK**.
    
  

## <a name="see-also"></a>См. также


#### <a name="tasks"></a>Задачи


  
    
    
 [Step 3: Deploying and Enabling UDFs](step-3-deploying-and-enabling-udfs.md)
  
    
    
 [How to: Create a UDF That Calls a Web Service](how-to-create-a-udf-that-calls-a-web-service.md)
  
    
    
 [How to: Trust a Location](how-to-trust-a-location.md)
#### <a name="concepts"></a>Основные понятия


  
    
    
 [Walkthrough: Developing a Managed-Code UDF](walkthrough-developing-a-managed-code-udf.md)
  
    
    
 [Frequently Asked Questions About Excel Services UDFs](frequently-asked-questions-about-excel-services-udfs.md)
  
    
    
 [Understanding Excel Services UDFs](understanding-excel-services-udfs.md)
  
    
    
 [Excel Services Alerts](excel-services-alerts.md)
  
    
    
 [Excel Services Known Issues and Tips](excel-services-known-issues-and-tips.md)
  
    
    
 [Excel Services Best Practices](excel-services-best-practices.md)
