---
title: "Включение пользовательских функций"
ms.date: 09/25/2017
keywords: how to,howdoi,howto,UDF list
f1_keywords:
- how to,howdoi,howto,UDF list
ms.prod: sharepoint
ms.assetid: 8c1af2eb-bb22-45e1-82de-a2b4b53d7a26
ms.openlocfilehash: e413bb036e33d905751d7fae0066242d6910c0b5
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="enable-udfs"></a><span data-ttu-id="54e38-103">Включение пользовательских функций</span><span class="sxs-lookup"><span data-stu-id="54e38-103">Enable UDFs</span></span>

<span data-ttu-id="54e38-104">Each Службы Excel trusted location in the Shared Services Provider (SSP) has an **AllowUdfs** flag.</span><span class="sxs-lookup"><span data-stu-id="54e38-104">Each Excel Services trusted location in the Shared Services Provider (SSP) has an **AllowUdfs** flag.</span></span>
  
> [!NOTE]
> <span data-ttu-id="54e38-105">[!Примечание] The **AllowUdfs** flag is denoted by the **User-defined functions allowed** option on the Excel Services Trusted File Locations page.</span><span class="sxs-lookup"><span data-stu-id="54e38-105">The **AllowUdfs** flag is denoted by the **User-defined functions allowed** option on the Excel Services Trusted File Locations page.</span></span>
  
    
    


<span data-ttu-id="54e38-p101">The default **AllowUdfs** value is **false**. If the **AllowUdfs** value is set to **false** in a particular trusted location, the workbooks in that trusted location are not allowed to call UDFs.</span><span class="sxs-lookup"><span data-stu-id="54e38-p101">The default **AllowUdfs** value is **false**. If the **AllowUdfs** value is set to **false** in a particular trusted location, the workbooks in that trusted location are not allowed to call UDFs.</span></span>
  
    
    

<span data-ttu-id="54e38-p102">In order to allow UDFs to be called from a specific trusted location, you set the **AllowUdfs** value to **true**.If the **AllowUdfs** value is **false** when a session is started on a workbook that has UDF calls in this trusted location, the UDF calls will fail. If you change the **AllowUdfs** value to **true** after a session has started, the UDF calls will also fail. This is because changes in the **AllowUdfs** flag take effect on the next session, after the configuration database has been updated.You can get around this by restarting the sessionfor example, by selecting **Reload Workbook** in Веб-клиент Excel.</span><span class="sxs-lookup"><span data-stu-id="54e38-p102">In order to allow UDFs to be called from a specific trusted location, you set the **AllowUdfs** value to **true**.If the **AllowUdfs** value is **false** when a session is started on a workbook that has UDF calls in this trusted location, the UDF calls will fail. If you change the **AllowUdfs** value to **true** after a session has started, the UDF calls will also fail. This is because changes in the **AllowUdfs** flag take effect on the next session, after the configuration database has been updated.You can get around this by restarting the session—for example, by selecting **Reload Workbook** in Excel Web Access.</span></span>
> <span data-ttu-id="54e38-111">**Осторожность:** Если вместо этого Сброс Microsoft Internet Information Services (IIS), будут завершены все текущие сеансы.</span><span class="sxs-lookup"><span data-stu-id="54e38-111">**Caution:** If you choose to reset Microsoft Internet Information Services (IIS) instead, it will end all current sessions.</span></span> 
  
    
    


## <a name="enabling-udfs"></a><span data-ttu-id="54e38-112">Enabling UDFs</span><span class="sxs-lookup"><span data-stu-id="54e38-112">Enabling UDFs</span></span>

<span data-ttu-id="54e38-113">To do the following steps, you need a computer that has Microsoft SharePoint Server 2010 installed.</span><span class="sxs-lookup"><span data-stu-id="54e38-113">To do the following steps, you need a computer that has Microsoft SharePoint Server 2010 installed.</span></span>
  
    
    

### <a name="to-enable-udfs"></a><span data-ttu-id="54e38-114">To enable UDFs</span><span class="sxs-lookup"><span data-stu-id="54e38-114">To enable UDFs</span></span>


1. <span data-ttu-id="54e38-115">On the **Start** menu, click **All Programs**.</span><span class="sxs-lookup"><span data-stu-id="54e38-115">On the **Start** menu, click **All Programs**.</span></span> 
    
  
2. <span data-ttu-id="54e38-116">Point to **Microsoft Office Server** and click **SharePoint Central Administration**.</span><span class="sxs-lookup"><span data-stu-id="54e38-116">Point to **Microsoft Office Server** and click **SharePoint Central Administration**.</span></span> 
    
  
3. <span data-ttu-id="54e38-117">On the Quick Launch, click your Shared Services Provider (SSP) linkfor example, "SharedServices1"to view the Shared Services home page for that particular SSP.</span><span class="sxs-lookup"><span data-stu-id="54e38-117">On the Quick Launch, click your Shared Services Provider (SSP) link—for example, "SharedServices1"—to view the Shared Services home page for that particular SSP.</span></span>
    
  
4. <span data-ttu-id="54e38-118">Under **Excel Services Settings**, click **User-defined functions**.</span><span class="sxs-lookup"><span data-stu-id="54e38-118">Under **Excel Services Settings**, click **User-defined functions**.</span></span> 
    
  
5. <span data-ttu-id="54e38-119">On the Excel Services User-Defined Functions page, click **Add User-Defined Function** to open the Excel Services Add User-Defined Function Assembly page.</span><span class="sxs-lookup"><span data-stu-id="54e38-119">On the Excel Services User-Defined Functions page, click **Add User-Defined Function** to open the Excel Services Add User-Defined Function Assembly page.</span></span>
    
  
6. <span data-ttu-id="54e38-p103">In the **Assembly** box, type the path to the UDF assembly. For example,C:\\MyUdfFolder\\MyUdf.dll.</span><span class="sxs-lookup"><span data-stu-id="54e38-p103">In the **Assembly** box, type the path to the UDF assembly. For example,C:\\MyUdfFolder\\MyUdf.dll.</span></span>
    
  
7. <span data-ttu-id="54e38-122">Under **Assembly Location**, click **Local file**.</span><span class="sxs-lookup"><span data-stu-id="54e38-122">Under **Assembly Location**, click **Local file**.</span></span>
    
    > [!NOTE]
  > <span data-ttu-id="54e38-p104">[!Примечание] The **Local file** option will be replaced with **File path** in future releases of Службы Excel. If you see **File path**, select that instead.</span><span class="sxs-lookup"><span data-stu-id="54e38-p104">The **Local file** option will be replaced with **File path** in future releases of Excel Services. If you see **File path**, select that instead.</span></span>   
  
8. <span data-ttu-id="54e38-125">Under **Enable Assembly**, the **Assembly enabled** check box should be selected by default.</span><span class="sxs-lookup"><span data-stu-id="54e38-125">Under **Enable Assembly**, the **Assembly enabled** check box should be selected by default.</span></span>
    
  
9. <span data-ttu-id="54e38-126">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="54e38-126">Click **OK**.</span></span>
    
  

## <a name="allowing-udf-calls"></a><span data-ttu-id="54e38-127">Allowing UDF Calls</span><span class="sxs-lookup"><span data-stu-id="54e38-127">Allowing UDF Calls</span></span>


### <a name="to-allow-udfs-to-be-called-from-a-workbook"></a><span data-ttu-id="54e38-128">To allow UDFs to be called from a workbook</span><span class="sxs-lookup"><span data-stu-id="54e38-128">To allow UDFs to be called from a workbook</span></span>


1. <span data-ttu-id="54e38-129">Open the Excel Services Add Trusted File Location page (if you are adding a new trusted location) or Excel Services Edit Trusted File Location page (if you are editing an existing trusted location).</span><span class="sxs-lookup"><span data-stu-id="54e38-129">Open the Excel Services Add Trusted File Location page (if you are adding a new trusted location) or Excel Services Edit Trusted File Location page (if you are editing an existing trusted location).</span></span> 
    
    > [!NOTE]
    > <span data-ttu-id="54e38-130">[!Примечание] For more information about trusting a location, see  [How to: Trust a Location](how-to-trust-a-location.md).</span><span class="sxs-lookup"><span data-stu-id="54e38-130">For more information about trusting a location, see  [How to: Trust a Location](how-to-trust-a-location.md).</span></span> 

2. <span data-ttu-id="54e38-131">Under **Allow User-Defined Functions**, select **User-defined functions allowed** to allow UDFs to be called from workbooks stored in this trusted location.</span><span class="sxs-lookup"><span data-stu-id="54e38-131">Under **Allow User-Defined Functions**, select **User-defined functions allowed** to allow UDFs to be called from workbooks stored in this trusted location.</span></span>
    
  
3. <span data-ttu-id="54e38-132">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="54e38-132">Click **OK**.</span></span>
    
  

## <a name="see-also"></a><span data-ttu-id="54e38-133">См. также</span><span class="sxs-lookup"><span data-stu-id="54e38-133">See also</span></span>

- [<span data-ttu-id="54e38-134">Step 3: Deploying and Enabling UDFs</span><span class="sxs-lookup"><span data-stu-id="54e38-134">Step 3: Deploying and Enabling UDFs</span></span>](step-3-deploying-and-enabling-udfs.md)
- [<span data-ttu-id="54e38-135">How to: Create a UDF That Calls a Web Service</span><span class="sxs-lookup"><span data-stu-id="54e38-135">How to: Create a UDF That Calls a Web Service</span></span>](how-to-create-a-udf-that-calls-a-web-service.md)
- [<span data-ttu-id="54e38-136">How to: Trust a Location</span><span class="sxs-lookup"><span data-stu-id="54e38-136">How to: Trust a Location</span></span>](how-to-trust-a-location.md)
- [<span data-ttu-id="54e38-137">Walkthrough: Developing a Managed-Code UDF</span><span class="sxs-lookup"><span data-stu-id="54e38-137">Walkthrough: Developing a Managed-Code UDF</span></span>](walkthrough-developing-a-managed-code-udf.md)
- [<span data-ttu-id="54e38-138">Frequently Asked Questions About Excel Services UDFs</span><span class="sxs-lookup"><span data-stu-id="54e38-138">Frequently Asked Questions About Excel Services UDFs</span></span>](frequently-asked-questions-about-excel-services-udfs.md)
- [<span data-ttu-id="54e38-139">Understanding Excel Services UDFs</span><span class="sxs-lookup"><span data-stu-id="54e38-139">Understanding Excel Services UDFs</span></span>](understanding-excel-services-udfs.md)
- [<span data-ttu-id="54e38-140">Excel Services Alerts</span><span class="sxs-lookup"><span data-stu-id="54e38-140">Excel Services Alerts</span></span>](excel-services-alerts.md)
- [<span data-ttu-id="54e38-141">Excel Services Known Issues and Tips</span><span class="sxs-lookup"><span data-stu-id="54e38-141">Excel Services Known Issues and Tips</span></span>](excel-services-known-issues-and-tips.md)
- [<span data-ttu-id="54e38-142">Excel Services Best Practices</span><span class="sxs-lookup"><span data-stu-id="54e38-142">Excel Services Best Practices</span></span>](excel-services-best-practices.md)
