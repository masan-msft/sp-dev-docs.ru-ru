---
title: "Создание преобразований системы показателей для служб PerformancePoint Services в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: cdcb54a17b5575524acfaa5400234401f150eaa1
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="create-scorecard-transforms-for-performancepoint-services-in-sharepoint"></a><span data-ttu-id="3c5f0-102">Создание преобразований системы показателей для служб PerformancePoint Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3c5f0-102">Create scorecard transforms for PerformancePoint Services in SharePoint</span></span>

<span data-ttu-id="3c5f0-103">Узнайте, как создать пользовательские преобразования системы показателей для служб PerformancePoint Services в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3c5f0-103">Learn how to create custom scorecard transforms for PerformancePoint Services in SharePoint.</span></span>

## <a name="what-are-scorecard-transforms-in-performancepoint-services"></a><span data-ttu-id="3c5f0-104">Что такое системы показателей преобразований в Службы PerformancePoint Services ?</span><span class="sxs-lookup"><span data-stu-id="3c5f0-104">What are scorecard transforms in PerformancePoint Services?</span></span>
<span data-ttu-id="3c5f0-105"><a name="bk_intro"> </a></span><span class="sxs-lookup"><span data-stu-id="3c5f0-105"><a name="bk_intro"> </a></span></span>

<span data-ttu-id="3c5f0-p101">В Службы PerformancePoint Services преобразований системы показателей изменение внешнего вида, содержимого или функций представлений систем показателей перед их отображением в панели мониторинга. Для получения дополнительных сведений см  [Обзор преобразований систем показателей PerformancePoint Services](http://msdn.microsoft.com/library/d69d171b-827a-48a8-a3e1-7aaf0bfbc7f8%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="3c5f0-p101">In PerformancePoint Services, scorecard transforms change the appearance, content, or functionality of scorecard views before they render in a dashboard. For more information, see  [Types of Transforms](http://msdn.microsoft.com/library/d69d171b-827a-48a8-a3e1-7aaf0bfbc7f8%28Office.15%29.aspx).</span></span>
  
    
    

## <a name="create-transforms-for-performancepoint-services-scorecards"></a><span data-ttu-id="3c5f0-108">Создание преобразований для Службы PerformancePoint Services систем показателей</span><span class="sxs-lookup"><span data-stu-id="3c5f0-108">Create transforms for PerformancePoint Services scorecards</span></span>
<span data-ttu-id="3c5f0-109"><a name="BKMK_CreateClass"> </a></span><span class="sxs-lookup"><span data-stu-id="3c5f0-109"><a name="BKMK_CreateClass"> </a></span></span>


1. <span data-ttu-id="3c5f0-p102">Установка Службы PerformancePoint Services или копирование библиотеки DLL, которые устанавливаются вместе с Службы PerformancePoint Services на своем компьютере. Для получения дополнительных сведений см  [Библиотеки DLL служб PerformancePoint, используемые в сценариях развертывания](http://msdn.microsoft.com/library/41e92619-8253-481d-82f9-35b6a6abc477%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="3c5f0-p102">Install PerformancePoint Services, or copy the DLLs that are installed with PerformancePoint Services to your computer. For more information, see  [DLLs with Class Libraries](http://msdn.microsoft.com/library/41e92619-8253-481d-82f9-35b6a6abc477%28Office.15%29.aspx).</span></span>
    
  
2. <span data-ttu-id="3c5f0-p103">В Visual Studio создайте библиотеку классов C#. Если библиотека классов для расширения уже создана, добавьте новый класс C#.</span><span class="sxs-lookup"><span data-stu-id="3c5f0-p103">In Visual Studio, create a C# class library. If you have already created a class library for your extension, add a new C# class.</span></span>
    
    <span data-ttu-id="3c5f0-p104">Необходимо подписать библиотеки DLL со строгим именем и убедитесь, что все сборки библиотеки DLL имеют строгих имен. Чтобы узнать, как подписать сборку со строгим именем и способы создания пары открытого и закрытого ключей, обратитесь к разделу  [How to: Create a Public/Private Key Pair](http://msdn.microsoft.com/library/05026813-f3bd-4d7c-9e0b-fc588eb3d114.aspx).</span><span class="sxs-lookup"><span data-stu-id="3c5f0-p104">You must sign your DLL with a strong name, and ensure that all assemblies referenced by your DLL have strong names. To learn how to sign an assembly with a strong name and how to create a public/private key pair, see  [How to: Create a Public/Private Key Pair](http://msdn.microsoft.com/library/05026813-f3bd-4d7c-9e0b-fc588eb3d114.aspx).</span></span>
    
  
3. <span data-ttu-id="3c5f0-116">Добавьте файл Microsoft.PerformancePoint.Scorecards.Client.dll как ссылку на сборку в проект.</span><span class="sxs-lookup"><span data-stu-id="3c5f0-116">Add Microsoft.PerformancePoint.Scorecards.Client.dll as an assembly reference to the project.</span></span>
    
  
4. <span data-ttu-id="3c5f0-117">Добавьте директивы **using** для следующих пространств имен:</span><span class="sxs-lookup"><span data-stu-id="3c5f0-117">Add **using** directives for the following namespaces:</span></span>
    
  - <span data-ttu-id="3c5f0-118">**Microsoft.PerformancePoint.Scorecards**</span><span class="sxs-lookup"><span data-stu-id="3c5f0-118">**Microsoft.PerformancePoint.Scorecards**</span></span>
    
  
  - <span data-ttu-id="3c5f0-119">**Microsoft.PerformancePoint.Scorecards.Extensions**</span><span class="sxs-lookup"><span data-stu-id="3c5f0-119">**Microsoft.PerformancePoint.Scorecards.Extensions**</span></span>
    
  
  - <span data-ttu-id="3c5f0-120">**System.Collections.Generic**</span><span class="sxs-lookup"><span data-stu-id="3c5f0-120">**System.Collections.Generic**</span></span>
    
  
5. <span data-ttu-id="3c5f0-121">Реализуйте интерфейс  [IGridViewTransform](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.IGridViewTransform.aspx) .</span><span class="sxs-lookup"><span data-stu-id="3c5f0-121">Implement the  [IGridViewTransform](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.IGridViewTransform.aspx) interface.</span></span>
    
  
6. <span data-ttu-id="3c5f0-p105">Переопределите метод  [GetId](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.IGridViewTransform.GetId.aspx) возвращает идентификатор строки для вашей преобразования. [GetId](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.IGridViewTransform.GetId.aspx) должен возвращать ту же строку в качестве атрибута **key**, который зарегистрирован для преобразования в файле web.config Службы PerformancePoint Services. Дополнительные сведения о регистрации преобразования системы показателей можно [Регистрация расширений служб PerformancePoint вручную](http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="3c5f0-p105">Override the  [GetId](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.IGridViewTransform.GetId.aspx) method to return the string identifier for your transform. [GetId](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.IGridViewTransform.GetId.aspx) must return the same string as the **key** attribute that is registered for the transform in the PerformancePoint Services web.config file. For more information about registering scorecard transforms, see [How to: Manually Register PerformancePoint Services Extensions](http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx).</span></span>
    
  
7. <span data-ttu-id="3c5f0-p106">Переопределите метод  [GetTransformType](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.IGridViewTransform.GetTransformType.aspx) для указания времени запуска преобразования. Оно зависит от его типа, определенного перечислением [GridViewTransformType](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.GridViewTransformType.aspx) : **PreQuery**, **PostQuery** или **PreRender**. Дополнительные сведения см. в стать  [Обзор преобразований систем показателей PerformancePoint Services](http://msdn.microsoft.com/library/d69d171b-827a-48a8-a3e1-7aaf0bfbc7f8%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="3c5f0-p106">Override the  [GetTransformType](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.IGridViewTransform.GetTransformType.aspx) method to specify when to run the transform. The point at which a transform runs depends on its type, as defined by the [GridViewTransformType](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.GridViewTransformType.aspx) enumeration: **PreQuery**, **PostQuery**, or **PreRender**. For more information, see  [Types of Transforms](http://msdn.microsoft.com/library/d69d171b-827a-48a8-a3e1-7aaf0bfbc7f8%28Office.15%29.aspx).</span></span>
    
  
8. <span data-ttu-id="3c5f0-p107">Переопределите метод  [Execute](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.IGridViewTransform.Execute.aspx) , чтобы определить, как преобразовать систему показателей. В следующих примерах кода показано добавление столбца в представление системы показателей и изменение форматирования пустых ячеек системы показателей.</span><span class="sxs-lookup"><span data-stu-id="3c5f0-p107">Override the  [Execute](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.IGridViewTransform.Execute.aspx) method to define how to transform the scorecard. The following code examples show how to add a column to a scorecard view and how to change the formatting of empty scorecard cells.</span></span>
    
  
<span data-ttu-id="3c5f0-130">После регистрации и построения библиотеки DLL установите расширение, как описано в статье  [Регистрация расширений служб PerformancePoint вручную](http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="3c5f0-130">After you sign and build your DLL, install the extension as described in  [How to: Manually Register PerformancePoint Services Extensions](http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx).</span></span>
## <a name="code-example-1-add-a-column-to-performancepoint-services-scorecards"></a><span data-ttu-id="3c5f0-131">Пример кода 1: Добавление столбца к Службы PerformancePoint Services систем показателей</span><span class="sxs-lookup"><span data-stu-id="3c5f0-131">Code example 1: Add a column to PerformancePoint Services scorecards</span></span>
<span data-ttu-id="3c5f0-132"><a name="bk_example1"> </a></span><span class="sxs-lookup"><span data-stu-id="3c5f0-132"><a name="bk_example1"> </a></span></span>

<span data-ttu-id="3c5f0-p108">В следующем примере кода создается **PreQuery** преобразования, которое добавляет столбец представления отображаемой системы показателей, содержащих ключевых индикаторов Производительности на уровне. (Если представления системы показателей включает элементам, расположенным ключевых показателей эффективности, столбец не добавлена.)</span><span class="sxs-lookup"><span data-stu-id="3c5f0-p108">The following code example creates a **PreQuery** transform that adds a column to rendered scorecard views that contain a KPI at the column leaf level. (If the scorecard view includes members below the KPIs, the column is not added.)</span></span>
  
    
    
<span data-ttu-id="3c5f0-135">Перед компиляцией этого примера кода необходимо настроить среду разработки, как описано в разделе  [Создание преобразований для Службы PerformancePoint Services систем показателей](#BKMK_CreateClass).</span><span class="sxs-lookup"><span data-stu-id="3c5f0-135">Before you can compile this code example, you must configure your development environment as described in  [Create transforms for PerformancePoint Services scorecards](#BKMK_CreateClass).</span></span>
  
    
    



```cs

using System;
using System.Collections.Generic;
using Microsoft.PerformancePoint.Scorecards;
using Microsoft.PerformancePoint.Scorecards.Extensions;

namespace Microsoft.PerformancePoint.SDK.Samples.ScorecardTransforms.PreQuery
{

    // Represents the class that adds columns of data to a scorecard view. 
    public class AddColumnTransform : IGridViewTransform
    {

        // Set transform type to PreQuery.
        public GridViewTransformType GetTransformType()
        {
            return GridViewTransformType.PreQuery;
        }

        // Return the string identifier of your transform. This value must
        // match the key attribute registered in the web.config file.
        public string GetId()
        {
            return "AddColumn";
        }

        // Run the transform to add a column. 
        public void Execute(GridViewData viewData, PropertyBag parameters, IGlobalCache cache)
        {
            // Verify the scorecard definition.
            if (viewData == null)
            {
                throw new ArgumentException("Parameter cannot be null", "viewData");
            }
                     
            List<GridHeaderItem> leafRowHeaders = viewData.RootRowHeader.GetAllLeafHeadersInTree();

            foreach (GridHeaderItem rowHeader in leafRowHeaders)
            {
                if (rowHeader.HeaderType == ScorecardNodeTypes.Kpi)
                {
                    Kpi kpi = cache.GetKpi(rowHeader.LinkedKpiLocation);
                    if (kpi != null &amp;&amp; viewData.RootColumnHeader != null)
                    {

                        // Create the column header and add it to the root.
                        GridHeaderItem theNewColumn = GridHeaderItem.CreateDetailsHeader(kpi.Owner.DisplayName);

                        // Set the GUIDs for the data headers.
                        // Setting the DefinitionGuid property to the
                        // same value as the root column header enables
                        // Dashboard Designer to display the scorecard. 
                        // Note: Do not try to modify or delete the new
                        // column from within Dashboard Designer.
                        theNewColumn.DefinitionGuid = viewData.RootColumnHeader.DefinitionGuid;
                        theNewColumn.Parent = viewData.RootColumnHeader;
                        theNewColumn.Guid = new Guid();

                        // Insert the column at the end of the collection
                        // of child elements.
                        if (viewData.RootColumnHeader.Children.Count != 0)
                        {
                            viewData.RootColumnHeader.Children.Insert(viewData.RootColumnHeader.Children.Count, theNewColumn);
                        }
                                                                         
                        break;
                    }
                }
            }
            viewData.RootColumnHeader.LinkAndIndexTreeFromRoot();
        }
    }
}
```


## <a name="code-example-2-change-the-format-of-empty-cells-in-performancepoint-services-scorecards"></a><span data-ttu-id="3c5f0-136">Код в примере 2: изменение формата пустые ячейки в системах показателей Службы PerformancePoint Services</span><span class="sxs-lookup"><span data-stu-id="3c5f0-136">Code example 2: Change the format of empty cells in PerformancePoint Services scorecards</span></span>
<span data-ttu-id="3c5f0-137"><a name="bk_example2"> </a></span><span class="sxs-lookup"><span data-stu-id="3c5f0-137"><a name="bk_example2"> </a></span></span>

<span data-ttu-id="3c5f0-138">Следующий пример кода создает преобразование **PreQuery**, которое применяет к пустым ячейкам системы показателей серый цвет фона.</span><span class="sxs-lookup"><span data-stu-id="3c5f0-138">The following code example creates a **PreQuery** transform that applies a grey background color to empty scorecard cells.</span></span>
  
> [!NOTE]
> <span data-ttu-id="3c5f0-p109">[!Примечание] Перед компиляцией этого примера кода необходимо настроить среду разработки, как описано в разделе  [Создание преобразований для Службы PerformancePoint Services систем показателей](#BKMK_CreateClass). Кроме того необходимо добавить ссылку на сборку **System.Drawing** в проект.</span><span class="sxs-lookup"><span data-stu-id="3c5f0-p109">Before you can compile this code example, you must configure your development environment as described in  [Create transforms for PerformancePoint Services scorecards](#BKMK_CreateClass). In addition, you must add a reference to the **System.Drawing** assembly to your project.</span></span>
  
    
    


```cs

using System;
using System.Collections.Generic;
using Microsoft.PerformancePoint.Scorecards;
using Microsoft.PerformancePoint.Scorecards.Extensions;

namespace Microsoft.PerformancePoint.SDK.Samples
{

    // Represents a transform that applies a grey background color to empty scorecard cells.
    public class GreyEmptiesTransform : IGridViewTransform
    {

        // Set the transform type to "PreRender".
        public GridViewTransformType GetTransformType()
        {
            return GridViewTransformType.PreRender;
        }

        // Return the string identifier of the transform.
        public string GetId()
        {
            return "GreyEmptyCells";
        }

        // Run the transform.
        public void Execute(GridViewData viewData, PropertyBag parameters, IGlobalCache cache)
        {
            // Validate parameters. 
            if (viewData == null)
            {
                throw new ArgumentException("Parameter cannot be null", "viewData");
            }

            // Get the headers under the root row header.
            List<GridHeaderItem> nonLeafRowHeaders = viewData.RootRowHeader.GetAllHeadersInTree();

            // Get the leaf headers under the root column header.
            List<GridHeaderItem> leafColumnHeaders = viewData.RootColumnHeader.GetAllLeafHeadersInTree();

            foreach (GridHeaderItem rowHeader in nonLeafRowHeaders)
            {
                foreach (GridHeaderItem columnHeader in leafColumnHeaders)
                {
                    // Get scorecard cells.
                    GridCell cell = viewData.Cells[rowHeader, columnHeader];

                    if (cell.IsCellEmpty || string.IsNullOrEmpty(cell.ActualValue.ToString()))
                    {
                        GridFormatInfo emptyFormat = new GridFormatInfo(viewData.DefaultCellFormatInfo);
                        emptyFormat.BackColor = new GridColor(System.Drawing.Color.Gray);
                        cell.FormatInfo = emptyFormat;
                    }
                    viewData.Cells[rowHeader, columnHeader] = cell;
                }
            }
        }
    }
}


```


## <a name="see-also"></a><span data-ttu-id="3c5f0-141">См. также</span><span class="sxs-lookup"><span data-stu-id="3c5f0-141">See also</span></span>
<span data-ttu-id="3c5f0-142"><a name="bk_addResources"> </a></span><span class="sxs-lookup"><span data-stu-id="3c5f0-142"><a name="bk_addResources"> </a></span></span>


-  [<span data-ttu-id="3c5f0-143">PerformancePoint Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3c5f0-143">PerformancePoint Services in SharePoint</span></span>](https://dev.office.com/sharepoint/docs/general-development/performancepoint-services-in-sharepoint)
    
  
-  [<span data-ttu-id="3c5f0-144">Системы показателей служб PerformancePoint</span><span class="sxs-lookup"><span data-stu-id="3c5f0-144">PerformancePoint Services Scorecards</span></span>](http://msdn.microsoft.com/library/e77eccdb-82b3-483a-bb91-dfdc716400dd%28Office.15%29.aspx)
    
  

