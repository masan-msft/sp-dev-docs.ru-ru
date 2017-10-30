---
title: Walkthrough Developing a Managed-Code UDF
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: e6a00833-0606-4a7d-91c3-b89a6e340348
ms.openlocfilehash: 6b946672852a8aa7b3dcfb17b16997048bb3f521
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="walkthrough-developing-a-managed-code-udf"></a>Walkthrough: Developing a Managed-Code UDF

This walkthrough describes the process for developing Службы Excel user-defined functions (UDFs) using Microsoft Visual C#.
  
    
    

During this walkthrough, you will learn how to:
- Create a project using the Microsoft Visual Studio 2005 class library project template.
    
  
- Add a reference to Microsoft.Office.Excel.Server.Udf.dll.
    
  
- Write UDFs for use in Службы Excel.
    
  
- Create a workbook to call custom functions from cells.
    
  
- Test and run UDFs in Службы Excel.
    
  

## <a name="prerequisites"></a>Prerequisites

In order to complete this walkthrough, you will need: 
  
    
    

- Microsoft SharePoint Server 2010. 
    
    > **Примечание:** Это самый простой способ получить все, что требуется на сервере, — это базовая, изолированной установки. Все, что вам нужно добавить, являющуюся надежным расположением. 
- Excel.
    
  
- Visual Studio or a similar Microsoft .NET Framework-compatible development tool.
    
  
- To enable running the UDF assembly.
    
  
- A trusted SharePoint document library in which to store a workbook, and to allow the workbook to call UDFs by setting the **AllowUdfs** value to **true**. 
    
  
- A sample workbook that calls the UDF stored in a trusted SharePoint document library. 
    
  
- Permissions to view and publish a workbook to a SharePoint document library. 
    
    > **Примечание:** Дополнительные сведения о настройке разрешений обратитесь к документации Windows SharePoint Services 3.0. 
- To create the workbook using Excel.
    
  
- To save the workbook as an .xlsx or .xlsb file.
    
    > **Примечание:** Дополнительные сведения о надежного расположения, включение пользовательских функций и установить флаг **AllowUdfs** можно [Шаг 3: развертывание и включение пользовательских функций](step-3-deploying-and-enabling-udfs.md). 

## <a name="see-also"></a>См. также


#### <a name="tasks"></a>Задачи


  
    
    
 [Step 1: Creating a Project and Adding a UDF Reference](step-1-creating-a-project-and-adding-a-udf-reference.md)
  
    
    
 [Step 2: Creating a Managed-Code UDF](step-2-creating-a-managed-code-udf.md)
  
    
    
 [Step 3: Deploying and Enabling UDFs](step-3-deploying-and-enabling-udfs.md)
  
    
    
 [Step 4: Testing and Calling UDFs from Cells](step-4-testing-and-calling-udfs-from-cells.md)
  
    
    
 [How to: Create a UDF That Calls a Web Service](how-to-create-a-udf-that-calls-a-web-service.md)
#### <a name="concepts"></a>Основные понятия


  
    
    
 [Understanding Excel Services UDFs](understanding-excel-services-udfs.md)
#### <a name="other-resources"></a>Другие ресурсы


  
    
    
 [Пошаговое руководство. Разработка настраиваемого приложения с помощью веб-служб Excel](walkthrough-developing-a-custom-application-using-excel-web-services.md)
