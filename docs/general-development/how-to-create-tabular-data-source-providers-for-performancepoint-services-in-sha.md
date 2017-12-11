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
# <a name="create-tabular-data-source-providers-for-performancepoint-services-in-sharepoint"></a>Создание поставщиков табличных источников данных для служб PerformancePoint Services в SharePoint

Узнайте, как создать компонент поставщика источника данных в модуле пользовательских табличных источников данных для Службы PerformancePoint Services.

## <a name="what-are-custom-data-source-providers-for-performancepoint-services"></a>Что такое настраиваемых поставщиков источников данных для Службы PerformancePoint Services ?
<a name="bk_intro"> </a>

Поставщики источников данных подключения к источнику данных, доступ к данным и затем возврата результатов. Службы PerformancePoint Services использует поставщиков табличных источников данных для доступа к данным из Excel и Службы Excel листы, списки SharePoint и Microsoft SQL Server таблицы. Можно создать поставщика настраиваемого источника данных, чтобы использовать данные из источника табличных данных, не поддерживаемый Службы PerformancePoint Services.
  
    
    
Основная функция поставщика источника табличных данных  создание и заполнение таблицу данных с данными из источника данных. Он также создает сопоставления столбцов, чтобы определить тип данных, что каждый столбец содержит (фактов, измерений или измерение времени). Базовая структура многомерные применяется к табличных данных.
  
    
    
Инструкции и примеры кода в этом разделе основаны на класс **WSTabularDataSourceProvider** из [настраиваемых объектов](http://msdn.microsoft.com/library/af021d52-7562-4e7a-9de4-e1fc5784a59d%28Office.15%29.aspx). Поставщик извлекает акций внешних веб-службе для указанного символов акций. Хранит данные журнала запасов квоты в файл кэша, который позволяет данные срез по времени. Полный код для класса, в разделе [пример кода: Создание поставщика источника данных для настраиваемых служб PerformancePoint Services табличные источники данных в SharePoint](#bk_example).
  
    
    
Мы рекомендуем использовать примера поставщика источника данных в качестве шаблона. В примере показано, как вызывать объекты в Службы PerformancePoint Services API и демонстрируется советы и рекомендации по разработке Службы PerformancePoint Services.
  
    
    

## <a name="create-data-source-providers-for-custom-performancepoint-services-tabular-data-sources"></a>Создание поставщики источников данных для настраиваемых Службы PerformancePoint Services табличные источники данных
<a name="BKMK_CreateClass"> </a>


1. Установка Службы PerformancePoint Services или копирование библиотеки DLL, которые использует расширения (перечисленных в шаге 3) на своем компьютере. Сведения содержатся в разделе  [Библиотеки DLL служб PerformancePoint, используемые в сценариях развертывания](http://msdn.microsoft.com/library/41e92619-8253-481d-82f9-35b6a6abc477%28Office.15%29.aspx).
    
  
2. В Visual Studio создайте библиотеку классов C#. Если библиотека классов для расширения уже создана, добавьте новый класс C#.
    
    DLL-библиотеку необходимо подписать строгим именем. Кроме того, убедитесь, что все сборки, на которые ссылается DLL-библиотека, имеют строгие имена. Процедура подписывания сборки строгим именем и создания пары из открытого и закрытого ключа рассматривается в разделе  [How to: Create a Public/Private Key Pair](http://msdn.microsoft.com/library/05026813-f3bd-4d7c-9e0b-fc588eb3d114.aspx).
    
  
3. Добавьте следующие Службы PerformancePoint Services библиотеки DLL в качестве ссылок на сборки в проект:
    
  - Microsoft.PerformancePoint.Scorecards.Client.dll
    
  
  - Microsoft.PerformancePoint.Scorecards.DataSourceProviders.Standard.dll
    
  

    В этом примере поставщика данных также используются ссылки на сборки System.Core.dll, System.ServiceModel.dll, System.Web.dll, System.Web.Services.dll и System.Xml.Linq.dll. В зависимости от функциональных возможностей расширения могут потребоваться другие сборки.
    
  
4. Добавьте ссылку на службу с именем **StockQuotes**, которая ссылается на веб-службу, расположенную по адресу  `http://www.webservicex.net/stockquote.asmx`. Эта веб-служба предоставляет котировки акций для примера поставщика источника данных.
    
  
5. Добавьте классы **BasicTabularDataSourceProvider** и **SampleDSCacheHandler** из примера в проект. Класс **BasicTabularDataSourceProvider** наследуется от класса [TabularDataSourceProvider](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSourceProviders.TabularDataSourceProvider.aspx) , который является базовым для поставщиков табличных источников данных.
    
    В этом примере источника данных также используется класс-контейнер для переопределенных абстрактных методов, которые не реализуются классом  [TabularDataSourceProvider](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSourceProviders.TabularDataSourceProvider.aspx) ( [GetDatabaseNames()](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.CustomDataSourceProvider.GetDatabaseNames.aspx) , [GetCubeNames()](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.CustomDataSourceProvider.GetCubeNames.aspx) , [GetCubeNameInfos()](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.CustomDataSourceProvider.GetCubeNameInfos.aspx) , [GetCubeMetaData](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.CustomDataSourceProvider.GetCubeMetaData.aspx) и [Validate()](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.CustomDataSourceProvider.Validate.aspx) ).
    
  
6. В классе поставщика добавьте директивы **using** для следующих пространств имен Службы PerformancePoint Services.
    
  -  [Microsoft.PerformancePoint.Scorecards](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.aspx)
    
  
  -  [Microsoft.PerformancePoint.Scorecards.ServerCommon](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.ServerCommon.aspx)
    
  
  - **Microsoft.PerformancePoint.SDK.Samples.StockQuotes** (представляет ссылку на службу StockQuotes, созданную на шаге 4)
    
  

    В зависимости от функциональности расширения могут потребоваться другие директивы **using**.
    
  
7. Наследуется от класса **BasicTabularDataSourceProvider**.
    
  
8. Объявите переменные и определите свойства, которые используются для синтаксического анализа, хранения и извлечения символов акций, местоположения файла кэша и идентификатора URI прокси-сервера.
    
  
9. Переопределите свойство  [IsConnectionStringSecure](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.CustomDataSourceProvider.IsConnectionStringSecure.aspx) . Это свойство не используется Службы PerformancePoint Services, но он предназначен для пользовательских приложений при необходимости использовать для определения, является ли строка подключения предоставляет сведения, которые могут привести к риску.
    
    Задайте возврат значения **true**, если в строке подключения к источнику данных в расширении содержатся конфиденциальные сведения, например, имя пользователя или пароль. Задайте возврат значения **false**, если конфиденциальные сведения не хранятся, или источник данных не использует строку подключения.
    
  
10. Переопределите метод  [GetId()](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.CustomDataSourceProvider.GetId.aspx) возвращает уникальный идентификатор для поставщика. [GetId()](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Extensions.CustomDataSourceProvider.GetId.aspx) должен возвращать ту же строку в качестве атрибута **key**, который зарегистрирован в файле web.config Службы PerformancePoint Services для поставщика настраиваемого источника данных.
    
  
11. Переопределите метод  [SetDataSource](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSourceProviders.TabularDataSourceProvider.SetDataSource.aspx) и определите сопоставления столбцов. Метод [SetDataSource](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSourceProviders.TabularDataSourceProvider.SetDataSource.aspx) вызывает метод **CreateDataColumnMappings**, чтобы определить столбцы источника данных как типы  [Fact](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.MappedColumnTypes.Fact.aspx) , [Dimension](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.MappedColumnTypes.Dimension.aspx) и [TimeDimension](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.MappedColumnTypes.TimeDimension.aspx) .
    
     Метод  [SetDataSource](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSourceProviders.TabularDataSourceProvider.SetDataSource.aspx) также извлекает символы акций, местоположение файла кэша и адрес прокси-сервера из свойства [CustomData](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSource.CustomData.aspx) объекта настраиваемого источника данных. Эти значения определяются автором панели мониторинга в редакторе примера источника данных.
    
  
12. Переопределите метод  [GetDataSet()](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSourceProviders.TabularDataSourceProvider.GetDataSet.aspx) и создайте объект [DataSet](https://msdn.microsoft.com/library/System.Data.DataSet.aspx) для хранения данных из источника. В примере источника данных для заполнения таблицы данными из веб-службы используются методы **FillResultsTable** и **GetLiveQuote**.
    
  

## <a name="code-example-create-a-data-source-provider-for-custom-performancepoint-services-tabular-data-sources-in-sharepoint"></a>Пример кода: Создание поставщика источника данных для настраиваемых служб PerformancePoint Services табличные источники данных в SharePoint
<a name="bk_example"> </a>

В классе в следующем примере кода создается поставщик табличного источника данных, который извлекает котировки акций из внешней веб-службы и преобразует эти данные в табличный формат.
  
    
    
Перед компиляцией этого примера кода необходимо настроить среду разработки, как описано в статье  [Создание поставщики источников данных для настраиваемых Службы PerformancePoint Services табличные источники данных](#BKMK_CreateClass).
  
    
    



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


## <a name="next-steps"></a>Дальнейшие действия
<a name="bk_next"> </a>

После создания поставщика источника данных и источник данных редактора (включая его пользовательского интерфейса, при необходимости), развертывание данное расширение имени файла, как описано в  [Регистрация расширений служб PerformancePoint вручную](http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx). 
  
    
    

## <a name="see-also"></a>См. также
<a name="bk_addResources"> </a>


-  [Как: создание табличных данных редакторы исходного для служб PerformancePoint Services в SharePoint](how-to-create-tabular-data-source-editors-for-performancepoint-services-in-share.md)
    
  
-  [PerformancePoint Services в SharePoint](performancepoint-services-in-sharepoint.md)
    
  

