# <a name="get-to-know-the-sharepoint-rest-service"></a>Знакомство со службой REST в SharePoint
Основы использования службы REST в SharePoint для чтения и изменения данных в SharePoint по веб-протоколам REST и OData.
 

 **Примечание.** Название "приложения для SharePoint" меняется на "надстройки SharePoint". Пока изменения не будут внесены полностью, в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio по-прежнему может встречаться термин "приложение". Дополнительные сведения см. в разделе [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).
 

В SharePoint появилась служба передачи репрезентативного состояния (REST), которую можно сравнить с уже входящими в состав SharePoint [клиентскими объектными моделями](http://msdn.microsoft.com/library/88e5e1b9-eab2-4f3b-a3f2-75c96b86f1f4%28Office.15%29.aspx). Теперь разработчики могут удаленно взаимодействовать непосредственно с данными SharePoint, используя любую технологию, поддерживающую веб-запросы REST. Это означает, что разработчики могут совершать операции **Create**, **Read**, **Update** и **Delete** (CRUD) из надстроек, решений и клиентских приложений SharePoint с помощью веб-технологий REST и стандартного синтаксиса Open Data Protocol (OData).
 

## <a name="prerequisites"></a>Необходимые компоненты

В этой статье предполагается, что у вас есть базовое представление о службе REST и создании запросов REST.
 

 

## <a name="how-the-sharepoint-rest-service-works"></a>Принцип работы службы REST в SharePoint
<a name="bk_how"> </a>

SharePoint позволяет удаленно взаимодействовать с сайтами SharePoint, используя REST. Теперь вы можете взаимодействовать непосредственно с объектами SharePoint, используя любую технологию, поддерживающую стандартные возможности REST.
 

 
Для доступа к ресурсам SharePoint с помощью REST необходимо создать HTTP-запрос RESTful, используя стандарт Open Data Protocol (OData), который соответствует необходимому API клиентской объектной модели. Пример:
 

 
 *Метод клиентской объектной модели:* 
 

 
List.GetByTitle(listname) 
 

 
 *Конечная точка REST:* 
 

 
 `http://server/site/_api/lists/getbytitle('listname')`
 

 
Веб-служба client.svc в SharePoint обрабатывает HTTP-запрос и предоставляет соответствующий ответ в формате Atom или JSON (JavaScript Object Notation). Затем его должно проанализировать ваше клиентское приложение. На следующем рисунке показано высокоуровневое представление архитектуры SharePoint REST.
 

 

**Архитектура службы REST в SharePoint**

 

 
![Архитектура службы REST в SharePoint](../../images/SPF15Con_REST_RESTStructure.png)
 
Благодаря функциональности и простоте использования этих клиентских объектных моделей разработчики чаще всего применяют их для обмена данными с сайтами SharePoint, используя управляемый код для .NET Framework, Silverlight или JavaScript.
 

 

### <a name="use-http-commands-with-the-sharepoint-rest-service"></a>Использование команд HTTP со службой REST в SharePoint
<a name="bk_usingHTTP"> </a>

Чтобы использовать возможности REST, встроенные в SharePoint, необходимо создать HTTP-запрос для REST, используя стандартный OData, что соответствует API клиентской объектной модели, которую вы хотите использовать. Веб-служба client.svc обрабатывает HTTP-запрос и предоставляет соответствующий ответ в формате Atom или JSON (JavaScript Object Notation). Затем его должно проанализировать клиентское приложение.
 

 
Конечные точки в службе REST SharePoint соответствуют типам и элементам клиентских объектных моделей SharePoint. С помощью HTTP-запросов вы можете использовать эти конечные точки REST для выполнения типичных операций CRUD с сущностями SharePoint, такими как списки и сайты. 
 

 
Ниже приводится краткое описание этих операций.
 

 


|**Задача**|**HTTP-запрос**|**Примечания**|
|:-----|:-----|:-----|
|Чтение ресурса|**GET**||
|Создание или обновление ресурса|**POST**|С помощью запроса **POST** можно создавать сущности, например списки и сайты. Служба REST в SharePoint поддерживает отправку команд **POST**, включающих определения объектов, конечным точкам, представляющим коллекции. В операциях **POST** для всех необязательных свойств задаются значения по умолчанию. При попытке задать доступное только для чтения свойство в рамках операции **POST** служба возвращает исключение.|
|Обновление или вставка ресурса |**PUT**| С помощью операций **PUT** и **MERGE** можно обновлять существующие объекты SharePoint. Любая конечная точка службы, представляющая операцию **set** для свойств объектов, поддерживает как запросы **PUT**, так и запросы **MERGE**. В запросах **MERGE** задавать свойства необязательно. Все свойства, не заданные в явном виде, сохраняют свои текущие значения. В запросах **PUT**, если не указать все обязательные свойства в обновлениях объекта, служба REST возвращает исключение. Кроме того, всем необязательным свойствам, не заданным в явном виде, присваиваются значения по умолчанию.|
|Удаление ресурса|**DELETE**|Используйте команду HTTP **DELETE** для URL-адреса определенной конечной точки, чтобы удалить объект SharePoint, представленный этой конечной точкой. Для повторно обрабатываемых объектов (например, списков, файлов и элементов списков) это приведет к выполнению операции **Recycle**.|

### <a name="construct-rest-urls-to-access-sharepoint-resources"></a>Составление URL-адресов REST для доступа к ресурсам SharePoint
<a name="bk_constructURLs"> </a>

Когда возможно, URI для этих конечных точек REST близко имитирует подпись API ресурса в клиентской объектной модели SharePoint. Главные точки входа для службы REST представляют семейство веб-сайтов и сайт указанного контекста. 
 

 
Для доступа к определенному семейству веб-сайтов используйте следующую конструкцию:
 

 
 `http://server/site/_api/site`
 

 
Для доступа к определенному сайту используйте следующую конструкцию:
 

 
 `http://server/site/_api/web`
 

 
В обоих случаях *server* представляет имя сервера, а *site* — имя определенного сайта или путь к нему.
 

 
С этой начальной точки вы можете создать более конкретные URI REST, ''обходя" объектную модель, с использованием имен API клиентской объектной модели, разделенных знаком косой черты (/).
 

 
Этот синтаксис не применяется к API REST SocialFeedManager или SocialFollowingManager. Подробнее см. в статьях  [Social feed REST API reference for SharePoint](http://msdn.microsoft.com/library/f1cb914f-1e91-4e23-bf53-d2ab323eac13%28Office.15%29.aspx) и [Following people and content REST API reference for SharePoint](http://msdn.microsoft.com/library/c05755df-846d-4a39-941d-950d066cc6d4%28Office.15%29.aspx).
 

 
В статье  [Определение универсальных кодов ресурсов (URI) конечных точек службы SharePoint REST](determine-sharepoint-rest-service-endpoint-uris) представлены дополнительные инструкции по определению URI конечных точек SharePoint REST из подписи соответствующих API клиентской объектной модели.
 

 

## <a name="sharepoint-rest-endpoint-examples"></a>Примеры конечных точек REST в SharePoint
<a name="bk_URLexamples"> </a>

В приведенной ниже таблице представлены типичные примеры URL-адресов для конечных точек REST, которые помогут вам приступить к работе с данными SharePoint. Чтобы составить полный URL-адрес REST, добавьте строку `http://server/site/_api/` в начале фрагментов URL-адресов, показанных в таблице. При необходимости для команд **POST** в таблице приводятся примеры данных, которые необходимо передать в тексте HTTP-запроса для создания указанного элемента SharePoint. Элементы, выделенные курсивом, представляют переменные, вместо которых необходимо подставить свои значения.
 

 


|**Описание**|**Конечная точка URL-адреса**|**Метод HTTP**|**Содержимое текста**|
|:-----|:-----|:-----|:-----|
|Получает заголовок списка| `web/title`|GET|Не применимо|
|Получает все списки на сайте| `lists`|GET|Не применимо|
|Получает метаданные одного списка| `lists/getbytitle('listname')`|GET|Не применимо|
|Получает элементы списка| `lists/getbytitle('listname')/items`|GET|Неприменимо|
|Получает определенное свойство документа (в данном случае это заголовок документа)| `lists/getbytitle('listname')?select=Title`|GET|Не применимо|
|Создает список| `lists`|POST|
```
{
  '__metadata':{'type':SP.List},
  'AllowContentTypes': true,
  'BaseTemplate': 104 ,
  'ContentTypesEnabled': true,
  'Description': 'My list description ',
  'Title': 'RestTest '
}
```

|Добавляет элемент в список| `lists/getbytitle('listname')/items`|POST|
```
{
  '__metadata':{'type': SP.Data.'listname'.ListItem},
  'Title': 'MyItem'
}

```

|

## <a name="batch-job-support"></a>Поддержка пакетных заданий
<a name="batch"> </a>

Служба REST SharePoint Online (а также локального выпуска SharePoint 2016 или более поздней версии) поддерживает объединение нескольких запросов в одном вызове службы с помощью параметра запроса OData  `$batch`. Дополнительные сведения и ссылки на примеры кода см. в разделе  [Создание пакетного запроса с помощью интерфейсов REST API](make-batch-requests-with-the-rest-apis).
 

 

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_learnmore"> </a>

Из перечисленных ниже ресурсов вы можете узнать больше об использовании службы REST в SharePoint.
 

 

|**Название**|**Описание**|
|:-----|:-----|
| [Выполнение базовых операций с использованием конечных точек SharePoint REST](complete-basic-operations-using-sharepoint-2013-rest-endpoints)|Узнайте, как выполнять операции CRUD (создание, чтение, обновление, удаление) с помощью интерфейса REST SharePoint.|
| [Работа со списками и элементами списков в службе REST](working-with-lists-and-list-items-with-rest)|Узнайте, как выполнять основные операции по созданию, чтению, обновлению и удалению списков и элементов списков с помощью интерфейса REST SharePoint.|
| [Работа с папками и файлами в службе REST](working-with-folders-and-files-with-rest)|Узнайте, как выполнять основные операции по созданию, чтению, обновлению и удалению папок и файлов с помощью интерфейса REST SharePoint.|
| [Навигация по структуре данных SharePoint, представленной в службе REST](navigate-the-sharepoint-data-structure-represented-in-the-rest-service)|Узнайте, как с помощью конечной точки REST в элементе SharePoint получить доступ к связанным элементам, например родительским сайтам или структуре библиотеки, в которой находится этот элемент.|
| [Определение универсальных кодов ресурсов (URI) конечных точек службы SharePoint REST](determine-sharepoint-rest-service-endpoint-uris)|В этой статье представлены общие инструкции, позволяющие определить URI конечных точек REST в SharePoint, используя подписи соответствующих API клиентской объектной модели.|
| [Использование операций запросов OData в запросах SharePoint REST](use-odata-query-operations-in-sharepoint-rest-requests)|Узнайте, как использовать широкий спектр операторов строки запроса OData для выбора, фильтрации и упорядочивания данных, запрашиваемых у службы REST SharePoint.|
| [SharePoint REST API, конечные точки и примеры](http://msdn.microsoft.com/library/rest-api-reference-and-samples%28Office.15%29.aspx)|На этой странице приведены ссылки на все ресурсы по REST, доступные для разработчиков SharePoint в MSDN.|
| [Общие сведения о REST API для службы поиска SharePoint](http://msdn.microsoft.com/library/8a4f7863-e4c1-4099-9189-a1894db36930%28Office.15%29.aspx)|Добавление функции поиска в клиентские и мобильные приложения с помощью службы поиска REST в SharePoint Server 2013 и в любой технологии, поддерживающей веб-запросы REST.|
| [Social feed REST API reference for SharePoint](http://msdn.microsoft.com/library/f1cb914f-1e91-4e23-bf53-d2ab323eac13%28Office.15%29.aspx)|Подробнее о конечных точках REST SharePoint для выполнения задач, связанных с каналами.|
| [Following people and content REST API reference for SharePoint](http://msdn.microsoft.com/library/c05755df-846d-4a39-941d-950d066cc6d4%28Office.15%29.aspx)|Подробнее о конечных точках REST SharePoint для подписки на людей и контент.|
| [Создание пакетного запроса с помощью интерфейсов REST API](make-batch-requests-with-the-rest-apis)|Узнайте, как объединить несколько запросов в один пот вызове службы REST.|
| [Синхронизация элементов SharePoint с помощью службы REST](synchronize-sharepoint-items-using-the-rest-service)|Узнайте, как синхронизировать элементы между SharePoint и надстройками или службами с помощью ресурса **GetListItemChangesSinceToken**, входящего в состав службы REST в SharePoint.|
| [Получение версий элементов из списка документов с помощью значений ETag через службы REST](http://msdn.microsoft.com/library/5f7e0579-46b7-44ab-b3b4-cdbc622dcd98%28Office.15%29.aspx)|Узнайте, как использовать теги HTML ETag в службе REST SharePoint для управления параллелизмом списков SharePoint и их элементов.|

## <a name="odata-resources"></a>Материалы по OData
<a name="SP15startREST_bk_addlresources"> </a>


 

 

-  [Знакомство с OData](http://msdn.microsoft.com/en-us/data/hh237663)
    
 
-  [Примеры для протокола Open Data Protocol](http://msdn.microsoft.com/ru-ru/library/ff478141.aspx)
    
 
-  [Open Data Protocol](http://www.odata.org/)
    
 
-  [Соглашения об URI для протокола OData](http://www.odata.org/documentation/odata-version-2-0/uri-conventions/)
    
 
-  [Адресация для операций службы](http://www.odata.org/documentation/odata-version-2-0/uri-conventions#AddressingServiceOperations)
    
 
-  [Операции протокола OData](http://www.odata.org/documentation/odata-version-2-0/operations/)
    
 
-  [Условия ошибок](http://www.odata.org/documentation/odata-version-2-0/operations#ErrorConditions)
    
 

