---
title: "Обзор объектной модели SharePoint для мобильных устройств"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 72319846-d02d-49e7-b830-48eb8f5715cb
ms.openlocfilehash: 171c14d60a6f3063e8a903387a0faad34cd34308
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="overview-of-the-sharepoint-mobile-object-model"></a>Обзор объектной модели SharePoint для мобильных устройств
Узнайте о новых общим классам в серверной объектной модели SharePoint и клиентская объектная модель Silverlight, которые используются для разработки интегрированные решения для SharePoint и Windows Phone 7.5.
## <a name="client-object-model-for-mobile-silverlight"></a>Клиентская объектная модель для мобильных устройств Silverlight
<a name="SP15OM_ClientOM"> </a>

Все классы в этом разделе содержатся в пространстве имен **Microsoft.SharePoint.Client**. В дополнение к API в этом разделе большая часть классов и членов в разделе Server объектной модели для мобильной работы SharePoint также можно вызвать в клиентской объектной модели. Для классов, которые начинаются с «Пакет обновления», имя клиента объектной модели имеет «Пакет обновления» удален. В других случаях указано имя клиента объектной модели. Имена элементов применяются в клиентской объектной модели, за исключением там, где указано иное.
  
    
    

### <a name="alternateurl-class"></a>Класс AlternateUrl

Представляет альтернативный URL-адрес для веб-приложения и зоны, к которой применяется.
  
    
    

```cs

public class AlternateUrl
```


#### <a name="properties"></a>Свойства

 **Uri** (только для чтения)
  
    
    
Возвращает URI альтернативный URL-адрес.
  
    
    



```cs
public String Uri
```

 **UrlZone** (только для чтения)
  
    
    
Получает зона альтернативного URL-адреса.
  
    
    



```
public UrlZone UrlZone
```

Класс UrlZone является версия объектной модели клиента класса SPUrlZone в серверной объектной модели. Дополнительные сведения о нем можно  [SharePoint 2010 Software Development Kit (SDK)](http://msdn.microsoft.com/en-us/library/ee557253.aspx).
  
    
    

### <a name="authenticationcompletedeventargs-class"></a>Класс AuthenticationCompletedEventArgs

Предоставляет данные о событии **AuthenticationCompleted**.
  
    
    

```cs
public sealed class AuthenticationCompletedEventArgs : AsyncCompletedEventArgs

```


#### <a name="constructors"></a>Конструкторы

Инициализирует новый экземпляр класса AuthenticationCompletedEventArgs.
  
    
    

```cs

public AuthenticationCompletedEventArgs(Exception error, bool canceled, HttpStatusCode userState)
```

 **Параметры**
  
    
    

-  _error_  это объект исключения, в случае отсутствия исключение при попытке проверки подлинности.
    
  
-  _canceled_ имеет значение true, если попытки проверки подлинности отменена, прежде чем оно может быть выполнен удачно или нет.
    
  
-  _userState_  это HttpStatusCode, возвращенные сервером.
    
  

#### <a name="properties"></a>Свойства

 **HttpStatusCode** (только для чтения)
  
    
    
Получает состояние, возвращенные сервером после при попытке проверки подлинности.
  
    
    



```cs
public HttpStatusCode HttpStatusCode
```


### <a name="authenticationstatus-enum"></a>Перечисление AuthenticationStatus

Указывает текущее состояние при попытке проверки подлинности.
  
    
    

- **NotStarted**
    
  
- **InProgress**
    
  
- **CompletedSuccess**
    
  
- **CompletedException**
    
  

### <a name="authenticator-class"></a>Класс проверки подлинности

Предоставляет методы для проверки подлинности пользователя на веб-сайте SharePoint.
  
    
    

```
public class Authenticator : ICredentials
```


#### <a name="constructors"></a>Конструкторы

Инициализирует новый экземпляр класса.
  
    
    

```cs
public Authenticator()

public Authenticator(Uri uagServerUrl)
```

 **Параметры**
  
    
    
 _uagServerUrl_  это полный URL-адрес сервера United Access Gateway (UAG).
  
    
    



```cs

public Authenticator(string userName, string password)
```

 **Параметры**
  
    
    
 _userName_  это имя для учетных данных.
  
    
    
 _password_  пароль для учетных данных.
  
    
    



```cs
public Authenticator(string userName, string password, string domain)
```

 **Параметры**
  
    
    
 _userName_  это имя для учетных данных.
  
    
    
 _password_  пароль для учетных данных.
  
    
    
 _domain_  это имя домена или компьютера, где проверяются учетные данные, обычно домена текущего пользователя.
  
    
    



```cs
public Authenticator(string userName, string password, Uri uagServerUrl)
```

 **Параметры**
  
    
    
 _userName_  это имя для учетных данных.
  
    
    
 _password_  пароль для учетных данных.
  
    
    
 _uagServerUrl_  это полный URL-адрес сервера United Access Gateway (UAG).
  
    
    



```cs
public Authenticator(string userName, string password, string domain, Uri uagServerUrl)
```

 **Параметры**
  
    
    
 _userName_  это имя для учетных данных.
  
    
    
 _password_  пароль для учетных данных.
  
    
    
 _domain_  это имя домена или компьютера, где проверяются учетные данные, обычно домена текущего пользователя.
  
    
    
 _uagServerUrl_  это полный URL-адрес сервера United Access Gateway (UAG).
  
    
    

#### <a name="methods"></a>Методы

 **ClearAllApplicationSettings**
  
    
    
Очищает все файлы cookie, учетные данные и параметры UAG из кэша.
  
    
    



```cs
public static void ClearAllApplicationSettings
```

 **ClearAllCookies**
  
    
    
Очищает все хранимые файлы cookie и присваивает свойству **Status** все объекты **Authenticator** значение **NotStarted**.
  
    
    



```cs
public static void ClearAllCookies()
```

 **ClearAllCredentials**
  
    
    
Очищает все учетные данные из кэша и устанавливает для свойства **Status** всех объектов **Authenticator** значение **NotStarted**.
  
    
    



```cs
public static void ClearAllCredentials()
```

 **GetCredential**
  
    
    
Возвращает объект учетных данных для указанного типа uri и режим проверки подлинности.
  
    
    



```
public NetworkCredential GetCredential(Uri uri, string authType)
```

 **Параметры**
  
    
    

-  _uri_  это URI, включая порт, для которого клиент предоставляет проверку подлинности.
    
  
-  _authType_  тип проверки подлинности, требуемой.
    
  
Этот метод используется только для анонимной проверки подлинности. Если  _authType_ не является "Basic", возвращается пустой объект. Дополнительные сведения о классе **NetworkCredential** можно [Класс NetworkCredential](http://msdn.microsoft.com/en-us/library/system.net.networkcredential.aspx).
  
    
    
 **IsRequestUnauthorized**
  
    
    
Возвращает значение true, если не удалось выполнить запрос авторизации из-за недопустимый файл cookie или учетные данные.
  
    
    



```cs
public static bool IsRequestUnauthorized(ClientRequestFailedEventArgs failedEventArgs)
```


#### <a name="properties"></a>Properties

 **AllowSmartRouting**
  
    
    
Получает или задает указывает, включена ли смарт-маршрутизации.
  
    
    



```
public bool AllowSmartRouting
```

При включении смарт-Маршрутизация объект **Authenticator** пытается подключиться к серверу под управлением SharePoint и сервер UAG и использует, какое из значений отвечает первым, как его канал связи. Если нет ни одного сервера UAG, это свойство игнорируется. Значение по умолчанию  **true**. Если параметр имеет значение **false**, сервер UAG всегда используется.
  
    
    
 **AuthenticatorMode**
  
    
    
Получает или задает режим проверки подлинности.
  
    
    



```cs
public ClientAuthenticationMode AuthenticationMode
```

Дополнительные сведения о **ClientAuthenticationMode** enum содержатся в этом документе.
  
    
    
 **CookieCachingEnabled**
  
    
    
Получает или задает указывает, является ли кэшируются файлы cookie.
  
    
    



```
public bool CookieCachingEnabled
```

Если включить кэширование файлов cookie, необходимо учитывайте, что файлы cookie к определенному моменту истечения срока действия. Если они истек срок действия при вызове **ExecuteQueryAsync**, затем происходит сбой и выполняется обратного вызова для сбоев. Соответственно Если этому свойству присвоено значение true, необходимо добавить код для обратного вызова для ошибки, очищает кэш в этом случае. Ниже приведен пример, где `execQueryArgs` имеет тип **ClientRequestFailedEventArgs**, переданного сбоя обратного вызова **ExecuteQueryAsync**.
  
    
    



```cs
if (Authenticator.IsRequestUnauthorized(execQueryArgs))
{
    (sender as Authenticator).ClearCookies();
}
```

 **CredentialCachingEnabled**
  
    
    
Получает или задает индикатор ли кэширование учетных данных.
  
    
    



```cs

public bool CredentialCachingEnabled
```

 **Domain**
  
    
    
Получает или задает домен или компьютер для учетных данных, обычно это домен текущего пользователя.
  
    
    



```cs
public string Domain
```

Если новое значение для этого свойства, свойство **Status** имеет значение NotStarted.
  
    
    
 **NavigateBackAfterAuthentication**
  
    
    
Получает или задает индикатор ли пользователь которому выполняется переход на предыдущую страницу со страницы входа в систему.
  
    
    



```cs
public bool NavigateBackAfterAuthentication
```

 **Password**
  
    
    
Получает или задает пароль для учетных данных.
  
    
    



```cs
public string Password
```

Если новое значение для этого свойства, свойство **Status** имеет значение **NotStarted**.
  
    
    
 **PromptOnFailure**
  
    
    
Получает или задает указывает, следует ли пользователь запрос на введите имя и пароль, если происходит сбой первоначальной проверки подлинности.
  
    
    



```cs
public bool PromptOnFailure
```

 **Status** (только для чтения)
  
    
    
Получает состояние попытки проверки подлинности.
  
    
    



```cs
public AuthenticationStatus Status
```

Просмотрите ранее в этом документе для получения сведений о классе **AuthenticationStatus**.
  
    
    
 **UagServerUrl**
  
    
    
Получает или задает URL-адрес сервера UAG.
  
    
    



```cs
public Uri UagServerUrl
```

 **Имя пользователя**
  
    
    
Получает или задает имя пользователя для учетных данных.
  
    
    



```cs
public string UserName
```

Если новое значение для этого свойства, свойство **Status** имеет значение **NotStarted**.
  
    
    

#### <a name="events"></a>События

 **AuthenticationCompleted**
  
    
    
Возникает после завершения попытки проверки подлинности, независимо от того, является ли выполнено успешно.
  
    
    



```cs
public event EventHandler<AuthenticationCompletedEventArgs> AuthenticationCompleted;
```


### <a name="clientauthenticationmode-enum"></a>Перечисление ClientAuthenticationMode

Задает режим проверки подлинности для объекта **Authenticator**. Это существующего enum, к которому новое значение **BrowserBasedAuthentication** был добавлен.
  
    
    


|**Значение по умолчанию**||
|:-----|:-----|
|**FormsAuthentication** <br/> |Представляет режим проверки подлинности на основе форм  <br/> |
|**Anonymous** <br/> |Представляет режим анонимного доступа  <br/> |
|**BrowserBasedAuthentication** <br/> |Представляет режим Microsoft Office Forms на основе проверки подлинности (MSOFBA)  <br/> |
   

### <a name="odataauthenticator-class"></a>Класс ODataAuthenticator

Предоставляет методы для проверки подлинности пользователя на веб-сайте SharePoint.
  
    
    

```cs
public class ODataAuthenticator : Authenticator
```


#### <a name="constructors"></a>Конструкторы

Конструкторы, совпадают конструкторы класса parent. Для получения дополнительных сведений см проверки подлинности данного документа.
  
    
    

#### <a name="methods"></a>Методы

 **Authenticate**
  
    
    
Выполняет проверку подлинности пользователя для указанного веб-сайта.
  
    
    



```cs
public new void Authenticate(Uri serverUrl)
```

Ключевое слово  `new` используется, поскольку в родительском классе внутренний метод с таким же именем.
  
    
    

#### <a name="properties"></a>Properties

 **CookieContainer** (только для чтения)
  
    
    
Получает контейнер с помощью файлов cookie для запросов к веб-сайту.
  
    
    



```cs
public new CookieContainer CookieContainer
```

Ключевое слово  `new` используется, поскольку в родительском классе внутренний метод с таким же именем.
  
    
    
 **ResolvedUrl** (только для чтения)
  
    
    
Получает URL-адрес, который используется для подключений к серверу, на котором работает SharePoint при использовании **ODataAuthenticator**. Это может быть опубликован на сервере UAG URL-адрес или, если свойство **AllowSmartRouting** имеет значение true, это может быть URL-адрес интрасети SharePoint, если он будет достигнуто первым при вызове метода **Authenticate**.
  
    
    



```cs
public Uri ResolvedUrl
```


### <a name="serversettings-class"></a>Класс ServerSettings

Предоставляет метод для получения альтернативные URL-адреса веб-приложения, который содержит веб-сайта.
  
    
    

```cs
public static class ServerSettings
```


#### <a name="methods"></a>Методы

 **GetAlternateUrls**
  
    
    
Получает альтернативные URL-адреса указанного веб-сайта.
  
    
    



```cs
public static ClientObjectList<AlternateUrl> GetAlternateUrls(ClientRuntimeContext context)
```

 **Параметры**
  
    
    
 _context_  это объект, представляющий текущий контекст клиента.
  
    
    
Просмотрите ранее в этом документе для получения сведений о классе **AlternateUrl**.
  
    
    

## <a name="server-object-model-for-sharepoint-mobility"></a>Серверная объектная модель для мобильной работы SharePoint
<a name="SP15OM_ServerOM"> </a>

Все классы в этом разделе содержатся в пространстве имен **Microsoft.SharePoint**. За исключением того, если он указан, все они доступны в клиентской объектной модели. Для классов, которые начинаются с «Пакет обновления», имя клиента объектной модели имеет «Пакет обновления» удален. В других случаях указано имя клиента объектной модели. Имена элементов применяются в клиентской объектной модели, за исключением там, где указано иное.
  
    
    

### <a name="geolocationfieldcontrol-class"></a>Класс GeolocationFieldControl

(Недоступно в клиентской объектной модели). 
  
    
    
Управляет визуализации поля **SPFieldGeolocation**. Объект этого типа используется как значение свойства **FieldRenderingControl** объекта **SPFieldGeolocation**.
  
    
    



```cs
public class GeolocationFieldControl : BaseFieldControl
```

Связи со этот класс также Обратите внимание, что существует шаблоны отображения двух: для режима отображения и для создания и редактирования режима. Они определены в файл % SHAREPOINTROOT%\\TEMPLATE\\ControlTemplates\\DefaultTemplates.ascx.
  
    
    

#### <a name="fields"></a>Fields

Факторы, используемые для отображения поля в режимах создания и редактирования.
  
    
    

```cs
protected TextBox m_latitudeBox;
protected TextBox m_longitudeBox;
protected Label m_longitudeLabel;
protected Label m_latitudeLabel;
```


#### <a name="methods"></a>Методы

Открытые свойства отсутствуют не полученных вводятся с помощью этого класса. Существует стандартного переопределения некоторых производные методов, как показано в следующей таблице.
  
    
    


|**Метод**|**В этом override???**|
|:-----|:-----|
|CreateChildControls  <br/> |Создает дочерние элементы управления, включая элемент управления карты JavaScript для режима отображения.  <br/> |
|центр конференций  <br/> |Переключает фокус дочернего элемента управления textbox долгота.  <br/> |
|OnPreRender  <br/> |Вызывает метод базового.  <br/> |
|Проверка  <br/> |Проверяет Широта и долгота значения, которые отображаются в пользовательском интерфейсе (UI). Не выполняет проверку свойства **Longitude** и **Latitude** базового объекта **SPFieldGeolocatonValue**, которое будет отличаться, если пользователь изменить одно или несколько из следующих значений в пользовательском Интерфейсе и не был сохранен изменения. <br/> |
   

#### <a name="properties"></a>Properties

Открытые свойства отсутствуют не полученных вводятся с помощью этого класса. Существует стандартного переопределения некоторых производные свойств, как указано в следующей таблице.
  
    
    


|**Свойство**|**Это переопределение...**|
|:-----|:-----|
|CssClass  <br/> |Ведет себя так же, как реализация parent.  <br/> |
|DefaultTemplateName  <br/> |Возвращает «GeolocationField»  <br/> |
|DisplayTemplateName  <br/> |Возвращает «GeolocationDisplayField»  <br/> |
|Значение  <br/> |Получает или задает значение, отображаемое с помощью объекта **SPFieldGeolocationValue**. <br/> |
   

### <a name="spfieldgeolocation-class"></a>Класс SPFieldGeolocation

Представляет поля (столбца), в котором размещается расположения в разных странах мира, определенные в долгота и широта и возможно высота.
  
    
    

```cs

public class SPFieldGeolocation : SPField
```

В связи с этот класс типа поля **Geolocation** определяется в % _SHAREPOINTROOT%_\\TEMPLATE\\XML\\fldtypes.xml.
  
    
    

#### <a name="constructors-overloaded"></a>Конструкторы (перегрузка)

Инициализирует новый экземпляр класса **SPFieldGeolocation**.
  
    
    

```cs
public SPFieldGeolocation(SPFieldCollection fields, string fieldName)
public SPFieldGeolocation(SPFieldCollection fields, string fieldName, string displayName)
```

 **Параметры**
  
    
    

-  _fields_ представляет коллекцию типов полей, к которым будет добавлен новый объект типа поля.
    
  
-  _fieldName_  это внутреннее имя нового типа поля.
    
  
-  _displayName_  это понятное имя нового типа поля.
    
  

#### <a name="methods"></a>Методы

 **GetFieldValueForClientRender**
  
    
    
Получает значение поля, чтобы он отображался на стороне клиента.
  
    
    



```cs

public override object GetFieldValueForClientRender(SPItem item, SPControlMode mode)
```

Параметры
  
    
    

-  _item_  это текущего элемента списка.
    
  
-  _mode_ является текущий режим отображения, такие как создание, изменение или отображение.
    
  
 **GetJsonClientFormFieldSchema**
  
    
    
Получает поле схемы в виде Нотация объектов JavaScript (JSON).
  
    
    



```cs
public override Dictionary<string, object> GetJsonClientFormFieldSchema(SPControlMode mode)
```

 **Параметры**
  
    
    
 _mode_ является текущий режим отображения, такие как создание, изменение или отображение.
  
    
    
 **ValidateAndParseValue**
  
    
    
Проверяет, что указанный элемент списка не равно null, а затем проверяется, что строка структурированы в соответствии с стандарты Open Consortium геопространственных (OGC) и возвращает его в качестве объекта, который является возможностью приведения к типу **SPFieldGeolocationValue**.
  
    
    



```cs
public override object ValidateAndParseValue(SPListItem item, string value)
```

 **Параметры**
  
    
    

-  _item_  элемент списка, который должен быть обновлено значением.
    
  
-  Строка  _value_ представляет значение географического расположения.
    
  
Следующие методы, стандартного переопределения унаследованных методов, которые были в SharePoint 2010. Сведения, относящиеся к этот класс является в следующей таблице.
  
    
    


|**Метод**|**Это переопределение...**|
|:-----|:-----|
|GetFieldValue (String s)  <br/> |Возвращает указанное значение как объект, который является возможностью приведения SPFieldGeolocationValue.  <br/> |
|GetFieldValueAsText (объект o)  <br/> |Перенос GetValidatedString.  <br/> |
|GetValidatedString (объект o)  <br/> |Проверяет, что указанное значение структурированы в соответствии с стандарты Open Consortium геопространственных (OGC) и возвращает как строку.  <br/> |
   

#### <a name="properties"></a>Properties

 **JSLink**
  
    
    
Получает или задает имя файла JavaScript, которая отображает поля типа **SPFieldGeolocation**.
  
> [!NOTE]
> [!Примечание] Перечислены JSLink, свойство не поддерживается в опросе или событий. Календарь SharePoint  это список событий. 
  
    
    




```cs
public override string JSLink
```

Значение по умолчанию  "clienttemplates.js| Geolocationfieldtemplate.js|SP.map.js".
  
    
    
 **FieldRenderingMobileWebControl**
  
    
    
Получает объект **SPMobileGeolocationField**, который отображает поле.
  
    
    



```cs
public override SPMobileBaseFieldControl FieldRenderingMobileControl
```

Это свойство заменяет устаревший **FieldRenderingMobileControl**.
  
    
    
Другие свойства  это стандартные переопределений наследуемые свойства, которые были в SharePoint 2010. Сведения, относящиеся к этот класс является в следующей таблице.
  
    
    


|**Свойство**|**Переопределение...**|
|:-----|:-----|
|FieldValueType  <br/> |Возвращает **typeof(SPFieldGeolocationValue)**.  <br/> |
|FieldRenderingControl  <br/> |Возвращает объект **GeolocationFieldControl**. <br/> |
|Filterable  <br/> |Возвращает **false**.  <br/> |
|Sortable  <br/> |Возвращает **false**.  <br/> |
|Устарел.  <br/> FieldRenderingMobileControl  <br/> |Возвращает объект **SPMobileGeolocationField**. <br/> |
   

### <a name="spfieldgeolocationvalue-class"></a>Класс SPFieldGeolocationValue

Представляет папку на разных странах мира, определенные в долгота и широта и возможно высота слишком.
  
    
    

```cs
public class SPFieldGeolocationValue : SPFieldGeographyValue
```


#### <a name="constructors-overloaded"></a>Конструкторы (перегрузка)

Инициализирует новый экземпляр класса **SPFieldGeolocationValue**.
  
    
    

```cs
public SPFieldGeolocationValue()
public SPFieldGeolocationValue(string fieldValue)
public SPFieldGeolocationValue(double latitude, double longitude)
public SPFieldGeolocationValue(double latitude, double longitude, double altitude, double measure)

```

 **Параметры**
  
    
    

-  _fieldValue_  это строка в одном из следующих форматов хорошо известные текста (WKT):
    
  - Приступая к работе "Точка ( _longitude_ _latitude_)", где  _longitude_ и _latitude_ являются строками из одного или нескольких цифр, при необходимости включая за один период (которые интерпретируются как десятичной запятой) и при необходимости с дефиса (которые интерпретируются как знак минус).
    
  
  - Приступая к работе "Точка ( _longitude_ _latitude_ _altitude_ _measure_)", где  _longitude_,  _latitude_,  _altitude_и  _measure_ являются строками из одного или нескольких цифр, при необходимости включая за один период (которые интерпретируются как десятичной запятой) и при необходимости с дефиса (которые интерпретируются как знак минус).
    
  
-  _latitude_ является Широта и должно быть между-90.0 и 90,0.
    
  
-  _longitude_ является долгота и должно быть между-180.0 и 180.0.
    
  
-  _altitude_  это высота.
    
  
-  _measure_  это альтернативное обозначение точки. Свойству **Measure** далее в этом разделе, для получения дополнительных сведений см.
    
  

#### <a name="methods"></a>Методы

 **ToString**
  
    
    
Это переопределение возвращает одно из следующих действий в зависимости от того, является ли **Altitude** или **Measure** свойств назначенных ненулевое значение.
  
    
    

- Если ни высота, ни мер назначенных ненулевое значение:
    
    Приступая к работе "Точка ( _longitude_ _latitude_)", где  _longitude_ и _latitude_ являются строками из одного или нескольких цифр, при необходимости включая за один период (которые интерпретируются как десятичной запятой) и при необходимости с дефиса (которые интерпретируются как знак минус).
    
  
- В противном случае (по крайней мере один из **Altitude** или **Measure** назначенных ненулевое значение):
    
    Приступая к работе "Точка (высота широта долгота мер)", где  _longitude_,  _latitude_,  _altitude_и  _measure_ являются строками из одного или нескольких цифр, при необходимости включая за один период (которые интерпретируются как десятичной запятой) и при необходимости с дефиса (которые интерпретируются как знак минус). Если **Altitude** или **Measure** не присвоен ненулевое значение, оно отображается как "0" в значение свойства **WellKnownText**. Обратное не хранит: Если **Altitude** или **Measure** отображается как 0, которая, возможно, поскольку он никогда не была назначена ненулевое значение, но может быть так, как она была назначена 0.
    
  



```cs

public override string ToString()
```

 **ToWellKnownText**
  
    
    
Перенос **ToString**.
  
    
    



```cs
public string ToWellKnownText()
```


#### <a name="properties"></a>Properties

 **Altitude**
  
    
    
Получает или задает высота расположения. Использование этого свойства является необязательной и предполагаемой единицы измерения (например, метры) и нулевой точки (например, уровень sea или центр earth) определенного пользователя.
  
    
    



```cs
public double Altitude
```

 **Latitude**
  
    
    
Получает или задает Широта расположения.
  
    
    



```cs
public double Latitude
```

Значение должно быть между-90.0 и 90,0.
  
    
    
 **Longitude**
  
    
    
Получает или задает Долгота расположения.
  
    
    



```cs
public double Longitude
```

Значение должно быть между-180.0 и 180.0...
  
    
    
 **Measure**
  
    
    
Получает или задает альтернативного обозначение точка расположении, определяемых пользователем. К примеру Если точку по магистраль с маркерами вех, это свойство может использоваться для хранения число вех, наиболее близко к точке. Если точка находится в общей области турпоходов с нумерованный campsites, это свойство может использоваться для хранения номера ближайшего campsite. Свойство семантика полностью определить пользователя и его использование не является обязательным.
  
    
    



```cs
public double Measure
```


### <a name="spfieldtype-enum"></a>Перечисление SPFieldType

Добавлен новое значение для данного перечисления:
  
    
    

```cs
Geolocation
```


### <a name="spphonenotificationcontent-class"></a>Класс SPPhoneNotificationContent

Базовый класс для классов, которые представляют содержимое phone уведомлений. Производные классы необходимо объявить поля или свойства для хранения контента и необходимо реализовать метод **PreparePayload** для преобразования содержимого в массив байтов.
  
    
    

```cs
public abstract class SPPhoneNotificationContent
```


#### <a name="methods"></a>Методы

 **PreparePayload**
  
    
    
При реализации в класс, производный преобразует содержимое в массив байтов, который отправляется по сети в службу уведомлений. Нет нет реализации по умолчанию, поэтому производный класс необходимо реализовать этот метод.
  
    
    



```cs
protected internal abstract byte[] PreparePayload();
```


#### <a name="properties"></a>Properties

 **NotificationType** (только для чтения)
  
    
    
Получает тип уведомления (например, плитки или всплывающего уведомления) предназначен контента.
  
    
    



```cs
public SPPhoneNotificationType NotificationType

```

Сведения о **SPPhoneNotificationType**содержатся в этом документе.
  
    
    
 **SubscriberType** (только для чтения)
  
    
    
Получает тип подписчика устройств, например, Windows Phone.
  
    
    



```cs

public SPPhoneNotificationSubscriberType SubscriberType
```

Сведения о **SPPhoneNotificationSubscriberType**содержатся в этом документе.
  
    
    

### <a name="spphonenotificationresponse-class"></a>Класс SPPhoneNotificationResponse

Отображает результат при попытке отправить уведомление.
  
    
    

```cs
public class SPPhoneNotificationResponse
```


#### <a name="methods"></a>Методы

 **Create**
  
    
    
Создает объект **SPPhoneNotificationResponse**.
  
    
    



```cs
public static SPPhoneNotificationResponse
Create(SPPhoneNotificationSubscriberType subscriberType, 
SPPhoneNotificationType notificationType, HttpWebResponse response)
```

 **Параметры**
  
    
    

-  _subscriberType_  это устройства, такие как Windows Phone 7.5.
    
  
-  _notificationType_  тип уведомлений, такие как всплывающее или плитки.
    
  
-  _response_  это объект HTTP-ответа, который был создан на сервере.
    
  
Дополнительные сведения о **SPPhoneNotificationSubscriberType** и **SPPhoneNotificationType**можно далее в этом документе.
  
    
    

#### <a name="properties"></a>Properties

 **NotificationType** (только для чтения)
  
    
    
Получает тип уведомления (например, всплывающее или заголовков).
  
    
    



```cs

public SPPhoneNotificationType NotificationType
```

Сведения о SPPhoneNotificationType содержатся в этом документе.
  
    
    
 **ServiceToken** (только для чтения)
  
    
    
Получает маркер службы уведомлений, который использовался в уведомлении.
  
    
    



```cs
public string ServiceToken
```

 **StatusCode** (только для чтения)
  
    
    
Получает код состояния HTTP. Строковая версия **HttpStatusCode** значение.
  
    
    



```cs
public string StatusCode
```

 **SubscriberType**
  
    
    
Получает или задает тип устройства, к которому было отправлено уведомление.
  
    
    



```cs
public SPPhoneNotificationSubscriberType SubscriberType
```

Сведения о **SPPhoneNotificationSubscriberType**содержатся в этом документе.
  
    
    
 **TimeStamp** (только для чтения)
  
    
    
Время UTC уведомления.
  
    
    



```cs
public DateTime Timestamp
```


### <a name="spphonenotificationsubscriber-class"></a>Класс SPPhoneNotificationSubscriber

Базовый класс для классов, которые представляют подписчика уведомлений, выданный приложения SharePoint на стороне сервера.
  
    
    

```cs
public abstract class SPPhoneNotificationSubscriber
```


#### <a name="methods"></a>Методы

Уведомления
  
    
    
Отправляет содержимое указанного уведомлений подписчика с проверки ошибок.
  
    
    



```cs
public SPPhoneNotificationResponse Notify(SPPhoneNotificationContent notificationContent)
```

 **Параметры**
  
    
    
 _notificationContent_, сведения о событии, инициирующую уведомления.
  
    
    
Этот метод не может быть переопределен. Он является оболочкой для метода абстрактный **NotifyInternal** и гарантирует, что некоторые проверки ошибок выполняется при вызове **NotifyInternal**.
  
    
    
Дополнительные сведения о классах **SPPhoneNotificationContent** и **SPPhoneNotificationResponse** можно выше в этом документе.
  
    
    
 **NotifyInternal**
  
    
    
При переопределении в производный класс, отправляет содержимое указанного уведомлений подписчика.
  
    
    



```cs
protected abstract SPPhoneNotificationResponse NotifyInternal(SPPhoneNotificationContent notificationContent);
```

 **Параметры**
  
    
    
 _notificationContent_, сведения о событии, инициирующую уведомления.
  
    
    
Дополнительные сведения о классах **SPPhoneNotificationContent** и **SPPhoneNotificationResponse** можно выше в этом документе.
  
    
    
 **ToString**
  
    
    
Возвращает свойства выбранного объекта в виде строки.
  
    
    



```cs
public override string ToString()
```

Реализация по умолчанию включает в себя свойства **ParentWeb**, **ApplicationTag**и **DeviceAppInstanceId**.
  
    
    
Update
  
    
    
Сохраняет объект (возможно, измененных) **SPPhoneNotificationSubscriber** хранилища подписчика веб-сайта.
  
    
    



```cs
public void Update()
```

 **ValidateSubscriberProperties**
  
    
    
При реализации в класс, производный проверяет выбранных свойств объекта.
  
    
    



```cs
protected abstract void ValidateSubscriberProperties();
```


#### <a name="properties"></a>Properties

 **CustomArgs**
  
    
    
Получает или задает строку пользовательские аргументы, который представляет состояние подписки на уведомления. Эта строка могут использоваться логики приложения для различения его подписчиков уведомлений для разных видов уведомлений.
  
    
    



```cs
public string CustomArgs
```

 **DeviceAppInstanceId** (только для чтения)
  
    
    
Получает идентификатор для конкретного экземпляра приложения на телефоне или другого мобильного устройства.
  
    
    



```cs
public Guid DeviceAppInstanceId
```

 **LastModifiedTimeStamp** (только для чтения)
  
    
    
Получает дату и время последнего изменения подписчика.
  
    
    



```cs
public DateTime LastModifiedTimeStamp
```

 **RegistrationTimeStamp** (только для чтения)
  
    
    
Получает дату и время, когда абонентского зарегистрированных для уведомлений.
  
    
    



```cs
public DateTime RegistrationTimeStamp
```

 **ServiceToken**
  
    
    
Получает или задает сведения о канала доставки, необходимая для службы уведомлений, такие как URI-канал.
  
    
    



```cs
public string ServiceToken
```

 **SubscriberType** (только для чтения)
  
    
    
Получает тип устройства, такие как Windows Phone 7.
  
    
    



```cs
public SPPhoneNotificationSubscriberType SubscriberType
```

Сведения о классе **SPPhoneNotificationSubscriberType** содержатся далее в этом документе.
  
    
    
 **User** (только для чтения)
  
    
    
Получает пользователя, который зарегистрирован для уведомлений.
  
    
    



```cs
public SPUser User
```


### <a name="spphonenotificationsubscribercollection-class"></a>Класс SPPhoneNotificationSubscriberCollection

Коллекция подписчиков уведомлений. Индексаторы **Int32** проходит объект коллекции.
  
    
    

```cs
public sealed class SPPhoneNotificationSubscriberCollection : SPBaseCollection
```


#### <a name="properties"></a>Properties

 **Count**
  
    
    
Возвращает число элементов в коллекции.
  
    
    



```cs
public override int Count
```


### <a name="spphonenotificationsubscribertype-enum"></a>Перечисление SPPhoneNotificationSubscriberType

Указывает тип устройства, который может получать уведомления.
  
    
    


|**Уведомление**|**Устройство**|
|:-----|:-----|
|||
|**WP7** <br/> |Windows Phone 7.5  <br/> |
|**Custom** <br/> |Все устройства, отличные от Windows Phone 7.5  <br/> |
   

### <a name="spphonenotificationtype-enum"></a>Перечисление SPPhoneNotificationType

Указывает тип уведомления.
  
    
    


|||
|:-----|:-----|
|**None** <br/> ||
|**Tile** <br/> ||
|**Toast** <br/> ||
|**Raw** <br/> ||
   

### <a name="spweb-class"></a>Класс SPWeb

Были добавлены следующие члены этого класса.
  
    
    

#### <a name="methods"></a>Методы

 **DoesPhoneNotificationSubscriberExist**
  
    
    
Получает значение, указывающее, является ли текущий пользователь подписчика для указанного экземпляра указанное приложение.
  
    
    



```cs
public bool DoesPhoneNotificationSubscriberExist(Guid deviceAppInstanceId)
```

 **GetPhoneNotificationSubscriber**
  
    
    
Получает подписчиков уведомлений с помощью указанного приложения и телефон идентификаторы из списка хранилища подписок уведомлений веб-сайта.
  
    
    



```cs
public SPPhoneNotificationSubscriber GetPhoneNotificationSubscriber(Guid deviceAppInstanceId)
```

 **Параметры**
  
    
    
 _deviceAppInstanceId_  это идентификатор экземпляра приложения на конкретных телефон или устройство.
  
    
    
Сведения о см класс **SPPhoneNotificationSubscriber** ранее в этом документе.
  
    
    
 **GetPhoneNotificationSubscribers** (перегрузка)
  
    
    
Получает коллекцию подписчиков уведомлений из списка хранилища подписок уведомлений веб-сайта, при необходимости фильтрации на код приложений телефона и, возможно, также на одном из следующих значений: некоторые пользовательские аргументы или пользователя.
  
    
    



```cs
public SPPhoneNotificationSubscriberCollection GetPhoneNotificationSubscribers(string customArgs)
```

> [!NOTE]
> [!Примечание] Имя объектной модели клиента  **GetPhoneNotificationSubscribersByArgs**. 
  
    
    




```cs
public SPPhoneNotificationSubscriberCollection GetPhoneNotificationSubscribers(string user)

```

> [!NOTE]
> [!Примечание] Имя объектной модели клиента  **GetPhoneNotificationSubscribersByUser**. 
  
    
    

 **Параметры**
  
    
    

-  _customArgs_  это дополнительные настраиваемые сведения, могут использовать несколько приложений с поддержкой уведомлений.
    
  
-  _user_  это пользователь, зарегистрированных для уведомлений.
    
  
Сведения о см класс **SPPhoneNotificationSubscriberCollection** ранее в этом документе.
  
    
    
 **RegisterPhoneNotificationSubscriber**
  
    
    
Регистрирует приложение phone на телефоне для получения уведомлений.
  
    
    



```cs

public SPPhoneNotificationSubscriber RegisterPhoneNotificationSubscriber(SPPhoneNotificationSubscriberType subscriberType, Guid deviceAppInstanceId, string serviceToken)
```

 **Параметры**
  
    
    

-  _subscriberType_  это тип устройства, такие как Windows Phone 7.
    
  
-  _deviceAppInstanceId_  это идентификатор экземпляра приложения на конкретных телефон или устройство.
    
  
-  _serviceToken_  это маркер, используемый службой уведомлений, который отправляет уведомления для подписчиков.
    
  
Сведения о **SPPhoneNotificationSubscriberType**содержатся в этом документе.
  
    
    
 **UnregisterPhoneNotificationSubscriber**
  
    
    
Отменяет регистрацию приложение phone на телефоне получать уведомления.
  
    
    



```cs
public void UnregisterPhoneNotificationSubscriber(Guid deviceAppInstanceId)
```

 **Параметры**
  
    
    
 _deviceAppInstanceId_  это идентификатор экземпляра приложения на конкретных телефон или устройство.
  
    
    

#### <a name="properties"></a>Properties

 **PhoneNotificationSubscribers** (только для чтения)
  
    
    
Получает коллекцию всех телефона подписчиков уведомлений в хранилище подписчика веб-сайта.
  
    
    



```cs
public SPPhoneNotificationSubscriberCollection PhoneNotificationSubscribers
```

Сведения о **SPPhoneNotificationSubscriberCollection** класса содержатся выше в этом документе.
  
    
    

### <a name="wp7notificationtilecontent-class"></a>Класс WP7NotificationTileContent

Представляет содержимое заголовков уведомлений.
  
    
    

```cs
public sealed class WP7NotificationTileContent : SPPhoneNotificationContent
```


#### <a name="constructors"></a>Конструкторы

Инициализирует новый экземпляр класса WP7NotificationTileContent.
  
    
    

```cs
public WP7NotificationTileContent()
```


#### <a name="methods"></a>Методы

 **PreparePayload**
  
    
    
Преобразует содержимое в массив **Byte**, отправляемые по сети в службу уведомлений.
  
    
    



```cs
protected internal override byte[] PreparePayload();
```


#### <a name="properties"></a>Properties

 **Count**
  
    
    
Получает или задает число уведомлений. Должна быть от -1 до 99 включительно.
  
    
    



```cs
public int Count
```

Для свойства значение -1, значение счетчика на иконку остаются без изменений.
  
    
    
 **Title**
  
    
    
Получает или задает заголовок заголовков уведомлений.
  
    
    



```cs
public string Title
```

 **BackgroundImagePath**
  
    
    
Получает или задает путь к плитки фонового изображения.
  
    
    



```cs
public string BackgroundImagePath
```

 **BackBackgroundImagePath**
  
    
    
Получает или задает фоновое изображение задней стороне транспонирования заголовков.
  
    
    



```cs
public string BackBackgroundImagePath
```

 **BackContent**
  
    
    
Получает или задает содержимое обратной стороне транспонирования заголовков.
  
    
    



```cs
public string BackContent
```

 **BackTitle**
  
    
    
Получает или задает заголовок, отображаемый на задней стороне транспонирования заголовков.
  
    
    



```cs
public string BackTitle
```

 **TileId**
  
    
    
Получает или задает идентификатор фрагмента.
  
    
    



```cs
public string TileId
```


### <a name="wp7notificationtoastcontent-class"></a>Класс WP7NotificationToastContent

Представляет содержимое всплывающее уведомление.
  
    
    

```cs
public sealed class WP7NotificationToastContent : SPPhoneNotificationContent
```


#### <a name="constructors"></a>Конструкторы

Инициализирует новый экземпляр класса WP7NotificationToastContent.
  
    
    

```cs
public WP7NotificationToastContent()
```


#### <a name="methods"></a>Методы

 **PreparePayload**
  
    
    
Преобразует содержимое в массив **Byte**, отправляемые по сети в службу уведомлений.
  
    
    



```cs
protected internal override byte[] PreparePayload();
```


#### <a name="properties"></a>Properties

 **Message**
  
    
    
Получает или задает сообщение всплывающее уведомление.
  
    
    



```cs
public string Message
```

 **Title**
  
    
    
Получает или задает заголовок всплывающее уведомление.
  
    
    



```cs
public string Title
```

 **Param**
  
    
    
Получает или задает пользовательских параметров данных, который передается в приложение-получатель, если пользователь отвечает на всплывающее уведомление.
  
    
    



```cs
public string Param
```

Это свойство можно использовать для передачи сведений в получающее приложение, например URL-адрес или набор пар "имя значение".
  
    
    

### <a name="wp7notificationrawcontent-class"></a>Класс WP7NotificationRawContent

Представляет содержимое необработанное уведомление.
  
    
    

```cs
public sealed class WP7NotificationRawContent : SPPhoneNotificationContent
```


#### <a name="constructors"></a>Конструкторы

Инициализирует новый экземпляр класса WP7NotificationRawContent.
  
    
    

```cs
public WP7NotificationRawContent()
```


#### <a name="methods"></a>Методы

 **PreparePayload**
  
    
    
Преобразует содержимое в массив байтов, который отправляется по сети в службу уведомлений.
  
    
    



```cs
protected internal override byte[] PreparePayload();
```


#### <a name="properties"></a>Properties

 **Message**
  
    
    
Получает или задает сообщение необработанное уведомление.
  
    
    



```cs
public string Message
```


### <a name="wp7phonenotificationresponse-class"></a>Класс WP7PhoneNotificationResponse

Отображает результат при попытке отправить уведомление подписчика Windows Phone 7.
  
    
    

```cs
public WP7PhoneNotificationResponse(SPPhoneNotificationType notificationType, HttpWebResponse response)
```

 **Параметры**
  
    
    

-  _notificationType_  тип уведомлений, такие как всплывающее или плитки.
    
  
-  _response_  это объект HTTP-ответа, который был создан на сервере.
    
  
Дополнительные сведения о **SPPhoneNotificationType**содержатся в этом документе.
  
    
    

#### <a name="properties"></a>Properties

 **NotificationStatus** (только для чтения)
  
    
    
Получает состояние уведомления, например, успешное или неудачное.
  
    
    



```cs
public string NotificationStatus
```

 **DeviceConnectionStatus** (только для чтения)
  
    
    
Получает состояние устройства во время уведомления.
  
    
    



```cs
public string DeviceConnectionStatus
```

 **SubscriptionStatus** (только для чтения)
  
    
    
Состояние подписки на устройство во время уведомления.
  
    
    



```cs
public string SubscriptionStatus
```

 **MessageId** (только для чтения)
  
    
    
Получает идентификатор сообщения, отправленного в уведомлении.
  
    
    



```
public string MessageId
```


## <a name="see-also"></a>См. также
<a name="SP15MobileOM_addlresources"> </a>


-  [Построение приложений Windows Phone, обращающихся к SharePoint](build-windows-phone-apps-that-access-sharepoint.md)
    
  
-  [Как: Настройка и использование push-уведомлений в SharePoint приложений для Windows Phone](how-to-configure-and-use-push-notifications-in-sharepoint-apps-for-windows.md)
    
  
-  [Интеграция расположение и карты функциональные возможности в SharePoint](integrating-location-and-map-functionality-in-sharepoint.md)
    
  
-  [Обзор объектной модели SharePoint мобильного клиента проверки подлинности](overview-of-the-sharepoint-mobile-client-authentication-object-model.md)
    
  

