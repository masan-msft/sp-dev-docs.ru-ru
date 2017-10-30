---
title: "Создание поставщиков данных фильтра для PerformancePoint Services в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 25508ec6-86bf-4eea-acf0-00f88e4faa55
ms.openlocfilehash: 14b0b02b1fdd365bb0f300ccf19ce6e7b9b21f98
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-create-filter-data-providers-for-performancepoint-services-in-sharepoint"></a><span data-ttu-id="2cda4-102">Как: создать фильтр поставщиков данных для служб PerformancePoint Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="2cda4-102">How to: Create filter data providers for PerformancePoint Services in SharePoint</span></span>
<span data-ttu-id="2cda4-103">Узнайте, как создать компонент поставщика данных в модуле пользовательских фильтров для Службы PerformancePoint Services.</span><span class="sxs-lookup"><span data-stu-id="2cda4-103">Learn how to create the data provider component in a custom filter extension for PerformancePoint Services.</span></span>
## <a name="what-are-custom-data-providers-for-performancepoint-services"></a><span data-ttu-id="2cda4-104">Что такое настраиваемые поставщики данных для Службы PerformancePoint Services ?</span><span class="sxs-lookup"><span data-stu-id="2cda4-104">What are custom data providers for PerformancePoint Services?</span></span>
<span data-ttu-id="2cda4-105"><a name="bk_introduction"> </a></span><span class="sxs-lookup"><span data-stu-id="2cda4-105"><a name="bk_introduction"> </a></span></span>

<span data-ttu-id="2cda4-p101">В Службы PerformancePoint Services настраиваемые поставщики данных извлечения данных из источника данных в фильтре и определяют, как использовать данные. Важнее поставщики данных укажите значения данных для представления элемента управления фильтра и данных, которые можно использовать в качестве начальную точку фильтра. Поставщик данных также сохраняет значение, выбранной пользователем в элементе управления фильтра, который отправляется в фильтрации объекты-получатели. Поставщики данных используйте два объекта  [DataTable](https://msdn.microsoft.com/library/System.Data.DataTable.aspx) для организации и хранения данных. Для получения дополнительных сведений см [Фильтры служб PerformancePoint](http://msdn.microsoft.com/library/915382d0-3997-495c-a65a-7db3fe0b8f85%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="2cda4-p101">In PerformancePoint Services, custom data providers retrieve data from a filter's underlying data source and define how to use the data. Most importantly, data providers specify the data values to expose in the filter control and the data that can be used as the filter's beginpoint. A data provider also stores the value that a user selects from the filter control, which is then sent to filter consumers. Data providers use two  [DataTable](https://msdn.microsoft.com/library/System.Data.DataTable.aspx) objects to organize and store data. For more information, see [Filters Overview](http://msdn.microsoft.com/library/915382d0-3997-495c-a65a-7db3fe0b8f85%28Office.15%29.aspx).</span></span>
  
    
    
<span data-ttu-id="2cda4-111">Следующие процедуры и примеры, показывающие, как создать, настроить и определите поставщика данных фильтра основаны на класс **SampleFilterDataProvider** из [настраиваемых объектов](http://msdn.microsoft.com/library/af021d52-7562-4e7a-9de4-e1fc5784a59d%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="2cda4-111">The following procedures and examples that show you how to create, configure, and define a filter data provider are based on the **SampleFilterDataProvider** class from the [custom objects sample](http://msdn.microsoft.com/library/af021d52-7562-4e7a-9de4-e1fc5784a59d%28Office.15%29.aspx).</span></span> <span data-ttu-id="2cda4-112">Редактор — тонкие веб-приложения, которое позволяет пользователям изменять имя и описание отчета.</span><span class="sxs-lookup"><span data-stu-id="2cda4-112">The editor is a thin web application that enables users to modify the report's name and description.</span></span> <span data-ttu-id="2cda4-113">Полный код для класса, в разделе [пример кода: Создание поставщика данных для настраиваемых фильтров PerformancePoint Services в SharePoint](#bk_example).</span><span class="sxs-lookup"><span data-stu-id="2cda4-113">For the complete code for the class, see  [Code example: Create a data provider for custom PerformancePoint Services filters in SharePoint](#bk_example).</span></span>
  
    
    
<span data-ttu-id="2cda4-p103">Мы рекомендуем использовать примера поставщика данных в качестве шаблона. В примере показано, как вызывать объекты в Службы PerformancePoint Services API и демонстрируется советы и рекомендации по разработке Службы PerformancePoint Services.</span><span class="sxs-lookup"><span data-stu-id="2cda4-p103">We recommend that you use the sample data provider as a template. The sample shows how to call objects in the PerformancePoint Services API and demonstrates best practices for PerformancePoint Servicesdevelopment.</span></span> 
  
    
    

## <a name="create-data-providers-for-custom-performancepoint-services-filters"></a><span data-ttu-id="2cda4-116">Создание поставщика данных для настраиваемых Службы PerformancePoint Services фильтров</span><span class="sxs-lookup"><span data-stu-id="2cda4-116">Create data providers for custom PerformancePoint Services filters</span></span>
<span data-ttu-id="2cda4-117"><a name="bk_createconfig"> </a></span><span class="sxs-lookup"><span data-stu-id="2cda4-117"><a name="bk_createconfig"> </a></span></span>


1. <span data-ttu-id="2cda4-p104">Установка Службы PerformancePoint Services или копирование библиотеки DLL, которые использует расширения (перечисленных в шаге 3) на своем компьютере. Для получения дополнительных сведений см  [Библиотеки DLL служб PerformancePoint, используемые в сценариях развертывания](http://msdn.microsoft.com/library/41e92619-8253-481d-82f9-35b6a6abc477%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="2cda4-p104">Install PerformancePoint Services, or copy the DLLs that your extension uses (listed in step 3) to your computer. For more information, see  [DLLs with Class Libraries](http://msdn.microsoft.com/library/41e92619-8253-481d-82f9-35b6a6abc477%28Office.15%29.aspx).</span></span>
    
  
2. <span data-ttu-id="2cda4-p105">В Visual Studio создайте библиотеку классов C#. Если библиотека классов для расширения уже создана, добавьте новый класс C#.</span><span class="sxs-lookup"><span data-stu-id="2cda4-p105">In Visual Studio, create a C# class library. If you have already created a class library for your extension, add a new C# class.</span></span>
    
    <span data-ttu-id="2cda4-p106">DLL-библиотеку необходимо подписать строгим именем. Кроме того, убедитесь, что все сборки, на которые ссылается DLL-библиотека, имеют строгие имена. Процедура подписывания сборки строгим именем и создания пары из открытого и закрытого ключа рассматривается в разделе  [How to: Create a Public/Private Key Pair](http://msdn.microsoft.com/library/05026813-f3bd-4d7c-9e0b-fc588eb3d114.aspx).</span><span class="sxs-lookup"><span data-stu-id="2cda4-p106">You must sign your DLL with a strong name. In addition, ensure that all assemblies referenced by your DLL have strong names. For information about how to sign an assembly with a strong name and how to create a public/private key pair, see  [How to: Create a Public/Private Key Pair](http://msdn.microsoft.com/library/05026813-f3bd-4d7c-9e0b-fc588eb3d114.aspx).</span></span>
    
  
3. <span data-ttu-id="2cda4-125">Добавьте следующие Службы PerformancePoint Services библиотеки DLL в качестве ссылок на сборки в проект:</span><span class="sxs-lookup"><span data-stu-id="2cda4-125">Add the following PerformancePoint Services DLLs as assembly references to the project:</span></span>
    
  - <span data-ttu-id="2cda4-126">Microsoft.PerformancePoint.Scorecards.Client.dll</span><span class="sxs-lookup"><span data-stu-id="2cda4-126">Microsoft.PerformancePoint.Scorecards.Client.dll</span></span>
    
  
  - <span data-ttu-id="2cda4-127">Microsoft.PerformancePoint.Scorecards.Server.dll</span><span class="sxs-lookup"><span data-stu-id="2cda4-127">Microsoft.PerformancePoint.Scorecards.Server.dll</span></span>
    
  

    <span data-ttu-id="2cda4-128">В зависимости от функциональности расширения могут потребоваться другие ссылки в проекте.</span><span class="sxs-lookup"><span data-stu-id="2cda4-128">Depending on your extension's functionality, other project references may be required.</span></span>
    
  
4. <span data-ttu-id="2cda4-129">В классе поставщика добавьте директивы **using** для следующих пространств имен Службы PerformancePoint Services.</span><span class="sxs-lookup"><span data-stu-id="2cda4-129">In your provider class, add **using** directives for the following PerformancePoint Services namespaces:</span></span>
    
  -  [<span data-ttu-id="2cda4-130">Microsoft.PerformancePoint.Scorecards</span><span class="sxs-lookup"><span data-stu-id="2cda4-130">Microsoft.PerformancePoint.Scorecards</span></span>](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.aspx)
    
  
  -  [<span data-ttu-id="2cda4-131">Microsoft.PerformancePoint.Scorecards.Server.Extensions</span><span class="sxs-lookup"><span data-stu-id="2cda4-131">Microsoft.PerformancePoint.Scorecards.Server.Extensions</span></span>](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.aspx)
    
  

    <span data-ttu-id="2cda4-132">В зависимости от функциональности расширения могут потребоваться другие директивы **using**.</span><span class="sxs-lookup"><span data-stu-id="2cda4-132">Depending on your extension's functionality, other **using** directives may be required.</span></span>
    
  
5. <span data-ttu-id="2cda4-133">Унаследуйте его от базового класса  [CustomParameterDataProvider](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.CustomParameterDataProvider.aspx) .</span><span class="sxs-lookup"><span data-stu-id="2cda4-133">Inherit from the  [CustomParameterDataProvider](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.CustomParameterDataProvider.aspx) base class.</span></span>
    
  
6. <span data-ttu-id="2cda4-p107">Задайте строковый идентификатор для имени поставщика данных. Он должен совпадать с ключом, добавленным в раздел **CustomParameterDataProviders** файла web.config при регистрации расширения. Дополнительные сведения см. в статье [Регистрация расширений служб PerformancePoint вручную](http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="2cda4-p107">Set the string identifier for the data provider name. This must match the key that you add to the **CustomParameterDataProviders** section of the web.config file when you register the extension. For more information, see [How to: Manually Register PerformancePoint Services Extensions](http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx).</span></span>
    
  
7. <span data-ttu-id="2cda4-137">Переопределите метод  [GetId()](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.CustomParameterDataProvider.GetId.aspx) для возвращения идентификатора поставщика данных.</span><span class="sxs-lookup"><span data-stu-id="2cda4-137">Override the  [GetId()](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.CustomParameterDataProvider.GetId.aspx) method to return the identifier for your data provider.</span></span>
    
  
8. <span data-ttu-id="2cda4-p108">Переопределите метод  [GetDisplayDataInternal](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.CustomParameterDataProvider.GetDisplayDataInternal.aspx) , чтобы определить объект [DataTable](https://msdn.microsoft.com/library/System.Data.DataTable.aspx) для хранения значений данных из источника данных. Фильтр использует этот метод для заполнения элемента управления фильтра. Таблица с отображаемыми данными должна содержать следующие имена столбцов.</span><span class="sxs-lookup"><span data-stu-id="2cda4-p108">Override the  [GetDisplayDataInternal](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.CustomParameterDataProvider.GetDisplayDataInternal.aspx) method to define a [DataTable](https://msdn.microsoft.com/library/System.Data.DataTable.aspx) object to store the data values from the underlying data source. The filter uses this method to populate the filter selection control. The display data table must contain the following column names:</span></span>
    
  - <span data-ttu-id="2cda4-p109">**Key** Уникальный идентификатор записи. Это значение не может быть равно NULL. В целях производительности и безопасности элементы управления выдают только ключ, но не значения из других столбцов.</span><span class="sxs-lookup"><span data-stu-id="2cda4-p109">**Key** The unique identifier for the record. This value cannot be null. For performance and security purposes, controls emit only a key; they do not emit values from the other columns.</span></span>
    
  
  - <span data-ttu-id="2cda4-144">**Display** Значение, которое отображается в элементе управления фильтра.</span><span class="sxs-lookup"><span data-stu-id="2cda4-144">**Display** The value that appears in the filter control.</span></span>
    
  
  - <span data-ttu-id="2cda4-145">**ParentKey** Это значение используется для упорядочения иерархических данных в элементе управления дерева.</span><span class="sxs-lookup"><span data-stu-id="2cda4-145">**ParentKey** This value is used to arrange hierarchical data in a tree control.</span></span>
    
  
  - <span data-ttu-id="2cda4-146">**IsDefault** Это значение используется для сохранения фильтра.</span><span class="sxs-lookup"><span data-stu-id="2cda4-146">**IsDefault** This value is used for filter persistence.</span></span>
    
    > <span data-ttu-id="2cda4-147">**Совет:** Можно добавить дополнительные столбцы для расширения функциональности фильтра.</span><span class="sxs-lookup"><span data-stu-id="2cda4-147">**Tip:** You can add more columns to extend the filter's functionality.</span></span> 

     <span data-ttu-id="2cda4-148">[GetDisplayDataInternal](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.CustomParameterDataProvider.GetDisplayDataInternal.aspx) вызывает метод [DataSourceRegistry.GetDataSource(DataSource)](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSourceRegistry.GetDataSource.aspx) для проверки типа источника данных по имени следующим образом.</span><span class="sxs-lookup"><span data-stu-id="2cda4-148">[GetDisplayDataInternal](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.CustomParameterDataProvider.GetDisplayDataInternal.aspx) calls the [DataSourceRegistry.GetDataSource(DataSource)](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSourceRegistry.GetDataSource.aspx) method to verify the data source type by name, as follows:</span></span>
    
  - <span data-ttu-id="2cda4-149">Он ссылается на тип источника данных с помощью свойства  [SubTypeId](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSource.SubTypeId.aspx) источника данных, который является совпадает со значением атрибута **subType**, который зарегистрирован в файле web.config Службы PerformancePoint Services для расширения источника данных.</span><span class="sxs-lookup"><span data-stu-id="2cda4-149">It references a custom data source type by using the  [SubTypeId](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSource.SubTypeId.aspx) property of the data source, which is the same value as the **subType** attribute that is registered in the PerformancePoint Services web.config file for the data source extension.</span></span>
    
  
  - <span data-ttu-id="2cda4-150">Он ссылается на собственный источник данных с помощью свойства  [SourceName](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSource.SourceName.aspx) , которое возвращает поле из класса [DataSourceNames](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSourceNames.aspx) .</span><span class="sxs-lookup"><span data-stu-id="2cda4-150">It references a native data source by using the  [SourceName](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSource.SourceName.aspx) property, which returns a field from the [DataSourceNames](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSourceNames.aspx) class.</span></span>
    
  
9. <span data-ttu-id="2cda4-p110">Переопределите метод  [GetMessageData](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.CustomParameterDataProvider.GetMessageData.aspx) для сохранения выбора пользователя из элемента управления фильтра. Фильтр использует этот метод при передаче выбора пользователя потребителям.</span><span class="sxs-lookup"><span data-stu-id="2cda4-p110">Override the  [GetMessageData](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.CustomParameterDataProvider.GetMessageData.aspx) method to store the user's selection from the filter control. The filter uses this method when it sends the user's selections to consumers.</span></span>
    
  

## <a name="code-example-create-a-data-provider-for-custom-performancepoint-services-filters-in-sharepoint"></a><span data-ttu-id="2cda4-153">Пример кода: Создание поставщика данных для настраиваемых фильтров PerformancePoint Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="2cda4-153">Code example: Create a data provider for custom PerformancePoint Services filters in SharePoint</span></span>
<span data-ttu-id="2cda4-154"><a name="bk_example"> </a></span><span class="sxs-lookup"><span data-stu-id="2cda4-154"><a name="bk_example"> </a></span></span>

<span data-ttu-id="2cda4-155">В следующем примере кода показано, как поставщик данных получает значения из веб-службы или таблицу Excel и возвращает объекты  [DataTable](https://msdn.microsoft.com/library/System.Data.DataTable.aspx) для отображения данных фильтра и данных сообщения.</span><span class="sxs-lookup"><span data-stu-id="2cda4-155">The following code example shows how a data provider retrieves values from a web service or an Excel worksheet and returns  [DataTable](https://msdn.microsoft.com/library/System.Data.DataTable.aspx) objects for the filter's display data and message data.</span></span>
  
    
    
<span data-ttu-id="2cda4-156">Перед компиляцией этого примера кода требуется настроить среду разработки, как описано в разделе  [Создание и настройка класса поставщика](#bk_createconfig).</span><span class="sxs-lookup"><span data-stu-id="2cda4-156">Before you can compile this code example, you must configure your development environment as described in  [To create and configure the provider class](#bk_createconfig).</span></span>
  
    
    



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


## <a name="next-steps"></a><span data-ttu-id="2cda4-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2cda4-157">Next steps</span></span>
<span data-ttu-id="2cda4-158"><a name="bk_next"> </a></span><span class="sxs-lookup"><span data-stu-id="2cda4-158"><a name="bk_next"> </a></span></span>

<span data-ttu-id="2cda4-159">После создания поставщика данных и редактор фильтра (включая его пользовательский интерфейс, если это необходимо), развертывание данное расширение имени файла, как описано в  [Регистрация расширений служб PerformancePoint вручную](http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="2cda4-159">After you create a data provider and a filter editor (including its user interface, if required), deploy the extension as described in  [How to: Manually Register PerformancePoint Services Extensions](http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx).</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="2cda4-160">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="2cda4-160">Additional resources</span></span>
<span data-ttu-id="2cda4-161"><a name="bk_next"> </a></span><span class="sxs-lookup"><span data-stu-id="2cda4-161"><a name="bk_next"> </a></span></span>


-  [<span data-ttu-id="2cda4-162">Как: создать фильтр редакторы для служб PerformancePoint Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="2cda4-162">How to: Create filter editors for PerformancePoint Services in SharePoint</span></span>](how-to-create-filter-editors-for-performancepoint-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="2cda4-163">PerformancePoint Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="2cda4-163">PerformancePoint Services in SharePoint</span></span>](performancepoint-services-in-sharepoint.md)
    
  

