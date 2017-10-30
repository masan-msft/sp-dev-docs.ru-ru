---
title: Step 4 Testing and Calling UDFs from Cells
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: d3e6aa72-2eb8-4b4b-a0eb-273486890d00
ms.openlocfilehash: 9c9c16029c58d217e860259abc9f11a4ee015dd3
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="step-4-testing-and-calling-udfs-from-cells"></a>Step 4: Testing and Calling UDFs from Cells

In this step, you will test the SampleUdf.dll assembly you created, deployed, and enabled in the previous steps. To test the user-defined function (UDF), you will:
  
    
    


1. Create a workbook with a named range and formulas that call the functions in SampleUdf.dll.
    
  
2. Save the workbook to a SharePoint document library that is a trusted location.
    
    > **Примечание:** Предполагается, что уже создан в библиотеке документов SharePoint и был очень надежного расположения. Сведения о том, как надежного расположения, обратитесь к разделу «Доверие расположение» в [Шаг 3: развертывание и включение пользовательских функций](step-3-deploying-and-enabling-udfs.md). 
3. Change parameters to recalculate the workbook.
    
  

## <a name="testing-udfs"></a>Testing UDFs


### <a name="to-call-udfs-from-cells"></a>To call UDFs from cells


1. Start Microsoft Office Excel 2007.
    
  
2. In cell A1, type the formula to call the  `MyDouble` function in SampleUdf.dll. The `MyDouble` function takes an argument of type **double**. In this example, you will take the argument from cell B1. In cell A1, type =MyDouble(B1).
    
    > **Примечание:** Формула будет возвращать значение «#NAME?» в Excel. Формула вычисляется только в том случае, когда книга отображается в службах Excel. 

    > **Примечание:** Пользовательские функции можно запустить в клиенте и на сервере. Будущая статьи, опубликованной на сайте MSDN будут рассмотрены следующие вопросы сведения. Они опускаются здесь для простоты. 
3. In cell B1, type the number 8.
    
  
4. Make cell B1 a named range. First click the **Formulas** tab. Then click cell B1 to select it. On the **Formulas** tab, in the **Named Cells** group, click **Name a Range**. In the **New Name** dialog box, in the **Name** box, type **MyDoubleParam**.
    
  
5. In cell A2, type the formula to call the  `ReturnDateTimeToday` function. Type=ReturnDateTimeToday().
    
  
6. In cell A3, type the formula to call the  `ReturnDateTimeToday` function. Type=ReturnDateTimeToday(). Next, right-click cell A3 to display the menu. Click **Format Cells**.
    
  
7. In the **Format Cells** dialog box, on the **Number** tab, select **Date**. Select a date format type from the **Type** listfor example, *3/4/2001.
    
  
8. Click **OK**.
    
  
9. Save the workbook to a location of your choice on the local drive. Name the workbook "TestSampleUdf.xlsx". 
    
  

### <a name="to-save-to-excel-services"></a>To save to Excel Services


1. Click the **Microsoft Office Button**, point to **Save As**, and click **Save for Excel Services**. 
    
  
2. In the **Save As** dialog box, click **Excel Services Options**.
    
  
3. In the **Excel Services Options** dialog box, on the **Show** tab, make sure that **Entire Workbook** is selected.
    
  
4. Click **Parameters**. 
    
  
5. In the **Add Parameters** list, select the **MyDoubleParam** check box.
    
  
6. Click **OK**. You should now see "MyDoubleParam" listed in the **Parameters** list.
    
  
7. Click **OK**.
    
  
8. In the **Save As** dialog box, make sure that the **Open this workbook in my browser after I save** check box is selected.
    
  
9. In the **File name** box, type the path to the trusted SharePoint document library where you want to store this workbook. For example, _http://MyServer002/Shared%20Documents/TestSampleUdf.xlsx_.
    
  
10. Click **Save**. You should see TestSampleUdf.xlsx in Веб-клиент Excel. In cell A1, you should see the number "72" because cell B1 * 9 = 8 * 9, which is 72. In cell A2 you should see a number. In cell A3, you should see the current date. 
    
    > **Примечание:** В ячейку A2 число представляет количество дней, начиная с 1/1/1900 (или 1/1/1904 при наличии «Использовать систему дат 1904» включен). Это, как Excel представляет даты во внутренней сети. 

### <a name="to-change-parameters-to-test-the-udf"></a>To change parameters to test the UDF


1. In the **Parameters** pane, you should see the named range for cell B1, that is, "MyDoubleParam".
    
  
2. You can change the value in cell B1 by typing a number in the box next to "MyDoubleParam". For example, if you type 3 and then click **Apply**, Службы Excel will recalculate the workbook. Cell A1 will contain "27" instead of "72". 
    
  

## <a name="see-also"></a>См. также


#### <a name="tasks"></a>Задачи


  
    
    
 [Step 1: Creating a Project and Adding a UDF Reference](step-1-creating-a-project-and-adding-a-udf-reference.md)
  
    
    
 [Step 2: Creating a Managed-Code UDF](step-2-creating-a-managed-code-udf.md)
  
    
    
 [Step 3: Deploying and Enabling UDFs](step-3-deploying-and-enabling-udfs.md)
  
    
    
 [How to: Create a UDF That Calls a Web Service](how-to-create-a-udf-that-calls-a-web-service.md)
#### <a name="concepts"></a>Основные понятия


  
    
    
 [Walkthrough: Developing a Managed-Code UDF](walkthrough-developing-a-managed-code-udf.md)
  
    
    
 [Understanding Excel Services UDFs](understanding-excel-services-udfs.md)
