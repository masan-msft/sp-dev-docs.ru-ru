---
title: "Создание преобразований системы показателей для служб PerformancePoint Services в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: e19f99c6bceffe5551d2d2f3c2c5e918e78acbb4
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="create-scorecard-transforms-for-performancepoint-services-in-sharepoint"></a>Создание преобразований системы показателей для служб PerformancePoint Services в SharePoint

Узнайте, как создать пользовательские преобразования системы показателей для служб PerformancePoint Services в SharePoint.

## <a name="what-are-scorecard-transforms-in-performancepoint-services"></a>Что такое системы показателей преобразований в Службы PerformancePoint Services ?
<a name="bk_intro"> </a>

В Службы PerformancePoint Services преобразований системы показателей изменение внешнего вида, содержимого или функций представлений систем показателей перед их отображением в панели мониторинга. Для получения дополнительных сведений см  [Обзор преобразований систем показателей PerformancePoint Services](http://msdn.microsoft.com/library/d69d171b-827a-48a8-a3e1-7aaf0bfbc7f8%28Office.15%29.aspx).
  
    
    

## <a name="create-transforms-for-performancepoint-services-scorecards"></a>Создание преобразований для Службы PerformancePoint Services систем показателей
<a name="BKMK_CreateClass"> </a>


1. Установка Службы PerformancePoint Services или копирование библиотеки DLL, которые устанавливаются вместе с Службы PerformancePoint Services на своем компьютере. Для получения дополнительных сведений см  [Библиотеки DLL служб PerformancePoint, используемые в сценариях развертывания](http://msdn.microsoft.com/library/41e92619-8253-481d-82f9-35b6a6abc477%28Office.15%29.aspx).
    
  
2. В Visual Studio создайте библиотеку классов C#. Если библиотека классов для расширения уже создана, добавьте новый класс C#.
    
    Необходимо подписать библиотеки DLL со строгим именем и убедитесь, что все сборки библиотеки DLL имеют строгих имен. Чтобы узнать, как подписать сборку со строгим именем и способы создания пары открытого и закрытого ключей, обратитесь к разделу  [How to: Create a Public/Private Key Pair](http://msdn.microsoft.com/library/05026813-f3bd-4d7c-9e0b-fc588eb3d114.aspx).
    
  
3. Добавьте файл Microsoft.PerformancePoint.Scorecards.Client.dll как ссылку на сборку в проект.
    
  
4. Добавьте директивы **using** для следующих пространств имен:
    
  - **Microsoft.PerformancePoint.Scorecards**
    
  
  - **Microsoft.PerformancePoint.Scorecards.Extensions**
    
  
  - **System.Collections.Generic**
    
  
5. Реализуйте интерфейс  [IGridViewTransform](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.IGridViewTransform.aspx) .
    
  
6. Переопределите метод  [GetId](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.IGridViewTransform.GetId.aspx) возвращает идентификатор строки для вашей преобразования. [GetId](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.IGridViewTransform.GetId.aspx) должен возвращать ту же строку в качестве атрибута **key**, который зарегистрирован для преобразования в файле web.config Службы PerformancePoint Services. Дополнительные сведения о регистрации преобразования системы показателей можно [Регистрация расширений служб PerformancePoint вручную](http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx).
    
  
7. Переопределите метод  [GetTransformType](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.IGridViewTransform.GetTransformType.aspx) для указания времени запуска преобразования. Оно зависит от его типа, определенного перечислением [GridViewTransformType](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.GridViewTransformType.aspx) : **PreQuery**, **PostQuery** или **PreRender**. Дополнительные сведения см. в стать  [Обзор преобразований систем показателей PerformancePoint Services](http://msdn.microsoft.com/library/d69d171b-827a-48a8-a3e1-7aaf0bfbc7f8%28Office.15%29.aspx).
    
  
8. Переопределите метод  [Execute](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.IGridViewTransform.Execute.aspx) , чтобы определить, как преобразовать систему показателей. В следующих примерах кода показано добавление столбца в представление системы показателей и изменение форматирования пустых ячеек системы показателей.
    
  
После регистрации и построения библиотеки DLL установите расширение, как описано в статье  [Регистрация расширений служб PerformancePoint вручную](http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx).
## <a name="code-example-1-add-a-column-to-performancepoint-services-scorecards"></a>Пример кода 1: Добавление столбца к Службы PerformancePoint Services систем показателей
<a name="bk_example1"> </a>

В следующем примере кода создается **PreQuery** преобразования, которое добавляет столбец представления отображаемой системы показателей, содержащих ключевых индикаторов Производительности на уровне. (Если представления системы показателей включает элементам, расположенным ключевых показателей эффективности, столбец не добавлена.)
  
    
    
Перед компиляцией этого примера кода необходимо настроить среду разработки, как описано в разделе  [Создание преобразований для Службы PerformancePoint Services систем показателей](#BKMK_CreateClass).
  
    
    



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


## <a name="code-example-2-change-the-format-of-empty-cells-in-performancepoint-services-scorecards"></a>Код в примере 2: изменение формата пустые ячейки в системах показателей Службы PerformancePoint Services
<a name="bk_example2"> </a>

Следующий пример кода создает преобразование **PreQuery**, которое применяет к пустым ячейкам системы показателей серый цвет фона.
  
    
    

> **Примечание:** Перед компиляцией этого примера кода необходимо настроить среду разработки, как описано в [Создание преобразований для систем показателей PerformancePoint Services](#BKMK_CreateClass). Кроме того необходимо добавить ссылку на сборку **System.Drawing** в проект.
  
    
    


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


## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addResources"> </a>


-  [PerformancePoint Services в SharePoint](https://dev.office.com/sharepoint/docs/general-development/performancepoint-services-in-sharepoint)
    
  
-  [Системы показателей служб PerformancePoint](http://msdn.microsoft.com/library/e77eccdb-82b3-483a-bb91-dfdc716400dd%28Office.15%29.aspx)
    
  

