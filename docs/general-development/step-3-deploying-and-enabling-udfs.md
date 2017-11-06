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
# <a name="step-3-deploying-and-enabling-udfs"></a><span data-ttu-id="e2ff8-102">Step 3: Deploying and Enabling UDFs</span><span class="sxs-lookup"><span data-stu-id="e2ff8-102">Step 3: Deploying and Enabling UDFs</span></span>

<span data-ttu-id="e2ff8-103">In this step, you will:</span><span class="sxs-lookup"><span data-stu-id="e2ff8-103">In this step, you will:</span></span>
  
    
    


1. <span data-ttu-id="e2ff8-104">Deploy SampleUdf.dll, which you created in  [Step 2: Creating a Managed-Code UDF](step-2-creating-a-managed-code-udf.md), to a folder on a computer that has Microsoft SharePoint Server 2010 installed.</span><span class="sxs-lookup"><span data-stu-id="e2ff8-104">Deploy SampleUdf.dll, which you created in  [Step 2: Creating a Managed-Code UDF](step-2-creating-a-managed-code-udf.md), to a folder on a computer that has Microsoft SharePoint Server 2010 installed.</span></span>
    
  
2. <span data-ttu-id="e2ff8-105">Allow user-defined functions (UDFs) to be called from a specific trusted location, for example, trusted Shared Documents location.</span><span class="sxs-lookup"><span data-stu-id="e2ff8-105">Allow user-defined functions (UDFs) to be called from a specific trusted location, for example, trusted Shared Documents location.</span></span> 
    
  
3. <span data-ttu-id="e2ff8-106">Enable SampleUdf.dll.</span><span class="sxs-lookup"><span data-stu-id="e2ff8-106">Enable SampleUdf.dll.</span></span>
    
  

## <a name="deploying-udfs"></a><span data-ttu-id="e2ff8-107">Deploying UDFs</span><span class="sxs-lookup"><span data-stu-id="e2ff8-107">Deploying UDFs</span></span>


### <a name="to-deploy-udfs"></a><span data-ttu-id="e2ff8-108">To deploy UDFs</span><span class="sxs-lookup"><span data-stu-id="e2ff8-108">To deploy UDFs</span></span>


1. <span data-ttu-id="e2ff8-p101">Create a folder named "UDFs" on the local drive of the computer to which you want to deploy UDFs. For example, "C:\\UDFs".</span><span class="sxs-lookup"><span data-stu-id="e2ff8-p101">Create a folder named "UDFs" on the local drive of the computer to which you want to deploy UDFs. For example, "C:\\UDFs".</span></span>
    
  
2. <span data-ttu-id="e2ff8-111">Copy the SampleUdf.dll assembly.</span><span class="sxs-lookup"><span data-stu-id="e2ff8-111">Copy the SampleUdf.dll assembly.</span></span>
    
  
3. <span data-ttu-id="e2ff8-112">Save SampleUdf.dll in "C:\\UDFs".</span><span class="sxs-lookup"><span data-stu-id="e2ff8-112">Save SampleUdf.dll in "C:\\UDFs".</span></span> 
    
  

## <a name="trusting-a-location"></a><span data-ttu-id="e2ff8-113">Trusting a Location</span><span class="sxs-lookup"><span data-stu-id="e2ff8-113">Trusting a Location</span></span>


### <a name="to-trust-a-location"></a><span data-ttu-id="e2ff8-114">To trust a location</span><span class="sxs-lookup"><span data-stu-id="e2ff8-114">To trust a location</span></span>


1. <span data-ttu-id="e2ff8-115">On the **Start** menu, click **All Programs**.</span><span class="sxs-lookup"><span data-stu-id="e2ff8-115">On the **Start** menu, click **All Programs**.</span></span> 
    
  
2. <span data-ttu-id="e2ff8-116">Point to **Microsoft SharePoint 2010 Products** and click **SharePoint Central Administration**.</span><span class="sxs-lookup"><span data-stu-id="e2ff8-116">Point to **Microsoft SharePoint 2010 Products** and click **SharePoint Central Administration**.</span></span> 
    
  
3. <span data-ttu-id="e2ff8-117">Under **Application Management** click **Manage service applications**.</span><span class="sxs-lookup"><span data-stu-id="e2ff8-117">Under **Application Management** click **Manage service applications**.</span></span>
    
  
4. <span data-ttu-id="e2ff8-118">On the Manage Service Applications page, click **Excel Services Application**.</span><span class="sxs-lookup"><span data-stu-id="e2ff8-118">On the Manage Service Applications page, click **Excel Services Application**.</span></span>
    
  
5. <span data-ttu-id="e2ff8-119">On the **Excel Services Application** page, click **Trusted File Locations**.</span><span class="sxs-lookup"><span data-stu-id="e2ff8-119">On the **Excel Services Application** page, click **Trusted File Locations**.</span></span>
    
  
6. <span data-ttu-id="e2ff8-120">On the Trusted File Locations page, click **Add Trusted File Location**.</span><span class="sxs-lookup"><span data-stu-id="e2ff8-120">On the Trusted File Locations page, click **Add Trusted File Location**.</span></span> 
    
  
7. <span data-ttu-id="e2ff8-121">On the Add Trusted File Location page, in the **Address** box, type the location where you will save your workbookfor example, _http://MyServer002/Shared%20Documents_.</span><span class="sxs-lookup"><span data-stu-id="e2ff8-121">On the Add Trusted File Location page, in the **Address** box, type the location where you will save your workbook—for example, _http://MyServer002/Shared%20Documents_.</span></span> 
    
  
8. <span data-ttu-id="e2ff8-p102">Under **Location type**, click the appropriate location type. In this example, select Microsoft SharePoint Foundation.</span><span class="sxs-lookup"><span data-stu-id="e2ff8-p102">Under **Location type**, click the appropriate location type. In this example, select Microsoft SharePoint Foundation.</span></span>
    
  
9. <span data-ttu-id="e2ff8-124">Under **Trust Children**, select **Children trusted** to trust child libraries or directories.</span><span class="sxs-lookup"><span data-stu-id="e2ff8-124">Under **Trust Children**, select **Children trusted** to trust child libraries or directories.</span></span>
    
  
10. <span data-ttu-id="e2ff8-125">Under **Allow User-Defined Functions**, select **User-defined functions allowed** to allow UDFs to be called from workbooks stored in this trusted location.</span><span class="sxs-lookup"><span data-stu-id="e2ff8-125">Under **Allow User-Defined Functions**, select **User-defined functions allowed** to allow UDFs to be called from workbooks stored in this trusted location.</span></span>
    
  
11. <span data-ttu-id="e2ff8-126">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="e2ff8-126">Click **OK**.</span></span>
    
  

## <a name="enabling-udfs"></a><span data-ttu-id="e2ff8-127">Enabling UDFs</span><span class="sxs-lookup"><span data-stu-id="e2ff8-127">Enabling UDFs</span></span>

<span data-ttu-id="e2ff8-128">To do the following steps, you need a computer that has SharePoint Server 2010 installed.</span><span class="sxs-lookup"><span data-stu-id="e2ff8-128">To do the following steps, you need a computer that has SharePoint Server 2010 installed.</span></span>
  
    
    

### <a name="to-enable-udfs"></a><span data-ttu-id="e2ff8-129">To enable UDFs</span><span class="sxs-lookup"><span data-stu-id="e2ff8-129">To enable UDFs</span></span>


1. <span data-ttu-id="e2ff8-130">Follow steps 1 through 3 in the previous procedure ("To trust a location") to display the Shared Services home page for an SSP.</span><span class="sxs-lookup"><span data-stu-id="e2ff8-130">Follow steps 1 through 3 in the previous procedure ("To trust a location") to display the Shared Services home page for an SSP.</span></span>
    
  
2. <span data-ttu-id="e2ff8-131">Under **Excel Services Settings**, click **User-defined function assemblies**.</span><span class="sxs-lookup"><span data-stu-id="e2ff8-131">Under **Excel Services Settings**, click **User-defined function assemblies**.</span></span> 
    
  
3. <span data-ttu-id="e2ff8-132">На странице "пользовательские функции служб Excel" щелкните **Добавить пользовательскую функцию** , чтобы открыть страницу "Добавить сборку пользовательских функций страницу".</span><span class="sxs-lookup"><span data-stu-id="e2ff8-132">On the Excel Services User-Defined Functions page, click **Add User-Defined Function** to open the ExcelServices Add User-Defined Function Assembly page.</span></span>
    
  
4. <span data-ttu-id="e2ff8-p103">In the **Assembly** box, type the path to the SampleUdf.dll assembly. In this example, it would be _C:\\UDFs\\SampleUdf.dll_.</span><span class="sxs-lookup"><span data-stu-id="e2ff8-p103">In the **Assembly** box, type the path to the SampleUdf.dll assembly. In this example, it would be _C:\\UDFs\\SampleUdf.dll_.</span></span>
    
  
5. <span data-ttu-id="e2ff8-135">Under **Assembly Location**, click **File path**.</span><span class="sxs-lookup"><span data-stu-id="e2ff8-135">Under **Assembly Location**, click **File path**.</span></span>
    
  
6. <span data-ttu-id="e2ff8-136">Under **Enable Assembly**, the **Assembly enabled** check box should be selected by default.</span><span class="sxs-lookup"><span data-stu-id="e2ff8-136">Under **Enable Assembly**, the **Assembly enabled** check box should be selected by default.</span></span>
    
  
7. <span data-ttu-id="e2ff8-137">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="e2ff8-137">Click **OK**.</span></span>
    
  

## <a name="robust-programming"></a><span data-ttu-id="e2ff8-138">Надежное программирование</span><span class="sxs-lookup"><span data-stu-id="e2ff8-138">Robust programming</span></span>

<span data-ttu-id="e2ff8-139">If the **AllowUdfs** value is **false** when a session is started on a workbook that has UDF calls, the UDF calls will fail.</span><span class="sxs-lookup"><span data-stu-id="e2ff8-139">If the **AllowUdfs** value is **false** when a session is started on a workbook that has UDF calls, the UDF calls will fail.</span></span>
  
    
    

> <span data-ttu-id="e2ff8-140">**Примечание:** Флаг **AllowUdfs** обозначается параметр **пользовательские функции разрешены** (в разделе шаг 9 в доверие» расположение «).</span><span class="sxs-lookup"><span data-stu-id="e2ff8-140">**Note:** The **AllowUdfs** flag is denoted by the **User-defined functions allowed** option (see step 9 in the "Trusting a Location" section).</span></span>
  
    
    

<span data-ttu-id="e2ff8-p104">If you change the **AllowUdfs** value to **true** after a session has started, the UDF calls will also fail. This is because changes in the **AllowUdfs** flag take effect on the next session. You can get around this by resetting Microsoft Internet Information Services (IIS). Resetting IIS will reload UDFs.</span><span class="sxs-lookup"><span data-stu-id="e2ff8-p104">If you change the **AllowUdfs** value to **true** after a session has started, the UDF calls will also fail. This is because changes in the **AllowUdfs** flag take effect on the next session. You can get around this by resetting Microsoft Internet Information Services (IIS). Resetting IIS will reload UDFs.</span></span>
  
    
    
<span data-ttu-id="e2ff8-145">For more information about resetting IIS, see  [How to: Enable UDFs](how-to-enable-udfs.md).</span><span class="sxs-lookup"><span data-stu-id="e2ff8-145">For more information about resetting IIS, see  [How to: Enable UDFs](how-to-enable-udfs.md).</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="e2ff8-146">См. также</span><span class="sxs-lookup"><span data-stu-id="e2ff8-146">See also</span></span>


#### <a name="tasks"></a><span data-ttu-id="e2ff8-147">Задачи</span><span class="sxs-lookup"><span data-stu-id="e2ff8-147">Tasks</span></span>


  
    
    
 [<span data-ttu-id="e2ff8-148">Step 1: Creating a Project and Adding a UDF Reference</span><span class="sxs-lookup"><span data-stu-id="e2ff8-148">Step 1: Creating a Project and Adding a UDF Reference</span></span>](step-1-creating-a-project-and-adding-a-udf-reference.md)
  
    
    
 [<span data-ttu-id="e2ff8-149">Step 2: Creating a Managed-Code UDF</span><span class="sxs-lookup"><span data-stu-id="e2ff8-149">Step 2: Creating a Managed-Code UDF</span></span>](step-2-creating-a-managed-code-udf.md)
  
    
    
 [<span data-ttu-id="e2ff8-150">Step 4: Testing and Calling UDFs from Cells</span><span class="sxs-lookup"><span data-stu-id="e2ff8-150">Step 4: Testing and Calling UDFs from Cells</span></span>](step-4-testing-and-calling-udfs-from-cells.md)
  
    
    
 [<span data-ttu-id="e2ff8-151">How to: Enable UDFs</span><span class="sxs-lookup"><span data-stu-id="e2ff8-151">How to: Enable UDFs</span></span>](how-to-enable-udfs.md)
#### <a name="concepts"></a><span data-ttu-id="e2ff8-152">Основные понятия</span><span class="sxs-lookup"><span data-stu-id="e2ff8-152">Concepts</span></span>


  
    
    
 [<span data-ttu-id="e2ff8-153">Walkthrough: Developing a Managed-Code UDF</span><span class="sxs-lookup"><span data-stu-id="e2ff8-153">Walkthrough: Developing a Managed-Code UDF</span></span>](walkthrough-developing-a-managed-code-udf.md)
  
    
    
 [<span data-ttu-id="e2ff8-154">Understanding Excel Services UDFs</span><span class="sxs-lookup"><span data-stu-id="e2ff8-154">Understanding Excel Services UDFs</span></span>](understanding-excel-services-udfs.md)