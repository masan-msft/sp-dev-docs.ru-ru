---
title: "Создание средств отображения отчетов для PerformancePoint Services в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: eeab12ad6c73463b15e9086b18cc054b501b71d5
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-create-report-renderers-for-performancepoint-services-in-sharepoint"></a>Как: создать средств отображения отчетов для PerformancePoint Services в SharePoint
Узнайте, как создать компонент модуля подготовки в модуле пользовательских отчетов для Службы PerformancePoint Services.
## <a name="what-are-custom-report-renderers-for-performancepoint-services"></a>Что такое средств отображения настраиваемых отчетов для Службы PerformancePoint Services ?
<a name="bk_intro"> </a>

В Службы PerformancePoint Services средств отображения настраиваемых отчетов, элемент управления, которые отображают настраиваемого отчета в веб-части. Обработчик записывает HTML-код для визуализации отчета (например, диаграммы или таблицы), предоставляет логику для обработки параметров отчетов и возвращает объект отчета из репозитория.
  
    
    
Следующие процедуры и примеры кода, зависят от класса **SampleReportRenderer** из [настраиваемых объектов](http://msdn.microsoft.com/library/af021d52-7562-4e7a-9de4-e1fc5784a59d%28Office.15%29.aspx). Средство визуализации отображает таблицу и заполняется значения, полученные из связанного фильтра. Полный код для класса, в разделе [пример кода: Создание модуля подготовки для настраиваемых отчетов служб PerformancePoint Services в SharePoint](#bk_example).
  
    
    
Мы рекомендуем использовать модуль подготовки отчетов образец как шаблон. В примере показано, как вызывать объекты в Службы PerformancePoint Services API и демонстрируется советы и рекомендации по разработке Службы PerformancePoint Services.
  
    
    

## <a name="create-renderers-for-custom-performancepoint-services-reports"></a>Создание средств отображения для настраиваемых Службы PerformancePoint Services отчетов
<a name="BKMK_ConfigRenderer"> </a>


  
    
    

1. Установка Службы PerformancePoint Services или копирование библиотеки DLL, которые использует расширения (перечисленных в шаге 3) на своем компьютере. Для получения дополнительных сведений см  [Библиотеки DLL служб PerformancePoint, используемые в сценариях развертывания](http://msdn.microsoft.com/library/41e92619-8253-481d-82f9-35b6a6abc477%28Office.15%29.aspx). 
    
  
2. В Visual Studio создайте библиотеку классов C#. Если библиотека классов для расширения уже создана, добавьте новый класс C#.
    
    DLL-библиотеку необходимо подписать строгим именем. Кроме того, убедитесь, что все сборки, на которые ссылается DLL-библиотека, имеют строгие имена. Процедура подписывания сборки строгим именем и создания пары из открытого и закрытого ключа рассматривается в разделе  [How to: Create a Public/Private Key Pair](http://msdn.microsoft.com/library/05026813-f3bd-4d7c-9e0b-fc588eb3d114.aspx).
    
  
3. Добавьте следующие Службы PerformancePoint Services библиотеки DLL в качестве ссылок на сборки в проект:
    
  - Файл Microsoft.PerformancePoint.Scorecards.Client.dll
    
  
  - Microsoft.PerformancePoint.Scorecards.Server.dll
    
  
  - Microsoft.PerformancePoint.Scorecards.Store.dll
    
  

    В зависимости от функциональности расширения могут потребоваться другие ссылки в проекте.
    
  
4. В классе визуализации добавьте директивы **using** для следующих пространств имен Службы PerformancePoint Services.
    
  -  [Microsoft.PerformancePoint.Scorecards](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.aspx)
    
  
  -  [Microsoft.PerformancePoint.Scorecards.Server.Extensions](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.aspx)
    
  
  -  [Microsoft.PerformancePoint.Scorecards.Store](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Store.aspx)
    
  

    В зависимости от функциональности расширения могут потребоваться другие директивы **using**.
    
  
5. Наследуйте содержимое базового класса  [ParameterizableControl](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.ParameterizableControl.aspx) .
    
  
6. Переопределите метод  [GetElement](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.ParameterizableControl.GetElement.aspx) , чтобы извлечь объект отчета из репозитория.
    
  
7. Переопределите метод  [SetData](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.ParameterizableControl.SetData.aspx) , чтобы настроить набор данных отчета и извлечь входящие значения параметров.
    
  
8. Переопределите метод  [Render](https://msdn.microsoft.com/library/System.Web.UI.WebControls.WebControl.Render.aspx) , чтобы отобразить HTML-код для визуализации отчета.
    
  

## <a name="code-example-create-a-renderer-for-custom-performancepoint-services-reports-in-sharepoint"></a>Пример кода: Создание модуля подготовки для настраиваемых отчетов служб PerformancePoint Services в SharePoint
<a name="bk_example"> </a>

Класс, определяемый в следующем примере кода, создает модуль подготовки отчетов, который отображает данные о запасах, передаваемые через образец фильтра.
  
    
    
Перед компиляцией этого примера кода требуется настроить среду разработки, как описано в разделе  [Создание и настройка класса визуализации](#BKMK_ConfigRenderer).
  
    
    



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


## <a name="next-steps"></a>Дальнейшие действия
<a name="bk_next"> </a>

После создания модуля подготовки отчетов и редактор отчета (включая его пользовательский интерфейс, если это необходимо), развертывание данное расширение имени файла, как описано в  [Регистрация расширений служб PerformancePoint вручную](http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx).
  
    
    

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addResources"> </a>


-  [Как: создание средств отображения отчетов для PerformancePoint Services в SharePoint](how-to-create-report-renderers-for-performancepoint-services-in-sharepoint.md)
    
  
-  [PerformancePoint Services в SharePoint](performancepoint-services-in-sharepoint.md)
    
  

