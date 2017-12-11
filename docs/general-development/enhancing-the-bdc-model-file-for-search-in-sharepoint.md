---
title: "Улучшение файла модели BDC для поиска в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 3c67b1cf-5fca-4805-a1b5-c9ac1ff8aede
ms.openlocfilehash: 26b06db6e478c15d47257b8a88de30da1f0bb0c1
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="enhancing-the-bdc-model-file-for-search-in-sharepoint"></a><span data-ttu-id="306d1-102">Улучшение файла модели BDC для поиска в SharePoint</span><span class="sxs-lookup"><span data-stu-id="306d1-102">Enhancing the BDC model file for Search in SharePoint</span></span>
<span data-ttu-id="306d1-103">Сведения о свойствах в модели метаданных BDC, которые могут быть применены соединители индексации BCS, позволяющие поиска в SharePoint для обхода внешних данных.</span><span class="sxs-lookup"><span data-stu-id="306d1-103">Learn about the properties in the BDC metadata model that are applicable to BCS indexing connectors which enable Search in SharePoint to crawl external data.</span></span>
## <a name="search-properties-for-bdc-model-files"></a><span data-ttu-id="306d1-104">Свойства поиска для файлов модели BDC</span><span class="sxs-lookup"><span data-stu-id="306d1-104">Search properties for BDC model files</span></span>
<span data-ttu-id="306d1-105"><a name="SearchBDCModelProperties_SearchProperties"> </a></span><span class="sxs-lookup"><span data-stu-id="306d1-105"></span></span>

<span data-ttu-id="306d1-p101">Платформа соединителей в Поиск позволяет обхода внешних данных, делая ее доступной в результатах поиска через соединители индексации BCS. Соединитель индексации BCS используется программой-обходчиком для взаимодействия с внешнего источника данных. Во время обхода контента программа-обходчик вызывает соединителя индексации BCS для извлечения данных из внешней системы и передать его программы-обходчика.</span><span class="sxs-lookup"><span data-stu-id="306d1-p101">The connector framework in Search enables you to crawl external data, making it available in search results through BCS indexing connectors. The BCS indexing connector is used by the crawler to communicate with the external data source. At crawl time, the crawler calls the BCS indexing connector to fetch the data from the external system and pass it back to the crawler.</span></span> 
  
    
    
<span data-ttu-id="306d1-109">Соединители индексации BCS состоят из следующих:</span><span class="sxs-lookup"><span data-stu-id="306d1-109">BCS indexing connectors are composed of the following:</span></span>
  
    
    


  
    
    
> <span data-ttu-id="306d1-110">**Файл модели BDC** Файл, который предоставляет данные для подключения к внешней системе и структуру данных.</span><span class="sxs-lookup"><span data-stu-id="306d1-110">**BDC model file** The file that provides the connection information to the external system and the structure of the data.</span></span>
    
  

  
    
    
> <span data-ttu-id="306d1-111">**Соединитель** Компонент, содержащий код, который подключается к внешней системе и анализ доступа идентификаторы URL-адреса и BCS.</span><span class="sxs-lookup"><span data-stu-id="306d1-111">**Connector** The component containing the code that connects to the external system and parses the access URLs and BCS identifiers.</span></span>
    
  
<span data-ttu-id="306d1-112">Модель метаданных BDC включает несколько свойств, которые могут быть применены к Поиск, многие из которых требуются для поддержки соединителя индексации BCS обхода контента.</span><span class="sxs-lookup"><span data-stu-id="306d1-112">The BDC metadata model includes several properties that are applicable to Search, many of which are required to support BCS indexing connector crawling.</span></span> 
  
    
    
<span data-ttu-id="306d1-113">В следующей таблице описываются свойства модели BDC, которые могут быть применены к Поиск.</span><span class="sxs-lookup"><span data-stu-id="306d1-113">The following table describes the BDC model properties that are applicable to Search.</span></span>
  
    
    

<span data-ttu-id="306d1-114">**Таблица 1. Свойства поиска для файлов модели BDC**</span><span class="sxs-lookup"><span data-stu-id="306d1-114">**Table 1. Search properties for BDC model files**</span></span>


|<span data-ttu-id="306d1-115">**Имя**</span><span class="sxs-lookup"><span data-stu-id="306d1-115">**Name**</span></span>|<span data-ttu-id="306d1-116">**Объект метаданных**</span><span class="sxs-lookup"><span data-stu-id="306d1-116">**Metadata Object**</span></span>|<span data-ttu-id="306d1-117">**Описание**</span><span class="sxs-lookup"><span data-stu-id="306d1-117">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="306d1-118">ShowInSearchUI</span><span class="sxs-lookup"><span data-stu-id="306d1-118">ShowInSearchUI</span></span>  <br/> |<span data-ttu-id="306d1-119">Model</span><span class="sxs-lookup"><span data-stu-id="306d1-119">Model</span></span>  <br/> |<span data-ttu-id="306d1-p102">Указывает, что элемент **LobSystemInstance** в файле модели должен отображаться в пользовательском интерфейсе поиска. Это значение для настраиваемых соединителей не учитывается.</span><span class="sxs-lookup"><span data-stu-id="306d1-p102">Specifies that an **LobSystemInstance** element in the model file should be displayed in the search user interface. This value is ignored for custom connectors. </span></span><br/> |
|<span data-ttu-id="306d1-122">InputUriProcessor</span><span class="sxs-lookup"><span data-stu-id="306d1-122">InputUriProcessor</span></span>  <br/> |<span data-ttu-id="306d1-123">Бизнес-системы</span><span class="sxs-lookup"><span data-stu-id="306d1-123">LobSystem</span></span>  <br/> |<span data-ttu-id="306d1-p103">Задает имя класса, который обрабатывает ввода URL-адреса перед передачей их в соединитель. Применяется к .NET и настраиваемые соединители индексации BCS. Для получения дополнительных сведений см  [Создание настраиваемого соединителя индексации](http://msdn.microsoft.com/library/ec2df34d-178c-4ae1-a2b0-a6af04ee57bd%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="306d1-p103">Specifies the name of the class that processes the input URL before passing it to the connector. Applies to .NET and custom BCS indexing connectors. For more information, see  [Creating a Custom Indexing Connector](http://msdn.microsoft.com/library/ec2df34d-178c-4ae1-a2b0-a6af04ee57bd%28Office.15%29.aspx).  </span></span><br/> |
|<span data-ttu-id="306d1-127">OutputUriProcessor</span><span class="sxs-lookup"><span data-stu-id="306d1-127">OutputUriProcessor</span></span>  <br/> |<span data-ttu-id="306d1-128">Бизнес-системы</span><span class="sxs-lookup"><span data-stu-id="306d1-128">LobSystem</span></span>  <br/> |<span data-ttu-id="306d1-p104">Задает имя класса, который обрабатывает URL-адрес выходных данных перед передачей их в поисковой системе из соединитель. Применяется к .NET и настраиваемые соединители индексации BCS. Для получения дополнительных сведений см  [Создание настраиваемого соединителя индексации](http://msdn.microsoft.com/library/ec2df34d-178c-4ae1-a2b0-a6af04ee57bd%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="306d1-p104">Specifies the name of the class that processes the output URL before passing it to the search system from the connector. Applies to .NET and custom BCS indexing connectors. For more information, see  [Creating a Custom Indexing Connector](http://msdn.microsoft.com/library/ec2df34d-178c-4ae1-a2b0-a6af04ee57bd%28Office.15%29.aspx).  </span></span><br/> |
|<span data-ttu-id="306d1-132">SystemUtilityTypeName</span><span class="sxs-lookup"><span data-stu-id="306d1-132">SystemUtilityTypeName</span></span>  <br/> |<span data-ttu-id="306d1-133">Бизнес-системы</span><span class="sxs-lookup"><span data-stu-id="306d1-133">LobSystem</span></span>  <br/> |<span data-ttu-id="306d1-p105">Указывает имя класса, реализующего класс **StructuredRepositorySystemUtility**. Применяется к настраиваемые соединители индексации BCS. Для получения дополнительных сведений см [Создание настраиваемого соединителя индексации](http://msdn.microsoft.com/library/ec2df34d-178c-4ae1-a2b0-a6af04ee57bd%28Office.15%29.aspx). </span><span class="sxs-lookup"><span data-stu-id="306d1-p105">Specifies the name of the class that implements the **StructuredRepositorySystemUtility** class. Applies to custom BCS indexing connectors. For more information, see [Creating a Custom Indexing Connector](http://msdn.microsoft.com/library/ec2df34d-178c-4ae1-a2b0-a6af04ee57bd%28Office.15%29.aspx).  </span></span><br/> |
|<span data-ttu-id="306d1-137">Название</span><span class="sxs-lookup"><span data-stu-id="306d1-137">Title</span></span>  <br/> |<span data-ttu-id="306d1-138">Entity</span><span class="sxs-lookup"><span data-stu-id="306d1-138">Entity</span></span>  <br/> |<span data-ttu-id="306d1-139">Указывает заголовок внешнего типа контента, отображаемый в результатах поиска.</span><span class="sxs-lookup"><span data-stu-id="306d1-139">Specifies the title of the external content type to display in search results.</span></span>  <br/> |
|<span data-ttu-id="306d1-140">DefaultLocale</span><span class="sxs-lookup"><span data-stu-id="306d1-140">DefaultLocale</span></span>  <br/> |<span data-ttu-id="306d1-141">Entity</span><span class="sxs-lookup"><span data-stu-id="306d1-141">Entity</span></span>  <br/> |<span data-ttu-id="306d1-p106">Указывает строку языковых стандартов. Это значение можно переопределить с помощью свойства **LCIDField** или **CultureField**. </span><span class="sxs-lookup"><span data-stu-id="306d1-p106">Specifies the locale string. You can override this value by using the **LCIDField** property or the **CultureField** property. </span></span><br/> |
|<span data-ttu-id="306d1-144">RootFinder</span><span class="sxs-lookup"><span data-stu-id="306d1-144">RootFinder</span></span>  <br/> |<span data-ttu-id="306d1-145">Метод</span><span class="sxs-lookup"><span data-stu-id="306d1-145">Method</span></span>  <br/> |<span data-ttu-id="306d1-p107">Указывает метод **Finder**, используемый для перечисления документов, предназначенных для обхода. Например, при подключении к базе данных это может быть инструкция **SELECT** или список таблиц для обхода. </span><span class="sxs-lookup"><span data-stu-id="306d1-p107">Specifies the **Finder** method to use to enumerate the items to crawl. For example, when connecting to a database, this could be the **SELECT** statement or the list of tables to crawl. </span></span><br/> |
|<span data-ttu-id="306d1-148">DirectoryLink</span><span class="sxs-lookup"><span data-stu-id="306d1-148">DirectoryLink</span></span>  <br/> |<span data-ttu-id="306d1-149">Метод</span><span class="sxs-lookup"><span data-stu-id="306d1-149">Method</span></span>  <br/> |<span data-ttu-id="306d1-p108">Указывает, что BCS должен перейти связей. Требуется для иерархической обхода контента.</span><span class="sxs-lookup"><span data-stu-id="306d1-p108">Specifies that BCS should navigate associations. Required for hierarchical crawling.</span></span>  <br/> |
|<span data-ttu-id="306d1-152">DeletedCountField</span><span class="sxs-lookup"><span data-stu-id="306d1-152">DeletedCountField</span></span>  <br/> |<span data-ttu-id="306d1-153">Метод</span><span class="sxs-lookup"><span data-stu-id="306d1-153">Method</span></span>  <br/> |<span data-ttu-id="306d1-p109">Указывает количество удаленных элементов. Это свойство не учитывается, если его значение меньше или равно нулю.</span><span class="sxs-lookup"><span data-stu-id="306d1-p109">Specifies the deleted count value. This property is ignored unless it contains an integer greater than zero.</span></span>  <br/> |
|<span data-ttu-id="306d1-156">WindowsSecurityDescriptorField</span><span class="sxs-lookup"><span data-stu-id="306d1-156">WindowsSecurityDescriptorField</span></span>  <br/> |<span data-ttu-id="306d1-157">Метод</span><span class="sxs-lookup"><span data-stu-id="306d1-157">Method</span></span>  <br/> |<span data-ttu-id="306d1-p110">Указывает для элемента дескриптор безопасности Windows. Если дескриптор не указан, вызывается метод **GetSecurityDescriptor**. Если метод **GetSecurityDescriptor** не определен, всем внешним элементам назначается список управления доступом (ACL) "Все". </span><span class="sxs-lookup"><span data-stu-id="306d1-p110">Specifies the Windows Security descriptor for the item. If not specified, the **GetSecurityDescriptor** method is called. If the **GetSecurityDescriptor** is not defined, all external items are assigned the Everyone access control list (ACL). </span></span><br/> |
|<span data-ttu-id="306d1-161">AuthorField</span><span class="sxs-lookup"><span data-stu-id="306d1-161">AuthorField</span></span>  <br/> |<span data-ttu-id="306d1-162">Метод</span><span class="sxs-lookup"><span data-stu-id="306d1-162">Method</span></span>  <br/> |<span data-ttu-id="306d1-163">Указывает имя автора, отображаемое в результатах поиска.</span><span class="sxs-lookup"><span data-stu-id="306d1-163">Specifies the author name to display in search results.</span></span>  <br/> |
|<span data-ttu-id="306d1-164">DisplayUriField</span><span class="sxs-lookup"><span data-stu-id="306d1-164">DisplayUriField</span></span>  <br/> |<span data-ttu-id="306d1-165">Метод</span><span class="sxs-lookup"><span data-stu-id="306d1-165">Method</span></span>  <br/> |<span data-ttu-id="306d1-p111">Задает URL-адрес для отображения в результатах поиска. Если указан, то это свойство переопределяет предоставлено BCS URL-адрес страницы профиля. Если не указан, отображаются в результатах поиска URL-адрес начинается с **bdc3: / /** и не понятен обозревателя.</span><span class="sxs-lookup"><span data-stu-id="306d1-p111">Specifies the URL to display in search results. If specified, this property overrides the profile page URL provided by BCS. If not specified, the URL displayed in search results starts with **bdc3://**, and is not understood by the browser. </span></span><br/> |
|<span data-ttu-id="306d1-169">LastModifiedTimeStampField</span><span class="sxs-lookup"><span data-stu-id="306d1-169">LastModifiedTimeStampField</span></span>  <br/> |<span data-ttu-id="306d1-170">Метод</span><span class="sxs-lookup"><span data-stu-id="306d1-170">Method</span></span>  <br/> |<span data-ttu-id="306d1-p112">Указывает отметку времени внешнего элемента, отображаемую в результатах поиска. Это значение также используется для добавочного обхода.</span><span class="sxs-lookup"><span data-stu-id="306d1-p112">Specifies the external item's timestamp to display in search results. This value is also used for incremental crawling.</span></span>  <br/> |
|<span data-ttu-id="306d1-173">DescriptionField</span><span class="sxs-lookup"><span data-stu-id="306d1-173">DescriptionField</span></span>  <br/> |<span data-ttu-id="306d1-174">Метод</span><span class="sxs-lookup"><span data-stu-id="306d1-174">Method</span></span>  <br/> |<span data-ttu-id="306d1-175">Указывает описание, отображаемое в результатах поиска.</span><span class="sxs-lookup"><span data-stu-id="306d1-175">Specifies the description to display in search results.</span></span>  <br/> |
|<span data-ttu-id="306d1-176">LCIDField</span><span class="sxs-lookup"><span data-stu-id="306d1-176">LCIDField</span></span>  <br/> |<span data-ttu-id="306d1-177">Метод</span><span class="sxs-lookup"><span data-stu-id="306d1-177">Method</span></span>  <br/> |<span data-ttu-id="306d1-p113">Указывает код языка (LCID) для **DescriptionField**. Если это значение не указано, используется средство разбиения текста на слова по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="306d1-p113">Specifies the locale ID (LCID) for the **DescriptionField**. If this is not specified, the default word breaker is used.  </span></span><br/> |
|<span data-ttu-id="306d1-180">CultureField</span><span class="sxs-lookup"><span data-stu-id="306d1-180">CultureField</span></span>  <br/> |<span data-ttu-id="306d1-181">Метод</span><span class="sxs-lookup"><span data-stu-id="306d1-181">Method</span></span>  <br/> |<span data-ttu-id="306d1-182">Указывает культуру для **DescriptionField**.</span><span class="sxs-lookup"><span data-stu-id="306d1-182">Specifies the culture for the **DescriptionField**.</span></span>  <br/> |
|<span data-ttu-id="306d1-183">Расширение</span><span class="sxs-lookup"><span data-stu-id="306d1-183">Extension</span></span>  <br/> |<span data-ttu-id="306d1-184">Метод</span><span class="sxs-lookup"><span data-stu-id="306d1-184">Method</span></span>  <br/> |<span data-ttu-id="306d1-p114">Указывает расширение файла для потока, предназначенного для обхода. Если оно не указано, по умолчанию используется расширение **TXT**.</span><span class="sxs-lookup"><span data-stu-id="306d1-p114">Specifies the file name extension for the crawlable stream. If not specified, the default extension is **.txt**. </span></span><br/> |
|<span data-ttu-id="306d1-187">MimeType</span><span class="sxs-lookup"><span data-stu-id="306d1-187">MimeType</span></span>  <br/> |<span data-ttu-id="306d1-188">Метод</span><span class="sxs-lookup"><span data-stu-id="306d1-188">Method</span></span>  <br/> |<span data-ttu-id="306d1-p115">Указывает тип MIME для потока, предназначенного для обхода. Если тип не указан, по умолчанию используется расширение **TXT**. Если задано и поле **Extension**, и поле **MimeType**, используется значение, указанное в поле **MimeType**. </span><span class="sxs-lookup"><span data-stu-id="306d1-p115">Specifies the MIME type for the crawlable stream. If not specified, the default extension is **.txt**. If the **Extension** field and **MimeType** field are both specified, the value specified in the **MimeType** field is used. </span></span><br/> |
|<span data-ttu-id="306d1-192">UseClientCachingForSearch</span><span class="sxs-lookup"><span data-stu-id="306d1-192">UseClientCachingForSearch</span></span>  <br/> |<span data-ttu-id="306d1-193">Метод</span><span class="sxs-lookup"><span data-stu-id="306d1-193">Method</span></span>  <br/> |<span data-ttu-id="306d1-p116">Указывает, будет ли программа-обходчик кэширует контента во время перечисления. Если кэширования содержимого программа-обходчик не выполняет другой приема-передачи источник содержимого, обход отдельных элементов.</span><span class="sxs-lookup"><span data-stu-id="306d1-p116">Specifies whether the crawler caches the content during enumeration. If the content is cached, the crawler does not make another trip to the content source when it crawls individual items.</span></span>  <br/> |
|<span data-ttu-id="306d1-196">EnumerateIdsOnly</span><span class="sxs-lookup"><span data-stu-id="306d1-196">EnumerateIdsOnly</span></span>  <br/> |<span data-ttu-id="306d1-197">Дескриптор фильтра</span><span class="sxs-lookup"><span data-stu-id="306d1-197">FilterDescriptor</span></span>  <br/> |<span data-ttu-id="306d1-198">Указывает, следует ли возвращать идентификаторы только в объекте **IDEnumerator**.</span><span class="sxs-lookup"><span data-stu-id="306d1-198">Specifies whether to return IDs only in the **IDEnumerator**.</span></span>  <br/> |
|<span data-ttu-id="306d1-199">CrawlStartTime</span><span class="sxs-lookup"><span data-stu-id="306d1-199">CrawlStartTime</span></span>  <br/> |<span data-ttu-id="306d1-200">Дескриптор фильтра</span><span class="sxs-lookup"><span data-stu-id="306d1-200">FilterDescriptor</span></span>  <br/> |<span data-ttu-id="306d1-201">Содержит время начала последнего обхода.</span><span class="sxs-lookup"><span data-stu-id="306d1-201">Contains the start time of the last crawl.</span></span>  <br/> |
|<span data-ttu-id="306d1-202">SynchronizationCookie</span><span class="sxs-lookup"><span data-stu-id="306d1-202">SynchronizationCookie</span></span>  <br/> |<span data-ttu-id="306d1-203">Дескриптор фильтра</span><span class="sxs-lookup"><span data-stu-id="306d1-203">FilterDescriptor</span></span>  <br/> |<span data-ttu-id="306d1-p117">Указывает, что внешний источник контента возвращает после обхода контента куки-файл, который повторно отправляется соединителем индексации во время следующего вызова перечисления. Внешний источник контента использует куки-файл для определения изменений, произошедших с момента последнего обхода контента. Это свойство используется с экземплярами методов **ChangedIDEnumerator** и **DeletedIDEnumerator**. </span><span class="sxs-lookup"><span data-stu-id="306d1-p117">Specifies that the external content source returns a cookie after a crawl, which is then resent by the indexing connector during the next enumeration call. The external content source uses the cookie to determine what has changed since the last crawl. This property is used with **ChangedIDEnumerator** and **DeletedIDEnumerator** method instances. </span></span><br/> |
|<span data-ttu-id="306d1-207">Свойство</span><span class="sxs-lookup"><span data-stu-id="306d1-207">Property</span></span>  <br/> |<span data-ttu-id="306d1-208">Дескриптор типа</span><span class="sxs-lookup"><span data-stu-id="306d1-208">TypeDescriptor</span></span>  <br/> | <span data-ttu-id="306d1-p118">Указывает массив **struct**, используемый при поиске свойств. Этот массив состоит из следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="306d1-p118">Specifies the **struct** array used by search for properties. Consists of the following: </span></span><br/> <ul><li><span data-ttu-id="306d1-211">**PropertyName**</span><span class="sxs-lookup"><span data-stu-id="306d1-211">**PropertyName**</span></span></li><li><span data-ttu-id="306d1-212">**PropertyValue**</span><span class="sxs-lookup"><span data-stu-id="306d1-212">**PropertyValue**</span></span></li><li><span data-ttu-id="306d1-213">**PropertyCulture**</span><span class="sxs-lookup"><span data-stu-id="306d1-213">**PropertyCulture**</span></span></li></ul> |
|<span data-ttu-id="306d1-214">Text</span><span class="sxs-lookup"><span data-stu-id="306d1-214">Text</span></span>  <br/> |<span data-ttu-id="306d1-215">Дескриптор типа</span><span class="sxs-lookup"><span data-stu-id="306d1-215">TypeDescriptor</span></span>  <br/> | <span data-ttu-id="306d1-p119">Указывает массив **struct**, используемый при поиске вложений. Этот массив состоит из следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="306d1-p119">Specifies the **struct** array used by search for attachments. Consists of the following: </span></span><br/> <ul><li><span data-ttu-id="306d1-218">**TextExtension**</span><span class="sxs-lookup"><span data-stu-id="306d1-218">**TextExtension**</span></span></li><li><span data-ttu-id="306d1-219">**TextContentType**</span><span class="sxs-lookup"><span data-stu-id="306d1-219">**TextContentType**</span></span></li><li><span data-ttu-id="306d1-220">**Текст**</span><span class="sxs-lookup"><span data-stu-id="306d1-220">**TextValue**</span></span></li></ul> <br/> |
   

## <a name="bdc-model-file-changes-to-improve-performance-when-crawling-external-data"></a><span data-ttu-id="306d1-221">Изменения файла модели BDC для повышения производительности при обходе контента внешних данных</span><span class="sxs-lookup"><span data-stu-id="306d1-221">BDC model file changes to improve performance when crawling external data</span></span>
<span data-ttu-id="306d1-222"><a name="SearchBDCModelProperties_Performance"> </a></span><span class="sxs-lookup"><span data-stu-id="306d1-222"></span></span>

<span data-ttu-id="306d1-p120">Если необходимо использовать для создания файла модели BDC для внешней системы, необходимо включить для поиска, можно улучшить файл модели для оптимизации производительности при обходе контента внешних систем. В этом разделе описываются способы изменения файла модели BDC и повышения производительности.</span><span class="sxs-lookup"><span data-stu-id="306d1-p120">When you want to create a BDC model file for an external system that you want to enable for search, you can enhance the model file to optimize performance when crawling external systems. This section describes ways to modify the BDC model file to improve performance.</span></span>
  
    
    

### <a name="use-inline-property-io-when-retrieving-large-scale-data"></a><span data-ttu-id="306d1-225">Использование ввода-вывода встроенного свойства при извлечении больших объемов данных</span><span class="sxs-lookup"><span data-stu-id="306d1-225">Use inline property I/O when retrieving large-scale data</span></span>

<span data-ttu-id="306d1-226">В общем случае, если элемент возвращает большой объем данных, вместо метода **SpecificFinder** для извлечения данных следует использовать один из следующих специализированных методов:</span><span class="sxs-lookup"><span data-stu-id="306d1-226">In general, if some of the data returned for an item is large scale, instead of returning it with the **SpecificFinder** method, you should use one of the following specialized methods to retrieve the data:</span></span>
  
    
    

- <span data-ttu-id="306d1-227">Метод **BinarySecurityDescriptorAccessor** используется при передаче списка управления доступом (ACL) вместо свойства **WindowsSecurityDescriptor**.</span><span class="sxs-lookup"><span data-stu-id="306d1-227">Use the **BinarySecurityDescriptorAccessor** method when passing a security access control list (ACL) instead of the **WindowsSecurityDescriptor** property.</span></span>
    
  
- <span data-ttu-id="306d1-228">Метод **StreamAccessor** используется при передаче потоков.</span><span class="sxs-lookup"><span data-stu-id="306d1-228">Use the **StreamAccessor** method when passing streams.</span></span>
    
  
<span data-ttu-id="306d1-229">В условиях отсутствия высоких задержек в сети улучшенная производительность как правило важнее, чем затраты на дополнительное обращение к внешней системе.</span><span class="sxs-lookup"><span data-stu-id="306d1-229">Unless network latency is high, the improved performance is usually better than the cost of an extra trip to the external system.</span></span>
  
    
    

### <a name="enumeration-optimization-when-crawling-external-systems"></a><span data-ttu-id="306d1-230">Оптимизация перечисления при обходе контента внешних систем</span><span class="sxs-lookup"><span data-stu-id="306d1-230">Enumeration optimization when crawling external systems</span></span>

<span data-ttu-id="306d1-p121">Не выполняйте перечисление более 100000 элементов за одно обращение к внешней системе. При продолжительных перечислениях могут возникать периодические прерывания связи, препятствующие завершению обхода контента. Рекомендуется, чтобы модель BDC структурировала данные в логические папки, для которых можно выполнить перечисление по отдельности, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="306d1-p121">Do not enumerate more than 100,000 items per call to the external system. Long-running enumerations can cause intermittent interruptions and prevent a crawl from completing. We recommend that your BDC model structures the data into logical folders that can be enumerated individually, as shown in the following example.</span></span> 
  
    
    
<span data-ttu-id="306d1-p122">В этом примере показано перечисление для таблицы базы данных с миллионом строк, но с фиксированным набором значений в столбце ColumnA. В таком сценарии можно считать столбец ColumnA внешним типом контента и написать перечислитель для этого набора значений, используя следующую инструкцию SQL.</span><span class="sxs-lookup"><span data-stu-id="306d1-p122">This example demonstrates enumerating against a database table with one million rows, but with a fixed set of values in ColumnA. In this scenario, you can consider ColumnA as the external content type and write an enumerator for this set of values by using the following SQL statement.</span></span> 
  
    
    



```sql

SELECT DISTINCT( ISNULL(ColumnA,'unknown')) as ColumnA  FROM table
```

<span data-ttu-id="306d1-236">Затем с помощью следующей инструкции SQL определяется специальный метод поиска.</span><span class="sxs-lookup"><span data-stu-id="306d1-236">Next, define the specific finder using the following SQL statement.</span></span> 
  
    
    



```sql
SELECT DISTINCT( ISNULL(ColumnA,'unknown')) as ColumnA  FROM table where ColumnA = @Value
```

<span data-ttu-id="306d1-237">Наконец, необходимо определить операцию перехода по связям, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="306d1-237">Finally, you must define the association navigation operation, as follows.</span></span> 
  
    
    



```sql
Select * from table where ColumnA=@value
```

<span data-ttu-id="306d1-p123">Любой метод должен начинать возврат результатов в течение двух минут, иначе программа-обходчик отменит вызов. Например, сложная инструкция SQL, использующая предложение **LIKE**, может выполняться более двух минут и, таким образом, привести к отмене вызова обходчиком.</span><span class="sxs-lookup"><span data-stu-id="306d1-p123">Any method should begin returning results within two minutes, or the crawler will cancel the call. For example, a complex SQL statement that uses a **LIKE** clause may take longer than two minutes to complete, and would cause the crawler to cancel the call.</span></span>
  
    
    

### <a name="improving-crawl-speed-with-the-useclientcachingforsearch-property"></a><span data-ttu-id="306d1-240">Увеличение скорости обхода контента с помощью свойства UseClientCachingForSearch</span><span class="sxs-lookup"><span data-stu-id="306d1-240">Improving crawl speed with the UseClientCachingForSearch property</span></span>

<span data-ttu-id="306d1-p124">Свойство **UseClientCachingForSearch** увеличивает скорость полного обхода контента, кэшируя элементы во время перечисления. Использование этого свойства также рекомендуется при реализации добавочного обхода контента, основанного на журналах изменений, так как это увеличит скорость добавочного обхода контента.</span><span class="sxs-lookup"><span data-stu-id="306d1-p124">The **UseClientCachingForSearch** property improves the speed of full crawls by caching the item during enumeration. Using this property is also recommended when implementing incremental crawls that are based on change logs, because it improves incremental crawl speed.</span></span>
  
    
    

> <span data-ttu-id="306d1-243">**Важные:** Если средний размер элементов превышает 30 килобайт в среднем, это свойство не задано, как его можно было привести к значительному количеству промахов кэша и сведет выигрыш в производительности.</span><span class="sxs-lookup"><span data-stu-id="306d1-243">**Important:** If items are larger than 30 kilobytes on average, do not set this property, as it will lead to a significant number of cache misses and negate performance gains.</span></span> 
  
    
    


## <a name="security-in-bdc-model-files"></a><span data-ttu-id="306d1-244">Безопасность в файлах модели BDC</span><span class="sxs-lookup"><span data-stu-id="306d1-244">Security in BDC model files</span></span>
<span data-ttu-id="306d1-245"><a name="SearchBDCModelProperties_Security"> </a></span><span class="sxs-lookup"><span data-stu-id="306d1-245"></span></span>

<span data-ttu-id="306d1-246">Если репозиторий использует проверку подлинности NTLM, рекомендуется задать для обхода контента сквозную проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="306d1-246">If the repository uses NTLM authentication, we recommend that you specify PassThrough authentication for crawling.</span></span>
  
    
    
<span data-ttu-id="306d1-p125">Страницы профиля могут требовать использования Служба Secure Store из-за проблемы многозвенного делегирования от интерфейсного веб-сервера. При возникновении этой проблемы можно оптимизировать обход и контента в то же время сохранить использование страниц профиля, создав два похожих экземпляра **LobSystemInstance**. Первый экземпляр должен использовать учетные данные из проверки подлинности Служба Secure Store. Этот экземпляр не должен содержать свойство **ShowInSearchUI**. Второй экземпляр должен использовать сквозную проверку подлинности и должен содержать свойство **ShowInSearchUI**. Страницы профиля используют первый экземпляр **LobSystemInstance**, а программа-обходчик  второй.</span><span class="sxs-lookup"><span data-stu-id="306d1-p125">Profile pages may require that you use the Secure Store Service because of the multi-hop delegation problem from the front-end web server. If you encounter this problem, you can optimize the crawl while still allowing profile pages by creating two similar **LobSystemInstance** instances. The first instance should use credentials from the Secure Store Service authentication. This instance should not contain the **ShowInSearchUI** property. The second instance should use PassThrough authentication, and should contain the **ShowInSearchUI** property. Profile pages use the first **LobSystemInstance** instance, and the crawler uses the second instance.</span></span>
  
> [!NOTE]
> <span data-ttu-id="306d1-253">[!Примечание] Для этого необходимо задать свойство **ShowInSearchUI** на уровне **LobSystemInstance**, а не на уровне **LobSystem**.</span><span class="sxs-lookup"><span data-stu-id="306d1-253">This requires that you set the **ShowInSearchUI** property at the **LobSystemInstance** level instead of at the **LobSystem** level.</span></span>


## <a name="see-also"></a><span data-ttu-id="306d1-254">См. также</span><span class="sxs-lookup"><span data-stu-id="306d1-254">See also</span></span>
<span data-ttu-id="306d1-255"><a name="SP15enhanceBDC_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="306d1-255"></span></span>


-  [<span data-ttu-id="306d1-256">Инфраструктура соединителей поиска в SharePoint</span><span class="sxs-lookup"><span data-stu-id="306d1-256">Search connector framework in SharePoint</span></span>](search-connector-framework-in-sharepoint.md)
    
  
-  [<span data-ttu-id="306d1-257">Инфраструктура модели подключения к бизнес-данным</span><span class="sxs-lookup"><span data-stu-id="306d1-257">BDC Model Infrastructure</span></span>](http://msdn.microsoft.com/library/2818ebdd-6cda-4d8f-82b2-7fde9fbf2633%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="306d1-258">Создание моделей подключения к бизнес-данным</span><span class="sxs-lookup"><span data-stu-id="306d1-258">Authoring BDC Models</span></span>](http://msdn.microsoft.com/library/170d1cfd-cf19-4162-b79f-ba6d3b4ad23b%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="306d1-259">Настройка среды разработки для BCS в SharePoint</span><span class="sxs-lookup"><span data-stu-id="306d1-259">Setting up a development environment for BCS in SharePoint</span></span>](setting-up-a-development-environment-for-bcs-in-sharepoint.md)
    
  
-  [<span data-ttu-id="306d1-260">Практическое руководство. Использование SharePoint Designer для создания файла модели подключения к бизнес-данным для настраиваемого соединителя</span><span class="sxs-lookup"><span data-stu-id="306d1-260">How to: Use SharePoint Designer to Create a BDC Model File for a Custom Connector</span></span>](http://msdn.microsoft.com/library/8f239482-0c82-4b60-817d-b0c4392e7e2e%28Office.15%29.aspx)
    
  

