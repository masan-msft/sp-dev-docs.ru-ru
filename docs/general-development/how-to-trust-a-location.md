---
title: "Определение надежных расположений"
ms.date: 09/25/2017
keywords: how to,howdoi,howto,trusted location
f1_keywords: how to,howdoi,howto,trusted location
ms.prod: sharepoint
ms.assetid: 0f396c0b-f578-4d1a-9e6b-a75f352265ab
ms.openlocfilehash: 2f22c1aa22fd81890d629c01ccdf8ba9adc50c66
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="trust-a-location"></a><span data-ttu-id="eb6a5-103">Определение надежных расположений</span><span class="sxs-lookup"><span data-stu-id="eb6a5-103">Trust a location</span></span>

<span data-ttu-id="eb6a5-p101">Workbooks that you want to access must be placed in a trusted location. If they are not, calls to open the workbooks will fail. This example shows you how to trust a location by using the SharePoint Central Administration page.</span><span class="sxs-lookup"><span data-stu-id="eb6a5-p101">Workbooks that you want to access must be placed in a trusted location. If they are not, calls to open the workbooks will fail. This example shows you how to trust a location by using the SharePoint Central Administration page.</span></span> 
  
    
    

<span data-ttu-id="eb6a5-p102">You can also trust a location by using Windows PowerShell. For more information, see the Microsoft SharePoint Server 2010 IT Pro and administration documentation on  [TechNet](http://technet.microsoft.com/en-us/library/ee428287%28office.14%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="eb6a5-p102">You can also trust a location by using Windows PowerShell. For more information, see the Microsoft SharePoint Server 2010 IT Pro and administration documentation on  [TechNet](http://technet.microsoft.com/en-us/library/ee428287%28office.14%29.aspx).</span></span> 
> <span data-ttu-id="eb6a5-109">**Совет:** Дополнительные сведения об улучшении администрирования и для просмотра снимков экрана страницы надежные расположения файлов [Служб Excel в усовершенствования администрирования SharePoint 2010](http://blogs.msdn.com/excel/archive/2009/11/16/excel-services-in-sharepoint-2010-administration-improvements.aspx)в блоге см.</span><span class="sxs-lookup"><span data-stu-id="eb6a5-109">**Tip:** For more information about administration improvement and to view screen shots of the Trusted File Locations page, see the blog post  [Excel Services in SharePoint 2010 Administration Improvements](http://blogs.msdn.com/excel/archive/2009/11/16/excel-services-in-sharepoint-2010-administration-improvements.aspx).</span></span> 
  
    
    


### <a name="to-trust-a-location"></a><span data-ttu-id="eb6a5-110">To trust a location</span><span class="sxs-lookup"><span data-stu-id="eb6a5-110">To trust a location</span></span>


1. <span data-ttu-id="eb6a5-111">On the **Start** menu, click **All Programs**.</span><span class="sxs-lookup"><span data-stu-id="eb6a5-111">On the **Start** menu, click **All Programs**.</span></span> 
    
  
2. <span data-ttu-id="eb6a5-112">Point to **Microsoft SharePoint 2010 Products**, and then click **SharePoint 2010 Central Administration**.</span><span class="sxs-lookup"><span data-stu-id="eb6a5-112">Point to **Microsoft SharePoint 2010 Products**, and then click **SharePoint 2010 Central Administration**.</span></span> 
    
  
3. <span data-ttu-id="eb6a5-113">On the SharePoint 2010 Central Administration page, under **Application Management**, click **Manage service applications**.</span><span class="sxs-lookup"><span data-stu-id="eb6a5-113">On the SharePoint 2010 Central Administration page, under **Application Management**, click **Manage service applications**.</span></span>
    
  
4. <span data-ttu-id="eb6a5-114">On the Manage Service Application page, click **Excel Services Application**.</span><span class="sxs-lookup"><span data-stu-id="eb6a5-114">On the Manage Service Application page, click **Excel Services Application**.</span></span>
    
  
5. <span data-ttu-id="eb6a5-115">On the Manage Excel Services Application page, click **Trusted File Locations**.</span><span class="sxs-lookup"><span data-stu-id="eb6a5-115">On the Manage Excel Services Application page, click **Trusted File Locations**.</span></span> 
    
  
6. <span data-ttu-id="eb6a5-116">On the Excel Services Application Trusted File Locations page, click **Add Trusted File Location**.</span><span class="sxs-lookup"><span data-stu-id="eb6a5-116">On the Excel Services Application Trusted File Locations page, click **Add Trusted File Location**.</span></span> 
    
  
7. <span data-ttu-id="eb6a5-117">On the Excel Services Application Add Trusted File Location page, in the **Address** text box, type the location to save your workbookfor example,http:// _MyServer002_/Shared%20Documents.</span><span class="sxs-lookup"><span data-stu-id="eb6a5-117">On the Excel Services Application Add Trusted File Location page, in the **Address** text box, type the location to save your workbook—for example,http:// _MyServer002_/Shared%20Documents.</span></span> 
    
  
8. <span data-ttu-id="eb6a5-p103">Under **Location type**, click the appropriate location type. In this example, select **SharePoint Foundation**.</span><span class="sxs-lookup"><span data-stu-id="eb6a5-p103">Under **Location type**, click the appropriate location type. In this example, select **SharePoint Foundation**.</span></span>
    
  
9. <span data-ttu-id="eb6a5-120">Under **Trust Children**, select **Children trusted** if you want to trust child libraries or directories.</span><span class="sxs-lookup"><span data-stu-id="eb6a5-120">Under **Trust Children**, select **Children trusted** if you want to trust child libraries or directories.</span></span>
    
  
10. <span data-ttu-id="eb6a5-121">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="eb6a5-121">Click **OK**.</span></span>
    
  

## <a name="see-also"></a><span data-ttu-id="eb6a5-122">См. также</span><span class="sxs-lookup"><span data-stu-id="eb6a5-122">See also</span></span>


#### <a name="tasks"></a><span data-ttu-id="eb6a5-123">Задачи</span><span class="sxs-lookup"><span data-stu-id="eb6a5-123">Tasks</span></span>


  
    
    
 [<span data-ttu-id="eb6a5-124">Step 3: Deploying and Enabling UDFs</span><span class="sxs-lookup"><span data-stu-id="eb6a5-124">Step 3: Deploying and Enabling UDFs</span></span>](step-3-deploying-and-enabling-udfs.md)
  
    
    
 [<span data-ttu-id="eb6a5-125">How to: Save from Excel Client to the Server</span><span class="sxs-lookup"><span data-stu-id="eb6a5-125">How to: Save from Excel Client to the Server</span></span>](how-to-save-from-excel-client-to-the-server.md)
#### <a name="concepts"></a><span data-ttu-id="eb6a5-126">Основные понятия</span><span class="sxs-lookup"><span data-stu-id="eb6a5-126">Concepts</span></span>


  
    
    
 [<span data-ttu-id="eb6a5-127">Excel Services Alerts</span><span class="sxs-lookup"><span data-stu-id="eb6a5-127">Excel Services Alerts</span></span>](excel-services-alerts.md)
#### <a name="other-resources"></a><span data-ttu-id="eb6a5-128">Другие ресурсы</span><span class="sxs-lookup"><span data-stu-id="eb6a5-128">Other resources</span></span>


  
    
    
 [<span data-ttu-id="eb6a5-129">Пошаговое руководство. Разработка настраиваемого приложения с помощью веб-служб Excel</span><span class="sxs-lookup"><span data-stu-id="eb6a5-129">Walkthrough: Developing a Custom Application Using Excel Web Services</span></span>](walkthrough-developing-a-custom-application-using-excel-web-services.md)
