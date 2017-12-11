---
title: "Создание фильтра поставщиков данных для служб PerformancePoint Services в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 25508ec6-86bf-4eea-acf0-00f88e4faa55
ms.openlocfilehash: 8b1057a13b9ae052d86b6d507d8f6e6bc0ece9f7
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="create-filter-data-providers-for-performancepoint-services-in-sharepoint"></a>Создание фильтра поставщиков данных для служб PerformancePoint Services в SharePoint

Узнайте, как создать компонент поставщика данных в модуле пользовательских фильтров для Службы PerformancePoint Services.

## <a name="what-are-custom-data-providers-for-performancepoint-services"></a>Что такое настраиваемые поставщики данных для Службы PerformancePoint Services ?
<a name="bk_introduction"> </a>

В Службы PerformancePoint Services настраиваемые поставщики данных извлечения данных из источника данных в фильтре и определяют, как использовать данные. Важнее поставщики данных укажите значения данных для представления элемента управления фильтра и данных, которые можно использовать в качестве начальную точку фильтра. Поставщик данных также сохраняет значение, выбранной пользователем в элементе управления фильтра, который отправляется в фильтрации объекты-получатели. Поставщики данных используйте два объекта  [DataTable](https://msdn.microsoft.com/library/System.Data.DataTable.aspx) для организации и хранения данных. Для получения дополнительных сведений см [Фильтры служб PerformancePoint](http://msdn.microsoft.com/library/915382d0-3997-495c-a65a-7db3fe0b8f85%28Office.15%29.aspx).
  
    
    
Следующие процедуры и примеры, показывающие, как создать, настроить и определите поставщика данных фильтра основаны на класс **SampleFilterDataProvider** из [настраиваемых объектов](http://msdn.microsoft.com/library/af021d52-7562-4e7a-9de4-e1fc5784a59d%28Office.15%29.aspx). Редактор — тонкие веб-приложения, которое позволяет пользователям изменять имя и описание отчета. Полный код для класса, в разделе [пример кода: Создание поставщика данных для настраиваемых фильтров PerformancePoint Services в SharePoint](#bk_example).
  
    
    
Мы рекомендуем использовать примера поставщика данных в качестве шаблона. В примере показано, как вызывать объекты в Службы PerformancePoint Services API и демонстрируется советы и рекомендации по разработке Службы PerformancePoint Services. 
  
    
    

## <a name="create-data-providers-for-custom-performancepoint-services-filters"></a>Создание поставщика данных для настраиваемых Службы PerformancePoint Services фильтров
<a name="bk_createconfig"> </a>


1. Установка Службы PerformancePoint Services или копирование библиотеки DLL, которые использует расширения (перечисленных в шаге 3) на своем компьютере. Для получения дополнительных сведений см  [Библиотеки DLL служб PerformancePoint, используемые в сценариях развертывания](http://msdn.microsoft.com/library/41e92619-8253-481d-82f9-35b6a6abc477%28Office.15%29.aspx).
    
  
2. В Visual Studio создайте библиотеку классов C#. Если библиотека классов для расширения уже создана, добавьте новый класс C#.
    
    DLL-библиотеку необходимо подписать строгим именем. Кроме того, убедитесь, что все сборки, на которые ссылается DLL-библиотека, имеют строгие имена. Процедура подписывания сборки строгим именем и создания пары из открытого и закрытого ключа рассматривается в разделе  [How to: Create a Public/Private Key Pair](http://msdn.microsoft.com/library/05026813-f3bd-4d7c-9e0b-fc588eb3d114.aspx).
    
  
3. Добавьте следующие Службы PerformancePoint Services библиотеки DLL в качестве ссылок на сборки в проект:
    
  - Microsoft.PerformancePoint.Scorecards.Client.dll
    
  
  - Microsoft.PerformancePoint.Scorecards.Server.dll
    
  

    В зависимости от функциональности расширения могут потребоваться другие ссылки в проекте.
    
  
4. В классе поставщика добавьте директивы **using** для следующих пространств имен Службы PerformancePoint Services.
    
  -  [Microsoft.PerformancePoint.Scorecards](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.aspx)
    
  
  -  [Microsoft.PerformancePoint.Scorecards.Server.Extensions](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.aspx)
    
  

    В зависимости от функциональности расширения могут потребоваться другие директивы **using**.
    
  
5. Унаследуйте его от базового класса  [CustomParameterDataProvider](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.CustomParameterDataProvider.aspx) .
    
  
6. Задайте строковый идентификатор для имени поставщика данных. Он должен совпадать с ключом, добавленным в раздел **CustomParameterDataProviders** файла web.config при регистрации расширения. Дополнительные сведения см. в статье [Регистрация расширений служб PerformancePoint вручную](http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx).
    
  
7. Переопределите метод  [GetId()](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.CustomParameterDataProvider.GetId.aspx) для возвращения идентификатора поставщика данных.
    
  
8. Переопределите метод  [GetDisplayDataInternal](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.CustomParameterDataProvider.GetDisplayDataInternal.aspx) , чтобы определить объект [DataTable](https://msdn.microsoft.com/library/System.Data.DataTable.aspx) для хранения значений данных из источника данных. Фильтр использует этот метод для заполнения элемента управления фильтра. Таблица с отображаемыми данными должна содержать следующие имена столбцов.
    
  - **Key** Уникальный идентификатор записи. Это значение не может быть равно NULL. В целях производительности и безопасности элементы управления выдают только ключ, но не значения из других столбцов.
    
  
  - **Display** Значение, которое отображается в элементе управления фильтра.
    
  
  - **ParentKey** Это значение используется для упорядочения иерархических данных в элементе управления дерева.
    
  
  - **IsDefault** Это значение используется для сохранения фильтра.
    
    > **Совет:** Можно добавить дополнительные столбцы для расширения функциональности фильтра. 

     [GetDisplayDataInternal](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.CustomParameterDataProvider.GetDisplayDataInternal.aspx) вызывает метод [DataSourceRegistry.GetDataSource(DataSource)](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSourceRegistry.GetDataSource.aspx) для проверки типа источника данных по имени следующим образом.
    
  - Он ссылается на тип источника данных с помощью свойства  [SubTypeId](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSource.SubTypeId.aspx) источника данных, который является совпадает со значением атрибута **subType**, который зарегистрирован в файле web.config Службы PerformancePoint Services для расширения источника данных.
    
  
  - Он ссылается на собственный источник данных с помощью свойства  [SourceName](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSource.SourceName.aspx) , которое возвращает поле из класса [DataSourceNames](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSourceNames.aspx) .
    
  
9. Переопределите метод  [GetMessageData](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.CustomParameterDataProvider.GetMessageData.aspx) для сохранения выбора пользователя из элемента управления фильтра. Фильтр использует этот метод при передаче выбора пользователя потребителям.
    
  

## <a name="code-example-create-a-data-provider-for-custom-performancepoint-services-filters-in-sharepoint"></a>Пример кода: Создание поставщика данных для настраиваемых фильтров PerformancePoint Services в SharePoint
<a name="bk_example"> </a>

В следующем примере кода показано, как поставщик данных получает значения из веб-службы или таблицу Excel и возвращает объекты  [DataTable](https://msdn.microsoft.com/library/System.Data.DataTable.aspx) для отображения данных фильтра и данных сообщения.
  
    
    
Перед компиляцией этого примера кода требуется настроить среду разработки, как описано в разделе  [Создание и настройка класса поставщика](#bk_createconfig).
  
    
    



```cs

using System.Data;
using Microsoft.PerformancePoint.Scorecards;
using Microsoft.PerformancePoint.Scorecards.Server.Extensions;

namespace Microsoft.PerformancePoint.SDK.Samples.SampleFilter
{

    // Represents the sample filter's data provider.
    public class SampleFilterDataProvider : CustomParameterDataProvider
    {

        // This value must match the key that you register for this extension
        // in the CustomParameterDataProviders section in the web.config file.
        private const string dataProviderName = "SampleFilterDataProvider";

        // Returns a table of all possible values (rows) for the
        // filter's beginpoints. The filter's BeginPoint property returns
        // one ParameterDefinition object.
        protected override DataTable GetDisplayDataInternal(ParameterDefinition parameterDefinition, RepositoryLocation parameterSourceLocation, object custom)
        {
            DataTable retrievedData = null;

            // Get the data source.
            DataSource parameterDataSource = SafeGetDataSource(parameterSourceLocation);
            if (null != parameterDataSource)
            {

                // Verify that the data source is the sample data source
                // or an Excel workbook, which are the types that the
                // sample supports.
                // If you modify these types of data source, you must make
                // the corresponding change in the filter's editor.
                if (parameterDataSource.SourceName == "WSTabularDataSource" || parameterDataSource.SourceName == DataSourceNames.ExcelWorkbook)
                {
                    IDataSourceProvider parameterDataSourceProvider =
                        DataSourceRegistry.GetDataSource(parameterDataSource);
                    if (null != parameterDataSourceProvider)
                    {
                        var dataSourceMetadata = parameterDataSourceProvider as IDataSourceMetadata;
                        if (null != dataSourceMetadata)
                        {

                            // Get the data and store it in the retrievedDataSet
                            // variable. The -1 parameter returns all records
                            // from the data source.
                            DataSet retrievedDataSet = dataSourceMetadata.GetPreviewDataSet(-1);

                            // Verify that the dataset contains data.  
                            if (retrievedDataSet != null &amp;&amp;
                                retrievedDataSet.Tables != null &amp;&amp;
                                retrievedDataSet.Tables.Count > 0 &amp;&amp;
                                retrievedDataSet.Tables[0] != null &amp;&amp;
                                retrievedDataSet.Tables[0].Columns != null &amp;&amp;
                                retrievedDataSet.Tables[0].Columns.Count > 0 &amp;&amp;
                                retrievedDataSet.Tables[0].Rows != null &amp;&amp;
                                retrievedDataSet.Tables[0].Rows.Count > 0 &amp;&amp;
                                retrievedDataSet.Tables[0].Columns.Contains(parameterDefinition.KeyColumn))
                            {
                                retrievedData = retrievedDataSet.Tables[0];
                            }
                        }
                    }
                }

                if (null != retrievedData)
                {
                    // Name the display data table.
                    retrievedData.TableName = "ParamData";

                    // Verify that the table has the correct structure. 
                    EnsureDataColumns(retrievedData, parameterDefinition);

                    bool firstRowSeen = false;
                    foreach (DataRow row in retrievedData.Rows)
                    {
                        // Set the ParentKeyColumn to null because the data
                        // does not have a hierarchical structure.
                        row[parameterDefinition.ParentKeyColumn] = null;

                        // Set the IsDefaultColumn column in the first row to true.
                        row[parameterDefinition.IsDefaultColumn] = !firstRowSeen;
                        if (!firstRowSeen)
                        {
                            firstRowSeen = true;
                        }
                    }

                    // Set the column visibility.
                    SetColumnVisibility(retrievedData);
                }
            }
            
            return retrievedData;
        }

        // Adds the ShowColumn extended property to a column in the display data table
        // and sets it to true. This exposes the column in Dashboard Designer as 
        // a source value for the beginpoint. 
        private static void SetColumnVisibility(DataTable displayData)
        {
            for (int i = 0; i < displayData.Columns.Count; i++)
            {
                if (!displayData.Columns[i].ExtendedProperties.Contains("ShowColumn"))
                {
                    displayData.Columns[i].ExtendedProperties.Add("ShowColumn", true);
                }
            }
        }

        // Verify that all required columns are in the data table.
        // The data table returned by this method is expected to contain a
        // Key, ParentKey, IsDefault, Display, and an arbitrary number of
        // Value columns.
        // The specific column names (except for Value columns) are defined
        // in the filter's ParameterDefinition object, which is referenced by
        // the filter's BeginPoint property.
        private static void EnsureDataColumns(DataTable dataTable, ParameterDefinition parameterDefinition)
        {
            if (!string.IsNullOrEmpty(parameterDefinition.KeyColumn) &amp;&amp; !dataTable.Columns.Contains(parameterDefinition.KeyColumn))
            {
                dataTable.Columns.Add(parameterDefinition.KeyColumn);
            }
            if (!string.IsNullOrEmpty(parameterDefinition.DisplayColumn) &amp;&amp; !dataTable.Columns.Contains(parameterDefinition.DisplayColumn))
            {
                dataTable.Columns.Add(parameterDefinition.DisplayColumn);
            }
            if (!string.IsNullOrEmpty(parameterDefinition.ParentKeyColumn) &amp;&amp; !dataTable.Columns.Contains(parameterDefinition.ParentKeyColumn))
            {
                dataTable.Columns.Add(parameterDefinition.ParentKeyColumn);
            }
            if (!string.IsNullOrEmpty(parameterDefinition.IsDefaultColumn) &amp;&amp; !dataTable.Columns.Contains(parameterDefinition.IsDefaultColumn))
            {
                dataTable.Columns.Add(parameterDefinition.IsDefaultColumn, typeof(bool));
            }
        }

        // Returns the unique string identifier of the data provider.
        // This value must match the key that you register for this extension
        // in the CustomParameterDataProviders section in the web.config file.
        public override string GetId()
        {
            return dataProviderName;
        }

        // Returns a table of rows that match the keys in the passed
        // ParameterMessage object.
        // This method is used by controls that accept parameters, such as
        // scorecard and reports. It can also apply a Post Formula.
        public override DataTable GetMessageData(RepositoryLocation providerLocation, ParameterMessage parameterMessage, RepositoryLocation parameterSourceLocation, ParameterMapping parameterMapping, object custom)
        {   
            DataTable msgTable = null;

            // The ParameterMapping object contains information about
            // linked dashboard items.
            // The CustomData object is optionally used to store information
            // that is not stored in other properties.
            DataTable displayTable = GetDisplayDataInternal(parameterMessage, parameterSourceLocation, custom);

            if (null != displayTable)
            {
                msgTable = displayTable.Clone();
                for (int i = 0;i < parameterMessage.Values.Rows.Count; i++)
                {
                    for (int j = 0;j < displayTable.Rows.Count; j++)
                    {
                        if (!parameterMessage.Values.Rows[i][parameterMessage.KeyColumn].Equals(displayTable.Rows[j][parameterMessage.KeyColumn].ToString())) 
                            continue;

                        msgTable.ImportRow(displayTable.Rows[j]);
                        break;
                    }
                }
            }

            return msgTable;
        }
    }
}
```


## <a name="next-steps"></a>Дальнейшие действия
<a name="bk_next"> </a>

После создания поставщика данных и редактор фильтра (включая его пользовательский интерфейс, если это необходимо), развертывание данное расширение имени файла, как описано в  [Регистрация расширений служб PerformancePoint вручную](http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx).
  
    
    

## <a name="see-also"></a>См. также
<a name="bk_next"> </a>


-  [Как: создать фильтр редакторы для служб PerformancePoint Services в SharePoint](how-to-create-filter-editors-for-performancepoint-services-in-sharepoint.md)
    
  
-  [PerformancePoint Services в SharePoint](performancepoint-services-in-sharepoint.md)
    
  

