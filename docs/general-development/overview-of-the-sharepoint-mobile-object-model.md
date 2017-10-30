---
title: "Обзор мобильных устройств объектной модели SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 72319846-d02d-49e7-b830-48eb8f5715cb
ms.openlocfilehash: 4f2f38a46c0afe3b534b7e2b2ee1c5a8dbbe0300
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="overview-of-the-sharepoint-mobile-object-model"></a><span data-ttu-id="6b0d4-102">Обзор мобильных устройств объектной модели SharePoint</span><span class="sxs-lookup"><span data-stu-id="6b0d4-102">Overview of the SharePoint mobile object model</span></span>
<span data-ttu-id="6b0d4-103">Узнайте о новых общим классам в серверной объектной модели SharePoint и клиентская объектная модель Silverlight, которые используются для разработки интегрированные решения для SharePoint и Windows Phone 7.5.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-103">Learn about the new public classes in the SharePoint server object model and Silverlight client object model that are used to develop integrated solutions for SharePoint and Windows Phone 7.5.</span></span>
## <a name="client-object-model-for-mobile-silverlight"></a><span data-ttu-id="6b0d4-104">Клиентская объектная модель для мобильных устройств Silverlight</span><span class="sxs-lookup"><span data-stu-id="6b0d4-104">Client object model for mobile Silverlight</span></span>
<span data-ttu-id="6b0d4-105"><a name="SP15OM_ClientOM"> </a></span><span class="sxs-lookup"><span data-stu-id="6b0d4-105"></span></span>

<span data-ttu-id="6b0d4-p101">Все классы в этом разделе содержатся в пространстве имен **Microsoft.SharePoint.Client**. В дополнение к API в этом разделе большая часть классов и членов в разделе Server объектной модели для мобильной работы SharePoint также можно вызвать в клиентской объектной модели. Для классов, которые начинаются с «Пакет обновления», имя клиента объектной модели имеет «Пакет обновления» удален. В других случаях указано имя клиента объектной модели. Имена элементов применяются в клиентской объектной модели, за исключением там, где указано иное.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-p101">All classes in this section are in the **Microsoft.SharePoint.Client** namespace. In addition to the APIs in this section, most of the classes and members in the section Server Object Model for SharePoint Mobility are also callable in the client object model. For classes that begin with "SP", the client object model name has the "SP" removed. In other cases, the client object model name is specified. Member names are the same in the client object model except where specified otherwise.</span></span>
  
    
    

### <a name="alternateurl-class"></a><span data-ttu-id="6b0d4-111">Класс AlternateUrl</span><span class="sxs-lookup"><span data-stu-id="6b0d4-111">AlternateUrl class</span></span>

<span data-ttu-id="6b0d4-112">Представляет альтернативный URL-адрес для веб-приложения и зоны, к которой применяется.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-112">Represents an alternative URL for a web application and the zone to which it applies.</span></span>
  
    
    

```cs

public class AlternateUrl
```


#### <a name="properties"></a><span data-ttu-id="6b0d4-113">Свойства</span><span class="sxs-lookup"><span data-stu-id="6b0d4-113">Properties</span></span>

 <span data-ttu-id="6b0d4-114">**Uri** (только для чтения)</span><span class="sxs-lookup"><span data-stu-id="6b0d4-114">**Uri** (read-only)</span></span>
  
    
    
<span data-ttu-id="6b0d4-115">Возвращает URI альтернативный URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-115">Gets the URI of the alternate URL.</span></span>
  
    
    



```cs
public String Uri
```

 <span data-ttu-id="6b0d4-116">**UrlZone** (только для чтения)</span><span class="sxs-lookup"><span data-stu-id="6b0d4-116">**UrlZone** (read-only)</span></span>
  
    
    
<span data-ttu-id="6b0d4-117">Получает зона альтернативного URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-117">Gets the zone of the alternate URL.</span></span>
  
    
    



```
public UrlZone UrlZone
```

<span data-ttu-id="6b0d4-p102">Класс UrlZone является версия объектной модели клиента класса SPUrlZone в серверной объектной модели. Дополнительные сведения о нем можно  [SharePoint 2010 Software Development Kit (SDK)](http://msdn.microsoft.com/en-us/library/ee557253.aspx).</span><span class="sxs-lookup"><span data-stu-id="6b0d4-p102">The UrlZone class is the client object model version of the SPUrlZone class in the server object model. For more information about it, see the  [SharePoint 2010 Software Development Kit (SDK)](http://msdn.microsoft.com/en-us/library/ee557253.aspx).</span></span>
  
    
    

### <a name="authenticationcompletedeventargs-class"></a><span data-ttu-id="6b0d4-120">Класс AuthenticationCompletedEventArgs</span><span class="sxs-lookup"><span data-stu-id="6b0d4-120">AuthenticationCompletedEventArgs class</span></span>

<span data-ttu-id="6b0d4-121">Предоставляет данные о событии **AuthenticationCompleted**.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-121">Provides data about an **AuthenticationCompleted** event.</span></span>
  
    
    

```cs
public sealed class AuthenticationCompletedEventArgs : AsyncCompletedEventArgs

```


#### <a name="constructors"></a><span data-ttu-id="6b0d4-122">Конструкторы</span><span class="sxs-lookup"><span data-stu-id="6b0d4-122">Constructors</span></span>

<span data-ttu-id="6b0d4-123">Инициализирует новый экземпляр класса AuthenticationCompletedEventArgs.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-123">Initializes a new instance of the AuthenticationCompletedEventArgs class.</span></span>
  
    
    

```cs

public AuthenticationCompletedEventArgs(Exception error, bool canceled, HttpStatusCode userState)
```

 <span data-ttu-id="6b0d4-124">**Параметры**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-124">**Parameters**</span></span>
  
    
    

-  <span data-ttu-id="6b0d4-125">_error_  это объект исключения, в случае отсутствия исключение при попытке проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-125">_error_ is the Exception object if there was an exception thrown in the authentication attempt.</span></span>
    
  
-  <span data-ttu-id="6b0d4-126">_canceled_ имеет значение true, если попытки проверки подлинности отменена, прежде чем оно может быть выполнен удачно или нет.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-126">_canceled_ is true if the authentication attempt was canceled before it could succeed or fail.</span></span>
    
  
-  <span data-ttu-id="6b0d4-127">_userState_  это HttpStatusCode, возвращенные сервером.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-127">_userState_ is the HttpStatusCode returned by the server.</span></span>
    
  

#### <a name="properties"></a><span data-ttu-id="6b0d4-128">Свойства</span><span class="sxs-lookup"><span data-stu-id="6b0d4-128">Properties</span></span>

 <span data-ttu-id="6b0d4-129">**HttpStatusCode** (только для чтения)</span><span class="sxs-lookup"><span data-stu-id="6b0d4-129">**HttpStatusCode** (read-only)</span></span>
  
    
    
<span data-ttu-id="6b0d4-130">Получает состояние, возвращенные сервером после при попытке проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-130">Gets the status returned by the server after an authentication attempt.</span></span>
  
    
    



```cs
public HttpStatusCode HttpStatusCode
```


### <a name="authenticationstatus-enum"></a><span data-ttu-id="6b0d4-131">Перечисление AuthenticationStatus</span><span class="sxs-lookup"><span data-stu-id="6b0d4-131">AuthenticationStatus enum</span></span>

<span data-ttu-id="6b0d4-132">Указывает текущее состояние при попытке проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-132">Specifies the current state of an authentication attempt.</span></span>
  
    
    

- <span data-ttu-id="6b0d4-133">**NotStarted**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-133">**NotStarted**</span></span>
    
  
- <span data-ttu-id="6b0d4-134">**InProgress**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-134">**InProgress**</span></span>
    
  
- <span data-ttu-id="6b0d4-135">**CompletedSuccess**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-135">**CompletedSuccess**</span></span>
    
  
- <span data-ttu-id="6b0d4-136">**CompletedException**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-136">**CompletedException**</span></span>
    
  

### <a name="authenticator-class"></a><span data-ttu-id="6b0d4-137">Класс проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="6b0d4-137">Authenticator class</span></span>

<span data-ttu-id="6b0d4-138">Предоставляет методы для проверки подлинности пользователя на веб-сайте SharePoint.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-138">Provides methods for authenticating a user on a SharePoint website.</span></span>
  
    
    

```
public class Authenticator : ICredentials
```


#### <a name="constructors"></a><span data-ttu-id="6b0d4-139">Конструкторы</span><span class="sxs-lookup"><span data-stu-id="6b0d4-139">Constructors</span></span>

<span data-ttu-id="6b0d4-140">Инициализирует новый экземпляр класса.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-140">Initializes a new instance of the class.</span></span>
  
    
    

```cs
public Authenticator()

public Authenticator(Uri uagServerUrl)
```

 <span data-ttu-id="6b0d4-141">**Параметры**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-141">**Parameters**</span></span>
  
    
    
 <span data-ttu-id="6b0d4-142">_uagServerUrl_  это полный URL-адрес сервера United Access Gateway (UAG).</span><span class="sxs-lookup"><span data-stu-id="6b0d4-142">_uagServerUrl_ is the absolute URL of a United Access Gateway (UAG) server.</span></span>
  
    
    



```cs

public Authenticator(string userName, string password)
```

 <span data-ttu-id="6b0d4-143">**Параметры**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-143">**Parameters**</span></span>
  
    
    
 <span data-ttu-id="6b0d4-144">_userName_  это имя для учетных данных.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-144">_userName_ is the name for the credentials.</span></span>
  
    
    
 <span data-ttu-id="6b0d4-145">_password_  пароль для учетных данных.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-145">_password_ is the password for the credentials.</span></span>
  
    
    



```cs
public Authenticator(string userName, string password, string domain)
```

 <span data-ttu-id="6b0d4-146">**Параметры**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-146">**Parameters**</span></span>
  
    
    
 <span data-ttu-id="6b0d4-147">_userName_  это имя для учетных данных.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-147">_userName_ is the name for the credentials.</span></span>
  
    
    
 <span data-ttu-id="6b0d4-148">_password_  пароль для учетных данных.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-148">_password_ is the password for the credentials.</span></span>
  
    
    
 <span data-ttu-id="6b0d4-149">_domain_  это имя домена или компьютера, где проверяются учетные данные, обычно домена текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-149">_domain_ is the name of the domain or computer where the credentials are verified, typically the domain of the current user.</span></span>
  
    
    



```cs
public Authenticator(string userName, string password, Uri uagServerUrl)
```

 <span data-ttu-id="6b0d4-150">**Параметры**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-150">**Parameters**</span></span>
  
    
    
 <span data-ttu-id="6b0d4-151">_userName_  это имя для учетных данных.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-151">_userName_ is the name for the credentials.</span></span>
  
    
    
 <span data-ttu-id="6b0d4-152">_password_  пароль для учетных данных.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-152">_password_ is the password for the credentials.</span></span>
  
    
    
 <span data-ttu-id="6b0d4-153">_uagServerUrl_  это полный URL-адрес сервера United Access Gateway (UAG).</span><span class="sxs-lookup"><span data-stu-id="6b0d4-153">_uagServerUrl_ is the absolute URL of a United Access Gateway (UAG) server.</span></span>
  
    
    



```cs
public Authenticator(string userName, string password, string domain, Uri uagServerUrl)
```

 <span data-ttu-id="6b0d4-154">**Параметры**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-154">**Parameters**</span></span>
  
    
    
 <span data-ttu-id="6b0d4-155">_userName_  это имя для учетных данных.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-155">_userName_ is the name for the credentials.</span></span>
  
    
    
 <span data-ttu-id="6b0d4-156">_password_  пароль для учетных данных.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-156">_password_ is the password for the credentials.</span></span>
  
    
    
 <span data-ttu-id="6b0d4-157">_domain_  это имя домена или компьютера, где проверяются учетные данные, обычно домена текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-157">_domain_ is the name of the domain or computer where the credentials are verified, typically the domain of the current user.</span></span>
  
    
    
 <span data-ttu-id="6b0d4-158">_uagServerUrl_  это полный URL-адрес сервера United Access Gateway (UAG).</span><span class="sxs-lookup"><span data-stu-id="6b0d4-158">_uagServerUrl_ is the absolute URL of a United Access Gateway (UAG) server.</span></span>
  
    
    

#### <a name="methods"></a><span data-ttu-id="6b0d4-159">Методы</span><span class="sxs-lookup"><span data-stu-id="6b0d4-159">Methods</span></span>

 <span data-ttu-id="6b0d4-160">**ClearAllApplicationSettings**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-160">**ClearAllApplicationSettings**</span></span>
  
    
    
<span data-ttu-id="6b0d4-161">Очищает все файлы cookie, учетные данные и параметры UAG из кэша.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-161">Clears all cookies, credentials, and UAG settings from the cache.</span></span>
  
    
    



```cs
public static void ClearAllApplicationSettings
```

 <span data-ttu-id="6b0d4-162">**ClearAllCookies**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-162">**ClearAllCookies**</span></span>
  
    
    
<span data-ttu-id="6b0d4-163">Очищает все хранимые файлы cookie и присваивает свойству **Status** все объекты **Authenticator** значение **NotStarted**.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-163">Clears all stored cookies and sets the **Status** property of all **Authenticator** objects to **NotStarted**.</span></span>
  
    
    



```cs
public static void ClearAllCookies()
```

 <span data-ttu-id="6b0d4-164">**ClearAllCredentials**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-164">**ClearAllCredentials**</span></span>
  
    
    
<span data-ttu-id="6b0d4-165">Очищает все учетные данные из кэша и устанавливает для свойства **Status** всех объектов **Authenticator** значение **NotStarted**.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-165">Clears all credentials from the cache and sets the **Status** property of all **Authenticator** objects to **NotStarted**.</span></span>
  
    
    



```cs
public static void ClearAllCredentials()
```

 <span data-ttu-id="6b0d4-166">**GetCredential**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-166">**GetCredential**</span></span>
  
    
    
<span data-ttu-id="6b0d4-167">Возвращает объект учетных данных для указанного типа uri и режим проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-167">Gets a credential object for the specified uri and authentication type.</span></span>
  
    
    



```
public NetworkCredential GetCredential(Uri uri, string authType)
```

 <span data-ttu-id="6b0d4-168">**Параметры**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-168">**Parameters**</span></span>
  
    
    

-  <span data-ttu-id="6b0d4-169">_uri_  это URI, включая порт, для которого клиент предоставляет проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-169">_uri_ is the URI, including port, for which the client is providing authentication.</span></span>
    
  
-  <span data-ttu-id="6b0d4-170">_authType_  тип проверки подлинности, требуемой.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-170">_authType_ is the type of authentication requested.</span></span>
    
  
<span data-ttu-id="6b0d4-p103">Этот метод используется только для анонимной проверки подлинности. Если  _authType_ не является "Basic", возвращается пустой объект. Дополнительные сведения о классе **NetworkCredential** можно [Класс NetworkCredential](http://msdn.microsoft.com/en-us/library/system.net.networkcredential.aspx).</span><span class="sxs-lookup"><span data-stu-id="6b0d4-p103">This method is only used for anonymous authentication. If  _authType_ is not "Basic", an empty object is returned. For more information about the **NetworkCredential** class, see [NetworkCredential Class](http://msdn.microsoft.com/en-us/library/system.net.networkcredential.aspx).</span></span>
  
    
    
 <span data-ttu-id="6b0d4-174">**IsRequestUnauthorized**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-174">**IsRequestUnauthorized**</span></span>
  
    
    
<span data-ttu-id="6b0d4-175">Возвращает значение true, если не удалось выполнить запрос авторизации из-за недопустимый файл cookie или учетные данные.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-175">Returns true if the authorization request failed because of an invalid cookie or credentials.</span></span>
  
    
    



```cs
public static bool IsRequestUnauthorized(ClientRequestFailedEventArgs failedEventArgs)
```


#### <a name="properties"></a><span data-ttu-id="6b0d4-176">Properties</span><span class="sxs-lookup"><span data-stu-id="6b0d4-176">Properties</span></span>

 <span data-ttu-id="6b0d4-177">**AllowSmartRouting**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-177">**AllowSmartRouting**</span></span>
  
    
    
<span data-ttu-id="6b0d4-178">Получает или задает указывает, включена ли смарт-маршрутизации.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-178">Gets or sets an indicator of whether smart routing is enabled.</span></span>
  
    
    



```
public bool AllowSmartRouting
```

<span data-ttu-id="6b0d4-p104">При включении смарт-Маршрутизация объект **Authenticator** пытается подключиться к серверу под управлением SharePoint и сервер UAG и использует, какое из значений отвечает первым, как его канал связи. Если нет ни одного сервера UAG, это свойство игнорируется. Значение по умолчанию  **true**. Если параметр имеет значение **false**, сервер UAG всегда используется.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-p104">When smart routing is enabled, the **Authenticator** object tries to connect to the server that is running SharePoint and the UAG server and uses whichever responds first as its communication channel. If there is no UAG server, this property is ignored. The default is **true**. If set to **false**, the UAG server is always used.</span></span>
  
    
    
 <span data-ttu-id="6b0d4-183">**AuthenticatorMode**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-183">**AuthenticatorMode**</span></span>
  
    
    
<span data-ttu-id="6b0d4-184">Получает или задает режим проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-184">Gets or sets the authentication mode.</span></span>
  
    
    



```cs
public ClientAuthenticationMode AuthenticationMode
```

<span data-ttu-id="6b0d4-185">Дополнительные сведения о **ClientAuthenticationMode** enum содержатся в этом документе.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-185">For more information about the **ClientAuthenticationMode** enum, see later in this document.</span></span>
  
    
    
 <span data-ttu-id="6b0d4-186">**CookieCachingEnabled**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-186">**CookieCachingEnabled**</span></span>
  
    
    
<span data-ttu-id="6b0d4-187">Получает или задает указывает, является ли кэшируются файлы cookie.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-187">Gets or sets an indicator of whether cookies are cached.</span></span>
  
    
    



```
public bool CookieCachingEnabled
```

<span data-ttu-id="6b0d4-p105">Если включить кэширование файлов cookie, необходимо учитывайте, что файлы cookie к определенному моменту истечения срока действия. Если они истек срок действия при вызове **ExecuteQueryAsync**, затем происходит сбой и выполняется обратного вызова для сбоев. Соответственно Если этому свойству присвоено значение true, необходимо добавить код для обратного вызова для ошибки, очищает кэш в этом случае. Ниже приведен пример, где `execQueryArgs` имеет тип **ClientRequestFailedEventArgs**, переданного сбоя обратного вызова **ExecuteQueryAsync**.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-p105">If you enable caching of cookies, consider that the cookies expire at some point. If they are expired when **ExecuteQueryAsync** is called, then it fails and the callback for failure runs. Accordingly, if you set this property to true, you must add code to the callback for failure that clears the cache if this happens. Here is an example, where `execQueryArgs` is of the type **ClientRequestFailedEventArgs** passed in the failure callback of **ExecuteQueryAsync**.</span></span>
  
    
    



```cs
if (Authenticator.IsRequestUnauthorized(execQueryArgs))
{
    (sender as Authenticator).ClearCookies();
}
```

 <span data-ttu-id="6b0d4-192">**CredentialCachingEnabled**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-192">**CredentialCachingEnabled**</span></span>
  
    
    
<span data-ttu-id="6b0d4-193">Получает или задает индикатор ли кэширование учетных данных.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-193">Gets or sets an indicator of whether credentials are cached.</span></span>
  
    
    



```cs

public bool CredentialCachingEnabled
```

 <span data-ttu-id="6b0d4-194">**Domain**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-194">**Domain**</span></span>
  
    
    
<span data-ttu-id="6b0d4-195">Получает или задает домен или компьютер для учетных данных, обычно это домен текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-195">Gets or sets the domain or computer for the credential, usually this is the domain of the current user.</span></span>
  
    
    



```cs
public string Domain
```

<span data-ttu-id="6b0d4-196">Если новое значение для этого свойства, свойство **Status** имеет значение NotStarted.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-196">When this property is set to a new value, the **Status** property is set to NotStarted.</span></span>
  
    
    
 <span data-ttu-id="6b0d4-197">**NavigateBackAfterAuthentication**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-197">**NavigateBackAfterAuthentication**</span></span>
  
    
    
<span data-ttu-id="6b0d4-198">Получает или задает индикатор ли пользователь которому выполняется переход на предыдущую страницу со страницы входа в систему.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-198">Gets or sets a indicator of whether the user should be navigated back to the previous page from the login page.</span></span>
  
    
    



```cs
public bool NavigateBackAfterAuthentication
```

 <span data-ttu-id="6b0d4-199">**Password**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-199">**Password**</span></span>
  
    
    
<span data-ttu-id="6b0d4-200">Получает или задает пароль для учетных данных.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-200">Gets or sets the password for the credential.</span></span>
  
    
    



```cs
public string Password
```

<span data-ttu-id="6b0d4-201">Если новое значение для этого свойства, свойство **Status** имеет значение **NotStarted**.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-201">When this property is set to a new value, the **Status** property is set to **NotStarted**.</span></span>
  
    
    
 <span data-ttu-id="6b0d4-202">**PromptOnFailure**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-202">**PromptOnFailure**</span></span>
  
    
    
<span data-ttu-id="6b0d4-203">Получает или задает указывает, следует ли пользователь запрос на введите имя и пароль, если происходит сбой первоначальной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-203">Gets or sets an indicator of whether the user should be prompted to enter a name and password if initial authentication fails.</span></span>
  
    
    



```cs
public bool PromptOnFailure
```

 <span data-ttu-id="6b0d4-204">**Status** (только для чтения)</span><span class="sxs-lookup"><span data-stu-id="6b0d4-204">**Status** (read-only)</span></span>
  
    
    
<span data-ttu-id="6b0d4-205">Получает состояние попытки проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-205">Gets the status of the attempt to authenticate.</span></span>
  
    
    



```cs
public AuthenticationStatus Status
```

<span data-ttu-id="6b0d4-206">Просмотрите ранее в этом документе для получения сведений о классе **AuthenticationStatus**.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-206">See earlier in this document for information about the **AuthenticationStatus** class.</span></span>
  
    
    
 <span data-ttu-id="6b0d4-207">**UagServerUrl**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-207">**UagServerUrl**</span></span>
  
    
    
<span data-ttu-id="6b0d4-208">Получает или задает URL-адрес сервера UAG.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-208">Gets or sets the URL of the UAG server.</span></span>
  
    
    



```cs
public Uri UagServerUrl
```

 <span data-ttu-id="6b0d4-209">**Имя пользователя**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-209">**UserName**</span></span>
  
    
    
<span data-ttu-id="6b0d4-210">Получает или задает имя пользователя для учетных данных.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-210">Gets or sets the user name for the credential.</span></span>
  
    
    



```cs
public string UserName
```

<span data-ttu-id="6b0d4-211">Если новое значение для этого свойства, свойство **Status** имеет значение **NotStarted**.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-211">When this property is set to a new value, the **Status** property is set to **NotStarted**.</span></span>
  
    
    

#### <a name="events"></a><span data-ttu-id="6b0d4-212">События</span><span class="sxs-lookup"><span data-stu-id="6b0d4-212">Events</span></span>

 <span data-ttu-id="6b0d4-213">**AuthenticationCompleted**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-213">**AuthenticationCompleted**</span></span>
  
    
    
<span data-ttu-id="6b0d4-214">Возникает после завершения попытки проверки подлинности, независимо от того, является ли выполнено успешно.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-214">Raised when the authentication attempt is completed, regardless of whether it succeeded.</span></span>
  
    
    



```cs
public event EventHandler<AuthenticationCompletedEventArgs> AuthenticationCompleted;
```


### <a name="clientauthenticationmode-enum"></a><span data-ttu-id="6b0d4-215">Перечисление ClientAuthenticationMode</span><span class="sxs-lookup"><span data-stu-id="6b0d4-215">ClientAuthenticationMode enum</span></span>

<span data-ttu-id="6b0d4-p106">Задает режим проверки подлинности для объекта **Authenticator**. Это существующего enum, к которому новое значение **BrowserBasedAuthentication** был добавлен.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-p106">Specifies an authentication mode for an **Authenticator** object. This is an existing enum to which a new value, **BrowserBasedAuthentication** has been added.</span></span>
  
    
    


|<span data-ttu-id="6b0d4-218">**Значение по умолчанию**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-218">**Default**</span></span>||
|:-----|:-----|
|<span data-ttu-id="6b0d4-219">**FormsAuthentication**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-219">**FormsAuthentication**</span></span> <br/> |<span data-ttu-id="6b0d4-220">Представляет режим проверки подлинности на основе форм</span><span class="sxs-lookup"><span data-stu-id="6b0d4-220">Represents forms-based authentication mode</span></span>  <br/> |
|<span data-ttu-id="6b0d4-221">**Anonymous**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-221">**Anonymous**</span></span> <br/> |<span data-ttu-id="6b0d4-222">Представляет режим анонимного доступа</span><span class="sxs-lookup"><span data-stu-id="6b0d4-222">Represents anonymous access mode</span></span>  <br/> |
|<span data-ttu-id="6b0d4-223">**BrowserBasedAuthentication**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-223">**BrowserBasedAuthentication**</span></span> <br/> |<span data-ttu-id="6b0d4-224">Представляет режим Microsoft Office Forms на основе проверки подлинности (MSOFBA)</span><span class="sxs-lookup"><span data-stu-id="6b0d4-224">Represents Microsoft Office Forms Based Authentication (MSOFBA) mode</span></span>  <br/> |
   

### <a name="odataauthenticator-class"></a><span data-ttu-id="6b0d4-225">Класс ODataAuthenticator</span><span class="sxs-lookup"><span data-stu-id="6b0d4-225">ODataAuthenticator class</span></span>

<span data-ttu-id="6b0d4-226">Предоставляет методы для проверки подлинности пользователя на веб-сайте SharePoint.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-226">Provides methods for authenticating a user on a SharePoint website.</span></span>
  
    
    

```cs
public class ODataAuthenticator : Authenticator
```


#### <a name="constructors"></a><span data-ttu-id="6b0d4-227">Конструкторы</span><span class="sxs-lookup"><span data-stu-id="6b0d4-227">Constructors</span></span>

<span data-ttu-id="6b0d4-p107">Конструкторы, совпадают конструкторы класса parent. Для получения дополнительных сведений см проверки подлинности данного документа.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-p107">The constructors are identical to the parent class constructors. For more information, see Authenticator Class earlier in this document.</span></span>
  
    
    

#### <a name="methods"></a><span data-ttu-id="6b0d4-230">Методы</span><span class="sxs-lookup"><span data-stu-id="6b0d4-230">Methods</span></span>

 <span data-ttu-id="6b0d4-231">**Authenticate**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-231">**Authenticate**</span></span>
  
    
    
<span data-ttu-id="6b0d4-232">Выполняет проверку подлинности пользователя для указанного веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-232">Authenticates a user to the specified website.</span></span>
  
    
    



```cs
public new void Authenticate(Uri serverUrl)
```

<span data-ttu-id="6b0d4-233">Ключевое слово  `new` используется, поскольку в родительском классе внутренний метод с таким же именем.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-233">The  `new` keyword is used because the parent class has an internal method of the same name.</span></span>
  
    
    

#### <a name="properties"></a><span data-ttu-id="6b0d4-234">Properties</span><span class="sxs-lookup"><span data-stu-id="6b0d4-234">Properties</span></span>

 <span data-ttu-id="6b0d4-235">**CookieContainer** (только для чтения)</span><span class="sxs-lookup"><span data-stu-id="6b0d4-235">**CookieContainer** (read-only)</span></span>
  
    
    
<span data-ttu-id="6b0d4-236">Получает контейнер с помощью файлов cookie для запросов к веб-сайту.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-236">Gets a container with the cookies for requests to the website.</span></span>
  
    
    



```cs
public new CookieContainer CookieContainer
```

<span data-ttu-id="6b0d4-237">Ключевое слово  `new` используется, поскольку в родительском классе внутренний метод с таким же именем.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-237">The  `new` keyword is used because the parent class has an internal method of the same name.</span></span>
  
    
    
 <span data-ttu-id="6b0d4-238">**ResolvedUrl** (только для чтения)</span><span class="sxs-lookup"><span data-stu-id="6b0d4-238">**ResolvedUrl** (read-only)</span></span>
  
    
    
<span data-ttu-id="6b0d4-p108">Получает URL-адрес, который используется для подключений к серверу, на котором работает SharePoint при использовании **ODataAuthenticator**. Это может быть опубликован на сервере UAG URL-адрес или, если свойство **AllowSmartRouting** имеет значение true, это может быть URL-адрес интрасети SharePoint, если он будет достигнуто первым при вызове метода **Authenticate**.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-p108">Gets the URL that is used for communication to the server that is running SharePoint when an **ODataAuthenticator** is being used. This may be the URL published on the UAG server or, if the **AllowSmartRouting** property is true, this may be the SharePoint intranet URL if it is reached first when the **Authenticate** method is called.</span></span>
  
    
    



```cs
public Uri ResolvedUrl
```


### <a name="serversettings-class"></a><span data-ttu-id="6b0d4-241">Класс ServerSettings</span><span class="sxs-lookup"><span data-stu-id="6b0d4-241">ServerSettings class</span></span>

<span data-ttu-id="6b0d4-242">Предоставляет метод для получения альтернативные URL-адреса веб-приложения, который содержит веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-242">Provides a method for getting the Alternate URLs of the web application that contains a website.</span></span>
  
    
    

```cs
public static class ServerSettings
```


#### <a name="methods"></a><span data-ttu-id="6b0d4-243">Методы</span><span class="sxs-lookup"><span data-stu-id="6b0d4-243">Methods</span></span>

 <span data-ttu-id="6b0d4-244">**GetAlternateUrls**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-244">**GetAlternateUrls**</span></span>
  
    
    
<span data-ttu-id="6b0d4-245">Получает альтернативные URL-адреса указанного веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-245">Gets the alternate URLs of the specified website.</span></span>
  
    
    



```cs
public static ClientObjectList<AlternateUrl> GetAlternateUrls(ClientRuntimeContext context)
```

 <span data-ttu-id="6b0d4-246">**Параметры**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-246">**Parameters**</span></span>
  
    
    
 <span data-ttu-id="6b0d4-247">_context_  это объект, представляющий текущий контекст клиента.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-247">_context_ is the an object that represents the current client context.</span></span>
  
    
    
<span data-ttu-id="6b0d4-248">Просмотрите ранее в этом документе для получения сведений о классе **AlternateUrl**.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-248">See earlier in this document for information about the **AlternateUrl** class.</span></span>
  
    
    

## <a name="server-object-model-for-sharepoint-mobility"></a><span data-ttu-id="6b0d4-249">Серверная объектная модель для мобильной работы SharePoint</span><span class="sxs-lookup"><span data-stu-id="6b0d4-249">Server object model for SharePoint mobility</span></span>
<span data-ttu-id="6b0d4-250"><a name="SP15OM_ServerOM"> </a></span><span class="sxs-lookup"><span data-stu-id="6b0d4-250"></span></span>

<span data-ttu-id="6b0d4-p109">Все классы в этом разделе содержатся в пространстве имен **Microsoft.SharePoint**. За исключением того, если он указан, все они доступны в клиентской объектной модели. Для классов, которые начинаются с «Пакет обновления», имя клиента объектной модели имеет «Пакет обновления» удален. В других случаях указано имя клиента объектной модели. Имена элементов применяются в клиентской объектной модели, за исключением там, где указано иное.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-p109">All classes in this section are in the **Microsoft.SharePoint** namespace. Except where specified, these are all available also in the client object model. For classes that begin with "SP", the client object model name has the "SP" removed. In other cases, the client object model name is specified. Member names are the same in the client object model except where specified otherwise.</span></span>
  
    
    

### <a name="geolocationfieldcontrol-class"></a><span data-ttu-id="6b0d4-256">Класс GeolocationFieldControl</span><span class="sxs-lookup"><span data-stu-id="6b0d4-256">GeolocationFieldControl class</span></span>

<span data-ttu-id="6b0d4-257">(Недоступно в клиентской объектной модели).</span><span class="sxs-lookup"><span data-stu-id="6b0d4-257">(Not available in client object model.)</span></span> 
  
    
    
<span data-ttu-id="6b0d4-p110">Управляет визуализации поля **SPFieldGeolocation**. Объект этого типа используется как значение свойства **FieldRenderingControl** объекта **SPFieldGeolocation**.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-p110">Governs the rendering of **SPFieldGeolocation** fields. An object of this type is used as the value of the **FieldRenderingControl** property of a **SPFieldGeolocation** object.</span></span>
  
    
    



```cs
public class GeolocationFieldControl : BaseFieldControl
```

<span data-ttu-id="6b0d4-p111">Связи со этот класс также Обратите внимание, что существует шаблоны отображения двух: для режима отображения и для создания и редактирования режима. Они определены в файл % SHAREPOINTROOT%\\TEMPLATE\\ControlTemplates\\DefaultTemplates.ascx.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-p111">In connection with this class, note also that there are two rendering templates, one for Display mode and one for New and Edit mode. They are defined in the file %SHAREPOINTROOT%\\TEMPLATE\\ControlTemplates\\DefaultTemplates.ascx.</span></span>
  
    
    

#### <a name="fields"></a><span data-ttu-id="6b0d4-262">Fields</span><span class="sxs-lookup"><span data-stu-id="6b0d4-262">Fields</span></span>

<span data-ttu-id="6b0d4-263">Факторы, используемые для отображения поля в режимах создания и редактирования.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-263">The following are used to render the field in the New and Edit modes.</span></span>
  
    
    

```cs
protected TextBox m_latitudeBox;
protected TextBox m_longitudeBox;
protected Label m_longitudeLabel;
protected Label m_latitudeLabel;
```


#### <a name="methods"></a><span data-ttu-id="6b0d4-264">Методы</span><span class="sxs-lookup"><span data-stu-id="6b0d4-264">Methods</span></span>

<span data-ttu-id="6b0d4-p112">Открытые свойства отсутствуют не полученных вводятся с помощью этого класса. Существует стандартного переопределения некоторых производные методов, как показано в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-p112">No non-derived public properties are introduced with this class. There are standard overrides of some derived methods as indicated in the following table.</span></span>
  
    
    


|<span data-ttu-id="6b0d4-267">**Метод**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-267">**Method**</span></span>|<span data-ttu-id="6b0d4-268">**В этом override???**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-268">**This override???**</span></span>|
|:-----|:-----|
|<span data-ttu-id="6b0d4-269">CreateChildControls</span><span class="sxs-lookup"><span data-stu-id="6b0d4-269">CreateChildControls</span></span>  <br/> |<span data-ttu-id="6b0d4-270">Создает дочерние элементы управления, включая элемент управления карты JavaScript для режима отображения.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-270">Creates the child controls including a JavaScript map control for Display mode.</span></span>  <br/> |
|<span data-ttu-id="6b0d4-271">центр конференций</span><span class="sxs-lookup"><span data-stu-id="6b0d4-271">Focus</span></span>  <br/> |<span data-ttu-id="6b0d4-272">Переключает фокус дочернего элемента управления textbox долгота.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-272">Gives focus to the longitude textbox child control.</span></span>  <br/> |
|<span data-ttu-id="6b0d4-273">OnPreRender</span><span class="sxs-lookup"><span data-stu-id="6b0d4-273">OnPreRender</span></span>  <br/> |<span data-ttu-id="6b0d4-274">Вызывает метод базового.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-274">Calls the base method.</span></span>  <br/> |
|<span data-ttu-id="6b0d4-275">Проверка</span><span class="sxs-lookup"><span data-stu-id="6b0d4-275">Validate</span></span>  <br/> |<span data-ttu-id="6b0d4-p113">Проверяет Широта и долгота значения, которые отображаются в пользовательском интерфейсе (UI). Не выполняет проверку свойства **Longitude** и **Latitude** базового объекта **SPFieldGeolocatonValue**, которое будет отличаться, если пользователь изменить одно или несколько из следующих значений в пользовательском Интерфейсе и не был сохранен изменения. </span><span class="sxs-lookup"><span data-stu-id="6b0d4-p113">Validates the latitude and longitude values that appear in the user interface (UI). This does not validate the **Longitude** and **Latitude** properties of the underlying **SPFieldGeolocatonValue** object, which will differ if the user has changed one or more of these values in the UI and not yet saved the changes. </span></span><br/> |
   

#### <a name="properties"></a><span data-ttu-id="6b0d4-278">Properties</span><span class="sxs-lookup"><span data-stu-id="6b0d4-278">Properties</span></span>

<span data-ttu-id="6b0d4-p114">Открытые свойства отсутствуют не полученных вводятся с помощью этого класса. Существует стандартного переопределения некоторых производные свойств, как указано в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-p114">No non-derived public properties are introduced with this class. There are standard overrides of some derived properties as indicated in the following table.</span></span>
  
    
    


|<span data-ttu-id="6b0d4-281">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-281">**Property**</span></span>|<span data-ttu-id="6b0d4-282">**Это переопределение...**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-282">**This override...**</span></span>|
|:-----|:-----|
|<span data-ttu-id="6b0d4-283">CssClass</span><span class="sxs-lookup"><span data-stu-id="6b0d4-283">CssClass</span></span>  <br/> |<span data-ttu-id="6b0d4-284">Ведет себя так же, как реализация parent.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-284">Behaves just like the parent implementation.</span></span>  <br/> |
|<span data-ttu-id="6b0d4-285">DefaultTemplateName</span><span class="sxs-lookup"><span data-stu-id="6b0d4-285">DefaultTemplateName</span></span>  <br/> |<span data-ttu-id="6b0d4-286">Возвращает «GeolocationField»</span><span class="sxs-lookup"><span data-stu-id="6b0d4-286">Returns "GeolocationField"</span></span>  <br/> |
|<span data-ttu-id="6b0d4-287">DisplayTemplateName</span><span class="sxs-lookup"><span data-stu-id="6b0d4-287">DisplayTemplateName</span></span>  <br/> |<span data-ttu-id="6b0d4-288">Возвращает «GeolocationDisplayField»</span><span class="sxs-lookup"><span data-stu-id="6b0d4-288">Returns "GeolocationDisplayField"</span></span>  <br/> |
|<span data-ttu-id="6b0d4-289">Значение</span><span class="sxs-lookup"><span data-stu-id="6b0d4-289">Value</span></span>  <br/> |<span data-ttu-id="6b0d4-290">Получает или задает значение, отображаемое с помощью объекта **SPFieldGeolocationValue**.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-290">Gets or sets the value that is rendered by using a **SPFieldGeolocationValue** object.</span></span> <br/> |
   

### <a name="spfieldgeolocation-class"></a><span data-ttu-id="6b0d4-291">Класс SPFieldGeolocation</span><span class="sxs-lookup"><span data-stu-id="6b0d4-291">SPFieldGeolocation class</span></span>

<span data-ttu-id="6b0d4-292">Представляет поля (столбца), в котором размещается расположения в разных странах мира, определенные в долгота и широта и возможно высота.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-292">Represents a field (column) that holds a location on the globe defined by longitude, latitude, and possibly altitude.</span></span>
  
    
    

```cs

public class SPFieldGeolocation : SPField
```

<span data-ttu-id="6b0d4-293">В связи с этот класс типа поля **Geolocation** определяется в % _SHAREPOINTROOT%_\\TEMPLATE\\XML\\fldtypes.xml.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-293">In connection with this class, the **Geolocation** field type is defined in % _SHAREPOINTROOT%_\\TEMPLATE\\XML\\fldtypes.xml.</span></span>
  
    
    

#### <a name="constructors-overloaded"></a><span data-ttu-id="6b0d4-294">Конструкторы (перегрузка)</span><span class="sxs-lookup"><span data-stu-id="6b0d4-294">Constructors (overloaded)</span></span>

<span data-ttu-id="6b0d4-295">Инициализирует новый экземпляр класса **SPFieldGeolocation**.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-295">Initializes a new instance of the **SPFieldGeolocation** class.</span></span>
  
    
    

```cs
public SPFieldGeolocation(SPFieldCollection fields, string fieldName)
public SPFieldGeolocation(SPFieldCollection fields, string fieldName, string displayName)
```

 <span data-ttu-id="6b0d4-296">**Параметры**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-296">**Parameters**</span></span>
  
    
    

-  <span data-ttu-id="6b0d4-297">_fields_ представляет коллекцию типов полей, к которым будет добавлен новый объект типа поля.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-297">_fields_ is the collection of field types to which the new field type object is added.</span></span>
    
  
-  <span data-ttu-id="6b0d4-298">_fieldName_  это внутреннее имя нового типа поля.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-298">_fieldName_ is an internal name of the new field type.</span></span>
    
  
-  <span data-ttu-id="6b0d4-299">_displayName_  это понятное имя нового типа поля.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-299">_displayName_ is a friendly name of the new field type.</span></span>
    
  

#### <a name="methods"></a><span data-ttu-id="6b0d4-300">Методы</span><span class="sxs-lookup"><span data-stu-id="6b0d4-300">Methods</span></span>

 <span data-ttu-id="6b0d4-301">**GetFieldValueForClientRender**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-301">**GetFieldValueForClientRender**</span></span>
  
    
    
<span data-ttu-id="6b0d4-302">Получает значение поля, чтобы он отображался на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-302">Gets the value of the field so that it can be rendered on the client.</span></span>
  
    
    



```cs

public override object GetFieldValueForClientRender(SPItem item, SPControlMode mode)
```

<span data-ttu-id="6b0d4-303">Параметры</span><span class="sxs-lookup"><span data-stu-id="6b0d4-303">Parameters</span></span>
  
    
    

-  <span data-ttu-id="6b0d4-304">_item_  это текущего элемента списка.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-304">_item_ is the current list item.</span></span>
    
  
-  <span data-ttu-id="6b0d4-305">_mode_ является текущий режим отображения, такие как создание, изменение или отображение.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-305">_mode_ is the current rendering mode such as New, Edit, or Display.</span></span>
    
  
 <span data-ttu-id="6b0d4-306">**GetJsonClientFormFieldSchema**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-306">**GetJsonClientFormFieldSchema**</span></span>
  
    
    
<span data-ttu-id="6b0d4-307">Получает поле схемы в виде Нотация объектов JavaScript (JSON).</span><span class="sxs-lookup"><span data-stu-id="6b0d4-307">Gets the field schema as JavaScript Object Notation (JSON).</span></span>
  
    
    



```cs
public override Dictionary<string, object> GetJsonClientFormFieldSchema(SPControlMode mode)
```

 <span data-ttu-id="6b0d4-308">**Параметры**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-308">**Parameters**</span></span>
  
    
    
 <span data-ttu-id="6b0d4-309">_mode_ является текущий режим отображения, такие как создание, изменение или отображение.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-309">_mode_ is the current rendering mode such as New, Edit, or Display.</span></span>
  
    
    
 <span data-ttu-id="6b0d4-310">**ValidateAndParseValue**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-310">**ValidateAndParseValue**</span></span>
  
    
    
<span data-ttu-id="6b0d4-311">Проверяет, что указанный элемент списка не равно null, а затем проверяется, что строка структурированы в соответствии с стандарты Open Consortium геопространственных (OGC) и возвращает его в качестве объекта, который является возможностью приведения к типу **SPFieldGeolocationValue**.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-311">Verifies that the specified list item is not null and then verifies that the string is structured in compliance with Open Geospatial Consortium (OGC) standards and returns it as an object that is castable to the **SPFieldGeolocationValue** type.</span></span>
  
    
    



```cs
public override object ValidateAndParseValue(SPListItem item, string value)
```

 <span data-ttu-id="6b0d4-312">**Параметры**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-312">**Parameters**</span></span>
  
    
    

-  <span data-ttu-id="6b0d4-313">_item_  элемент списка, который должен быть обновлено значением.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-313">_item_ is a list item that is to be updated with the value.</span></span>
    
  
-  <span data-ttu-id="6b0d4-314">Строка  _value_ представляет значение географического расположения.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-314">_value_ is a string representation of a geolocation value.</span></span>
    
  
<span data-ttu-id="6b0d4-p115">Следующие методы, стандартного переопределения унаследованных методов, которые были в SharePoint 2010. Сведения, относящиеся к этот класс является в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-p115">The following methods are standard overrides of inherited methods that were in SharePoint 2010. The specific information for this class is in the following table.</span></span>
  
    
    


|<span data-ttu-id="6b0d4-317">**Метод**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-317">**Method**</span></span>|<span data-ttu-id="6b0d4-318">**Это переопределение...**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-318">**This override...**</span></span>|
|:-----|:-----|
|<span data-ttu-id="6b0d4-319">GetFieldValue (String s)</span><span class="sxs-lookup"><span data-stu-id="6b0d4-319">GetFieldValue(String s)</span></span>  <br/> |<span data-ttu-id="6b0d4-320">Возвращает указанное значение как объект, который является возможностью приведения SPFieldGeolocationValue.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-320">Returns the specified value as an Object that is castable to SPFieldGeolocationValue.</span></span>  <br/> |
|<span data-ttu-id="6b0d4-321">GetFieldValueAsText (объект o)</span><span class="sxs-lookup"><span data-stu-id="6b0d4-321">GetFieldValueAsText(Object o)</span></span>  <br/> |<span data-ttu-id="6b0d4-322">Перенос GetValidatedString.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-322">Wraps GetValidatedString.</span></span>  <br/> |
|<span data-ttu-id="6b0d4-323">GetValidatedString (объект o)</span><span class="sxs-lookup"><span data-stu-id="6b0d4-323">GetValidatedString(Object o)</span></span>  <br/> |<span data-ttu-id="6b0d4-324">Проверяет, что указанное значение структурированы в соответствии с стандарты Open Consortium геопространственных (OGC) и возвращает как строку.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-324">Verifies that the specified value is structured in compliance with Open Geospatial Consortium (OGC) standards and returns it as a string.</span></span>  <br/> |
   

#### <a name="properties"></a><span data-ttu-id="6b0d4-325">Properties</span><span class="sxs-lookup"><span data-stu-id="6b0d4-325">Properties</span></span>

 <span data-ttu-id="6b0d4-326">**JSLink**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-326">**JSLink**</span></span>
  
    
    
<span data-ttu-id="6b0d4-327">Получает или задает имя файла JavaScript, которая отображает поля типа **SPFieldGeolocation**.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-327">Gets or sets the name of the JavaScript file that renders the fields of the **SPFieldGeolocation** type.</span></span>
  
    
    

> <span data-ttu-id="6b0d4-328">**Примечание:** Перечислены JSLink, свойство не поддерживается в опросе или событий.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-328">**Note:** The JSLink property is not supported on Survey or Events lists.</span></span> <span data-ttu-id="6b0d4-329">Календарь SharePoint — это список событий.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-329">A SharePoint calendar is an Events list.</span></span> 
  
    
    




```cs
public override string JSLink
```

<span data-ttu-id="6b0d4-330">Значение по умолчанию  "clienttemplates.js| Geolocationfieldtemplate.js|SP.map.js".</span><span class="sxs-lookup"><span data-stu-id="6b0d4-330">The default value is "clienttemplates.js|Geolocationfieldtemplate.js|sp.map.js".</span></span>
  
    
    
 <span data-ttu-id="6b0d4-331">**FieldRenderingMobileWebControl**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-331">**FieldRenderingMobileWebControl**</span></span>
  
    
    
<span data-ttu-id="6b0d4-332">Получает объект **SPMobileGeolocationField**, который отображает поле.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-332">Gets the **SPMobileGeolocationField** object that renders the field.</span></span>
  
    
    



```cs
public override SPMobileBaseFieldControl FieldRenderingMobileControl
```

<span data-ttu-id="6b0d4-333">Это свойство заменяет устаревший **FieldRenderingMobileControl**.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-333">This property replaces the obsolete **FieldRenderingMobileControl**.</span></span>
  
    
    
<span data-ttu-id="6b0d4-p117">Другие свойства  это стандартные переопределений наследуемые свойства, которые были в SharePoint 2010. Сведения, относящиеся к этот класс является в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-p117">The other properties are standard overrides of inherited properties that were in SharePoint 2010. The specific information for this class is in the following table.</span></span>
  
    
    


|<span data-ttu-id="6b0d4-336">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-336">**Property**</span></span>|<span data-ttu-id="6b0d4-337">**Переопределение...**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-337">**The override...**</span></span>|
|:-----|:-----|
|<span data-ttu-id="6b0d4-338">FieldValueType</span><span class="sxs-lookup"><span data-stu-id="6b0d4-338">FieldValueType</span></span>  <br/> |<span data-ttu-id="6b0d4-339">Возвращает **typeof(SPFieldGeolocationValue)**.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-339">Returns **typeof(SPFieldGeolocationValue)**.</span></span>  <br/> |
|<span data-ttu-id="6b0d4-340">FieldRenderingControl</span><span class="sxs-lookup"><span data-stu-id="6b0d4-340">FieldRenderingControl</span></span>  <br/> |<span data-ttu-id="6b0d4-341">Возвращает объект **GeolocationFieldControl**.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-341">Returns a **GeolocationFieldControl** object.</span></span> <br/> |
|<span data-ttu-id="6b0d4-342">Filterable</span><span class="sxs-lookup"><span data-stu-id="6b0d4-342">Filterable</span></span>  <br/> |<span data-ttu-id="6b0d4-343">Возвращает **false**.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-343">Returns **false**.</span></span>  <br/> |
|<span data-ttu-id="6b0d4-344">Sortable</span><span class="sxs-lookup"><span data-stu-id="6b0d4-344">Sortable</span></span>  <br/> |<span data-ttu-id="6b0d4-345">Возвращает **false**.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-345">Returns **false**.</span></span>  <br/> |
|<span data-ttu-id="6b0d4-346">Устарел.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-346">[Obsolete]</span></span>  <br/> <span data-ttu-id="6b0d4-347">FieldRenderingMobileControl</span><span class="sxs-lookup"><span data-stu-id="6b0d4-347">FieldRenderingMobileControl</span></span>  <br/> |<span data-ttu-id="6b0d4-348">Возвращает объект **SPMobileGeolocationField**.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-348">Returns a **SPMobileGeolocationField** object.</span></span> <br/> |
   

### <a name="spfieldgeolocationvalue-class"></a><span data-ttu-id="6b0d4-349">Класс SPFieldGeolocationValue</span><span class="sxs-lookup"><span data-stu-id="6b0d4-349">SPFieldGeolocationValue class</span></span>

<span data-ttu-id="6b0d4-350">Представляет папку на разных странах мира, определенные в долгота и широта и возможно высота слишком.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-350">Represents a location on the globe defined by longitude, latitude, and possibly altitude too.</span></span>
  
    
    

```cs
public class SPFieldGeolocationValue : SPFieldGeographyValue
```


#### <a name="constructors-overloaded"></a><span data-ttu-id="6b0d4-351">Конструкторы (перегрузка)</span><span class="sxs-lookup"><span data-stu-id="6b0d4-351">Constructors (overloaded)</span></span>

<span data-ttu-id="6b0d4-352">Инициализирует новый экземпляр класса **SPFieldGeolocationValue**.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-352">Initializes a new instance of the **SPFieldGeolocationValue** class.</span></span>
  
    
    

```cs
public SPFieldGeolocationValue()
public SPFieldGeolocationValue(string fieldValue)
public SPFieldGeolocationValue(double latitude, double longitude)
public SPFieldGeolocationValue(double latitude, double longitude, double altitude, double measure)

```

 <span data-ttu-id="6b0d4-353">**Параметры**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-353">**Parameters**</span></span>
  
    
    

-  <span data-ttu-id="6b0d4-354">_fieldValue_  это строка в одном из следующих форматов хорошо известные текста (WKT):</span><span class="sxs-lookup"><span data-stu-id="6b0d4-354">_fieldValue_ is a string in one of the following Well-Known Text (WKT) formats:</span></span>
    
  - <span data-ttu-id="6b0d4-355">Приступая к работе "Точка ( _longitude_ _latitude_)", где  _longitude_ и _latitude_ являются строками из одного или нескольких цифр, при необходимости включая за один период (которые интерпретируются как десятичной запятой) и при необходимости с дефиса (которые интерпретируются как знак минус).</span><span class="sxs-lookup"><span data-stu-id="6b0d4-355">"Point( _longitude_ _latitude_)", where  _longitude_ and _latitude_ are strings of one or more numerals, optionally including one period (which is interpreted as a decimal point) and optionally beginning with a hyphen (which is interpreted as a negative sign).</span></span>
    
  
  - <span data-ttu-id="6b0d4-356">Приступая к работе "Точка ( _longitude_ _latitude_ _altitude_ _measure_)", где  _longitude_,  _latitude_,  _altitude_и  _measure_ являются строками из одного или нескольких цифр, при необходимости включая за один период (которые интерпретируются как десятичной запятой) и при необходимости с дефиса (которые интерпретируются как знак минус).</span><span class="sxs-lookup"><span data-stu-id="6b0d4-356">"Point( _longitude_ _latitude_ _altitude_ _measure_)", where  _longitude_,  _latitude_,  _altitude_, and  _measure_ are strings of one or more numerals, optionally including one period (which is interpreted as a decimal point) and optionally beginning with a hyphen (which is interpreted as a negative sign).</span></span>
    
  
-  <span data-ttu-id="6b0d4-357">_latitude_ является Широта и должно быть между-90.0 и 90,0.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-357">_latitude_ is the latitude and must be between -90.0 and 90.0.</span></span>
    
  
-  <span data-ttu-id="6b0d4-358">_longitude_ является долгота и должно быть между-180.0 и 180.0.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-358">_longitude_ is the longitude and must be between -180.0 and 180.0.</span></span>
    
  
-  <span data-ttu-id="6b0d4-359">_altitude_  это высота.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-359">_altitude_ is the altitude.</span></span>
    
  
-  <span data-ttu-id="6b0d4-p118">_measure_  это альтернативное обозначение точки. Свойству **Measure** далее в этом разделе, для получения дополнительных сведений см.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-p118">_measure_ is an alternate designation of the point. See the **Measure** property later in this section for more information.</span></span>
    
  

#### <a name="methods"></a><span data-ttu-id="6b0d4-362">Методы</span><span class="sxs-lookup"><span data-stu-id="6b0d4-362">Methods</span></span>

 <span data-ttu-id="6b0d4-363">**ToString**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-363">**ToString**</span></span>
  
    
    
<span data-ttu-id="6b0d4-364">Это переопределение возвращает одно из следующих действий в зависимости от того, является ли **Altitude** или **Measure** свойств назначенных ненулевое значение.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-364">This override returns one of the following, depending on whether the **Altitude** or **Measure** properties have been assigned a non-null value.</span></span>
  
    
    

- <span data-ttu-id="6b0d4-365">Если ни высота, ни мер назначенных ненулевое значение:</span><span class="sxs-lookup"><span data-stu-id="6b0d4-365">If neither Altitude nor Measure have been assigned a non-null value:</span></span>
    
    <span data-ttu-id="6b0d4-366">Приступая к работе "Точка ( _longitude_ _latitude_)", где  _longitude_ и _latitude_ являются строками из одного или нескольких цифр, при необходимости включая за один период (которые интерпретируются как десятичной запятой) и при необходимости с дефиса (которые интерпретируются как знак минус).</span><span class="sxs-lookup"><span data-stu-id="6b0d4-366">"Point( _longitude_ _latitude_)", where  _longitude_ and _latitude_ are strings of one or more numerals, optionally including one period (which is interpreted as a decimal point) and optionally beginning with a hyphen (which is interpreted as a negative sign).</span></span>
    
  
- <span data-ttu-id="6b0d4-367">В противном случае (по крайней мере один из **Altitude** или **Measure** назначенных ненулевое значение):</span><span class="sxs-lookup"><span data-stu-id="6b0d4-367">Otherwise (at least one of **Altitude** or **Measure** have been assigned a non-null value):</span></span>
    
    <span data-ttu-id="6b0d4-p119">Приступая к работе "Точка (высота широта долгота мер)", где  _longitude_,  _latitude_,  _altitude_и  _measure_ являются строками из одного или нескольких цифр, при необходимости включая за один период (которые интерпретируются как десятичной запятой) и при необходимости с дефиса (которые интерпретируются как знак минус). Если **Altitude** или **Measure** не присвоен ненулевое значение, оно отображается как "0" в значение свойства **WellKnownText**. Обратное не хранит: Если **Altitude** или **Measure** отображается как 0, которая, возможно, поскольку он никогда не была назначена ненулевое значение, но может быть так, как она была назначена 0.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-p119">"Point(longitude latitude altitude measure)", where  _longitude_,  _latitude_,  _altitude_, and  _measure_ are strings of one or more numerals, optionally including one period (which is interpreted as a decimal point) and optionally beginning with a hyphen (which is interpreted as a negative sign). If either **Altitude** or **Measure** has not been assigned a non-null value, it is reported as "0" in the value of the **WellKnownText** property. The converse does not hold: if either **Altitude** or **Measure** is reported as 0, that might be because it was never assigned a non-null value, but it might be because it was assigned 0.</span></span>
    
  



```cs

public override string ToString()
```

 <span data-ttu-id="6b0d4-371">**ToWellKnownText**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-371">**ToWellKnownText**</span></span>
  
    
    
<span data-ttu-id="6b0d4-372">Перенос **ToString**.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-372">Wraps **ToString**.</span></span>
  
    
    



```cs
public string ToWellKnownText()
```


#### <a name="properties"></a><span data-ttu-id="6b0d4-373">Properties</span><span class="sxs-lookup"><span data-stu-id="6b0d4-373">Properties</span></span>

 <span data-ttu-id="6b0d4-374">**Altitude**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-374">**Altitude**</span></span>
  
    
    
<span data-ttu-id="6b0d4-p120">Получает или задает высота расположения. Использование этого свойства является необязательной и предполагаемой единицы измерения (например, метры) и нулевой точки (например, уровень sea или центр earth) определенного пользователя.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-p120">Gets or sets the altitude of the location. Use of this property is optional and the assumed unit-of-measure (for example, meters) and zero-point (for example, sea level or center-of-the-earth) is user-defined.</span></span>
  
    
    



```cs
public double Altitude
```

 <span data-ttu-id="6b0d4-377">**Latitude**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-377">**Latitude**</span></span>
  
    
    
<span data-ttu-id="6b0d4-378">Получает или задает Широта расположения.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-378">Gets or sets the latitude of the location.</span></span>
  
    
    



```cs
public double Latitude
```

<span data-ttu-id="6b0d4-379">Значение должно быть между-90.0 и 90,0.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-379">The value must be between -90.0 and 90.0.</span></span>
  
    
    
 <span data-ttu-id="6b0d4-380">**Longitude**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-380">**Longitude**</span></span>
  
    
    
<span data-ttu-id="6b0d4-381">Получает или задает Долгота расположения.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-381">Gets or sets the longitude of the location.</span></span>
  
    
    



```cs
public double Longitude
```

<span data-ttu-id="6b0d4-382">Значение должно быть между-180.0 и 180.0...</span><span class="sxs-lookup"><span data-stu-id="6b0d4-382">The value must be between -180.0 and 180.0..</span></span>
  
    
    
 <span data-ttu-id="6b0d4-383">**Measure**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-383">**Measure**</span></span>
  
    
    
<span data-ttu-id="6b0d4-p121">Получает или задает альтернативного обозначение точка расположении, определяемых пользователем. К примеру Если точку по магистраль с маркерами вех, это свойство может использоваться для хранения число вех, наиболее близко к точке. Если точка находится в общей области турпоходов с нумерованный campsites, это свойство может использоваться для хранения номера ближайшего campsite. Свойство семантика полностью определить пользователя и его использование не является обязательным.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-p121">Gets or sets a user-defined alternate designation of the location point. For example, if the point is along a highway with milestone markers, this property could be used to hold the number of the milestone that is nearest to the point. If the point is in a public camping area with numbered campsites, this property could be used to hold the number of the nearest campsite. The semantics of the property are entirely user-determined and its use is optional.</span></span>
  
    
    



```cs
public double Measure
```


### <a name="spfieldtype-enum"></a><span data-ttu-id="6b0d4-388">Перечисление SPFieldType</span><span class="sxs-lookup"><span data-stu-id="6b0d4-388">SPFieldType enum</span></span>

<span data-ttu-id="6b0d4-389">Добавлен новое значение для данного перечисления:</span><span class="sxs-lookup"><span data-stu-id="6b0d4-389">A new value has been added to this enum:</span></span>
  
    
    

```cs
Geolocation
```


### <a name="spphonenotificationcontent-class"></a><span data-ttu-id="6b0d4-390">Класс SPPhoneNotificationContent</span><span class="sxs-lookup"><span data-stu-id="6b0d4-390">SPPhoneNotificationContent class</span></span>

<span data-ttu-id="6b0d4-p122">Базовый класс для классов, которые представляют содержимое phone уведомлений. Производные классы необходимо объявить поля или свойства для хранения контента и необходимо реализовать метод **PreparePayload** для преобразования содержимого в массив байтов.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-p122">A base class for classes that represent the content of a phone notification. Derived classes must declare one or more fields or properties to hold the content and must implement the **PreparePayload** method to transform the content into a byte array.</span></span>
  
    
    

```cs
public abstract class SPPhoneNotificationContent
```


#### <a name="methods"></a><span data-ttu-id="6b0d4-393">Методы</span><span class="sxs-lookup"><span data-stu-id="6b0d4-393">Methods</span></span>

 <span data-ttu-id="6b0d4-394">**PreparePayload**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-394">**PreparePayload**</span></span>
  
    
    
<span data-ttu-id="6b0d4-p123">При реализации в класс, производный преобразует содержимое в массив байтов, который отправляется по сети в службу уведомлений. Нет нет реализации по умолчанию, поэтому производный класс необходимо реализовать этот метод.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-p123">When implemented in a derived class, transforms the content into a Byte array that is sent over the wire to the notification service. There is no default implementation so a derived class must implement this method.</span></span>
  
    
    



```cs
protected internal abstract byte[] PreparePayload();
```


#### <a name="properties"></a><span data-ttu-id="6b0d4-397">Properties</span><span class="sxs-lookup"><span data-stu-id="6b0d4-397">Properties</span></span>

 <span data-ttu-id="6b0d4-398">**NotificationType** (только для чтения)</span><span class="sxs-lookup"><span data-stu-id="6b0d4-398">**NotificationType** (read-only)</span></span>
  
    
    
<span data-ttu-id="6b0d4-399">Получает тип уведомления (например, плитки или всплывающего уведомления) предназначен контента.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-399">Gets the type of notification (for example, tile or toast) for which the content is intended.</span></span>
  
    
    



```cs
public SPPhoneNotificationType NotificationType

```

<span data-ttu-id="6b0d4-400">Сведения о **SPPhoneNotificationType**содержатся в этом документе.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-400">For information about the **SPPhoneNotificationType**, see later in this document.</span></span>
  
    
    
 <span data-ttu-id="6b0d4-401">**SubscriberType** (только для чтения)</span><span class="sxs-lookup"><span data-stu-id="6b0d4-401">**SubscriberType** (read-only)</span></span>
  
    
    
<span data-ttu-id="6b0d4-402">Получает тип подписчика устройств, например, Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-402">Gets the type of the subscriber's device, for example, a Windows Phone.</span></span>
  
    
    



```cs

public SPPhoneNotificationSubscriberType SubscriberType
```

<span data-ttu-id="6b0d4-403">Сведения о **SPPhoneNotificationSubscriberType**содержатся в этом документе.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-403">For information about the **SPPhoneNotificationSubscriberType**, see later in this document.</span></span>
  
    
    

### <a name="spphonenotificationresponse-class"></a><span data-ttu-id="6b0d4-404">Класс SPPhoneNotificationResponse</span><span class="sxs-lookup"><span data-stu-id="6b0d4-404">SPPhoneNotificationResponse class</span></span>

<span data-ttu-id="6b0d4-405">Отображает результат при попытке отправить уведомление.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-405">Represents the outcome of an attempt to send a notification.</span></span>
  
    
    

```cs
public class SPPhoneNotificationResponse
```


#### <a name="methods"></a><span data-ttu-id="6b0d4-406">Методы</span><span class="sxs-lookup"><span data-stu-id="6b0d4-406">Methods</span></span>

 <span data-ttu-id="6b0d4-407">**Create**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-407">**Create**</span></span>
  
    
    
<span data-ttu-id="6b0d4-408">Создает объект **SPPhoneNotificationResponse**.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-408">Creates an **SPPhoneNotificationResponse** object.</span></span>
  
    
    



```cs
public static SPPhoneNotificationResponse
Create(SPPhoneNotificationSubscriberType subscriberType, 
SPPhoneNotificationType notificationType, HttpWebResponse response)
```

 <span data-ttu-id="6b0d4-409">**Параметры**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-409">**Parameters**</span></span>
  
    
    

-  <span data-ttu-id="6b0d4-410">_subscriberType_  это устройства, такие как Windows Phone 7.5.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-410">_subscriberType_ is the device, such as Windows Phone 7.5.</span></span>
    
  
-  <span data-ttu-id="6b0d4-411">_notificationType_  тип уведомлений, такие как всплывающее или плитки.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-411">_notificationType_ is the type of notification, such as toast or tile.</span></span>
    
  
-  <span data-ttu-id="6b0d4-412">_response_  это объект HTTP-ответа, который был создан на сервере.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-412">_response_ is the HTTP response object that was generated by the server.</span></span>
    
  
<span data-ttu-id="6b0d4-413">Дополнительные сведения о **SPPhoneNotificationSubscriberType** и **SPPhoneNotificationType**можно далее в этом документе.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-413">For more information about **SPPhoneNotificationSubscriberType** and **SPPhoneNotificationType**, see later in this document.</span></span>
  
    
    

#### <a name="properties"></a><span data-ttu-id="6b0d4-414">Properties</span><span class="sxs-lookup"><span data-stu-id="6b0d4-414">Properties</span></span>

 <span data-ttu-id="6b0d4-415">**NotificationType** (только для чтения)</span><span class="sxs-lookup"><span data-stu-id="6b0d4-415">**NotificationType** (read-only)</span></span>
  
    
    
<span data-ttu-id="6b0d4-416">Получает тип уведомления (например, всплывающее или заголовков).</span><span class="sxs-lookup"><span data-stu-id="6b0d4-416">Gets the type of notification (for example, toast or tile).</span></span>
  
    
    



```cs

public SPPhoneNotificationType NotificationType
```

<span data-ttu-id="6b0d4-417">Сведения о SPPhoneNotificationType содержатся в этом документе.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-417">For information about the SPPhoneNotificationType, see later in this document.</span></span>
  
    
    
 <span data-ttu-id="6b0d4-418">**ServiceToken** (только для чтения)</span><span class="sxs-lookup"><span data-stu-id="6b0d4-418">**ServiceToken** (read-only)</span></span>
  
    
    
<span data-ttu-id="6b0d4-419">Получает маркер службы уведомлений, который использовался в уведомлении.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-419">Gets the token of the notification service that was used in the notification.</span></span>
  
    
    



```cs
public string ServiceToken
```

 <span data-ttu-id="6b0d4-420">**StatusCode** (только для чтения)</span><span class="sxs-lookup"><span data-stu-id="6b0d4-420">**StatusCode** (read-only)</span></span>
  
    
    
<span data-ttu-id="6b0d4-p124">Получает код состояния HTTP. Строковая версия **HttpStatusCode** значение.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-p124">Gets the HTTP status code. A string version of a **HttpStatusCode** value.</span></span>
  
    
    



```cs
public string StatusCode
```

 <span data-ttu-id="6b0d4-423">**SubscriberType**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-423">**SubscriberType**</span></span>
  
    
    
<span data-ttu-id="6b0d4-424">Получает или задает тип устройства, к которому было отправлено уведомление.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-424">Gets or sets the type of device to which the notification was sent.</span></span>
  
    
    



```cs
public SPPhoneNotificationSubscriberType SubscriberType
```

<span data-ttu-id="6b0d4-425">Сведения о **SPPhoneNotificationSubscriberType**содержатся в этом документе.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-425">For information about the **SPPhoneNotificationSubscriberType**, see later in this document.</span></span>
  
    
    
 <span data-ttu-id="6b0d4-426">**TimeStamp** (только для чтения)</span><span class="sxs-lookup"><span data-stu-id="6b0d4-426">**TimeStamp** (read-only)</span></span>
  
    
    
<span data-ttu-id="6b0d4-427">Время UTC уведомления.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-427">The UTC time of the notification.</span></span>
  
    
    



```cs
public DateTime Timestamp
```


### <a name="spphonenotificationsubscriber-class"></a><span data-ttu-id="6b0d4-428">Класс SPPhoneNotificationSubscriber</span><span class="sxs-lookup"><span data-stu-id="6b0d4-428">SPPhoneNotificationSubscriber class</span></span>

<span data-ttu-id="6b0d4-429">Базовый класс для классов, которые представляют подписчика уведомлений, выданный приложения SharePoint на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-429">A base class for classes that represent a subscriber to notifications issued by a server-side SharePoint application.</span></span>
  
    
    

```cs
public abstract class SPPhoneNotificationSubscriber
```


#### <a name="methods"></a><span data-ttu-id="6b0d4-430">Методы</span><span class="sxs-lookup"><span data-stu-id="6b0d4-430">Methods</span></span>

<span data-ttu-id="6b0d4-431">Уведомления</span><span class="sxs-lookup"><span data-stu-id="6b0d4-431">Notify</span></span>
  
    
    
<span data-ttu-id="6b0d4-432">Отправляет содержимое указанного уведомлений подписчика с проверки ошибок.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-432">Sends the specified notification content to the subscriber with error checking.</span></span>
  
    
    



```cs
public SPPhoneNotificationResponse Notify(SPPhoneNotificationContent notificationContent)
```

 <span data-ttu-id="6b0d4-433">**Параметры**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-433">**Parameters**</span></span>
  
    
    
 <span data-ttu-id="6b0d4-434">_notificationContent_, сведения о событии, инициирующую уведомления.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-434">_notificationContent_ is information about the event that triggered the notification.</span></span>
  
    
    
<span data-ttu-id="6b0d4-p125">Этот метод не может быть переопределен. Он является оболочкой для метода абстрактный **NotifyInternal** и гарантирует, что некоторые проверки ошибок выполняется при вызове **NotifyInternal**.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-p125">This method cannot be overridden. It wraps the abstract **NotifyInternal** method and ensures that certain error checking is done when **NotifyInternal** is called.</span></span>
  
    
    
<span data-ttu-id="6b0d4-437">Дополнительные сведения о классах **SPPhoneNotificationContent** и **SPPhoneNotificationResponse** можно выше в этом документе.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-437">For more information about the **SPPhoneNotificationContent** and **SPPhoneNotificationResponse** classes, see earlier in this document.</span></span>
  
    
    
 <span data-ttu-id="6b0d4-438">**NotifyInternal**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-438">**NotifyInternal**</span></span>
  
    
    
<span data-ttu-id="6b0d4-439">При переопределении в производный класс, отправляет содержимое указанного уведомлений подписчика.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-439">When overridden in a derived class, sends the specified notification content to the subscriber.</span></span>
  
    
    



```cs
protected abstract SPPhoneNotificationResponse NotifyInternal(SPPhoneNotificationContent notificationContent);
```

 <span data-ttu-id="6b0d4-440">**Параметры**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-440">**Parameters**</span></span>
  
    
    
 <span data-ttu-id="6b0d4-441">_notificationContent_, сведения о событии, инициирующую уведомления.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-441">_notificationContent_ is information about the event that triggered the notification.</span></span>
  
    
    
<span data-ttu-id="6b0d4-442">Дополнительные сведения о классах **SPPhoneNotificationContent** и **SPPhoneNotificationResponse** можно выше в этом документе.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-442">For more information about the **SPPhoneNotificationContent** and **SPPhoneNotificationResponse** classes, see earlier in this document.</span></span>
  
    
    
 <span data-ttu-id="6b0d4-443">**ToString**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-443">**ToString**</span></span>
  
    
    
<span data-ttu-id="6b0d4-444">Возвращает свойства выбранного объекта в виде строки.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-444">Returns selected properties of the object as a string.</span></span>
  
    
    



```cs
public override string ToString()
```

<span data-ttu-id="6b0d4-445">Реализация по умолчанию включает в себя свойства **ParentWeb**, **ApplicationTag**и **DeviceAppInstanceId**.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-445">The default implementation includes the **ParentWeb**, **ApplicationTag**, and **DeviceAppInstanceId** properties.</span></span>
  
    
    
<span data-ttu-id="6b0d4-446">Update</span><span class="sxs-lookup"><span data-stu-id="6b0d4-446">Update</span></span>
  
    
    
<span data-ttu-id="6b0d4-447">Сохраняет объект (возможно, измененных) **SPPhoneNotificationSubscriber** хранилища подписчика веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-447">Saves a (possibly changed) **SPPhoneNotificationSubscriber** object to the website's Subscriber Store.</span></span>
  
    
    



```cs
public void Update()
```

 <span data-ttu-id="6b0d4-448">**ValidateSubscriberProperties**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-448">**ValidateSubscriberProperties**</span></span>
  
    
    
<span data-ttu-id="6b0d4-449">При реализации в класс, производный проверяет выбранных свойств объекта.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-449">When implemented in a derived class, validates selected properties of the object.</span></span>
  
    
    



```cs
protected abstract void ValidateSubscriberProperties();
```


#### <a name="properties"></a><span data-ttu-id="6b0d4-450">Properties</span><span class="sxs-lookup"><span data-stu-id="6b0d4-450">Properties</span></span>

 <span data-ttu-id="6b0d4-451">**CustomArgs**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-451">**CustomArgs**</span></span>
  
    
    
<span data-ttu-id="6b0d4-p126">Получает или задает строку пользовательские аргументы, который представляет состояние подписки на уведомления. Эта строка могут использоваться логики приложения для различения его подписчиков уведомлений для разных видов уведомлений.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-p126">Gets or sets a custom arguments string which represents the state of the notifications subscription. This string could be used by the application logic to differentiate between its notification subscribers for different kinds of notifications.</span></span>
  
    
    



```cs
public string CustomArgs
```

 <span data-ttu-id="6b0d4-454">**DeviceAppInstanceId** (только для чтения)</span><span class="sxs-lookup"><span data-stu-id="6b0d4-454">**DeviceAppInstanceId** (read-only)</span></span>
  
    
    
<span data-ttu-id="6b0d4-455">Получает идентификатор для конкретного экземпляра приложения на телефоне или другого мобильного устройства.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-455">Gets an ID for the specific instance of the application on the phone or other mobile device.</span></span>
  
    
    



```cs
public Guid DeviceAppInstanceId
```

 <span data-ttu-id="6b0d4-456">**LastModifiedTimeStamp** (только для чтения)</span><span class="sxs-lookup"><span data-stu-id="6b0d4-456">**LastModifiedTimeStamp** (read-only)</span></span>
  
    
    
<span data-ttu-id="6b0d4-457">Получает дату и время последнего изменения подписчика.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-457">Gets the date and time when the subscriber was last modified.</span></span>
  
    
    



```cs
public DateTime LastModifiedTimeStamp
```

 <span data-ttu-id="6b0d4-458">**RegistrationTimeStamp** (только для чтения)</span><span class="sxs-lookup"><span data-stu-id="6b0d4-458">**RegistrationTimeStamp** (read-only)</span></span>
  
    
    
<span data-ttu-id="6b0d4-459">Получает дату и время, когда абонентского зарегистрированных для уведомлений.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-459">Gets the date and time when the subscriber registered for notifications.</span></span>
  
    
    



```cs
public DateTime RegistrationTimeStamp
```

 <span data-ttu-id="6b0d4-460">**ServiceToken**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-460">**ServiceToken**</span></span>
  
    
    
<span data-ttu-id="6b0d4-461">Получает или задает сведения о канала доставки, необходимая для службы уведомлений, такие как URI-канал.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-461">Gets or sets delivery channel information that is needed by a notification service, such as channel URI.</span></span>
  
    
    



```cs
public string ServiceToken
```

 <span data-ttu-id="6b0d4-462">**SubscriberType** (только для чтения)</span><span class="sxs-lookup"><span data-stu-id="6b0d4-462">**SubscriberType** (read-only)</span></span>
  
    
    
<span data-ttu-id="6b0d4-463">Получает тип устройства, такие как Windows Phone 7.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-463">Gets the type of the device, such as Windows Phone 7.</span></span>
  
    
    



```cs
public SPPhoneNotificationSubscriberType SubscriberType
```

<span data-ttu-id="6b0d4-464">Сведения о классе **SPPhoneNotificationSubscriberType** содержатся далее в этом документе.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-464">For information about the **SPPhoneNotificationSubscriberType** class, see later in this document.</span></span>
  
    
    
 <span data-ttu-id="6b0d4-465">**User** (только для чтения)</span><span class="sxs-lookup"><span data-stu-id="6b0d4-465">**User** (read-only)</span></span>
  
    
    
<span data-ttu-id="6b0d4-466">Получает пользователя, который зарегистрирован для уведомлений.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-466">Gets the user who registered for notifications.</span></span>
  
    
    



```cs
public SPUser User
```


### <a name="spphonenotificationsubscribercollection-class"></a><span data-ttu-id="6b0d4-467">Класс SPPhoneNotificationSubscriberCollection</span><span class="sxs-lookup"><span data-stu-id="6b0d4-467">SPPhoneNotificationSubscriberCollection class</span></span>

<span data-ttu-id="6b0d4-p127">Коллекция подписчиков уведомлений. Индексаторы **Int32** проходит объект коллекции.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-p127">A collection of notification subscribers. The collection object takes **Int32** indexers.</span></span>
  
    
    

```cs
public sealed class SPPhoneNotificationSubscriberCollection : SPBaseCollection
```


#### <a name="properties"></a><span data-ttu-id="6b0d4-470">Properties</span><span class="sxs-lookup"><span data-stu-id="6b0d4-470">Properties</span></span>

 <span data-ttu-id="6b0d4-471">**Count**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-471">**Count**</span></span>
  
    
    
<span data-ttu-id="6b0d4-472">Возвращает число элементов в коллекции.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-472">Gets the number of items in the collection.</span></span>
  
    
    



```cs
public override int Count
```


### <a name="spphonenotificationsubscribertype-enum"></a><span data-ttu-id="6b0d4-473">Перечисление SPPhoneNotificationSubscriberType</span><span class="sxs-lookup"><span data-stu-id="6b0d4-473">SPPhoneNotificationSubscriberType enum</span></span>

<span data-ttu-id="6b0d4-474">Указывает тип устройства, который может получать уведомления.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-474">Specifies a type of device that can receive notifications.</span></span>
  
    
    


|<span data-ttu-id="6b0d4-475">**Уведомление**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-475">**Notification**</span></span>|<span data-ttu-id="6b0d4-476">**Устройство**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-476">**Device**</span></span>|
|:-----|:-----|
|||
|<span data-ttu-id="6b0d4-477">**WP7**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-477">**WP7**</span></span> <br/> |<span data-ttu-id="6b0d4-478">Windows Phone 7.5</span><span class="sxs-lookup"><span data-stu-id="6b0d4-478">Windows Phone 7.5</span></span>  <br/> |
|<span data-ttu-id="6b0d4-479">**Custom**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-479">**Custom**</span></span> <br/> |<span data-ttu-id="6b0d4-480">Все устройства, отличные от Windows Phone 7.5</span><span class="sxs-lookup"><span data-stu-id="6b0d4-480">Any device other than Windows Phone 7.5</span></span>  <br/> |
   

### <a name="spphonenotificationtype-enum"></a><span data-ttu-id="6b0d4-481">Перечисление SPPhoneNotificationType</span><span class="sxs-lookup"><span data-stu-id="6b0d4-481">SPPhoneNotificationType enum</span></span>

<span data-ttu-id="6b0d4-482">Указывает тип уведомления.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-482">Specifies the type of notification.</span></span>
  
    
    


|||
|:-----|:-----|
|<span data-ttu-id="6b0d4-483">**None**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-483">**None**</span></span> <br/> ||
|<span data-ttu-id="6b0d4-484">**Tile**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-484">**Tile**</span></span> <br/> ||
|<span data-ttu-id="6b0d4-485">**Toast**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-485">**Toast**</span></span> <br/> ||
|<span data-ttu-id="6b0d4-486">**Raw**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-486">**Raw**</span></span> <br/> ||
   

### <a name="spweb-class"></a><span data-ttu-id="6b0d4-487">Класс SPWeb</span><span class="sxs-lookup"><span data-stu-id="6b0d4-487">SPWeb class</span></span>

<span data-ttu-id="6b0d4-488">Были добавлены следующие члены этого класса.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-488">The following members have been added to this class.</span></span>
  
    
    

#### <a name="methods"></a><span data-ttu-id="6b0d4-489">Методы</span><span class="sxs-lookup"><span data-stu-id="6b0d4-489">Methods</span></span>

 <span data-ttu-id="6b0d4-490">**DoesPhoneNotificationSubscriberExist**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-490">**DoesPhoneNotificationSubscriberExist**</span></span>
  
    
    
<span data-ttu-id="6b0d4-491">Получает значение, указывающее, является ли текущий пользователь подписчика для указанного экземпляра указанное приложение.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-491">Gets a value that indicates whether the current user is a subscriber for the specified instance of the specified app.</span></span>
  
    
    



```cs
public bool DoesPhoneNotificationSubscriberExist(Guid deviceAppInstanceId)
```

 <span data-ttu-id="6b0d4-492">**GetPhoneNotificationSubscriber**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-492">**GetPhoneNotificationSubscriber**</span></span>
  
    
    
<span data-ttu-id="6b0d4-493">Получает подписчиков уведомлений с помощью указанного приложения и телефон идентификаторы из списка хранилища подписок уведомлений веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-493">Gets a notification subscriber with the specified application and phone IDs from the website's notification Subscription Store list.</span></span>
  
    
    



```cs
public SPPhoneNotificationSubscriber GetPhoneNotificationSubscriber(Guid deviceAppInstanceId)
```

 <span data-ttu-id="6b0d4-494">**Параметры**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-494">**Parameters**</span></span>
  
    
    
 <span data-ttu-id="6b0d4-495">_deviceAppInstanceId_  это идентификатор экземпляра приложения на конкретных телефон или устройство.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-495">_deviceAppInstanceId_ is an ID for the instance of the application on a specific phone or device.</span></span>
  
    
    
<span data-ttu-id="6b0d4-496">Сведения о см класс **SPPhoneNotificationSubscriber** ранее в этом документе.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-496">For information about the **SPPhoneNotificationSubscriber** class see earlier in this document.</span></span>
  
    
    
 <span data-ttu-id="6b0d4-497">**GetPhoneNotificationSubscribers** (перегрузка)</span><span class="sxs-lookup"><span data-stu-id="6b0d4-497">**GetPhoneNotificationSubscribers** (overloaded)</span></span>
  
    
    
<span data-ttu-id="6b0d4-498">Получает коллекцию подписчиков уведомлений из списка хранилища подписок уведомлений веб-сайта, при необходимости фильтрации на код приложений телефона и, возможно, также на одном из следующих значений: некоторые пользовательские аргументы или пользователя.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-498">Gets a collection of notification subscribers from the website's notification Subscription Store list, optionally filtering on the ID of the phone applications and possibly also on one of the following: the user or some custom arguments.</span></span>
  
    
    



```cs
public SPPhoneNotificationSubscriberCollection GetPhoneNotificationSubscribers(string customArgs)
```


> <span data-ttu-id="6b0d4-499">**Примечание:** Имя объектной модели клиента — **GetPhoneNotificationSubscribersByArgs**.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-499">**Note:** Client object model name is **GetPhoneNotificationSubscribersByArgs**.</span></span> 
  
    
    




```cs
public SPPhoneNotificationSubscriberCollection GetPhoneNotificationSubscribers(string user)

```


> <span data-ttu-id="6b0d4-500">**Примечание:** Имя объектной модели клиента — **GetPhoneNotificationSubscribersByUser**.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-500">**Note:** Client object model name is **GetPhoneNotificationSubscribersByUser**.</span></span> 
  
    
    

 <span data-ttu-id="6b0d4-501">**Параметры**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-501">**Parameters**</span></span>
  
    
    

-  <span data-ttu-id="6b0d4-502">_customArgs_  это дополнительные настраиваемые сведения, могут использовать несколько приложений с поддержкой уведомлений.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-502">_customArgs_ are additional custom information that some notification-enabled applications may use.</span></span>
    
  
-  <span data-ttu-id="6b0d4-503">_user_  это пользователь, зарегистрированных для уведомлений.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-503">_user_ is the user who registered for the notifications.</span></span>
    
  
<span data-ttu-id="6b0d4-504">Сведения о см класс **SPPhoneNotificationSubscriberCollection** ранее в этом документе.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-504">For information about the **SPPhoneNotificationSubscriberCollection** class see earlier in this document.</span></span>
  
    
    
 <span data-ttu-id="6b0d4-505">**RegisterPhoneNotificationSubscriber**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-505">**RegisterPhoneNotificationSubscriber**</span></span>
  
    
    
<span data-ttu-id="6b0d4-506">Регистрирует приложение phone на телефоне для получения уведомлений.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-506">Registers a phone app on a phone to receive notifications.</span></span>
  
    
    



```cs

public SPPhoneNotificationSubscriber RegisterPhoneNotificationSubscriber(SPPhoneNotificationSubscriberType subscriberType, Guid deviceAppInstanceId, string serviceToken)
```

 <span data-ttu-id="6b0d4-507">**Параметры**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-507">**Parameters**</span></span>
  
    
    

-  <span data-ttu-id="6b0d4-508">_subscriberType_  это тип устройства, такие как Windows Phone 7.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-508">_subscriberType_ is the device type, such as Windows Phone 7.</span></span>
    
  
-  <span data-ttu-id="6b0d4-509">_deviceAppInstanceId_  это идентификатор экземпляра приложения на конкретных телефон или устройство.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-509">_deviceAppInstanceId_ is an ID for the instance of the app on a specific phone or device.</span></span>
    
  
-  <span data-ttu-id="6b0d4-510">_serviceToken_  это маркер, используемый службой уведомлений, который отправляет уведомления для подписчиков.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-510">_serviceToken_ is the token that is used by the notification service that sends notifications to the subscriber.</span></span>
    
  
<span data-ttu-id="6b0d4-511">Сведения о **SPPhoneNotificationSubscriberType**содержатся в этом документе.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-511">For information about **SPPhoneNotificationSubscriberType**, see earlier in this document.</span></span>
  
    
    
 <span data-ttu-id="6b0d4-512">**UnregisterPhoneNotificationSubscriber**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-512">**UnregisterPhoneNotificationSubscriber**</span></span>
  
    
    
<span data-ttu-id="6b0d4-513">Отменяет регистрацию приложение phone на телефоне получать уведомления.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-513">Unregisters a phone app on a phone from receiving notifications.</span></span>
  
    
    



```cs
public void UnregisterPhoneNotificationSubscriber(Guid deviceAppInstanceId)
```

 <span data-ttu-id="6b0d4-514">**Параметры**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-514">**Parameters**</span></span>
  
    
    
 <span data-ttu-id="6b0d4-515">_deviceAppInstanceId_  это идентификатор экземпляра приложения на конкретных телефон или устройство.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-515">_deviceAppInstanceId_ is an ID for the instance of the app on a specific phone or device.</span></span>
  
    
    

#### <a name="properties"></a><span data-ttu-id="6b0d4-516">Properties</span><span class="sxs-lookup"><span data-stu-id="6b0d4-516">Properties</span></span>

 <span data-ttu-id="6b0d4-517">**PhoneNotificationSubscribers** (только для чтения)</span><span class="sxs-lookup"><span data-stu-id="6b0d4-517">**PhoneNotificationSubscribers** (read-only)</span></span>
  
    
    
<span data-ttu-id="6b0d4-518">Получает коллекцию всех телефона подписчиков уведомлений в хранилище подписчика веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-518">Gets a collection of all the phone notification subscribers in the website's Subscriber Store.</span></span>
  
    
    



```cs
public SPPhoneNotificationSubscriberCollection PhoneNotificationSubscribers
```

<span data-ttu-id="6b0d4-519">Сведения о **SPPhoneNotificationSubscriberCollection** класса содержатся выше в этом документе.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-519">For information about the **SPPhoneNotificationSubscriberCollection** class, see earlier in this document.</span></span>
  
    
    

### <a name="wp7notificationtilecontent-class"></a><span data-ttu-id="6b0d4-520">Класс WP7NotificationTileContent</span><span class="sxs-lookup"><span data-stu-id="6b0d4-520">WP7NotificationTileContent class</span></span>

<span data-ttu-id="6b0d4-521">Представляет содержимое заголовков уведомлений.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-521">Represents the content of a tile notification.</span></span>
  
    
    

```cs
public sealed class WP7NotificationTileContent : SPPhoneNotificationContent
```


#### <a name="constructors"></a><span data-ttu-id="6b0d4-522">Конструкторы</span><span class="sxs-lookup"><span data-stu-id="6b0d4-522">Constructors</span></span>

<span data-ttu-id="6b0d4-523">Инициализирует новый экземпляр класса WP7NotificationTileContent.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-523">Initializes a new instance of the WP7NotificationTileContent class.</span></span>
  
    
    

```cs
public WP7NotificationTileContent()
```


#### <a name="methods"></a><span data-ttu-id="6b0d4-524">Методы</span><span class="sxs-lookup"><span data-stu-id="6b0d4-524">Methods</span></span>

 <span data-ttu-id="6b0d4-525">**PreparePayload**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-525">**PreparePayload**</span></span>
  
    
    
<span data-ttu-id="6b0d4-526">Преобразует содержимое в массив **Byte**, отправляемые по сети в службу уведомлений.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-526">Transforms the content into a **Byte** array that is sent over the wire to the notification service.</span></span>
  
    
    



```cs
protected internal override byte[] PreparePayload();
```


#### <a name="properties"></a><span data-ttu-id="6b0d4-527">Properties</span><span class="sxs-lookup"><span data-stu-id="6b0d4-527">Properties</span></span>

 <span data-ttu-id="6b0d4-528">**Count**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-528">**Count**</span></span>
  
    
    
<span data-ttu-id="6b0d4-p128">Получает или задает число уведомлений. Должна быть от -1 до 99 включительно.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-p128">Gets or sets the count of the notification. Must be from -1 to 99 inclusive.</span></span>
  
    
    



```cs
public int Count
```

<span data-ttu-id="6b0d4-531">Для свойства значение -1, значение счетчика на иконку остаются без изменений.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-531">Setting the property to -1 will not change the count over the tile.</span></span>
  
    
    
 <span data-ttu-id="6b0d4-532">**Title**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-532">**Title**</span></span>
  
    
    
<span data-ttu-id="6b0d4-533">Получает или задает заголовок заголовков уведомлений.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-533">Gets or sets the title of the tile notification.</span></span>
  
    
    



```cs
public string Title
```

 <span data-ttu-id="6b0d4-534">**BackgroundImagePath**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-534">**BackgroundImagePath**</span></span>
  
    
    
<span data-ttu-id="6b0d4-535">Получает или задает путь к плитки фонового изображения.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-535">Gets or sets the path to the tile's background image.</span></span>
  
    
    



```cs
public string BackgroundImagePath
```

 <span data-ttu-id="6b0d4-536">**BackBackgroundImagePath**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-536">**BackBackgroundImagePath**</span></span>
  
    
    
<span data-ttu-id="6b0d4-537">Получает или задает фоновое изображение задней стороне транспонирования заголовков.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-537">Gets or sets the background image of the back side of a flipping tile.</span></span>
  
    
    



```cs
public string BackBackgroundImagePath
```

 <span data-ttu-id="6b0d4-538">**BackContent**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-538">**BackContent**</span></span>
  
    
    
<span data-ttu-id="6b0d4-539">Получает или задает содержимое обратной стороне транспонирования заголовков.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-539">Gets or sets the content of the back side of a flipping tile.</span></span>
  
    
    



```cs
public string BackContent
```

 <span data-ttu-id="6b0d4-540">**BackTitle**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-540">**BackTitle**</span></span>
  
    
    
<span data-ttu-id="6b0d4-541">Получает или задает заголовок, отображаемый на задней стороне транспонирования заголовков.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-541">Gets or sets of the title that appears on the back side of a flipping tile.</span></span>
  
    
    



```cs
public string BackTitle
```

 <span data-ttu-id="6b0d4-542">**TileId**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-542">**TileId**</span></span>
  
    
    
<span data-ttu-id="6b0d4-543">Получает или задает идентификатор фрагмента.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-543">Gets or sets the ID of the tile.</span></span>
  
    
    



```cs
public string TileId
```


### <a name="wp7notificationtoastcontent-class"></a><span data-ttu-id="6b0d4-544">Класс WP7NotificationToastContent</span><span class="sxs-lookup"><span data-stu-id="6b0d4-544">WP7NotificationToastContent class</span></span>

<span data-ttu-id="6b0d4-545">Представляет содержимое всплывающее уведомление.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-545">Represents the content of a toast notification.</span></span>
  
    
    

```cs
public sealed class WP7NotificationToastContent : SPPhoneNotificationContent
```


#### <a name="constructors"></a><span data-ttu-id="6b0d4-546">Конструкторы</span><span class="sxs-lookup"><span data-stu-id="6b0d4-546">Constructors</span></span>

<span data-ttu-id="6b0d4-547">Инициализирует новый экземпляр класса WP7NotificationToastContent.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-547">Initializes a new instance of the WP7NotificationToastContent class.</span></span>
  
    
    

```cs
public WP7NotificationToastContent()
```


#### <a name="methods"></a><span data-ttu-id="6b0d4-548">Методы</span><span class="sxs-lookup"><span data-stu-id="6b0d4-548">Methods</span></span>

 <span data-ttu-id="6b0d4-549">**PreparePayload**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-549">**PreparePayload**</span></span>
  
    
    
<span data-ttu-id="6b0d4-550">Преобразует содержимое в массив **Byte**, отправляемые по сети в службу уведомлений.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-550">Transforms the content into a **Byte** array that is sent over the wire to the notification service.</span></span>
  
    
    



```cs
protected internal override byte[] PreparePayload();
```


#### <a name="properties"></a><span data-ttu-id="6b0d4-551">Properties</span><span class="sxs-lookup"><span data-stu-id="6b0d4-551">Properties</span></span>

 <span data-ttu-id="6b0d4-552">**Message**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-552">**Message**</span></span>
  
    
    
<span data-ttu-id="6b0d4-553">Получает или задает сообщение всплывающее уведомление.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-553">Gets or sets the message of the toast notification.</span></span>
  
    
    



```cs
public string Message
```

 <span data-ttu-id="6b0d4-554">**Title**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-554">**Title**</span></span>
  
    
    
<span data-ttu-id="6b0d4-555">Получает или задает заголовок всплывающее уведомление.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-555">Gets or sets the title of the toast notification.</span></span>
  
    
    



```cs
public string Title
```

 <span data-ttu-id="6b0d4-556">**Param**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-556">**Param**</span></span>
  
    
    
<span data-ttu-id="6b0d4-557">Получает или задает пользовательских параметров данных, который передается в приложение-получатель, если пользователь отвечает на всплывающее уведомление.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-557">Gets or sets custom settings data that is passed to the receiving application if the user responds to the toast notification.</span></span>
  
    
    



```cs
public string Param
```

<span data-ttu-id="6b0d4-558">Это свойство можно использовать для передачи сведений в получающее приложение, например URL-адрес или набор пар "имя значение".</span><span class="sxs-lookup"><span data-stu-id="6b0d4-558">This property can be used to pass information to the receiving application such as a URL or a set of name-value pairs.</span></span>
  
    
    

### <a name="wp7notificationrawcontent-class"></a><span data-ttu-id="6b0d4-559">Класс WP7NotificationRawContent</span><span class="sxs-lookup"><span data-stu-id="6b0d4-559">WP7NotificationRawContent class</span></span>

<span data-ttu-id="6b0d4-560">Представляет содержимое необработанное уведомление.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-560">Represents the content of a raw notification.</span></span>
  
    
    

```cs
public sealed class WP7NotificationRawContent : SPPhoneNotificationContent
```


#### <a name="constructors"></a><span data-ttu-id="6b0d4-561">Конструкторы</span><span class="sxs-lookup"><span data-stu-id="6b0d4-561">Constructors</span></span>

<span data-ttu-id="6b0d4-562">Инициализирует новый экземпляр класса WP7NotificationRawContent.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-562">Initializes a new instance of the WP7NotificationRawContent class.</span></span>
  
    
    

```cs
public WP7NotificationRawContent()
```


#### <a name="methods"></a><span data-ttu-id="6b0d4-563">Методы</span><span class="sxs-lookup"><span data-stu-id="6b0d4-563">Methods</span></span>

 <span data-ttu-id="6b0d4-564">**PreparePayload**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-564">**PreparePayload**</span></span>
  
    
    
<span data-ttu-id="6b0d4-565">Преобразует содержимое в массив байтов, который отправляется по сети в службу уведомлений.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-565">Transforms the content into a Byte array that is sent over the wire to the notification service.</span></span>
  
    
    



```cs
protected internal override byte[] PreparePayload();
```


#### <a name="properties"></a><span data-ttu-id="6b0d4-566">Properties</span><span class="sxs-lookup"><span data-stu-id="6b0d4-566">Properties</span></span>

 <span data-ttu-id="6b0d4-567">**Message**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-567">**Message**</span></span>
  
    
    
<span data-ttu-id="6b0d4-568">Получает или задает сообщение необработанное уведомление.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-568">Gets or sets the message of the raw notification.</span></span>
  
    
    



```cs
public string Message
```


### <a name="wp7phonenotificationresponse-class"></a><span data-ttu-id="6b0d4-569">Класс WP7PhoneNotificationResponse</span><span class="sxs-lookup"><span data-stu-id="6b0d4-569">WP7PhoneNotificationResponse class</span></span>

<span data-ttu-id="6b0d4-570">Отображает результат при попытке отправить уведомление подписчика Windows Phone 7.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-570">Represents the outcome of an attempt to send a notification to a Windows Phone 7 subscriber.</span></span>
  
    
    

```cs
public WP7PhoneNotificationResponse(SPPhoneNotificationType notificationType, HttpWebResponse response)
```

 <span data-ttu-id="6b0d4-571">**Параметры**</span><span class="sxs-lookup"><span data-stu-id="6b0d4-571">**Parameters**</span></span>
  
    
    

-  <span data-ttu-id="6b0d4-572">_notificationType_  тип уведомлений, такие как всплывающее или плитки.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-572">_notificationType_ is the type of notification, such as toast or tile.</span></span>
    
  
-  <span data-ttu-id="6b0d4-573">_response_  это объект HTTP-ответа, который был создан на сервере.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-573">_response_ is the HTTP response object that was generated by the server.</span></span>
    
  
<span data-ttu-id="6b0d4-574">Дополнительные сведения о **SPPhoneNotificationType**содержатся в этом документе.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-574">For more information about **SPPhoneNotificationType**, see earlier in this document.</span></span>
  
    
    

#### <a name="properties"></a><span data-ttu-id="6b0d4-575">Properties</span><span class="sxs-lookup"><span data-stu-id="6b0d4-575">Properties</span></span>

 <span data-ttu-id="6b0d4-576">**NotificationStatus** (только для чтения)</span><span class="sxs-lookup"><span data-stu-id="6b0d4-576">**NotificationStatus** (read-only)</span></span>
  
    
    
<span data-ttu-id="6b0d4-577">Получает состояние уведомления, например, успешное или неудачное.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-577">Gets the notification status, for example, success or failure.</span></span>
  
    
    



```cs
public string NotificationStatus
```

 <span data-ttu-id="6b0d4-578">**DeviceConnectionStatus** (только для чтения)</span><span class="sxs-lookup"><span data-stu-id="6b0d4-578">**DeviceConnectionStatus** (read-only)</span></span>
  
    
    
<span data-ttu-id="6b0d4-579">Получает состояние устройства во время уведомления.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-579">Gets the status of the device at the time of the notification.</span></span>
  
    
    



```cs
public string DeviceConnectionStatus
```

 <span data-ttu-id="6b0d4-580">**SubscriptionStatus** (только для чтения)</span><span class="sxs-lookup"><span data-stu-id="6b0d4-580">**SubscriptionStatus** (read-only)</span></span>
  
    
    
<span data-ttu-id="6b0d4-581">Состояние подписки на устройство во время уведомления.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-581">The subscription status of the device at the time of the notification.</span></span>
  
    
    



```cs
public string SubscriptionStatus
```

 <span data-ttu-id="6b0d4-582">**MessageId** (только для чтения)</span><span class="sxs-lookup"><span data-stu-id="6b0d4-582">**MessageId** (read-only)</span></span>
  
    
    
<span data-ttu-id="6b0d4-583">Получает идентификатор сообщения, отправленного в уведомлении.</span><span class="sxs-lookup"><span data-stu-id="6b0d4-583">Gets the ID of the message that was sent in the notification.</span></span>
  
    
    



```
public string MessageId
```


## <a name="additional-resources"></a><span data-ttu-id="6b0d4-584">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="6b0d4-584">Additional resources</span></span>
<span data-ttu-id="6b0d4-585"><a name="SP15MobileOM_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="6b0d4-585"></span></span>


-  [<span data-ttu-id="6b0d4-586">Построение приложений Windows Phone, обращающихся к SharePoint</span><span class="sxs-lookup"><span data-stu-id="6b0d4-586">Build Windows Phone apps that access SharePoint</span></span>](build-windows-phone-apps-that-access-sharepoint.md)
    
  
-  [<span data-ttu-id="6b0d4-587">Как: Настройка и использование push-уведомлений в SharePoint приложений для Windows Phone</span><span class="sxs-lookup"><span data-stu-id="6b0d4-587">How to: Configure and use push notifications in SharePoint apps for Windows Phone</span></span>](how-to-configure-and-use-push-notifications-in-sharepoint-apps-for-windows.md)
    
  
-  [<span data-ttu-id="6b0d4-588">Интеграция расположение и карты функциональные возможности в SharePoint</span><span class="sxs-lookup"><span data-stu-id="6b0d4-588">Integrating location and map functionality in SharePoint</span></span>](integrating-location-and-map-functionality-in-sharepoint.md)
    
  
-  [<span data-ttu-id="6b0d4-589">Обзор объектной модели SharePoint мобильного клиента проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="6b0d4-589">Overview of the SharePoint mobile client authentication object model</span></span>](overview-of-the-sharepoint-mobile-client-authentication-object-model.md)
    
  

