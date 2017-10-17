---
title: "Новые возможности веб-служб Excel"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: cb342e94-0308-4608-b027-b73ebe8107b0
ms.openlocfilehash: dfbce895961adaf9ca435000cad0d16b87f3e9d2
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="whats-new-in-excel-web-services"></a>Новые возможности веб-служб Excel

This topic lists the new types and members added to Веб-службы Excel.
  
    
    


## <a name="excel-web-services-enhancements"></a>Excel Web Services Enhancements

Веб-службы Excel is expanded and enhanced in Microsoft SharePoint Server 2010. In SharePoint Server 2010, you can edit and save a workbook programmatically. In addition, the Веб-службы Excel now supports opening workbooks in edit sessions in SharePoint Server 2010. In this scenario, you can use code to edit a workbook at the same time that other users are co-authoring the workbook.
  
    
    
For more information about the Веб-службы Excel API and more detailed remarks about the new methods, enumerations, and types, see **Microsoft.Office.Excel.Server.WebServices**.
  
    
    

### <a name="new-methods"></a>Новые методы

The following are new methods added to Веб-службы Excel, in alphabetical order: 
  
    
    

- **GetChartImageUrl** Gets a URL value to the chart or PivotChart image file in a workbook.
    
  
- **GetPublishedItemNames** Gets a list of published items in a workbook.
    
  
- **GetSheetNames** Gets a list of all of the sheet names present in a workbook.
    
  
- **OpenWorkbookForEditing** Opens a workbook for editing.
    
  
- **SaveWorkbook** Saves a workbook in the original format (.xlsx, .xlsb, .xlsm).
    
  
- **SaveWorkbookCopy** Saves a workbook by using a different file name and/or saves a workbook to a different SharePoint document library.
    
  
- **SetCalculationOptions** Changes the calculation mode setting for workbooks.
    
  
- **SetParameters** Sets multiple published parameters with a single Web Service call.
    
  
Кроме того:
  
    
    

- You can now set formulas by using the set value methods.
    
  
- Dynamic ranges are supported in Веб-службы Excel in SharePoint Server 2010.
    
  

### <a name="new-enumerations"></a>New Enumerations

The following are new enumerations added to Веб-службы Excel, in alphabetical order:
  
    
    

- **ItemType** Indicates the types of the returned items.
    
  
- **SheetType** Indicates the types of the returned sheets.
    
  
- **SheetVisibility** Indicates whether the returned sheets are visible.
    
  
- **SaveOptions** Specifies whether to overwrite an existing, unlocked file.
    
  
- **WorkbookCalculation** Defines the calculation mode setting for a workbook.
    
  

### <a name="new-types"></a>New Types

The following are new types added to Веб-службы Excel, in alphabetical order:
  
    
    

- **ParameterInfo** Gets or sets the name and values of a parameter.
    
  
- **SheetInfo** Contains information about a sheet in a workbook.
    
  
- **Size** Defines the width and height of the chart image
    
  
- **WorkbookItem** Represents named items in the workbook.
    
  

## <a name="see-also"></a>См. также


#### <a name="other-resources"></a>Другие ресурсы


  
    
    
 [Пошаговое руководство. Разработка настраиваемого приложения с помощью веб-служб Excel](walkthrough-developing-a-custom-application-using-excel-web-services.md)
