---
title: "Создание поставщиков табличных источников данных для служб PerformancePoint Services в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 8d734ed6-7636-40c5-a99b-bc038362cffe
ms.openlocfilehash: d3e07812b180244e76e991e7b06dec1d94ad6b69
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="create-tabular-data-source-providers-for-performancepoint-services-in-sharepoint"></a><span data-ttu-id="a5f68-102">Создание поставщиков табличных источников данных для служб PerformancePoint Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="a5f68-102">Create tabular data source providers for PerformancePoint Services in SharePoint</span></span>

<span data-ttu-id="a5f68-103">Узнайте, как создать компонент поставщика источника данных в модуле пользовательских табличных источников данных для Службы PerformancePoint Services.</span><span class="sxs-lookup"><span data-stu-id="a5f68-103">Learn how to create the data source provider component in a custom tabular data source extension for PerformancePoint Services.</span></span>

## <a name="what-are-custom-data-source-providers-for-performancepoint-services"></a><span data-ttu-id="a5f68-104">Что такое настраиваемых поставщиков источников данных для Службы PerformancePoint Services ?</span><span class="sxs-lookup"><span data-stu-id="a5f68-104">What are custom data source providers for PerformancePoint Services?</span></span>
<span data-ttu-id="a5f68-105"><a name="bk_intro"> </a></span><span class="sxs-lookup"><span data-stu-id="a5f68-105"><a name="bk_intro"> </a></span></span>

<span data-ttu-id="a5f68-p101">Поставщики источников данных подключения к источнику данных, доступ к данным и затем возврата результатов. Службы PerformancePoint Services использует поставщиков табличных источников данных для доступа к данным из Excel и Службы Excel листы, списки SharePoint и Microsoft SQL Server таблицы. Можно создать поставщика настраиваемого источника данных, чтобы использовать данные из источника табличных данных, не поддерживаемый Службы PerformancePoint Services.</span><span class="sxs-lookup"><span data-stu-id="a5f68-p101">Data source providers connect to a data source, access its data, and then return query results. PerformancePoint Services uses tabular data source providers to access data from Excel and Excel Services worksheets, SharePoint lists, and Microsoft SQL Server tables. You can create a custom data source provider to use data from a tabular data source that is not supported by PerformancePoint Services.</span></span>
  
    
    
<span data-ttu-id="a5f68-p102">Основная функция поставщика источника табличных данных  создание и заполнение таблицу данных с данными из источника данных. Он также создает сопоставления столбцов, чтобы определить тип данных, что каждый столбец содержит (фактов, измерений или измерение времени). Базовая структура многомерные применяется к табличных данных.</span><span class="sxs-lookup"><span data-stu-id="a5f68-p102">The main function of a tabular data source provider is to create and populate a data table with data from the data source. It also creates column mappings to define the type of data that each column contains (fact, dimension, or time dimension). This applies a basic multidimensional structure to the tabular data.</span></span>
  
    
    
<span data-ttu-id="a5f68-112">Инструкции и примеры кода в этом разделе основаны на класс **WSTabularDataSourceProvider** из [настраиваемых объектов](http://msdn.microsoft.com/library/af021d52-7562-4e7a-9de4-e1fc5784a59d%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="a5f68-112">The procedures and code examples in this topic are based on the **WSTabularDataSourceProvider** class from the [custom objects sample](http://msdn.microsoft.com/library/af021d52-7562-4e7a-9de4-e1fc5784a59d%28Office.15%29.aspx).</span></span> <span data-ttu-id="a5f68-113">Поставщик извлекает акций внешних веб-службе для указанного символов акций.</span><span class="sxs-lookup"><span data-stu-id="a5f68-113">The provider retrieves stock quotes from an external web service for specified stock symbols.</span></span> <span data-ttu-id="a5f68-114">Хранит данные журнала запасов квоты в файл кэша, который позволяет данные срез по времени.</span><span class="sxs-lookup"><span data-stu-id="a5f68-114">It stores historical stock quote data in a cache file, which enables the data to be sliced by time.</span></span> <span data-ttu-id="a5f68-115">Полный код для класса, в разделе [пример кода: Создание поставщика источника данных для настраиваемых служб PerformancePoint Services табличные источники данных в SharePoint](#bk_example).</span><span class="sxs-lookup"><span data-stu-id="a5f68-115">For the complete code for the class, see  [Code example: Create a data source provider for custom PerformancePoint Services tabular data sources in SharePoint](#bk_example).</span></span>
  
    
    
<span data-ttu-id="a5f68-p104">Мы рекомендуем использовать примера поставщика источника данных в качестве шаблона. В примере показано, как вызывать объекты в Службы PerformancePoint Services API и демонстрируется советы и рекомендации по разработке Службы PerformancePoint Services.</span><span class="sxs-lookup"><span data-stu-id="a5f68-p104">We recommend that you use the sample data source provider as a template. The sample shows how to call objects in the PerformancePoint Services API and demonstrates best practices for PerformancePoint Services development.</span></span>
  
    
    

## <a name="create-data-source-providers-for-custom-performancepoint-services-tabular-data-sources"></a><span data-ttu-id="a5f68-118">Создание поставщики источников данных для настраиваемых Службы PerformancePoint Services табличные источники данных</span><span class="sxs-lookup"><span data-stu-id="a5f68-118">Create data source providers for custom PerformancePoint Services tabular data sources</span></span>
<span data-ttu-id="a5f68-119"><a name="BKMK_CreateClass"> </a></span><span class="sxs-lookup"><span data-stu-id="a5f68-119"><a name="BKMK_CreateClass"> </a></span></span>


1. <span data-ttu-id="a5f68-p105">Установка Службы PerformancePoint Services или копирование библиотеки DLL, которые использует расширения (перечисленных в шаге 3) на своем компьютере. Сведения содержатся в разделе  [Библиотеки DLL служб PerformancePoint, используемые в сценариях развертывания](http://msdn.microsoft.com/library/41e92619-8253-481d-82f9-35b6a6abc477%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="a5f68-p105">Install PerformancePoint Services, or copy the DLLs that your extension uses (listed in step 3) to your computer. For instructions, see  [DLLs with Class Libraries](http://msdn.microsoft.com/library/41e92619-8253-481d-82f9-35b6a6abc477%28Office.15%29.aspx).</span></span>
    
  
2. <span data-ttu-id="a5f68-p106">В Visual Studio создайте библиотеку классов C#. Если библиотека классов для расширения уже создана, добавьте новый класс C#.</span><span class="sxs-lookup"><span data-stu-id="a5f68-p106">In Visual Studio, create a C# class library. If you have already created a class library for your extension, add a new C# class.</span></span>
    
    <span data-ttu-id="a5f68-p107">DLL-библиотеку необходимо подписать строгим именем. Кроме того, убедитесь, что все сборки, на которые ссылается DLL-библиотека, имеют строгие имена. Процедура подписывания сборки строгим именем и создания пары из открытого и закрытого ключа рассматривается в разделе  [How to: Create a Public/Private Key Pair](http://msdn.microsoft.com/library/05026813-f3bd-4d7c-9e0b-fc588eb3d114.aspx).</span><span class="sxs-lookup"><span data-stu-id="a5f68-p107">You must sign your DLL with a strong name. In addition, ensure that all assemblies referenced by your DLL have strong names. For information about how to sign an assembly with a strong name and how to create a public/private key pair, see  [How to: Create a Public/Private Key Pair](http://msdn.microsoft.com/library/05026813-f3bd-4d7c-9e0b-fc588eb3d114.aspx).</span></span>
    
  
3. <span data-ttu-id="a5f68-127">Добавьте следующие Службы PerformancePoint Services библиотеки DLL в качестве ссылок на сборки в проект:</span><span class="sxs-lookup"><span data-stu-id="a5f68-127">Add the following PerformancePoint Services DLLs as assembly references to the project:</span></span>
    
  - <span data-ttu-id="a5f68-128">Microsoft.PerformancePoint.Scorecards.Client.dll</span><span class="sxs-lookup"><span data-stu-id="a5f68-128">Microsoft.PerformancePoint.Scorecards.Client.dll</span></span>
    
  
  - <span data-ttu-id="a5f68-129">Microsoft.PerformancePoint.Scorecards.DataSourceProviders.Standard.dll</span><span class="sxs-lookup"><span data-stu-id="a5f68-129">Microsoft.PerformancePoint.Scorecards.DataSourceProviders.Standard.dll</span></span>
    
  

    <span data-ttu-id="a5f68-p108">В этом примере поставщика данных также используются ссылки на сборки System.Core.dll, System.ServiceModel.dll, System.Web.dll, System.Web.Services.dll и System.Xml.Linq.dll. В зависимости от функциональных возможностей расширения могут потребоваться другие сборки.</span><span class="sxs-lookup"><span data-stu-id="a5f68-p108">The sample data source provider also contains assembly references to System.Core.dll, System.ServiceModel.dll, System.Web.dll, System.Web.Services.dll, and System.Xml.Linq.dll. Depending on your extension's functionality, other project references may be required.</span></span>
    
  
4. <span data-ttu-id="a5f68-p109">Добавьте ссылку на службу с именем **StockQuotes**, которая ссылается на веб-службу, расположенную по адресу  `http://www.webservicex.net/stockquote.asmx`. Эта веб-служба предоставляет котировки акций для примера поставщика источника данных.</span><span class="sxs-lookup"><span data-stu-id="a5f68-p109">Add a service reference named **StockQuotes** that references the Web service located at the address `http://www.webservicex.net/stockquote.asmx`. This is the Web service that provides stock quotes for the sample data source.</span></span>
    
  
5. <span data-ttu-id="a5f68-p110">Добавьте классы **BasicTabularDataSourceProvider** и **SampleDSCacheHandler** из примера в проект. Класс **BasicTabularDataSourceProvider** наследуется от класса [TabularDataSourceProvider](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSourceProviders.TabularDataSourceProvider.aspx) , который является базовым для поставщиков табличных источников данных.</span><span class="sxs-lookup"><span data-stu-id="a5f68-p110">Add the **BasicTabularDataSourceProvider** and **SampleDSCacheHandler** classes from the sample to your project. **BasicTabularDataSourceProvider** inherits from the [TabularDataSourceProvider](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSourceProviders.TabularDataSourceProvider.aspx) class, which is the base class for tabular data source providers.</span></span>
    
    <span data-ttu-id="a5f68-136">В этом примере источника данных также используется класс-контейнер для переопределенных абстрактных методов, которые не реализуются классом  [TabularDataSourceProvider](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSourceProviders.TabularDataSourceProvider.aspx) ( [GetDatabaseNames()](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.CustomDataSourceProvider.GetDatabaseNames.aspx) , [GetCubeNames()](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.CustomDataSourceProvider.GetCubeNames.aspx) , [GetCubeNameInfos()](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.CustomDataSourceProvider.GetCubeNameInfos.aspx) , [GetCubeMetaData](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.CustomDataSourceProvider.GetCubeMetaData.aspx) и [Validate()](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.CustomDataSourceProvider.Validate.aspx) ).</span><span class="sxs-lookup"><span data-stu-id="a5f68-136">The sample data source also uses the class as a container for the overridden abstract methods that  [TabularDataSourceProvider](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSourceProviders.TabularDataSourceProvider.aspx) does not implement ( [GetDatabaseNames()](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.CustomDataSourceProvider.GetDatabaseNames.aspx) , [GetCubeNames()](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.CustomDataSourceProvider.GetCubeNames.aspx) , [GetCubeNameInfos()](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.CustomDataSourceProvider.GetCubeNameInfos.aspx) , [GetCubeMetaData](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.CustomDataSourceProvider.GetCubeMetaData.aspx) , and [Validate()](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.CustomDataSourceProvider.Validate.aspx) ).</span></span>
    
  
6. <span data-ttu-id="a5f68-137">В классе поставщика добавьте директивы **using** для следующих пространств имен Службы PerformancePoint Services.</span><span class="sxs-lookup"><span data-stu-id="a5f68-137">In your provider class, add **using** directives for the following PerformancePoint Services namespaces:</span></span>
    
  -  [<span data-ttu-id="a5f68-138">Microsoft.PerformancePoint.Scorecards</span><span class="sxs-lookup"><span data-stu-id="a5f68-138">Microsoft.PerformancePoint.Scorecards</span></span>](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.aspx)
    
  
  -  [<span data-ttu-id="a5f68-139">Microsoft.PerformancePoint.Scorecards.ServerCommon</span><span class="sxs-lookup"><span data-stu-id="a5f68-139">Microsoft.PerformancePoint.Scorecards.ServerCommon</span></span>](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.ServerCommon.aspx)
    
  
  - <span data-ttu-id="a5f68-140">**Microsoft.PerformancePoint.SDK.Samples.StockQuotes** (представляет ссылку на службу StockQuotes, созданную на шаге 4)</span><span class="sxs-lookup"><span data-stu-id="a5f68-140">**Microsoft.PerformancePoint.SDK.Samples.StockQuotes** (represents the StockQuotes service reference created in step 4)</span></span>
    
  

    <span data-ttu-id="a5f68-141">В зависимости от функциональности расширения могут потребоваться другие директивы **using**.</span><span class="sxs-lookup"><span data-stu-id="a5f68-141">Depending on your extension's functionality, other **using** directives may be required.</span></span>
    
  
7. <span data-ttu-id="a5f68-142">Наследуется от класса **BasicTabularDataSourceProvider**.</span><span class="sxs-lookup"><span data-stu-id="a5f68-142">Inherit from the **BasicTabularDataSourceProvider** class.</span></span>
    
  
8. <span data-ttu-id="a5f68-143">Объявите переменные и определите свойства, которые используются для синтаксического анализа, хранения и извлечения символов акций, местоположения файла кэша и идентификатора URI прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="a5f68-143">Declare variables and define properties that are used for parsing, storing, and retrieving stock symbols, the cache file location, and the URI of the proxy server.</span></span>
    
  
9. <span data-ttu-id="a5f68-p111">Переопределите свойство  [IsConnectionStringSecure](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.CustomDataSourceProvider.IsConnectionStringSecure.aspx) . Это свойство не используется Службы PerformancePoint Services, но он предназначен для пользовательских приложений при необходимости использовать для определения, является ли строка подключения предоставляет сведения, которые могут привести к риску.</span><span class="sxs-lookup"><span data-stu-id="a5f68-p111">Override the  [IsConnectionStringSecure](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.CustomDataSourceProvider.IsConnectionStringSecure.aspx) property. This property is not used by PerformancePoint Services, but it is intended for custom applications to optionally use to identify whether a connection string exposes information that might pose a security risk.</span></span>
    
    <span data-ttu-id="a5f68-p112">Задайте возврат значения **true**, если в строке подключения к источнику данных в расширении содержатся конфиденциальные сведения, например, имя пользователя или пароль. Задайте возврат значения **false**, если конфиденциальные сведения не хранятся, или источник данных не использует строку подключения.</span><span class="sxs-lookup"><span data-stu-id="a5f68-p112">Return **true** if your extension stores sensitive information—such as a user name or password—in the connection string for your data source. Return **false** if it does not store sensitive information or if your data source does not use a connection string.</span></span>
    
  
10. <span data-ttu-id="a5f68-p113">Переопределите метод  [GetId()](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.CustomDataSourceProvider.GetId.aspx) возвращает уникальный идентификатор для поставщика. [GetId()](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.CustomDataSourceProvider.GetId.aspx) должен возвращать ту же строку в качестве атрибута **key**, который зарегистрирован в файле web.config Службы PerformancePoint Services для поставщика настраиваемого источника данных.</span><span class="sxs-lookup"><span data-stu-id="a5f68-p113">Override the  [GetId()](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.CustomDataSourceProvider.GetId.aspx) method to return the unique identifier for your provider. [GetId()](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.CustomDataSourceProvider.GetId.aspx) must return the same string as the **key** attribute that is registered in the PerformancePoint Services web.config file for the custom data source provider.</span></span>
    
  
11. <span data-ttu-id="a5f68-p114">Переопределите метод  [SetDataSource](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSourceProviders.TabularDataSourceProvider.SetDataSource.aspx) и определите сопоставления столбцов. Метод [SetDataSource](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSourceProviders.TabularDataSourceProvider.SetDataSource.aspx) вызывает метод **CreateDataColumnMappings**, чтобы определить столбцы источника данных как типы  [Fact](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.MappedColumnTypes.Fact.aspx) , [Dimension](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.MappedColumnTypes.Dimension.aspx) и [TimeDimension](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.MappedColumnTypes.TimeDimension.aspx) .</span><span class="sxs-lookup"><span data-stu-id="a5f68-p114">Override the  [SetDataSource](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSourceProviders.TabularDataSourceProvider.SetDataSource.aspx) method to define column mappings. [SetDataSource](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSourceProviders.TabularDataSourceProvider.SetDataSource.aspx) calls the **CreateDataColumnMappings** method to define data source columns as [Fact](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.MappedColumnTypes.Fact.aspx) , [Dimension](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.MappedColumnTypes.Dimension.aspx) , and [TimeDimension](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.MappedColumnTypes.TimeDimension.aspx) types.</span></span>
    
     <span data-ttu-id="a5f68-p115">Метод  [SetDataSource](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSourceProviders.TabularDataSourceProvider.SetDataSource.aspx) также извлекает символы акций, местоположение файла кэша и адрес прокси-сервера из свойства [CustomData](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSource.CustomData.aspx) объекта настраиваемого источника данных. Эти значения определяются автором панели мониторинга в редакторе примера источника данных.</span><span class="sxs-lookup"><span data-stu-id="a5f68-p115">[SetDataSource](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSourceProviders.TabularDataSourceProvider.SetDataSource.aspx) also retrieves the stock symbols, cache file location, and proxy server address from the [CustomData](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSource.CustomData.aspx) property of the custom data source object. These values are defined by dashboard authors in the sample data source editor.</span></span>
    
  
12. <span data-ttu-id="a5f68-p116">Переопределите метод  [GetDataSet()](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSourceProviders.TabularDataSourceProvider.GetDataSet.aspx) и создайте объект [DataSet](https://msdn.microsoft.com/library/System.Data.DataSet.aspx) для хранения данных из источника. В примере источника данных для заполнения таблицы данными из веб-службы используются методы **FillResultsTable** и **GetLiveQuote**.</span><span class="sxs-lookup"><span data-stu-id="a5f68-p116">Override the  [GetDataSet()](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSourceProviders.TabularDataSourceProvider.GetDataSet.aspx) method to create a [DataSet](https://msdn.microsoft.com/library/System.Data.DataSet.aspx) object to store the data from the data source. The sample data source provider uses the **FillResultsTable** and **GetLiveQuote** methods to populate a data table with data from a Web service.</span></span>
    
  

## <a name="code-example-create-a-data-source-provider-for-custom-performancepoint-services-tabular-data-sources-in-sharepoint"></a><span data-ttu-id="a5f68-156">Пример кода: Создание поставщика источника данных для настраиваемых служб PerformancePoint Services табличные источники данных в SharePoint</span><span class="sxs-lookup"><span data-stu-id="a5f68-156">Code example: Create a data source provider for custom PerformancePoint Services tabular data sources in SharePoint</span></span>
<span data-ttu-id="a5f68-157"><a name="bk_example"> </a></span><span class="sxs-lookup"><span data-stu-id="a5f68-157"><a name="bk_example"> </a></span></span>

<span data-ttu-id="a5f68-158">В классе в следующем примере кода создается поставщик табличного источника данных, который извлекает котировки акций из внешней веб-службы и преобразует эти данные в табличный формат.</span><span class="sxs-lookup"><span data-stu-id="a5f68-158">The class in the following code example creates a tabular data source provider that retrieves stock quotes from an external Web service and then transforms the data into a tabular format.</span></span>
  
    
    
<span data-ttu-id="a5f68-159">Перед компиляцией этого примера кода необходимо настроить среду разработки, как описано в статье  [Создание поставщики источников данных для настраиваемых Службы PerformancePoint Services табличные источники данных](#BKMK_CreateClass).</span><span class="sxs-lookup"><span data-stu-id="a5f68-159">Before you can compile this code example, you must configure your development environment as described in  [Create data source providers for custom PerformancePoint Services tabular data sources](#BKMK_CreateClass).</span></span>
  
    
    



```cs

using System;
using System.Data;
using System.IO;
using System.Linq;
using System.Xml.Linq;
using Microsoft.PerformancePoint.Scorecards;
using Microsoft.PerformancePoint.Scorecards.ServerCommon;
using Microsoft.PerformancePoint.SDK.Samples.StockQuotes;
using System.ServiceModel;

namespace Microsoft.PerformancePoint.SDK.Samples.SampleDataSource
{

    // Represents the class that defines the sample data source provider.
    // It inherits from the BasicTabularDataSourceProvider class, which
    // contains overridden abstract methods that are not implemented.
    public class WSTabularDataSourceProvider : BasicTabularDataSourceProvider
    {
        #region Constants
        private const int StockSymbolsIndex = 0;
        private const int CacheFileLocationIndex = 1;
        private const int ProxyAddressIndex = 2;
        #endregion

        #region Properties

        // This property stores the stock symbols that are used
        // to query the Web service.
        // Its value is obtained by parsing the CustomData property
        // of the data source object. 
        private string[] StockSymbols
        {
            get;
            set;
        }

        // The address of the proxy server.
        private Uri ProxyAddress
        {
            get;
            set;
        }

        // This property is not used by PerformancePoint Services.
        // Its intended use is for custom applications to indicate
        // whether a provider stores sensitive information in the
        // connection string, such as user name and password.
        // This sample does not, so it returns false. 
        public override bool IsConnectionStringSecure
        {
            get { return false; }
        }
        #endregion

        #region Overridden methods

        // The source name for your data source. This value must match the key
        // attribute that is registered in the web.config file.
        public override string GetId()
        {
            return "WSTabularDataSource";
        }

        // Add column mappings for the sample columns if they do not exist.
        // Column mappings may be missing if the custom data source has never
        // been edited or if the workspace was not refreshed, which saves
        // changes to the server.
        public override void SetDataSource(DataSource dataSource)
        {

            base.SetDataSource(dataSource);

            // Check for symbols stored in the CustomData
            // property of the data source.
            if (null == dataSource ||
                 string.IsNullOrEmpty(dataSource.CustomData))
            {

                // Create a symbol for testing purposes.
                StockSymbols = new[] { "MSFT" };
            }
            else
            {
                string[] splitCustomData = dataSource.CustomData.Split('&amp;');
                if (splitCustomData.Length > 2)
                {
                    StockSymbols = splitCustomData[StockSymbolsIndex].ToUpper().Split(',');
                    for (int iLoop = 0; iLoop < StockSymbols.Length; iLoop++)
                    {
                        StockSymbols[iLoop] = StockSymbols[iLoop].Trim();
                    }

                    SampleDSCacheHandler.CacheFileLocation = splitCustomData[CacheFileLocationIndex];
                    ProxyAddress = new Uri(splitCustomData[ProxyAddressIndex]);
                }
            }

            // Check whether column mappings exist. Do not overwrite them.
            if (dataSource.DataTableMapping.ColumnMappings.Count == 0)
            {
                dataSource.DataTableMapping = CreateDataColumnMappings();
            }
        }

        // Get the data from the data source.
        // GetDataSet contains the core logic for the provider.
        public override DataSet GetDataSet()
        {

            // Create a dataset and a data table to store the data.
            DataSet resultSet = new DataSet();
            DataTable resultTable = resultSet.Tables.Add();

            // Define column names and the type of data that they contain. 
            resultTable.Columns.Add("Symbol", typeof(string));
            resultTable.Columns.Add("Value", typeof(float));
            resultTable.Columns.Add("P-E Ratio", typeof(float));
            resultTable.Columns.Add("Percentage Change", typeof(float));
            resultTable.Columns.Add("Date", typeof(DateTime));

            FillResultTable(ref resultTable);

            return resultSet;
        }
        #endregion

        #region Internal methods

        // Fill the data table with the stock quote values from
        // the Web service and local cache file.
        protected void FillResultTable(ref DataTable resultsTable)
        {

            // Check the sematic validity of symbols (out of scope for this sample).
            if (null != StockSymbols &amp;&amp;
                StockSymbols.Length > 0 &amp;&amp;
                !string.IsNullOrEmpty(SampleDSCacheHandler.CacheFileLocation))
            {
                try
                {
                    if (!File.Exists(SampleDSCacheHandler.CacheFileLocation))
                    {

                        // Create the cache file.
                        XDocument doc = SampleDSCacheHandler.DefaultCacheFileContent;
                        doc.Save(@SampleDSCacheHandler.CacheFileLocation);
                    }

                    // Get real-time quotes and update cache file.
                    string wsResult = GetLiveQuote();

                    SampleDSCacheHandler.UpdateXMLCacheFile(wsResult);

                    // Check if a valid cache file location exists.
                    if (SampleDSCacheHandler.CacheFileContent != null)
                    {
                        var query = from c in SampleDSCacheHandler.CacheFileContent.Elements("StockQuotes").Elements("StockQuote")
                                    where StockSymbols.Contains(c.Attribute("Symbol").Value)
                                    select c;

                        foreach (var stockQuote in query)
                        {
                            DataRow row = resultsTable.NewRow();
                            row["Symbol"] = stockQuote.Attribute("Symbol").Value;
                            row["Value"] = stockQuote.Element("Value").Value;
                            row["Percentage Change"] = stockQuote.Element("PercentageChange").Value;
                            row["Date"] = stockQuote.Element("Date").Value;

                            decimal peRatio;

                            // Handle symbols that return 'N/A' for this field.
                            if (decimal.TryParse(stockQuote.Element("PERatio").Value, out peRatio))
                            {
                                row["P-E Ratio"] = peRatio;
                            }

                            resultsTable.Rows.Add(row);
                        }
                    }
                }
                catch (Exception ex)
                {
                    ServerUtils.HandleException(ex);
                }
            }
        }

        // Get real-time quotes from the Web service.
        protected string GetLiveQuote()
        {
            EndpointAddress endpoint = new EndpointAddress("http://www.webservicex.net/stockquote.asmx");
            BasicHttpBinding binding = new BasicHttpBinding();
            binding.ReceiveTimeout = new TimeSpan(0, 0, 120);
            binding.ProxyAddress = ProxyAddress;
            binding.UseDefaultWebProxy = false;

            StockQuotes.StockQuoteSoapClient wsStockQuoteService = new StockQuoteSoapClient(binding, endpoint);

            // Check the sematic validity of symbols (out of scope for this sample).
            if (null != StockSymbols &amp;&amp;
                StockSymbols.Length > 0)
            {
                try
                {
                    string quoteRequest = StockSymbols[0];
                    for (int iLoop = 1; iLoop < StockSymbols.Length; iLoop++)
                    {
                        quoteRequest = string.Format("{0}, {1}", quoteRequest, StockSymbols[iLoop]);
                    }

                    string wsResult = wsStockQuoteService.GetQuote(quoteRequest);
                    return wsResult;
                }
                catch (Exception ex)
                {
                    ServerUtils.HandleException(ex);
                }
            }
            return string.Empty;
        }

        // Create the column mappings.
        internal static DataTableMapping CreateDataColumnMappings()
        {
            DataTableMapping dtTableMapping = new DataTableMapping();

            // Define the data in the Symbol column as dimension data.
            dtTableMapping.ColumnMappings.Add(new DataColumnMapping
            {
                SourceColumnName = "Symbol",
                FriendlyColumnName = "Symbol",
                UniqueName = "Symbol",
                ColumnType = MappedColumnTypes.Dimension,
                FactAggregation = FactAggregations.None,
                ColumnDataType = MappedColumnDataTypes.String
            });

            // Define the data in the Value column as fact data.
            dtTableMapping.ColumnMappings.Add(new DataColumnMapping
            {
                SourceColumnName = "Value",
                FriendlyColumnName = "Value",
                UniqueName = "Value",
                ColumnType = MappedColumnTypes.Fact,
                FactAggregation = FactAggregations.Average,
                ColumnDataType = MappedColumnDataTypes.Number
            });

            // Define the data in the P-E Ratio column as fact data.
            dtTableMapping.ColumnMappings.Add(new DataColumnMapping
            {
                SourceColumnName = "P-E Ratio",
                FriendlyColumnName = "P-E Ratio",
                UniqueName = "P-E Ratio",
                ColumnType = MappedColumnTypes.Fact,
                FactAggregation = FactAggregations.Average,
                ColumnDataType = MappedColumnDataTypes.Number
            });

            // Define the data in the Percentage Change column as fact data.
            dtTableMapping.ColumnMappings.Add(new DataColumnMapping
            {
                SourceColumnName = "Percentage Change",
                FriendlyColumnName = "Percentage Change",
                UniqueName = "Percentage Change",
                ColumnType = MappedColumnTypes.Fact,
                FactAggregation = FactAggregations.Average,
                ColumnDataType = MappedColumnDataTypes.Number
            });

            // Define the Date column as a time dimension.
            dtTableMapping.ColumnMappings.Add(new DataColumnMapping
            {
                SourceColumnName = "Date",
                FriendlyColumnName = "Date",
                UniqueName = "Date",
                ColumnType = MappedColumnTypes.TimeDimension,
                FactAggregation = FactAggregations.None,
                ColumnDataType = MappedColumnDataTypes.DateTime
            });

            // Increase the granularity of the time dimension.
            dtTableMapping.DateAggregationType |= DateAggregationTypes.Quarter;
            dtTableMapping.DateAggregationType |= DateAggregationTypes.Month;
            dtTableMapping.DateAggregationType |= DateAggregationTypes.Week;
            dtTableMapping.DateAggregationType |= DateAggregationTypes.Day;

            return dtTableMapping;
        }
        #endregion
    }
}

```


## <a name="next-steps"></a><span data-ttu-id="a5f68-160">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a5f68-160">Next steps</span></span>
<span data-ttu-id="a5f68-161"><a name="bk_next"> </a></span><span class="sxs-lookup"><span data-stu-id="a5f68-161"><a name="bk_next"> </a></span></span>

<span data-ttu-id="a5f68-162">После создания поставщика источника данных и источник данных редактора (включая его пользовательского интерфейса, при необходимости), развертывание данное расширение имени файла, как описано в  [Регистрация расширений служб PerformancePoint вручную](http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="a5f68-162">After you create a data source provider and a data source editor (including its user interface, if required), deploy the extension as described in  [How to: Manually Register PerformancePoint Services Extensions](http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx).</span></span> 
  
    
    

## <a name="see-also"></a><span data-ttu-id="a5f68-163">См. также</span><span class="sxs-lookup"><span data-stu-id="a5f68-163">See also</span></span>
<span data-ttu-id="a5f68-164"><a name="bk_addResources"> </a></span><span class="sxs-lookup"><span data-stu-id="a5f68-164"><a name="bk_addResources"> </a></span></span>


-  [<span data-ttu-id="a5f68-165">Как: создание табличных данных редакторы исходного для служб PerformancePoint Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="a5f68-165">How to: Create tabular data source editors for PerformancePoint Services in SharePoint</span></span>](how-to-create-tabular-data-source-editors-for-performancepoint-services-in-share.md)
    
  
-  [<span data-ttu-id="a5f68-166">PerformancePoint Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="a5f68-166">PerformancePoint Services in SharePoint</span></span>](performancepoint-services-in-sharepoint.md)
    
  

