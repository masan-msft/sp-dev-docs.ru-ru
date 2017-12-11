---
title: Step 1 Creating a Project and Adding a UDF Reference
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 4c6f1279-28df-45af-8488-42a6573d526d
ms.openlocfilehash: f4ccef885ce00bdad740154890d81c9495b02c86
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="step-1-creating-a-project-and-adding-a-udf-reference"></a><span data-ttu-id="3bdf9-102">Step 1: Creating a Project and Adding a UDF Reference</span><span class="sxs-lookup"><span data-stu-id="3bdf9-102">Step 1: Creating a Project and Adding a UDF Reference</span></span>

<span data-ttu-id="3bdf9-103">In this step, you will create a project and add a reference to Microsoft.Office.Excel.Server.Udf.dll.</span><span class="sxs-lookup"><span data-stu-id="3bdf9-103">In this step, you will create a project and add a reference to Microsoft.Office.Excel.Server.Udf.dll.</span></span> 
  
    
    


## <a name="creating-the-project"></a><span data-ttu-id="3bdf9-104">Creating the Project</span><span class="sxs-lookup"><span data-stu-id="3bdf9-104">Creating the Project</span></span>

<span data-ttu-id="3bdf9-105">The following project uses Microsoft Visual Studio 2005.</span><span class="sxs-lookup"><span data-stu-id="3bdf9-105">The following project uses Microsoft Visual Studio 2005.</span></span>
  
> [!NOTE]
> <span data-ttu-id="3bdf9-106">[!Примечание] Depending on which settings you use in the Visual Studio integrated development environment (IDE), the process to create a project could be slightly different.</span><span class="sxs-lookup"><span data-stu-id="3bdf9-106">Depending on which settings you use in the Visual Studio integrated development environment (IDE), the process to create a project could be slightly different.</span></span> 
  
    
    


### <a name="to-create-a-project"></a><span data-ttu-id="3bdf9-107">To create a project</span><span class="sxs-lookup"><span data-stu-id="3bdf9-107">To create a project</span></span>


1. <span data-ttu-id="3bdf9-108">Start Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3bdf9-108">Start Visual Studio.</span></span>
    
  
2. <span data-ttu-id="3bdf9-p101">On the **File** menu, point to **New**, and then click **Project**. The **New Project** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="3bdf9-p101">On the **File** menu, point to **New**, and then click **Project**. The **New Project** dialog box appears.</span></span>
    
  
3. <span data-ttu-id="3bdf9-111">In the **Project Type** pane, select **Visual C# Projects**.</span><span class="sxs-lookup"><span data-stu-id="3bdf9-111">In the **Project Type** pane, select **Visual C# Projects**.</span></span>
    
  
4. <span data-ttu-id="3bdf9-112">In the **Templates** pane, click **Class Library**.</span><span class="sxs-lookup"><span data-stu-id="3bdf9-112">In the **Templates** pane, click **Class Library**.</span></span>
    
  
5. <span data-ttu-id="3bdf9-113">In the **Name** box, type **SampleUdf**.</span><span class="sxs-lookup"><span data-stu-id="3bdf9-113">In the **Name** box, type **SampleUdf**.</span></span>
    
  
6. <span data-ttu-id="3bdf9-114">In the **Location** box, type the path where you want to save your project, or click **Browse** to navigate to the folder.</span><span class="sxs-lookup"><span data-stu-id="3bdf9-114">In the **Location** box, type the path where you want to save your project, or click **Browse** to navigate to the folder.</span></span>
    
  
7. <span data-ttu-id="3bdf9-p102">Click **OK**. Your new project appears in **Solution Explorer**. You also will see that a file with the default name of Class1.cs has been added to your project.</span><span class="sxs-lookup"><span data-stu-id="3bdf9-p102">Click **OK**. Your new project appears in **Solution Explorer**. You also will see that a file with the default name of Class1.cs has been added to your project.</span></span>
    
  
8. <span data-ttu-id="3bdf9-118">You should see the following code in the Class1.cs file:</span><span class="sxs-lookup"><span data-stu-id="3bdf9-118">You should see the following code in the Class1.cs file:</span></span>
    
```cs
  
using System;
using System.Collections.Generic;
using System.Text;

namespace SampleUdf
{
    public class Class1
    {
    }
}
```


```VB.net
  
Imports System
Imports System.Collections.Generic
Imports System.Text

Namespace SampleUdf
Public Class Class1
End Class
End Namespace
```


## <a name="adding-a-reference"></a><span data-ttu-id="3bdf9-119">Adding a Reference</span><span class="sxs-lookup"><span data-stu-id="3bdf9-119">Adding a Reference</span></span>

<span data-ttu-id="3bdf9-120">The following steps show how to locate Microsoft.Office.Excel.Server.Udf.dll and how to add a reference to it.</span><span class="sxs-lookup"><span data-stu-id="3bdf9-120">The following steps show how to locate Microsoft.Office.Excel.Server.Udf.dll and how to add a reference to it.</span></span> 
  
    
    

### <a name="to-add-a-reference"></a><span data-ttu-id="3bdf9-121">To add a reference</span><span class="sxs-lookup"><span data-stu-id="3bdf9-121">To add a reference</span></span>


1. <span data-ttu-id="3bdf9-122">On the **Project** menu, click **Add Reference**.</span><span class="sxs-lookup"><span data-stu-id="3bdf9-122">On the **Project** menu, click **Add Reference**.</span></span>
    
  
2. <span data-ttu-id="3bdf9-123">In the **Add Reference** dialog box, on the **.NET** tab, select **Excel Services UDF Framework**.</span><span class="sxs-lookup"><span data-stu-id="3bdf9-123">In the **Add Reference** dialog box, on the **.NET** tab, select **Excel Services UDF Framework**.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="3bdf9-124">[!Примечание] You can also open the **Add Reference** dialog box in **Solution Explorer** by right-clicking **References** and selecting **Add Reference**.</span><span class="sxs-lookup"><span data-stu-id="3bdf9-124">You can also open the **Add Reference** dialog box in **Solution Explorer** by right-clicking **References** and selecting **Add Reference**.</span></span> 

3. <span data-ttu-id="3bdf9-125">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="3bdf9-125">Click **OK**.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="3bdf9-p103">[!Примечание] The previous steps assume that you are building the project on a computer that has Microsoft SharePoint Server 2010 installed. On the computer where you have installed SharePoint Server 2010, you can find a copy of Microsoft.Office.Excel.Server.Udf.dll at: > [drive:]\\Program Files\\Common Files\\Microsoft Shared\\web server extensions\\14\\ISAPI</span><span class="sxs-lookup"><span data-stu-id="3bdf9-p103">The previous steps assume that you are building the project on a computer that has Microsoft SharePoint Server 2010 installed. On the computer where you have installed SharePoint Server 2010, you can find a copy of Microsoft.Office.Excel.Server.Udf.dll at: > [drive:]\\Program Files\\Common Files\\Microsoft Shared\\web server extensions\\14\\ISAPI</span></span> 

## <a name="see-also"></a><span data-ttu-id="3bdf9-128">См. также</span><span class="sxs-lookup"><span data-stu-id="3bdf9-128">See also</span></span>

- [<span data-ttu-id="3bdf9-129">Step 2: Creating a Managed-Code UDF</span><span class="sxs-lookup"><span data-stu-id="3bdf9-129">Step 2: Creating a Managed-Code UDF</span></span>](step-2-creating-a-managed-code-udf.md)
- [<span data-ttu-id="3bdf9-130">Step 3: Deploying and Enabling UDFs</span><span class="sxs-lookup"><span data-stu-id="3bdf9-130">Step 3: Deploying and Enabling UDFs</span></span>](step-3-deploying-and-enabling-udfs.md)
- [<span data-ttu-id="3bdf9-131">Step 4: Testing and Calling UDFs from Cells</span><span class="sxs-lookup"><span data-stu-id="3bdf9-131">Step 4: Testing and Calling UDFs from Cells</span></span>](step-4-testing-and-calling-udfs-from-cells.md)
- [<span data-ttu-id="3bdf9-132">How to: Create a UDF That Calls a Web Service</span><span class="sxs-lookup"><span data-stu-id="3bdf9-132">How to: Create a UDF That Calls a Web Service</span></span>](how-to-create-a-udf-that-calls-a-web-service.md)
- [<span data-ttu-id="3bdf9-133">Walkthrough: Developing a Managed-Code UDF</span><span class="sxs-lookup"><span data-stu-id="3bdf9-133">Walkthrough: Developing a Managed-Code UDF</span></span>](walkthrough-developing-a-managed-code-udf.md)
- [<span data-ttu-id="3bdf9-134">Understanding Excel Services UDFs</span><span class="sxs-lookup"><span data-stu-id="3bdf9-134">Understanding Excel Services UDFs</span></span>](understanding-excel-services-udfs.md)
