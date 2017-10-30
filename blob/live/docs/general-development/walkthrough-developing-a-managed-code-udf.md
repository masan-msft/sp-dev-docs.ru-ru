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
# <a name="walkthrough-developing-a-managed-code-udf"></a><span data-ttu-id="07d1f-102">Walkthrough: Developing a Managed-Code UDF</span><span class="sxs-lookup"><span data-stu-id="07d1f-102">Walkthrough: Developing a Managed-Code UDF</span></span>

<span data-ttu-id="07d1f-103">This walkthrough describes the process for developing Службы Excel user-defined functions (UDFs) using Microsoft Visual C#.</span><span class="sxs-lookup"><span data-stu-id="07d1f-103">This walkthrough describes the process for developing Excel Services user-defined functions (UDFs) using Microsoft Visual C#.</span></span>
  
    
    

<span data-ttu-id="07d1f-104">During this walkthrough, you will learn how to:</span><span class="sxs-lookup"><span data-stu-id="07d1f-104">During this walkthrough, you will learn how to:</span></span>
- <span data-ttu-id="07d1f-105">Create a project using the Microsoft Visual Studio 2005 class library project template.</span><span class="sxs-lookup"><span data-stu-id="07d1f-105">Create a project using the Microsoft Visual Studio 2005 class library project template.</span></span>
    
  
- <span data-ttu-id="07d1f-106">Add a reference to Microsoft.Office.Excel.Server.Udf.dll.</span><span class="sxs-lookup"><span data-stu-id="07d1f-106">Add a reference to Microsoft.Office.Excel.Server.Udf.dll.</span></span>
    
  
- <span data-ttu-id="07d1f-107">Write UDFs for use in Службы Excel.</span><span class="sxs-lookup"><span data-stu-id="07d1f-107">Write UDFs for use in Excel Services.</span></span>
    
  
- <span data-ttu-id="07d1f-108">Create a workbook to call custom functions from cells.</span><span class="sxs-lookup"><span data-stu-id="07d1f-108">Create a workbook to call custom functions from cells.</span></span>
    
  
- <span data-ttu-id="07d1f-109">Test and run UDFs in Службы Excel.</span><span class="sxs-lookup"><span data-stu-id="07d1f-109">Test and run UDFs in Excel Services.</span></span>
    
  

## <a name="prerequisites"></a><span data-ttu-id="07d1f-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="07d1f-110">Prerequisites</span></span>

<span data-ttu-id="07d1f-111">In order to complete this walkthrough, you will need:</span><span class="sxs-lookup"><span data-stu-id="07d1f-111">In order to complete this walkthrough, you will need:</span></span> 
  
    
    

- <span data-ttu-id="07d1f-112">Microsoft SharePoint Server 2010.</span><span class="sxs-lookup"><span data-stu-id="07d1f-112">Microsoft SharePoint Server 2010.</span></span> 
    
    > <span data-ttu-id="07d1f-113">**Примечание:** Это самый простой способ получить все, что требуется на сервере, — это базовая, изолированной установки.</span><span class="sxs-lookup"><span data-stu-id="07d1f-113">**Note:** The easiest way to get all you need on the server is to do a basic, stand-alone install.</span></span> <span data-ttu-id="07d1f-114">Все, что вам нужно добавить, являющуюся надежным расположением.</span><span class="sxs-lookup"><span data-stu-id="07d1f-114">All you need to add on top of that is a trusted location.</span></span> 
- <span data-ttu-id="07d1f-115">Excel.</span><span class="sxs-lookup"><span data-stu-id="07d1f-115">Excel.</span></span>
    
  
- <span data-ttu-id="07d1f-116">Visual Studio or a similar Microsoft .NET Framework-compatible development tool.</span><span class="sxs-lookup"><span data-stu-id="07d1f-116">Visual Studio or a similar Microsoft .NET Framework-compatible development tool.</span></span>
    
  
- <span data-ttu-id="07d1f-117">To enable running the UDF assembly.</span><span class="sxs-lookup"><span data-stu-id="07d1f-117">To enable running the UDF assembly.</span></span>
    
  
- <span data-ttu-id="07d1f-118">A trusted SharePoint document library in which to store a workbook, and to allow the workbook to call UDFs by setting the **AllowUdfs** value to **true**.</span><span class="sxs-lookup"><span data-stu-id="07d1f-118">A trusted SharePoint document library in which to store a workbook, and to allow the workbook to call UDFs by setting the **AllowUdfs** value to **true**.</span></span> 
    
  
- <span data-ttu-id="07d1f-119">A sample workbook that calls the UDF stored in a trusted SharePoint document library.</span><span class="sxs-lookup"><span data-stu-id="07d1f-119">A sample workbook that calls the UDF stored in a trusted SharePoint document library.</span></span> 
    
  
- <span data-ttu-id="07d1f-120">Permissions to view and publish a workbook to a SharePoint document library.</span><span class="sxs-lookup"><span data-stu-id="07d1f-120">Permissions to view and publish a workbook to a SharePoint document library.</span></span> 
    
    > <span data-ttu-id="07d1f-121">**Примечание:** Дополнительные сведения о настройке разрешений обратитесь к документации Windows SharePoint Services 3.0.</span><span class="sxs-lookup"><span data-stu-id="07d1f-121">**Note:** For more information about setting permissions, see the Windows SharePoint Services 3.0 documentation.</span></span> 
- <span data-ttu-id="07d1f-122">To create the workbook using Excel.</span><span class="sxs-lookup"><span data-stu-id="07d1f-122">To create the workbook using Excel.</span></span>
    
  
- <span data-ttu-id="07d1f-123">To save the workbook as an .xlsx or .xlsb file.</span><span class="sxs-lookup"><span data-stu-id="07d1f-123">To save the workbook as an .xlsx or .xlsb file.</span></span>
    
    > <span data-ttu-id="07d1f-124">**Примечание:** Дополнительные сведения о надежного расположения, включение пользовательских функций и установить флаг **AllowUdfs** можно [Шаг 3: развертывание и включение пользовательских функций](step-3-deploying-and-enabling-udfs.md).</span><span class="sxs-lookup"><span data-stu-id="07d1f-124">**Note:** For more information about how to trust a location, how to enable UDFs, and how to set the **AllowUdfs** flag, see [Step 3: Deploying and Enabling UDFs](step-3-deploying-and-enabling-udfs.md).</span></span> 

## <a name="see-also"></a><span data-ttu-id="07d1f-125">См. также</span><span class="sxs-lookup"><span data-stu-id="07d1f-125">See also</span></span>


#### <a name="tasks"></a><span data-ttu-id="07d1f-126">Задачи</span><span class="sxs-lookup"><span data-stu-id="07d1f-126">Tasks</span></span>


  
    
    
 [<span data-ttu-id="07d1f-127">Step 1: Creating a Project and Adding a UDF Reference</span><span class="sxs-lookup"><span data-stu-id="07d1f-127">Step 1: Creating a Project and Adding a UDF Reference</span></span>](step-1-creating-a-project-and-adding-a-udf-reference.md)
  
    
    
 [<span data-ttu-id="07d1f-128">Step 2: Creating a Managed-Code UDF</span><span class="sxs-lookup"><span data-stu-id="07d1f-128">Step 2: Creating a Managed-Code UDF</span></span>](step-2-creating-a-managed-code-udf.md)
  
    
    
 [<span data-ttu-id="07d1f-129">Step 3: Deploying and Enabling UDFs</span><span class="sxs-lookup"><span data-stu-id="07d1f-129">Step 3: Deploying and Enabling UDFs</span></span>](step-3-deploying-and-enabling-udfs.md)
  
    
    
 [<span data-ttu-id="07d1f-130">Step 4: Testing and Calling UDFs from Cells</span><span class="sxs-lookup"><span data-stu-id="07d1f-130">Step 4: Testing and Calling UDFs from Cells</span></span>](step-4-testing-and-calling-udfs-from-cells.md)
  
    
    
 [<span data-ttu-id="07d1f-131">How to: Create a UDF That Calls a Web Service</span><span class="sxs-lookup"><span data-stu-id="07d1f-131">How to: Create a UDF That Calls a Web Service</span></span>](how-to-create-a-udf-that-calls-a-web-service.md)
#### <a name="concepts"></a><span data-ttu-id="07d1f-132">Основные понятия</span><span class="sxs-lookup"><span data-stu-id="07d1f-132">Concepts</span></span>


  
    
    
 [<span data-ttu-id="07d1f-133">Understanding Excel Services UDFs</span><span class="sxs-lookup"><span data-stu-id="07d1f-133">Understanding Excel Services UDFs</span></span>](understanding-excel-services-udfs.md)
#### <a name="other-resources"></a><span data-ttu-id="07d1f-134">Другие ресурсы</span><span class="sxs-lookup"><span data-stu-id="07d1f-134">Other resources</span></span>


  
    
    
 [<span data-ttu-id="07d1f-135">Пошаговое руководство. Разработка настраиваемого приложения с помощью веб-служб Excel</span><span class="sxs-lookup"><span data-stu-id="07d1f-135">Walkthrough: Developing a Custom Application Using Excel Web Services</span></span>](walkthrough-developing-a-custom-application-using-excel-web-services.md)
