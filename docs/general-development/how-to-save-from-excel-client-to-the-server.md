---
title: "Сохраните из клиента Excel на сервере"
ms.date: 09/25/2017
keywords: how to,howdoi,howto
f1_keywords: how to,howdoi,howto
ms.prod: sharepoint
ms.assetid: 28716ba5-0774-44df-833b-0034d2c63319
ms.openlocfilehash: 1601689491584b8a359a5bffa4b0596d10ab9e6f
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="save-from-excel-client-to-the-server"></a><span data-ttu-id="fa54e-103">Сохраните из клиента Excel на сервере</span><span class="sxs-lookup"><span data-stu-id="fa54e-103">Save from Excel client to the server</span></span>

<span data-ttu-id="fa54e-104">This example shows you how to:</span><span class="sxs-lookup"><span data-stu-id="fa54e-104">This example shows you how to:</span></span>
  
    
    


1. <span data-ttu-id="fa54e-105">Create a workbook with editable ranges.</span><span class="sxs-lookup"><span data-stu-id="fa54e-105">Create a workbook with editable ranges.</span></span>
    
  
2. <span data-ttu-id="fa54e-106">Save the workbook to a SharePoint document library that is a trusted location.</span><span class="sxs-lookup"><span data-stu-id="fa54e-106">Save the workbook to a SharePoint document library that is a trusted location.</span></span>
    
    > <span data-ttu-id="fa54e-107">**Примечание:** Предполагается, что уже создан в библиотеке документов SharePoint и был очень надежного расположения.</span><span class="sxs-lookup"><span data-stu-id="fa54e-107">**Note:** It is assumed that you have already created a SharePoint document library and made it a trusted location.</span></span> <span data-ttu-id="fa54e-108">Дополнительные сведения можно [как: надежного расположения](how-to-trust-a-location.md).</span><span class="sxs-lookup"><span data-stu-id="fa54e-108">For more information, see  [How to: Trust a Location](how-to-trust-a-location.md).</span></span> 
3. <span data-ttu-id="fa54e-109">Change values in a workbook by using the parameters pane in Веб-клиент Excel.</span><span class="sxs-lookup"><span data-stu-id="fa54e-109">Change values in a workbook by using the parameters pane in Excel Web Access.</span></span>
    
  

## <a name="saving-a-workbook-to-excel-services"></a><span data-ttu-id="fa54e-110">Saving a Workbook to Excel Services</span><span class="sxs-lookup"><span data-stu-id="fa54e-110">Saving a Workbook to Excel Services</span></span>


### <a name="to-create-a-workbook-with-ranges"></a><span data-ttu-id="fa54e-111">To create a workbook with ranges</span><span class="sxs-lookup"><span data-stu-id="fa54e-111">To create a workbook with ranges</span></span>


1. <span data-ttu-id="fa54e-112">Start Excel.</span><span class="sxs-lookup"><span data-stu-id="fa54e-112">Start Excel.</span></span>
    
  
2. <span data-ttu-id="fa54e-113">In cell A1, type 8.</span><span class="sxs-lookup"><span data-stu-id="fa54e-113">In cell A1, type 8.</span></span>
    
  
3. <span data-ttu-id="fa54e-114">In cell A2, type =3*A1.</span><span class="sxs-lookup"><span data-stu-id="fa54e-114">In cell A2, type =3*A1.</span></span>
    
  
4. <span data-ttu-id="fa54e-115">To make cell A1 editable in Веб-клиент Excel, you must first make cell A1 into a named range:</span><span class="sxs-lookup"><span data-stu-id="fa54e-115">To make cell A1 editable in Excel Web Access, you must first make cell A1 into a named range:</span></span> 
    
1. <span data-ttu-id="fa54e-116">Click the **Formulas** tab, and then click cell **A1** to select it.</span><span class="sxs-lookup"><span data-stu-id="fa54e-116">Click the **Formulas** tab, and then click cell **A1** to select it.</span></span>
    
  
2. <span data-ttu-id="fa54e-117">On the **Formulas** tab, in the **Defined Names** group, click **Define Name**.</span><span class="sxs-lookup"><span data-stu-id="fa54e-117">On the **Formulas** tab, in the **Defined Names** group, click **Define Name**.</span></span>
    
  
3. <span data-ttu-id="fa54e-118">In the **New Name** dialog box, in the **Name** text box, typeMyAOneParam.</span><span class="sxs-lookup"><span data-stu-id="fa54e-118">In the **New Name** dialog box, in the **Name** text box, typeMyAOneParam.</span></span>
    
  

### <a name="to-save-to-excel-services"></a><span data-ttu-id="fa54e-119">To save to Excel Services</span><span class="sxs-lookup"><span data-stu-id="fa54e-119">To save to Excel Services</span></span>


1. <span data-ttu-id="fa54e-120">On the **File** menu, click **Save &amp; Send**, and then click **Save to SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="fa54e-120">On the **File** menu, click **Save &amp; Send**, and then click **Save to SharePoint**.</span></span> 
    
  
2. <span data-ttu-id="fa54e-121">In the **Save to SharePoint** dialog box, click **Publish Options**.</span><span class="sxs-lookup"><span data-stu-id="fa54e-121">In the **Save to SharePoint** dialog box, click **Publish Options**.</span></span>
    
  
3. <span data-ttu-id="fa54e-122">In the **Publish Options** dialog box, on the **Show** tab, ensure that **Entire Workbook** is selected.</span><span class="sxs-lookup"><span data-stu-id="fa54e-122">In the **Publish Options** dialog box, on the **Show** tab, ensure that **Entire Workbook** is selected.</span></span>
    
  
4. <span data-ttu-id="fa54e-123">On the **Parameters** tab, click **Add**..</span><span class="sxs-lookup"><span data-stu-id="fa54e-123">On the **Parameters** tab, click **Add**..</span></span>
    
  
5. <span data-ttu-id="fa54e-124">In the **Add Parameters** list, select the **MyAOneParam** check box.</span><span class="sxs-lookup"><span data-stu-id="fa54e-124">In the **Add Parameters** list, select the **MyAOneParam** check box.</span></span>
    
  
6. <span data-ttu-id="fa54e-p102">Click **OK**. You should now see "MyAOneParam" in the **Parameters** list.</span><span class="sxs-lookup"><span data-stu-id="fa54e-p102">Click **OK**. You should now see "MyAOneParam" in the **Parameters** list.</span></span>
    
  
7. <span data-ttu-id="fa54e-127">Click **OK** to close the **Publish Options** dialog box.</span><span class="sxs-lookup"><span data-stu-id="fa54e-127">Click **OK** to close the **Publish Options** dialog box.</span></span>
    
  
8. <span data-ttu-id="fa54e-128">In the **Save to SharePoint** dialog box, click **Save As**.</span><span class="sxs-lookup"><span data-stu-id="fa54e-128">In the **Save to SharePoint** dialog box, click **Save As**.</span></span>
    
  
9. <span data-ttu-id="fa54e-129">In the **Save As** dialog box, ensure that the **Open with Excel in the browser** check box is selected.</span><span class="sxs-lookup"><span data-stu-id="fa54e-129">In the **Save As** dialog box, ensure that the **Open with Excel in the browser** check box is selected.</span></span>
    
  
10. <span data-ttu-id="fa54e-p103">In the **File name** text box, type the path to the trusted SharePoint document library where you want to store this workbook. For example,http:// _MyServer002_/Shared%20Documents/TestParam.xlsx.</span><span class="sxs-lookup"><span data-stu-id="fa54e-p103">In the **File name** text box, type the path to the trusted SharePoint document library where you want to store this workbook. For example,http:// _MyServer002_/Shared%20Documents/TestParam.xlsx.</span></span>
    
  
11. <span data-ttu-id="fa54e-p104">Click **Save**. You should see TestParam.xlsx in Веб-клиент Excel.</span><span class="sxs-lookup"><span data-stu-id="fa54e-p104">Click **Save**. You should see TestParam.xlsx in Excel Web Access.</span></span> 
    
  

### <a name="to-change-values-by-using-parameters"></a><span data-ttu-id="fa54e-134">To change values by using parameters</span><span class="sxs-lookup"><span data-stu-id="fa54e-134">To change values by using parameters</span></span>


1. <span data-ttu-id="fa54e-135">In the **Parameters** pane, you should see the named range for cell **A1**that is, **MyAOneParam**.</span><span class="sxs-lookup"><span data-stu-id="fa54e-135">In the **Parameters** pane, you should see the named range for cell **A1**—that is, **MyAOneParam**.</span></span> 
    
  
2. <span data-ttu-id="fa54e-p105">You can change the values in cell **A1** and cell **A2** by typing a number in the text box next to **MyAOneParam**. For example, if you type 10 and then click **Apply**, cell **A1** changes to **10** and cell **A2** changes to **30**.</span><span class="sxs-lookup"><span data-stu-id="fa54e-p105">You can change the values in cell **A1** and cell **A2** by typing a number in the text box next to **MyAOneParam**. For example, if you type 10 and then click **Apply**, cell **A1** changes to **10** and cell **A2** changes to **30**.</span></span> 
    
  

## <a name="see-also"></a><span data-ttu-id="fa54e-138">См. также</span><span class="sxs-lookup"><span data-stu-id="fa54e-138">See also</span></span>


#### <a name="tasks"></a><span data-ttu-id="fa54e-139">Задачи</span><span class="sxs-lookup"><span data-stu-id="fa54e-139">Tasks</span></span>


  
    
    
 [<span data-ttu-id="fa54e-140">How to: Save to the Server to Prepare for Programmatic Access</span><span class="sxs-lookup"><span data-stu-id="fa54e-140">How to: Save to the Server to Prepare for Programmatic Access</span></span>](how-to-save-to-the-server-to-prepare-for-programmatic-access.md)
#### <a name="concepts"></a><span data-ttu-id="fa54e-141">Основные понятия</span><span class="sxs-lookup"><span data-stu-id="fa54e-141">Concepts</span></span>


  
    
    
 [<span data-ttu-id="fa54e-142">Доступ к API SOAP</span><span class="sxs-lookup"><span data-stu-id="fa54e-142">Accessing the SOAP API</span></span>](accessing-the-soap-api.md)
  
    
    
 [<span data-ttu-id="fa54e-143">Loop-Back SOAP Calls and Direct Linking</span><span class="sxs-lookup"><span data-stu-id="fa54e-143">Loop-Back SOAP Calls and Direct Linking</span></span>](loop-back-soap-calls-and-direct-linking.md)
  
    
    
 [<span data-ttu-id="fa54e-144">Excel Services Alerts</span><span class="sxs-lookup"><span data-stu-id="fa54e-144">Excel Services Alerts</span></span>](excel-services-alerts.md)
#### <a name="other-resources"></a><span data-ttu-id="fa54e-145">Другие ресурсы</span><span class="sxs-lookup"><span data-stu-id="fa54e-145">Other resources</span></span>


  
    
    
 [<span data-ttu-id="fa54e-146">Пошаговое руководство. Разработка настраиваемого приложения с помощью веб-служб Excel</span><span class="sxs-lookup"><span data-stu-id="fa54e-146">Walkthrough: Developing a Custom Application Using Excel Web Services</span></span>](walkthrough-developing-a-custom-application-using-excel-web-services.md)