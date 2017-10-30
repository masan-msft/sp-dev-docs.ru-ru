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
# <a name="step-4-testing-and-calling-udfs-from-cells"></a><span data-ttu-id="dded5-102">Step 4: Testing and Calling UDFs from Cells</span><span class="sxs-lookup"><span data-stu-id="dded5-102">Step 4: Testing and Calling UDFs from Cells</span></span>

<span data-ttu-id="dded5-p101">In this step, you will test the SampleUdf.dll assembly you created, deployed, and enabled in the previous steps. To test the user-defined function (UDF), you will:</span><span class="sxs-lookup"><span data-stu-id="dded5-p101">In this step, you will test the SampleUdf.dll assembly you created, deployed, and enabled in the previous steps. To test the user-defined function (UDF), you will:</span></span>
  
    
    


1. <span data-ttu-id="dded5-105">Create a workbook with a named range and formulas that call the functions in SampleUdf.dll.</span><span class="sxs-lookup"><span data-stu-id="dded5-105">Create a workbook with a named range and formulas that call the functions in SampleUdf.dll.</span></span>
    
  
2. <span data-ttu-id="dded5-106">Save the workbook to a SharePoint document library that is a trusted location.</span><span class="sxs-lookup"><span data-stu-id="dded5-106">Save the workbook to a SharePoint document library that is a trusted location.</span></span>
    
    > <span data-ttu-id="dded5-107">**Примечание:** Предполагается, что уже создан в библиотеке документов SharePoint и был очень надежного расположения.</span><span class="sxs-lookup"><span data-stu-id="dded5-107">**Note:** It is assumed that you have already created a SharePoint document library and made it a trusted location.</span></span> <span data-ttu-id="dded5-108">Сведения о том, как надежного расположения, обратитесь к разделу «Доверие расположение» в [Шаг 3: развертывание и включение пользовательских функций](step-3-deploying-and-enabling-udfs.md).</span><span class="sxs-lookup"><span data-stu-id="dded5-108">For information about how to trust a location, see the "Trusting a Location" section in  [Step 3: Deploying and Enabling UDFs](step-3-deploying-and-enabling-udfs.md).</span></span> 
3. <span data-ttu-id="dded5-109">Change parameters to recalculate the workbook.</span><span class="sxs-lookup"><span data-stu-id="dded5-109">Change parameters to recalculate the workbook.</span></span>
    
  

## <a name="testing-udfs"></a><span data-ttu-id="dded5-110">Testing UDFs</span><span class="sxs-lookup"><span data-stu-id="dded5-110">Testing UDFs</span></span>


### <a name="to-call-udfs-from-cells"></a><span data-ttu-id="dded5-111">To call UDFs from cells</span><span class="sxs-lookup"><span data-stu-id="dded5-111">To call UDFs from cells</span></span>


1. <span data-ttu-id="dded5-112">Start Microsoft Office Excel 2007.</span><span class="sxs-lookup"><span data-stu-id="dded5-112">Start Microsoft Office Excel 2007.</span></span>
    
  
2. <span data-ttu-id="dded5-p103">In cell A1, type the formula to call the  `MyDouble` function in SampleUdf.dll. The `MyDouble` function takes an argument of type **double**. In this example, you will take the argument from cell B1. In cell A1, type =MyDouble(B1).</span><span class="sxs-lookup"><span data-stu-id="dded5-p103">In cell A1, type the formula to call the  `MyDouble` function in SampleUdf.dll. The `MyDouble` function takes an argument of type **double**. In this example, you will take the argument from cell B1. In cell A1, type =MyDouble(B1).</span></span>
    
    > <span data-ttu-id="dded5-117">**Примечание:** Формула будет возвращать значение «#NAME?»</span><span class="sxs-lookup"><span data-stu-id="dded5-117">**Note:** The formula will evaluate to "#NAME?"</span></span> <span data-ttu-id="dded5-118">в Excel.</span><span class="sxs-lookup"><span data-stu-id="dded5-118">in Excel.</span></span> <span data-ttu-id="dded5-119">Формула вычисляется только в том случае, когда книга отображается в службах Excel.</span><span class="sxs-lookup"><span data-stu-id="dded5-119">The formula will be evaluated only when the workbook is displayed in Excel Services.</span></span> 

    > <span data-ttu-id="dded5-120">**Примечание:** Пользовательские функции можно запустить в клиенте и на сервере.</span><span class="sxs-lookup"><span data-stu-id="dded5-120">**Note:** You can run UDFs on both the client and server.</span></span> <span data-ttu-id="dded5-121">Будущая статьи, опубликованной на сайте MSDN будут рассмотрены следующие вопросы сведения.</span><span class="sxs-lookup"><span data-stu-id="dded5-121">A future article published on MSDN will explain the details.</span></span> <span data-ttu-id="dded5-122">Они опускаются здесь для простоты.</span><span class="sxs-lookup"><span data-stu-id="dded5-122">They are omitted here for the sake of simplicity.</span></span> 
3. <span data-ttu-id="dded5-123">In cell B1, type the number 8.</span><span class="sxs-lookup"><span data-stu-id="dded5-123">In cell B1, type the number 8.</span></span>
    
  
4. <span data-ttu-id="dded5-p106">Make cell B1 a named range. First click the **Formulas** tab. Then click cell B1 to select it. On the **Formulas** tab, in the **Named Cells** group, click **Name a Range**. In the **New Name** dialog box, in the **Name** box, type **MyDoubleParam**.</span><span class="sxs-lookup"><span data-stu-id="dded5-p106">Make cell B1 a named range. First click the **Formulas** tab. Then click cell B1 to select it. On the **Formulas** tab, in the **Named Cells** group, click **Name a Range**. In the **New Name** dialog box, in the **Name** box, type **MyDoubleParam**.</span></span>
    
  
5. <span data-ttu-id="dded5-p107">In cell A2, type the formula to call the  `ReturnDateTimeToday` function. Type=ReturnDateTimeToday().</span><span class="sxs-lookup"><span data-stu-id="dded5-p107">In cell A2, type the formula to call the  `ReturnDateTimeToday` function. Type=ReturnDateTimeToday().</span></span>
    
  
6. <span data-ttu-id="dded5-p108">In cell A3, type the formula to call the  `ReturnDateTimeToday` function. Type=ReturnDateTimeToday(). Next, right-click cell A3 to display the menu. Click **Format Cells**.</span><span class="sxs-lookup"><span data-stu-id="dded5-p108">In cell A3, type the formula to call the  `ReturnDateTimeToday` function. Type=ReturnDateTimeToday(). Next, right-click cell A3 to display the menu. Click **Format Cells**.</span></span>
    
  
7. <span data-ttu-id="dded5-p109">In the **Format Cells** dialog box, on the **Number** tab, select **Date**. Select a date format type from the **Type** listfor example, *3/4/2001.</span><span class="sxs-lookup"><span data-stu-id="dded5-p109">In the **Format Cells** dialog box, on the **Number** tab, select **Date**. Select a date format type from the **Type** list—for example, *3/4/2001.</span></span>
    
  
8. <span data-ttu-id="dded5-136">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="dded5-136">Click **OK**.</span></span>
    
  
9. <span data-ttu-id="dded5-p110">Save the workbook to a location of your choice on the local drive. Name the workbook "TestSampleUdf.xlsx".</span><span class="sxs-lookup"><span data-stu-id="dded5-p110">Save the workbook to a location of your choice on the local drive. Name the workbook "TestSampleUdf.xlsx".</span></span> 
    
  

### <a name="to-save-to-excel-services"></a><span data-ttu-id="dded5-139">To save to Excel Services</span><span class="sxs-lookup"><span data-stu-id="dded5-139">To save to Excel Services</span></span>


1. <span data-ttu-id="dded5-140">Click the **Microsoft Office Button**, point to **Save As**, and click **Save for Excel Services**.</span><span class="sxs-lookup"><span data-stu-id="dded5-140">Click the **Microsoft Office Button**, point to **Save As**, and click **Save for Excel Services**.</span></span> 
    
  
2. <span data-ttu-id="dded5-141">In the **Save As** dialog box, click **Excel Services Options**.</span><span class="sxs-lookup"><span data-stu-id="dded5-141">In the **Save As** dialog box, click **Excel Services Options**.</span></span>
    
  
3. <span data-ttu-id="dded5-142">In the **Excel Services Options** dialog box, on the **Show** tab, make sure that **Entire Workbook** is selected.</span><span class="sxs-lookup"><span data-stu-id="dded5-142">In the **Excel Services Options** dialog box, on the **Show** tab, make sure that **Entire Workbook** is selected.</span></span>
    
  
4. <span data-ttu-id="dded5-143">Click **Parameters**.</span><span class="sxs-lookup"><span data-stu-id="dded5-143">Click **Parameters**.</span></span> 
    
  
5. <span data-ttu-id="dded5-144">In the **Add Parameters** list, select the **MyDoubleParam** check box.</span><span class="sxs-lookup"><span data-stu-id="dded5-144">In the **Add Parameters** list, select the **MyDoubleParam** check box.</span></span>
    
  
6. <span data-ttu-id="dded5-p111">Click **OK**. You should now see "MyDoubleParam" listed in the **Parameters** list.</span><span class="sxs-lookup"><span data-stu-id="dded5-p111">Click **OK**. You should now see "MyDoubleParam" listed in the **Parameters** list.</span></span>
    
  
7. <span data-ttu-id="dded5-147">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="dded5-147">Click **OK**.</span></span>
    
  
8. <span data-ttu-id="dded5-148">In the **Save As** dialog box, make sure that the **Open this workbook in my browser after I save** check box is selected.</span><span class="sxs-lookup"><span data-stu-id="dded5-148">In the **Save As** dialog box, make sure that the **Open this workbook in my browser after I save** check box is selected.</span></span>
    
  
9. <span data-ttu-id="dded5-p112">In the **File name** box, type the path to the trusted SharePoint document library where you want to store this workbook. For example, _http://MyServer002/Shared%20Documents/TestSampleUdf.xlsx_.</span><span class="sxs-lookup"><span data-stu-id="dded5-p112">In the **File name** box, type the path to the trusted SharePoint document library where you want to store this workbook. For example, _http://MyServer002/Shared%20Documents/TestSampleUdf.xlsx_.</span></span>
    
  
10. <span data-ttu-id="dded5-p113">Click **Save**. You should see TestSampleUdf.xlsx in Веб-клиент Excel. In cell A1, you should see the number "72" because cell B1 * 9 = 8 * 9, which is 72. In cell A2 you should see a number. In cell A3, you should see the current date.</span><span class="sxs-lookup"><span data-stu-id="dded5-p113">Click **Save**. You should see TestSampleUdf.xlsx in Excel Web Access. In cell A1, you should see the number "72" because cell B1 * 9 = 8 * 9, which is 72. In cell A2 you should see a number. In cell A3, you should see the current date.</span></span> 
    
    > <span data-ttu-id="dded5-156">**Примечание:** В ячейку A2 число представляет количество дней, начиная с 1/1/1900 (или 1/1/1904 при наличии «Использовать систему дат 1904» включен).</span><span class="sxs-lookup"><span data-stu-id="dded5-156">**Note:** In cell A2, the number represents the number of days since 1/1/1900 (or 1/1/1904 if you have "Use 1904 Date System" turned on).</span></span> <span data-ttu-id="dded5-157">Это, как Excel представляет даты во внутренней сети.</span><span class="sxs-lookup"><span data-stu-id="dded5-157">It's how Excel represents dates internally.</span></span> 

### <a name="to-change-parameters-to-test-the-udf"></a><span data-ttu-id="dded5-158">To change parameters to test the UDF</span><span class="sxs-lookup"><span data-stu-id="dded5-158">To change parameters to test the UDF</span></span>


1. <span data-ttu-id="dded5-159">In the **Parameters** pane, you should see the named range for cell B1, that is, "MyDoubleParam".</span><span class="sxs-lookup"><span data-stu-id="dded5-159">In the **Parameters** pane, you should see the named range for cell B1, that is, "MyDoubleParam".</span></span>
    
  
2. <span data-ttu-id="dded5-p115">You can change the value in cell B1 by typing a number in the box next to "MyDoubleParam". For example, if you type 3 and then click **Apply**, Службы Excel will recalculate the workbook. Cell A1 will contain "27" instead of "72".</span><span class="sxs-lookup"><span data-stu-id="dded5-p115">You can change the value in cell B1 by typing a number in the box next to "MyDoubleParam". For example, if you type 3 and then click **Apply**, Excel Services will recalculate the workbook. Cell A1 will contain "27" instead of "72".</span></span> 
    
  

## <a name="see-also"></a><span data-ttu-id="dded5-163">См. также</span><span class="sxs-lookup"><span data-stu-id="dded5-163">See also</span></span>


#### <a name="tasks"></a><span data-ttu-id="dded5-164">Задачи</span><span class="sxs-lookup"><span data-stu-id="dded5-164">Tasks</span></span>


  
    
    
 [<span data-ttu-id="dded5-165">Step 1: Creating a Project and Adding a UDF Reference</span><span class="sxs-lookup"><span data-stu-id="dded5-165">Step 1: Creating a Project and Adding a UDF Reference</span></span>](step-1-creating-a-project-and-adding-a-udf-reference.md)
  
    
    
 [<span data-ttu-id="dded5-166">Step 2: Creating a Managed-Code UDF</span><span class="sxs-lookup"><span data-stu-id="dded5-166">Step 2: Creating a Managed-Code UDF</span></span>](step-2-creating-a-managed-code-udf.md)
  
    
    
 [<span data-ttu-id="dded5-167">Step 3: Deploying and Enabling UDFs</span><span class="sxs-lookup"><span data-stu-id="dded5-167">Step 3: Deploying and Enabling UDFs</span></span>](step-3-deploying-and-enabling-udfs.md)
  
    
    
 [<span data-ttu-id="dded5-168">How to: Create a UDF That Calls a Web Service</span><span class="sxs-lookup"><span data-stu-id="dded5-168">How to: Create a UDF That Calls a Web Service</span></span>](how-to-create-a-udf-that-calls-a-web-service.md)
#### <a name="concepts"></a><span data-ttu-id="dded5-169">Основные понятия</span><span class="sxs-lookup"><span data-stu-id="dded5-169">Concepts</span></span>


  
    
    
 [<span data-ttu-id="dded5-170">Walkthrough: Developing a Managed-Code UDF</span><span class="sxs-lookup"><span data-stu-id="dded5-170">Walkthrough: Developing a Managed-Code UDF</span></span>](walkthrough-developing-a-managed-code-udf.md)
  
    
    
 [<span data-ttu-id="dded5-171">Understanding Excel Services UDFs</span><span class="sxs-lookup"><span data-stu-id="dded5-171">Understanding Excel Services UDFs</span></span>](understanding-excel-services-udfs.md)
