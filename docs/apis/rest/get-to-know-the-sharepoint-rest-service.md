# <a name="get-to-know-the-sharepoint-rest-service"></a>Знакомство со службой REST в SharePoint
Основы использования службы REST в SharePoint для чтения и изменения данных в SharePoint по веб-протоколам REST и OData.

В SharePoint 2013 появилась служба REST (Representational State Transfer), сравнимая с имеющимися в SharePoint [клиентскими объектными моделями](http://msdn.microsoft.com/library/88e5e1b9-eab2-4f3b-a3f2-75c96b86f1f4%28Office.15%29.aspx). Теперь разработчики могут удаленно работать с данными SharePoint при помощи любой технологии, поддерживающей веб-запросы REST. Это означает, что разработчики могут выполнять операции **создания**, **чтения**, **обновления** и **удаления** (CRUD) из надстроек, решений и клиентских приложений для SharePoint, используя веб-технологии REST и стандартный синтаксис протокола OData (Open Data Protocol).
 
## <a name="prerequisites"></a>Необходимые условия
В этой статье предполагается, что у вас есть базовое представление о службе REST и создании запросов REST.

## <a name="how-the-sharepoint-rest-service-works"></a>Принцип работы службы REST в SharePoint
<a name="bk_how"> </a> В SharePoint 2013 появилась возможность удаленной работы с сайтами SharePoint с помощью REST. Теперь вы можете работать с объектами SharePoint напрямую, используя любую технологию, поддерживающую стандартные возможности REST.
  
Для доступа к ресурсам SharePoint с помощью REST необходимо создать HTTP-запрос RESTful, используя стандарт Open Data Protocol (OData), который соответствует необходимому API клиентской объектной модели. Пример:
 
 *Метод клиентской объектной модели:* 

```
List.GetByTitle(listname) 
``` 

 *Конечная точка REST:* 
 
 ```
 http://server/site/_api/lists/getbytitle('listname')
 ```

Веб-служба client.svc в SharePoint обрабатывает HTTP-запрос и предоставляет соответствующий ответ в формате Atom или JSON (JavaScript Object Notation). Затем его должно проанализировать ваше клиентское приложение. На следующем рисунке показано высокоуровневое представление архитектуры SharePoint REST.
 
**Архитектура службы REST в SharePoint**

![Архитектура службы REST в SharePoint](../../../images/REST_RESTStructure.png)
 
Благодаря функциональности и простоте использования этих клиентских объектных моделей разработчики чаще всего применяют их для обмена данными с сайтами SharePoint, используя управляемый код для .NET Framework, Silverlight или JavaScript.
 
### <a name="use-http-commands-with-the-sharepoint-rest-service"></a>Использование команд HTTP со службой REST в SharePoint
<a name="bk_usingHTTP"> </a> Чтоб использовать возможности REST, встроенные в SharePoint, необходимо создать HTTP-запрос RESTful, используя стандарт OData, соответствующий нужному API клиентской объектной модели. Веб-служба client.svc обрабатывает HTTP-запрос и возвращает подходящий отклик в формате Atom или нотации объектов JavaScript (JSON). Затем клиентское приложение должно проанализировать этот отклик.
 
Конечные точки в службе REST SharePoint соответствуют типам и элементам клиентских объектных моделей SharePoint. С помощью HTTP-запросов вы можете использовать эти конечные точки REST для выполнения типичных операций CRUD с сущностями SharePoint, такими как списки и сайты. 
 
Ниже приводится краткое описание этих операций.

|**Задача**|**HTTP-запрос**|**Примечания**|
|:-----|:-----|:-----|
|Чтение ресурса|**GET**||
|Создание или обновление ресурса|**POST**|С помощью запроса **POST** можно создавать сущности, например списки и сайты. Служба REST в SharePoint поддерживает отправку команд **POST**, включающих определения объектов, конечным точкам, представляющим коллекции. В операциях **POST** для всех необязательных свойств задаются значения по умолчанию. При попытке задать доступное только для чтения свойство в рамках операции **POST** служба возвращает исключение.|
|Обновление или вставка ресурса |**PUT**| С помощью операций **PUT** и **MERGE** можно обновлять существующие объекты SharePoint. Любая конечная точка службы, представляющая операцию **set** для свойств объектов, поддерживает как запросы **PUT**, так и запросы **MERGE**. В запросах **MERGE** задавать свойства необязательно. Все свойства, не заданные в явном виде, сохраняют свои текущие значения. В запросах **PUT**, если не указать все обязательные свойства в обновлениях объекта, служба REST возвращает исключение. Кроме того, всем необязательным свойствам, не заданным в явном виде, присваиваются значения по умолчанию.|
|Удаление ресурса|**DELETE**|Используйте команду HTTP **DELETE** для URL-адреса определенной конечной точки, чтобы удалить объект SharePoint, представленный этой конечной точкой. Для повторно обрабатываемых объектов (например, списков, файлов и элементов списков) это приведет к выполнению операции **Recycle**.|

### <a name="construct-rest-urls-to-access-sharepoint-resources"></a>Создание URL-адресов REST для доступа к ресурсам SharePoint
<a name="bk_constructURLs"> </a> URI для этих конечных точек REST, насколько это возможно, совпадает с подписью API ресурса в клиентской объектной модели SharePoint. Основные точки входа для службы REST представляют семейство веб-сайтов и сайт указанного контекста. 
  
Для доступа к определенному семейству веб-сайтов используйте следующую конструкцию:
 
 `http://server/site/_api/site`
 
Для доступа к определенному сайту используйте следующую конструкцию:
 
 `http://server/site/_api/web`
 
В обоих случаях *server* представляет имя сервера, а *site* — имя определенного сайта или путь к нему.
 
С этой начальной точки вы можете создать более конкретные URI REST, ''обходя" объектную модель, с использованием имен API клиентской объектной модели, разделенных знаком косой черты (/).
 
Этот синтаксис неприменим к REST API SocialFeedManager и SocialFollowingManager. Дополнительные сведения см. в [справочнике по REST API каналов социальных медиа для SharePoint 2013](http://msdn.microsoft.com/library/f1cb914f-1e91-4e23-bf53-d2ab323eac13%28Office.15%29.aspx) и [справочнике по REST API отслеживания пользователей и контента для SharePoint 2013](http://msdn.microsoft.com/library/c05755df-846d-4a39-941d-950d066cc6d4%28Office.15%29.aspx).
 
В статье [Как определить URI конечных точек службы REST в SharePoint](determine-sharepoint-rest-service-endpoint-uris.md) представлены дополнительные указания, позволяющие определить URI для конечных точек службы REST в SharePoint, используя подписи соответствующих API клиентской объектной модели.
 
## <a name="sharepoint-rest-endpoint-examples"></a>Примеры конечных точек REST в SharePoint
<a name="bk_URLexamples"> </a>

В приведенной ниже таблице представлены типичные примеры URL-адресов для конечных точек REST, которые помогут вам приступить к работе с данными SharePoint. Чтобы составить полный URL-адрес REST, добавьте строку `http://server/site/_api/` в начале фрагментов URL-адресов, показанных в таблице. При необходимости для команд **POST** в таблице приводятся примеры данных, которые необходимо передать в тексте HTTP-запроса для создания указанного элемента SharePoint. Элементы, выделенные курсивом, представляют переменные, вместо которых необходимо подставить свои значения.

|**Описание**|**Конечная точка URL-адреса**|**Метод HTTP**|**Основное содержимое**|
|:-----|:-----|:-----|:-----|
|Получает заголовок сайта| `web/title`|GET|Не применимо|
|Получает все списки на сайте| `lists`|GET|Не применимо|
|Получает метаданные одного списка| `lists/getbytitle('listname')`|GET|Не применимо|
|Получает элементы списка| `lists/getbytitle('listname')/items`|GET|Неприменимо|
|Получает определенное свойство документа (в данном случае это заголовок документа)| `lists/getbytitle('listname')?select=Title`|GET|Не применимо|
|Создает список| `lists`|POST|
```
{
  '_metadata':{'type':SP.List},
  'AllowContentTypes': true,
  'BaseTemplate': 104 ,
  'ContentTypesEnabled': true,
  'Description': 'My list description ',
  'Title': 'RestTest '
}
```

|
|Добавляет элемент в список| `lists/getbytitle('listname')/items`|POST|
```
{
  '_metadata':{'type':SP.listname ListItem},
  'Title': 'MyItem'
}

```

|

## <a name="batch-job-support"></a>Поддержка пакетных заданий
<a name="batch"> </a>

Служба REST в SharePoint Online (а также локальной среде SharePoint 2016 или более поздней версии) поддерживает объединение нескольких запросов в один при вызове службы с помощью параметра запроса OData `$batch`. Подробные сведения и ссылки на примеры кода см. в статье [Выполнение пакетных запросов с помощью REST API](make-batch-requests-with-the-rest-apis.md).
 
## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_learnmore"> </a> В перечисленных ниже статьях вы найдете дополнительные сведения об использовании службы REST в SharePoint.
 
|||
|:-----|:-----|
| [Выполнение базовых операций с использованием конечных точек REST в SharePoint](complete-basic-operations-using-sharepoint-rest-endpoints.md)|Узнайте, как выполнять операции CRUD (создание, чтение, обновление, удаление) с помощью интерфейса REST SharePoint.|
| [Работа со списками и элементами списков в службе REST](working-with-lists-and-list-items-with-rest.md)|Узнайте, как выполнять основные операции по созданию, чтению, обновлению и удалению списков и элементов списков с помощью интерфейса REST SharePoint.|
| [Работа с папками и файлами в службе REST](working-with-folders-and-files-with-rest.md)|Узнайте, как выполнять основные операции по созданию, чтению, обновлению и удалению папок и файлов с помощью интерфейса REST SharePoint.|
| [Навигация по структуре данных SharePoint, представленной в службе REST](navigate-the-sharepoint-data-structure-represented-in-the-rest-service.md)|Узнайте, как с помощью конечной точки REST в элементе SharePoint получить доступ к связанным элементам, например родительским сайтам или структуре библиотеки, в которой находится этот элемент.|
| [Как определить URI конечных точек службы REST в SharePoint](determine-sharepoint-rest-service-endpoint-uris.md)|В этой статье представлены общие инструкции, позволяющие определить URI конечных точек REST в SharePoint, используя подписи соответствующих API клиентской объектной модели.|
| [Использование операций запросов OData в запросах REST SharePoint](use-odata-query-operations-in-sharepoint-rest-requests.md)|Узнайте, как использовать широкий спектр операторов строки запроса OData для выбора, фильтрации и упорядочивания данных, запрашиваемых у службы REST SharePoint.|
| [Справочные материалы и примеры по REST API](http://msdn.microsoft.com/library/02128c70-9d27-4388-9374-a11bce68fdb8%28Office.15%29.aspx)|На этой странице представлены ссылки на все ресурсы REST, доступные разработчикам SharePoint 2013 на сайте MSDN.|
| [Общие сведения о REST API для службы поиска SharePoint](http://msdn.microsoft.com/library/8a4f7863-e4c1-4099-9189-a1894db36930%28Office.15%29.aspx)|Узнайте, как добавлять функции поиска в клиентские и мобильные приложения с помощью службы REST поиска в SharePoint Server 2013 и любой технологии, поддерживающей веб-запросы REST.|
| [Справочник по REST API каналов социальных медиа для SharePoint 2013](http://msdn.microsoft.com/library/f1cb914f-1e91-4e23-bf53-d2ab323eac13%28Office.15%29.aspx)|Сведения о конечных точках REST в SharePoint 2013 для выполнения задач, связанных с каналами.|
| [Справочник по REST API отслеживания пользователей и контента для SharePoint 2013](http://msdn.microsoft.com/library/c05755df-846d-4a39-941d-950d066cc6d4%28Office.15%29.aspx)|Сведения о конечных точках REST в SharePoint 2013 для отслеживания пользователей и контента.|
| [Отправка пакетных запросов с помощью интерфейсов REST API](make-batch-requests-with-the-rest-apis.md)|Узнайте, как объединить несколько запросов в один пот вызове службы REST.|
| [Синхронизация элементов SharePoint с помощью службы REST](synchronize-sharepoint-items-using-the-rest-service.md)|Узнайте, как синхронизировать элементы между SharePoint и надстройками или службами с помощью ресурса **GetListItemChangesSinceToken**, входящего в состав службы REST в SharePoint.|
| [Получение версий списков документов с помощью значений ETag в службе REST](http://msdn.microsoft.com/library/use-etag-values-through-the-rest-service-to-get-document-list-item-versioning%28Office.15%29.aspx)|Узнайте, как использовать теги HTML ETag в службе REST SharePoint для управления параллелизмом списков SharePoint и их элементов.|

## <a name="odata-resources"></a>Материалы по OData
<a name="SP15startREST_bk_addlresources"> </a>

-  [Знакомство с OData](http://msdn.microsoft.com/en-us/data/hh237663) 
-  [Примеры для протокола Open Data Protocol](http://msdn.microsoft.com/en-us/library/ff478141.aspx)
-  [Open Data Protocol](http://www.odata.org/)
-  [Соглашения об URI для протокола OData](http://www.odata.org/documentation/odata-version-2-0/uri-conventions/)
-  [Адресация для операций службы](http://www.odata.org/documentation/odata-version-2-0/uri-conventions#AddressingServiceOperations)
-  [Операции протокола OData](http://www.odata.org/documentation/odata-version-2-0/operations/)
-  [Условия ошибок](http://www.odata.org/documentation/odata-version-2-0/operations#ErrorConditions)
    
 

