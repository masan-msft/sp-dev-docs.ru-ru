---
title: "Создание мобильных приложений для других платформ с помощью SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 017df869-44fb-4ffe-82fb-4654e01329ad
ms.openlocfilehash: 79a29d982ffaf0ef91732090c3a989a5d10a2814
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="build-mobile-apps-for-other-platforms-using-sharepoint"></a>Создание мобильных приложений для других платформ с помощью SharePoint
Сведения об использовании представлений состояния (REST) для создания мобильного приложения SharePoint для любой платформы.
Мобильные устройства становятся более мощные и удобные в настоящее время. Ноутбуки, нетбуков, планшетных ПК и мобильных телефонов предоставляют доступ к информации и приложений, которые необходимы для выполнения их работы сотрудников. И разработка приложений для мобильных устройств является теперь проще, чем когда-либо. В результате больше бизнес-сценарии запросами интеграции клиентских приложений с бизнес-процессами. В этой статье описывается, как интегрировать приложения мобильного клиента вместе с SharePoint. Можно создать мобильного приложения для просмотра SharePoint содержимого из любого места и подключать к спискам SharePoint и библиотеки для доступа к данным.
  
    
    

Для разработки мобильных приложений, который взаимодействует с SharePoint, можно использовать общие службы, которые может осуществляться с использованием open протоколы. SharePoint Foundation 2010 представлено клиентских объектных моделей, которые включены разработчиков выполнение удаленной связи с SharePoint с помощью веб-программирования технологии выбранного: .NET Framework, Microsoft Silverlight или JavaScript. SharePoint представляется представлений состояния (REST) служба, которая полностью сравнимые клиентской объектной модели. В SharePoint практически все API клиентской объектной модели будет иметь соответствующую конечную точку REST. Теперь разработчики могут удаленного взаимодействия с помощью объектной модели SharePoint с помощью любой технологии, поддерживающей веб-запросы REST. REST может использоваться любой язык программирования, который вы хотите использовать для разработки мобильных приложений.
Можно выполнять базовые создания, чтения, обновления и удаления (CRUD) операции с помощью интерфейса REST, доступного в SharePoint. REST предоставляет всех объектов SharePoint и операции, доступные в другие клиентские интерфейсы API SharePoint. Одним из преимуществ использования REST — это, что у вас нет для добавления ссылки на любой библиотеки SharePoint или клиентских сборок. Вместо этого сделать HTTP-запросов для соответствующих конечных точек для извлечения или обновления объектов SharePoint, такие как веб-сайтов, списков и элементов списка. Подробное введение в интерфейс SharePoint REST и ее архитектуры в разделе [операции запросов OData используется в запросах SharePoint REST](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx).
  
    
    


## <a name="rest-endpoints-in-sharepoint"></a>Конечные точки REST в SharePoint
<a name="BuildMobileAppsInSharePoint2013ForNonWindowsPhone_REST_EndpointsInSharePoint2013"> </a>

Чтобы использовать возможности REST, которые встроены в SharePoint, можно создать RESTful HTTP-запросов с использованием стандарта Open Data Protocol (OData), соответствующий API желаемую клиентской объектной модели. Веб-службы client.svc обрабатывает HTTP-запрос и обслуживает соответствующий ответ в формате Atom или JavaScript Object Notation (JSON). Клиентское приложение затем необходимо выполнить синтаксический анализ этого ответа. На рисунке 1 показано высокоуровневое представление архитектуры SharePoint REST.
  
    
    

**На рисунке 1. Архитектура SharePoint REST**

  
    
    

  
    
    
![Архитектура REST SharePoint](../images/SP15Con_BuildSharePointAppsForMobileDevices_Fig2.png)
  
    
    
Конечные точки в службе SharePoint REST соответствуют типы и элементы в объектной модели клиента SharePoint. С помощью HTTP-запросов, можно использовать эти конечные точки REST для выполнения типичных операций CRUD с SharePoint артефакты, такие как списки и сайты.
  
    
    
В следующей таблице приведены общие правила.
  
    
    

- Конечные точки, представляющие операций чтения сопоставление команд **GET** HTTP.
    
  
- Конечные точки, представляющие карты операции обновления **POST** команд HTTP.
    
  
- Конечные точки, представляющие обновление или Вставка карты операции по командам **PUT** HTTP.
    
  
При выборе HTTP-запросы для использования, необходимо учитывать следующее:
  
    
    

- **POST** используется для создания артефакты, такие как списки и сайты. Службы SharePoint REST поддерживает отправку **POST** -команд, включая определения объектов, конечные точки, представляющие семейств сайтов.
    
  
- Для операций **POST** значения по умолчанию устанавливаются все свойства, которые не являются обязательными. При попытке задать свойство только для чтения в процессе выполнения операции **POST** служба возвращает исключение.
    
  
- Используйте **PUT**, **PATCH**и **MERGE** операций для обновления существующих объектов SharePoint. Каждая конечная точка службы, представляющий операцию **set** свойства объектов поддерживает **PUT** запросы и запросы на **MERGE**. Для запросов **MERGE** Установка свойств является необязательным; все свойства, которые явно не задана сохранение их текущее свойство. Но для команды **PUT** свойств, которые явно не задан значение их свойства по умолчанию. Кроме того Если не указать все настраиваемые свойства в объект обновления при использовании команд **PUT** HTTP, службы REST возвращает исключение.
    
  
- Используйте команду HTTP **DELETE** для определенного URL-адреса конечной точки, чтобы удалить объект SharePoint, представленный этой конечной точкой. Для пригодными объекты, такие как списки, файлов и элементов списка в результате **перезапуска** операции. Дополнительные сведения можно [узнать службы SharePoint REST](http://msdn.microsoft.com/library/2de035a0-ac75-43bd-9665-5c5a59c4c590%28Office.15%29.aspx).
    
  

## <a name="authenticate-users-to-sharepoint"></a>Проверка подлинности пользователей в SharePoint
<a name="BuildMobileAppsInSharePoint2013ForNonWindowsPhone_AuthenticatingNonWindowsAppForSharePoint"> </a>

Чтобы проверить подлинность мобильного приложения с помощью SharePoint, можно использовать протокол MS-OFBA. Дополнительные сведения можно  [[MS-OFBA]: спецификация протокола проверки подлинности на основе Office Forms](http://msdn.microsoft.com/library/30c7bbe9-b284-421f-b866-4e7ed4866027%28Office.15%29.aspx). Клиент протокола настроен для хранения и передачи файлов cookie. Клиента протокола использует протокол удаленного сервера для установки удостоверение пользователя как один или несколько файлов cookie HTTP. После установки удостоверение пользователя, затем клиент передает каждый файл cookie с каждого последующего запроса HHT.
  
    
    
При входе пользователя в систему SharePoint, маркер пользователя проверка и затем используется для входа в SharePoint. Маркер пользователя — это маркер безопасности, выданный поставщика удостоверений. SharePoint поддерживает несколько типов проверки подлинности. Для получения дополнительных сведений см [проверки подлинности, авторизации и безопасности в SharePoint](authentication-authorization-and-security-in-sharepoint.md). Для проверки подлинности пользователя, можно использовать интерфейс REST. Процесс авторизации проверяет наличие прошедшего проверку подлинности темы, (приложения или пользователя, который на of.md имени действует приложение) разрешения для выполнения определенных операций или получить доступ к определенным ресурсам (например, список или folder.md документов SharePoint).
  
    
    
OData позволяет получить доступ к источнику данных, таких как базы данных, просмотрев имеющиеся специально созданный URL-адрес. Это позволяет упрощенный подход для подключений и работа с источниками данных, размещенным внутри организации. OData  это протокол, который используется HTTP, Atom и Нотация объектов JavaScript (JSON) позволяет разработчикам создавать приложения, которые взаимодействуют с возрастающих число источников данных. Microsoft поддерживает создание этот стандарт, чтобы разрешить обмен данными между приложениями и хранилища данных, доступных из Интернета. Новый соединитель OData позволяет связываться с поставщиками OData SharePoint. Для получения дополнительных сведений см  [Open Data Protocol](http://www.odata.org).
  
    
    
Следующий код демонстрирует способ проверки подлинности приложения для SharePoint с использованием конечные точки REST для проверки подлинности basic или на основе форм. В следующем примере кода, записывается в C#, но можно использовать другие языки программирования для создания запроса Http, согласно требования платформы.
  
    
    



```cs

string SharePointUrl = "https://Target SharePoint site";

private void AuthenticateToSharePoint(object sender, RoutedEventArgs e)
{
    ODataAuthenticator odataAt = new ODataAuthenticator("<Username>", "<password>");
    odataAt.CookieCachingEnabled = true;
    odataAt.AuthenticationCompleted += new EventHandler<AuthenticationCompletedEventArgs>(odataAt_AuthenticationCompleted);
    odataAt.Authenticate(new Uri(SharePointUrl, UriKind.Absolute));
}

void odataAt_AuthenticationCompleted(object sender, AuthenticationCompletedEventArgs e)
{
    HttpWebRequest endpointRequest = (HttpWebRequest)HttpWebRequest.Create(SharePointUrl.ToString() + "/_api/web/lists");
    endpointRequest.Method = "GET";
    endpointRequest.Accept = "application/json;odata=verbose";
          endpointRequest.CookieContainer = (sender as ODataAuthenticator).CookieContainer;
    
    endpointRequest.BeginGetResponse(new AsyncCallback((IAsyncResult res) =>
    {
        HttpWebRequest webReq = res.AsyncState as HttpWebRequest;
        WebResponse response = webReq.EndGetResponse(res);

        HttpWebResponse httpResponse = response as HttpWebResponse;
        HttpStatusCode code = httpResponse.StatusCode;
        this.Dispatcher.BeginInvoke(() =>
        {
            MessageBox.Show(code.ToString());
        });
    }), endpointRequest);
}

```

Для проверки подлинности **HttpWebrequest** в конечную точку, вы должны сначала выполнять проверку подлинности в SharePoint с классом **ODataAuthenticator**. До вызова метода **Authenticate**, зарегистрируйте объект **ODataAuthenticator** к событию **AuthenticationCompleted**.
  
    
    
После проверки подлинности выполняется внутри события **OnAuthenticationCompleted**, можно использовать свойство **CookieContainer** на объект **ODataAuthenticator**, который можно присоединить к объекту **HttpWebRequest** для проверки подлинности вызовов REST для SharePoint.
  
    
    

## <a name="work-with-sharepoint-list-items-using-rest"></a>Работа с элементами списков SharePoint с помощью REST
<a name="BuildMobileAppsInSharePoint2013ForNonWindowsPhone_WorkingWithTheSharePointListItemUsingREST"> </a>

В следующем примере показывается, как **получить** все элементы списка.
  
    
    

```

url: http://site url/_api/web/lists/GetByTitle('Test')/items
method: GET
headers:
// MS-OFBA protocol returns a cookie.
  Cookie: cookie


    accept: "application/json;odata=verbose" or "application/atom+xml"

```

В следующем примере показывается, как **получить** определенный элемент списка.
  
    
    



```

url: http://site url/_api/web/lists/GetByTitle('Test')/items(item id)
method: GET
headers:
    
// MS-OFBA protocol return a cookie.
  Cookie: cookie
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

В следующем XML показывается пример свойств элементов списка, которые возвращаются при вашем запросе типа контента XML.
  
    
    



```XML

<content type="application/xml">
        <m:properties>
        <d:FileSystemObjectType m:type="Edm.Int32">0</d:FileSystemObjectType>
        <d:Id m:type="Edm.Int32">1</d:Id>
        <d:ID m:type="Edm.Int32">1</d:ID>
        <d:ContentTypeId>0x010049564F321A0F0543BA8C6303316C8C0F</d:ContentTypeId>
        <d:Title>an item</d:Title>
        <d:Modified m:type="Edm.DateTime">2012-07-24T22:47:26Z</d:Modified>
        <d:Created m:type="Edm.DateTime">2012-07-24T22:47:26Z</d:Created>
        <d:AuthorId m:type="Edm.Int32">11</d:AuthorId>
        <d:EditorId m:type="Edm.Int32">11</d:EditorId>
        <d:OData__UIVersionString>1.0</d:OData__UIVersionString>
        <d:Attachments m:type="Edm.Boolean">false</d:Attachments>
        <d:GUID m:type="Edm.Guid">eb6850c5-9a30-4636-b282-234eda8b1057</d:GUID>
    </m:properties>
</content>
```

В следующем примере показывается, как **создать** элемент списка.
  
    
    

> **Примечание:** Для выполнения этой операции необходимо знать свойство **ListItemEntityTypeFullName** списка и передать его как значение **типа** в тексте запроса HTTP.
  
    
    




```

url: http://site url/_api/web/lists/GetByTitle('Test')/items
method: POST
body: { '__metadata': { 'type': 'SP.Data.TestListItem' }, 'Title': 'Test'}
headers:
    
// MS-OFBA protocol returns a cookie.
  Cookie: cookie
     X-RequestDigest = form digest value
    accept: "application/json;odata=verbose"
    content-type: "application/json;odata=verbose"
    content-length:length of post body
```

В следующем примере показывается, как **обновить** элемент списка.
  
    
    

> **Примечание:** Для выполнения этой операции необходимо знать свойство **ListItemEntityTypeFullName** списка и передать его как значение **типа** в тексте запроса HTTP.
  
    
    




```

url: http://site url/_api/web/lists/GetByTitle('Test')/items(item id)
method: POST
body: { '__metadata': { 'type': 'SP.Data.TestListItem' }, 'Title': 'TestUpdated'}
headers:
// MS-OFBA protocol returns a cookie.
  Cookie: cookie
     X-RequestDigest = form digest value
    "IF-MATCH": etag or "*"
    "X-HTTP-Method":"MERGE",
    accept: "application/json;odata=verbose"
    content-type: "application/json;odata=verbose"
    content-length:length of post body
```

В следующем примере показывается, как **удалить** элемент списка.
  
    
    



```

url: http://site url/_api/web/lists/GetByTitle('Test')/items(item id)
method: POST
headers:
// MS-OFBA protocol returns a cookie.
  Cookie: cookie
     X-RequestDigest = form digest value
    "IF-MATCH": etag or "*"
    "X-HTTP-Method":"DELETE"

```

Для получения дополнительных сведений см [выполнения базовых операций с помощью конечных точек SharePoint REST](http://msdn.microsoft.com/library/e3000415-50a0-426e-b304-b7de18f2f7d9%28Office.15%29.aspx).
  
    
    

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>


-  [Построение приложений Windows Phone, обращающихся к SharePoint](build-windows-phone-apps-that-access-sharepoint.md)
    
  
-  [С помощью службы SharePoint REST](http://msdn.microsoft.com/library/e1ff2979-1c16-4cb0-a57e-9168dfe20a7c.aspx)
    
  
-  [Построение приложений Windows Phone, обращающихся к SharePoint](build-windows-phone-apps-that-access-sharepoint.md)
    
  
-  [Выбор правильного набора API в SharePoint](choose-the-right-api-set-in-sharepoint.md)
    
  
-  [Использование операций запросов OData в запросах REST SharePoint](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx)
    
  
-  [Знакомство со службой REST в SharePoint](http://msdn.microsoft.com/library/2de035a0-ac75-43bd-9665-5c5a59c4c590%28Office.15%29.aspx)
    
  
-  [Выполнение вызовов REST при помощи C# и JavaScript для SharePoint](http://www.microsoft.com/resources/msdn/en-us/office/media/video/videol?cid=sdc&amp;from=mscomsdc&amp;VideoID=4e4cc094-ff69-405b-852f-2ac7c41293c5)
    
  
-  [Выполнение вызовов REST при помощи C# и JavaScript для демоверсии SharePoint](http://www.microsoft.com/resources/msdn/en-us/office/media/video/videol?cid=sdc&amp;from=mscomsdc&amp;VideoID=b1e7c9c5-0f62-4a78-bb7b-8e283c86145c)
    
  
-  [Open Data Protocol](http://www.odata.org/)
    
  
-  [Авторизация и проверка подлинности для надстроек в SharePoint 2013](http://msdn.microsoft.com/library/bde5647a-fff1-4b51-b67b-2139de79ce4a%28Office.15%29.aspx)
    
  
-  [Windows Phone SDK 8.0](http://www.microsoft.com/en-us/download/details.aspx?id=35471)
    
  
-  [Пакет SDK Microsoft SharePoint для Windows Phone 8](http://www.microsoft.com/en-us/download/details.aspx?id=36818)
    
  

