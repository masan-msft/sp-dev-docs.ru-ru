---
title: "Создание средств отображения отчетов для PerformancePoint Services в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 14533254c82bcca8e5aaa53c7b37c54824106842
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="create-report-renderers-for-performancepoint-services-in-sharepoint"></a><span data-ttu-id="63278-102">Создание средств отображения отчетов для PerformancePoint Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="63278-102">Create report renderers for PerformancePoint Services in SharePoint</span></span>

<span data-ttu-id="63278-103">Узнайте, как создать компонент модуля подготовки в модуле пользовательских отчетов для Службы PerformancePoint Services.</span><span class="sxs-lookup"><span data-stu-id="63278-103">Learn how to create the renderer component in a custom report extension for PerformancePoint Services.</span></span>

## <a name="what-are-custom-report-renderers-for-performancepoint-services"></a><span data-ttu-id="63278-104">Что такое средств отображения настраиваемых отчетов для Службы PerformancePoint Services ?</span><span class="sxs-lookup"><span data-stu-id="63278-104">What are custom report renderers for PerformancePoint Services?</span></span>
<span data-ttu-id="63278-105"><a name="bk_intro"> </a></span><span class="sxs-lookup"><span data-stu-id="63278-105"></span></span>

<span data-ttu-id="63278-p101">В Службы PerformancePoint Services средств отображения настраиваемых отчетов, элемент управления, которые отображают настраиваемого отчета в веб-части. Обработчик записывает HTML-код для визуализации отчета (например, диаграммы или таблицы), предоставляет логику для обработки параметров отчетов и возвращает объект отчета из репозитория.</span><span class="sxs-lookup"><span data-stu-id="63278-p101">In PerformancePoint Services, custom report renderers are web server controls that render a custom report in a Web Part. A renderer writes the HTML for the report visualization (such as a table or chart), provides logic to handle report parameters, and retrieves the report object from the repository.</span></span>
  
    
    
<span data-ttu-id="63278-108">Следующие процедуры и примеры кода, зависят от класса **SampleReportRenderer** из [настраиваемых объектов](http://msdn.microsoft.com/library/af021d52-7562-4e7a-9de4-e1fc5784a59d%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="63278-108">The following procedures and code examples are based on the **SampleReportRenderer** class from the [custom objects sample](http://msdn.microsoft.com/library/af021d52-7562-4e7a-9de4-e1fc5784a59d%28Office.15%29.aspx).</span></span> <span data-ttu-id="63278-109">Средство визуализации отображает таблицу и заполняется значения, полученные из связанного фильтра.</span><span class="sxs-lookup"><span data-stu-id="63278-109">The renderer renders a table and populates it with values received from a linked filter.</span></span> <span data-ttu-id="63278-110">Полный код для класса, в разделе [пример кода: Создание модуля подготовки для настраиваемых отчетов служб PerformancePoint Services в SharePoint](#bk_example).</span><span class="sxs-lookup"><span data-stu-id="63278-110">For the complete code for the class, see  [Code example: Create a renderer for custom PerformancePoint Services reports in SharePoint](#bk_example).</span></span>
  
    
    
<span data-ttu-id="63278-p103">Мы рекомендуем использовать модуль подготовки отчетов образец как шаблон. В примере показано, как вызывать объекты в Службы PerformancePoint Services API и демонстрируется советы и рекомендации по разработке Службы PerformancePoint Services.</span><span class="sxs-lookup"><span data-stu-id="63278-p103">We recommend that you use the sample report renderer as a template. The sample shows how to call objects in the PerformancePoint Services API and demonstrates best practices for PerformancePoint Services development.</span></span>
  
    
    

## <a name="create-renderers-for-custom-performancepoint-services-reports"></a><span data-ttu-id="63278-113">Создание средств отображения для настраиваемых Службы PerformancePoint Services отчетов</span><span class="sxs-lookup"><span data-stu-id="63278-113">Create renderers for custom PerformancePoint Services reports</span></span>
<span data-ttu-id="63278-114"><a name="BKMK_ConfigRenderer"> </a></span><span class="sxs-lookup"><span data-stu-id="63278-114"></span></span>


  
    
    

1. <span data-ttu-id="63278-p104">Установка Службы PerformancePoint Services или копирование библиотеки DLL, которые использует расширения (перечисленных в шаге 3) на своем компьютере. Для получения дополнительных сведений см  [Библиотеки DLL служб PerformancePoint, используемые в сценариях развертывания](http://msdn.microsoft.com/library/41e92619-8253-481d-82f9-35b6a6abc477%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="63278-p104">Install PerformancePoint Services, or copy the DLLs that your extension uses (listed in step 3) to your computer. For more information, see  [DLLs with Class Libraries](http://msdn.microsoft.com/library/41e92619-8253-481d-82f9-35b6a6abc477%28Office.15%29.aspx).</span></span> 
    
  
2. <span data-ttu-id="63278-p105">В Visual Studio создайте библиотеку классов C#. Если библиотека классов для расширения уже создана, добавьте новый класс C#.</span><span class="sxs-lookup"><span data-stu-id="63278-p105">In Visual Studio, create a C# class library. If you have already created a class library for your extension, add a new C# class.</span></span>
    
    <span data-ttu-id="63278-p106">DLL-библиотеку необходимо подписать строгим именем. Кроме того, убедитесь, что все сборки, на которые ссылается DLL-библиотека, имеют строгие имена. Процедура подписывания сборки строгим именем и создания пары из открытого и закрытого ключа рассматривается в разделе  [How to: Create a Public/Private Key Pair](http://msdn.microsoft.com/library/05026813-f3bd-4d7c-9e0b-fc588eb3d114.aspx).</span><span class="sxs-lookup"><span data-stu-id="63278-p106">You must sign your DLL with a strong name. In addition, ensure that all assemblies referenced by your DLL have strong names. For information about how to sign an assembly with a strong name and how to create a public/private key pair, see  [How to: Create a Public/Private Key Pair](http://msdn.microsoft.com/library/05026813-f3bd-4d7c-9e0b-fc588eb3d114.aspx).</span></span>
    
  
3. <span data-ttu-id="63278-122">Добавьте следующие Службы PerformancePoint Services библиотеки DLL в качестве ссылок на сборки в проект:</span><span class="sxs-lookup"><span data-stu-id="63278-122">Add the following PerformancePoint Services DLLs as assembly references to the project:</span></span>
    
  - <span data-ttu-id="63278-123">Файл Microsoft.PerformancePoint.Scorecards.Client.dll</span><span class="sxs-lookup"><span data-stu-id="63278-123">Microsoft.PerformancePoint.Scorecards.Client.dll</span></span>
    
  
  - <span data-ttu-id="63278-124">Microsoft.PerformancePoint.Scorecards.Server.dll</span><span class="sxs-lookup"><span data-stu-id="63278-124">Microsoft.PerformancePoint.Scorecards.Server.dll</span></span>
    
  
  - <span data-ttu-id="63278-125">Microsoft.PerformancePoint.Scorecards.Store.dll</span><span class="sxs-lookup"><span data-stu-id="63278-125">Microsoft.PerformancePoint.Scorecards.Store.dll</span></span>
    
  

    <span data-ttu-id="63278-126">В зависимости от функциональности расширения могут потребоваться другие ссылки в проекте.</span><span class="sxs-lookup"><span data-stu-id="63278-126">Depending on your extension's functionality, other project references may be required.</span></span>
    
  
4. <span data-ttu-id="63278-127">В классе визуализации добавьте директивы **using** для следующих пространств имен Службы PerformancePoint Services.</span><span class="sxs-lookup"><span data-stu-id="63278-127">In your renderer class, add **using** directives for the following PerformancePoint Services namespaces:</span></span>
    
  -  [<span data-ttu-id="63278-128">Microsoft.PerformancePoint.Scorecards</span><span class="sxs-lookup"><span data-stu-id="63278-128">Microsoft.PerformancePoint.Scorecards</span></span>](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.aspx)
    
  
  -  [<span data-ttu-id="63278-129">Microsoft.PerformancePoint.Scorecards.Server.Extensions</span><span class="sxs-lookup"><span data-stu-id="63278-129">Microsoft.PerformancePoint.Scorecards.Server.Extensions</span></span>](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.aspx)
    
  
  -  [<span data-ttu-id="63278-130">Microsoft.PerformancePoint.Scorecards.Store</span><span class="sxs-lookup"><span data-stu-id="63278-130">Microsoft.PerformancePoint.Scorecards.Store</span></span>](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Store.aspx)
    
  

    <span data-ttu-id="63278-131">В зависимости от функциональности расширения могут потребоваться другие директивы **using**.</span><span class="sxs-lookup"><span data-stu-id="63278-131">Depending on your extension's functionality, other **using** directives may be required.</span></span>
    
  
5. <span data-ttu-id="63278-132">Наследуйте содержимое базового класса  [ParameterizableControl](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.ParameterizableControl.aspx) .</span><span class="sxs-lookup"><span data-stu-id="63278-132">Inherit from the  [ParameterizableControl](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.ParameterizableControl.aspx) base class.</span></span>
    
  
6. <span data-ttu-id="63278-133">Переопределите метод  [GetElement](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.ParameterizableControl.GetElement.aspx) , чтобы извлечь объект отчета из репозитория.</span><span class="sxs-lookup"><span data-stu-id="63278-133">Override the  [GetElement](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.ParameterizableControl.GetElement.aspx) method to retrieve the report object from the repository.</span></span>
    
  
7. <span data-ttu-id="63278-134">Переопределите метод  [SetData](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.ParameterizableControl.SetData.aspx) , чтобы настроить набор данных отчета и извлечь входящие значения параметров.</span><span class="sxs-lookup"><span data-stu-id="63278-134">Override the  [SetData](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.ParameterizableControl.SetData.aspx) method to set up the report dataset and retrieve incoming parameter values.</span></span>
    
  
8. <span data-ttu-id="63278-135">Переопределите метод  [Render](https://msdn.microsoft.com/library/System.Web.UI.WebControls.WebControl.Render.aspx) , чтобы отобразить HTML-код для визуализации отчета.</span><span class="sxs-lookup"><span data-stu-id="63278-135">Override the  [Render](https://msdn.microsoft.com/library/System.Web.UI.WebControls.WebControl.Render.aspx) method to render the HTML for the report visualization.</span></span>
    
  

## <a name="code-example-create-a-renderer-for-custom-performancepoint-services-reports-in-sharepoint"></a><span data-ttu-id="63278-136">Пример кода: Создание модуля подготовки для настраиваемых отчетов служб PerformancePoint Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="63278-136">Code example: Create a renderer for custom PerformancePoint Services reports in SharePoint</span></span>
<span data-ttu-id="63278-137"><a name="bk_example"> </a></span><span class="sxs-lookup"><span data-stu-id="63278-137"></span></span>

<span data-ttu-id="63278-138">Класс, определяемый в следующем примере кода, создает модуль подготовки отчетов, который отображает данные о запасах, передаваемые через образец фильтра.</span><span class="sxs-lookup"><span data-stu-id="63278-138">The class in the following code example creates a report renderer that displays stock information passed in from the sample filter.</span></span>
  
    
    
<span data-ttu-id="63278-139">Перед компиляцией этого примера кода требуется настроить среду разработки, как описано в разделе  [Создание и настройка класса визуализации](#BKMK_ConfigRenderer).</span><span class="sxs-lookup"><span data-stu-id="63278-139">Before you can compile this code example, you must configure your development environment as described in  [To create and configure the renderer class](#BKMK_ConfigRenderer).</span></span>
  
    
    



```cs

using System;
using System.Collections.Generic;
using System.Data;
using System.Web.UI;
using Microsoft.PerformancePoint.Scorecards;
using Microsoft.PerformancePoint.Scorecards.Server.Extensions;
using Microsoft.PerformancePoint.Scorecards.Store;

namespace Microsoft.PerformancePoint.SDK.Samples.SampleReport
{

    // The class that define the sample report's renderer.
    public class SampleReportRenderer : ParameterizableControl 
    {
        private ReportView reportView;

        private ReportView ReportView
        {
            get
            {

                // The GetElement method is used internally by this property, which is used
                // in turn by the SetData method.
                reportView = GetElement(ElementLocation) as ReportView;
                return reportView;
            }
        }

        // Initializes the current instance according to a standard interface. This method
        // sets up the dataset.
        public override void SetData(RepositoryLocation elementLocation, string resourcePath, string targetControlId, BIDataContainer dataContainer, bool accessibilityMode)
        {

            // The renderer must call the base implementation of the SetData method
            // to set report properties.
            base.SetData(elementLocation, resourcePath, targetControlId, dataContainer, accessibilityMode);
        
            if (null != ReportView)
            {

                // If the report view's custom data represents a serialized object, deserialize
                // it, and then use it to access a data source or other object.
                string customData = ReportView.CustomData;
                if (!string.IsNullOrEmpty(customData))
                {
                    System.Diagnostics.Debug.WriteLine(string.Format("Report view '{0}' has the following custom data: {1}", ReportView.Name.Text, customData));
                }
                
                // Iterate through the user's selections sent by the filter. 
                // The MultiSelectTreeControl filter control can send multiple
                // rows of data but other native controls send one message only.
                foreach (ParameterMessage message in BIDataContainer.ParameterMessages)
                {
                    // This line demonstrates how to do something with each incoming parameter message.
                    System.Diagnostics.Debug.WriteLine(string.Format("Parameter message: {0}", message.DisplayName));
                }
            }
        }
        
        // Render page content using the specified writer.
        protected override void Render(HtmlTextWriter output)
        {
            try
            {
                if (null != ReportView &amp;&amp; !string.IsNullOrEmpty(ReportView.CustomData))
                {
                    output.RenderBeginTag(HtmlTextWriterTag.P);
                    output.RenderBeginTag(HtmlTextWriterTag.B);

                    // This line shows how to retrieve the content of the
                    // report's optional CustomData property. CustomData can store
                    // information that the report does not store elsewhere.
                    output.Write(string.Format("The ReportView &amp;quot;{0}&amp;quot; has CustomData information. The CustomData is &amp;quot;{1}&amp;quot;", 
                        ReportView.Name.Text, ReportView.CustomData));
                    output.RenderEndTag(); // B
                    output.RenderEndTag(); // P
                }

                Dictionary<Guid, ParameterMessage> parametersIndex =
                    IndexParameterMessages(BIDataContainer.ParameterMessages.ToArray());

                // Each connection gets a unique identifier.
                foreach (Guid parameterMappingId in parametersIndex.Keys)
                {
                    ParameterMessage message = parametersIndex[parameterMappingId];

                    output.RenderBeginTag(HtmlTextWriterTag.Table);
                    
                    output.AddAttribute(HtmlTextWriterAttribute.Style, "ms-partline");
                    output.RenderBeginTag(HtmlTextWriterTag.Tr);

                    output.AddAttribute(HtmlTextWriterAttribute.Colspan, "5");
                    output.RenderBeginTag(HtmlTextWriterTag.Td);
                    
                    output.RenderBeginTag(HtmlTextWriterTag.B);
                    output.Write(string.Format("EndPoint name is: {0}", message.Values.TableName));

                    output.RenderEndTag();  // B
                    output.RenderEndTag();  // Td
                    output.RenderEndTag();  // Tr

                    output.AddAttribute(HtmlTextWriterAttribute.Style, "\\"border-bottom:solid 10px #ffdd00; background:PapayaWhip\\"");
                    output.RenderBeginTag(HtmlTextWriterTag.Tr);

                    // Read the message.Values data table and print the column names.
                    foreach (DataColumn col in message.Values.Columns)
                    {
                        output.RenderBeginTag(HtmlTextWriterTag.Td);
                        output.Write(string.IsNullOrEmpty(col.Caption) ? "&amp;nbsp;" : col.Caption);
                        output.RenderEndTag();
                    }
                    output.RenderEndTag();  // Tr

                    // Print the data from the Values property, which is a data table.
                    foreach (DataRow row in message.Values.Rows)
                    {
                        output.RenderBeginTag(HtmlTextWriterTag.Tr);
                        for (int i = 0; i < message.Values.Columns.Count; i++)
                        {
                            output.RenderBeginTag(HtmlTextWriterTag.Td);
                            output.Write(string.IsNullOrEmpty(row[i].ToString()) ? "&amp;nbsp;" : row[i].ToString());
                            output.RenderEndTag();
                        }
                        output.RenderEndTag();  // Tr
                    }
                    output.RenderEndTag(); // table
                }
            }
            catch (Exception e)
            {
                output.RenderBeginTag(HtmlTextWriterTag.H1);
                output.Write("Error! An exception has occurred!");
                output.RenderEndTag();
                
                output.RenderBeginTag(HtmlTextWriterTag.P);
                output.Write(e.Message);
                output.RenderEndTag();

                output.RenderBeginTag(HtmlTextWriterTag.P); 
                output.Write(e.StackTrace);
                output.RenderEndTag();
            }
        }

        // Get the report object.
        protected override Element GetElement(RepositoryLocation elementLocation)
        {
            ReportView rv = null;
            if (!RepositoryLocation.IsNullOrEmpty(elementLocation))
            {
                rv = SPDataStore.GlobalDataStore.GetReportViewForExecution(elementLocation);
            }
            return (rv);
        }
    }
}
```


## <a name="next-steps"></a><span data-ttu-id="63278-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="63278-140">Next steps</span></span>
<span data-ttu-id="63278-141"><a name="bk_next"> </a></span><span class="sxs-lookup"><span data-stu-id="63278-141"></span></span>

<span data-ttu-id="63278-142">После создания модуля подготовки отчетов и редактор отчета (включая его пользовательский интерфейс, если это необходимо), развертывание данное расширение имени файла, как описано в  [Регистрация расширений служб PerformancePoint вручную](http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="63278-142">After you create a report renderer and a report editor (including its user interface, if required), deploy the extension as described in  [How to: Manually Register PerformancePoint Services Extensions](http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx).</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="63278-143">См. также</span><span class="sxs-lookup"><span data-stu-id="63278-143">See also</span></span>
<span data-ttu-id="63278-144"><a name="bk_addResources"> </a></span><span class="sxs-lookup"><span data-stu-id="63278-144"></span></span>


-  [<span data-ttu-id="63278-145">Как: создание средств отображения отчетов для PerformancePoint Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="63278-145">How to: Create report renderers for PerformancePoint Services in SharePoint</span></span>](how-to-create-report-renderers-for-performancepoint-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="63278-146">PerformancePoint Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="63278-146">PerformancePoint Services in SharePoint</span></span>](performancepoint-services-in-sharepoint.md)
    
  

