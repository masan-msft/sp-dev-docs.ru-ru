---
title: Walkthrough Developing a Managed-Code UDF
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: e6a00833-0606-4a7d-91c3-b89a6e340348
ms.openlocfilehash: 6e7539703fd642349a0b7a4f54f703cad3de7b61
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
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
  
    
    

- Microsoft SharePoint Server 2010 
    
    > [!NOTE] 
    > [!Примечание] The easiest way to get all you need on the server is to do a basic, stand-alone install. All you need to add on top of that is a trusted location. 

- Excel
    
  
- Visual Studio или аналогичное средство разработки совместимое с платформой Microsoft .NET Framework
    
  
- Возможность разрешения запуска сборки UDF
    
  
- Надежная библиотека документов SharePoint, в котором сохраняется книга и разрешить книге было разрешено вызывать пользовательские функции путем установки для параметра **AllowUdfs** значения **true**
    
  
- Пример книги, вызывающий пользовательские функции, хранимые в надежной библиотеке документов SharePoint
    
  
- Разрешения на просмотр и публикация книги в библиотеке документов SharePoint
    
    > [!NOTE] 
    > [!Примечание] For more information about setting permissions, see the Службы Windows SharePoint Services 3.0 documentation. 

- Создание книги с помощью Excel
    
  
- Сохранение книги в формате XLSX или xlsb
    
    > [!NOTE] 
    > [!Примечание] For more information about how to trust a location, how to enable UDFs, and how to set the **AllowUdfs** flag, see [Step 3: Deploying and Enabling UDFs](step-3-deploying-and-enabling-udfs.md). 

## <a name="see-also"></a>См. также

- [Step 1: Creating a Project and Adding a UDF Reference](step-1-creating-a-project-and-adding-a-udf-reference.md)
- [Step 2: Creating a Managed-Code UDF](step-2-creating-a-managed-code-udf.md)
- [Step 3: Deploying and Enabling UDFs](step-3-deploying-and-enabling-udfs.md)
- [Step 4: Testing and Calling UDFs from Cells](step-4-testing-and-calling-udfs-from-cells.md)
- [How to: Create a UDF That Calls a Web Service](how-to-create-a-udf-that-calls-a-web-service.md)
- [Understanding Excel Services UDFs](understanding-excel-services-udfs.md)
- [Пошаговое руководство. Разработка настраиваемого приложения с помощью веб-служб Excel](walkthrough-developing-a-custom-application-using-excel-web-services.md)
