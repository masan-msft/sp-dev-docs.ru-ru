---
title: "Обработка маркеров безопасности в надстройках SharePoint с низким уровнем доверия, размещенных у поставщика"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: eee92f719ac3747f845f4aea807f71356f982fdb
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="handle-security-tokens-in-provider-hosted-low-trust-sharepoint-add-ins"></a><span data-ttu-id="3d87e-102">Обработка маркеров безопасности в надстройках SharePoint с низким уровнем доверия, размещенных у поставщика</span><span class="sxs-lookup"><span data-stu-id="3d87e-102">Handle security tokens in provider-hosted low-trust SharePoint Add-ins</span></span>
<span data-ttu-id="3d87e-103">Узнайте о маркерах контекста, доступа и обновления, используемых для авторизации в Надстройки SharePoint с низким уровнем доверия и размещением у поставщика, а также о принципах работы с ними в коде.</span><span class="sxs-lookup"><span data-stu-id="3d87e-103">Learn about the context, access, and refresh tokens that are used for authorization by low-trust, provider-hosted SharePoint Add-ins, and how to work with them in your code.</span></span>
 

 <span data-ttu-id="3d87e-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="3d87e-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 


 <span data-ttu-id="3d87e-p102">**Важно!**   **Эта статья полностью посвящена использованию токенов безопасности в системах авторизации с низким уровнем доверия.** Сведения об использовании маркеров в системах с высоким уровнем доверия см. в статье [Создание и использование маркеров доступа в надстройках с высоким уровнем доверия для SharePoint, размещаемых у поставщика](create-and-use-access-tokens-in-provider-hosted-high-trust-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="3d87e-p102">**Important**   **This article is entirely about the use of security tokens in the low-trust authorization system, not the high-trust system.** For information about the use of tokens in the high-trust system, see [Create and use access tokens in provider-hosted high-trust SharePoint Add-ins](create-and-use-access-tokens-in-provider-hosted-high-trust-sharepoint-add-ins.md).</span></span>
 


 <span data-ttu-id="3d87e-p103">**Надстройки SharePoint, которые для получения доступа к данным SharePoint используют  [систему авторизации с низким уровнем доверия](creating-sharepoint-add-ins-that-use-low-trust-authorization.md). Они участвуют в потоке OAuth, связанном с прохождением токенов безопасности (в формате [JSON Web Token](http://datatracker.ietf.org/doc/draft-ietf-oauth-json-web-token/)) в SharePoint, Служба контроля доступа Microsoft Azure (ACS), удаленных компонентах Надстройка SharePoint и, в некоторых случаях, браузере пользователя.** Потоки отличаются в зависимости от дизайна надстройки, но все они связаны по крайней мере с такими двумя типами маркеров:</span><span class="sxs-lookup"><span data-stu-id="3d87e-p103">**SharePoint Add-ins that use the  [low-trust authorization system](creating-sharepoint-add-ins-that-use-low-trust-authorization.md) to gain access to SharePoint data participate in an OAuthflow that involves the passing of security tokens (in [JSON Web Token](http://datatracker.ietf.org/doc/draft-ietf-oauth-json-web-token/) format) among SharePoint, Microsoft Azure Access Control Service (ACS), the remote components of the SharePoint Add-in, and, in some cases, the user's browser.** There are different flows depending on the design of the add-in, but all of them involve at least the following two types of tokens:</span></span>
 


-  <span data-ttu-id="3d87e-p104">**Маркер доступа.** Входит в каждый запрос на создание, считывание, обновление или удаление, который удаленные компоненты надстройки отправляют в SharePoint. SharePoint проверяет маркер и обрабатывает запрос.</span><span class="sxs-lookup"><span data-stu-id="3d87e-p104">**Access token:** Included in each create, read, update, or delete (CRUD) request from the remote components of the add-in to SharePoint. SharePoint validates the token and serves the request.</span></span>
    
 
-  <span data-ttu-id="3d87e-113">**Маркер обновления.** Служит для получения первого маркера доступа в [потоке маркера контекста](creating-sharepoint-add-ins-that-use-low-trust-authorization.md#Flows) и замены маркеров доступа в нем и [потоке кода авторизации](creating-sharepoint-add-ins-that-use-low-trust-authorization.md#Flows) системы авторизации с низким уровнем доверия после истечения срока их действия.</span><span class="sxs-lookup"><span data-stu-id="3d87e-113">**Refresh token:** Used to obtain a first access token in the [Context Token flow](creating-sharepoint-add-ins-that-use-low-trust-authorization.md#Flows), and to replace expiring access tokens in both the Context Token flow and the  [Authorization Code flow](creating-sharepoint-add-ins-that-use-low-trust-authorization.md#Flows) of the low-trust authorization system.</span></span>
    
 
<span data-ttu-id="3d87e-114">В зависимости от того, какой поток OAuth использует надстройка, в процесс включается один из указанных ниже элементов.</span><span class="sxs-lookup"><span data-stu-id="3d87e-114">Depending on which OAuth flow the add-in is using, one or the other of the following is also part of the process:</span></span>
 

-  <span data-ttu-id="3d87e-115">**Маркер контекста.** С его помощью в потоке маркера контекста удаленный компонент получает маркер обновления и сведения, необходимые для запроса маркера доступа из Azure ACS.</span><span class="sxs-lookup"><span data-stu-id="3d87e-115">**Context token:** Used, in the Context Token flow, to provide the remote component with a refresh token and with information that it needs to request an access token from Azure ACS.</span></span>
    
 
-  <span data-ttu-id="3d87e-p105">**Код авторизации.** Он уникален для каждой пары пользователя и приложения. Используется в потоке кода авторизации для получения первого маркера доступа и маркера обновления.</span><span class="sxs-lookup"><span data-stu-id="3d87e-p105">**Authorizaton code:** Not a token, but an authorization code, unique to each pair of user and application. It is used in the Authorization Code flow to obtain a first access token, and a refresh token.</span></span>
    
 

## <a name="understand-the-handling-of-access-tokens"></a><span data-ttu-id="3d87e-118">Общие сведения об обработке маркеров доступа</span><span class="sxs-lookup"><span data-stu-id="3d87e-118">Understand the handling of access tokens</span></span>
<span data-ttu-id="3d87e-119"><a name="AccessTokens"> </a></span><span class="sxs-lookup"><span data-stu-id="3d87e-119"></span></span>

<span data-ttu-id="3d87e-p106">В системах авторизации с низким уровнем доверия Azure ACS создает маркеры доступа и отправляет их удаленным компонентам надстройки SharePoint. (На момент написания этой статьи продолжительность существования маркера доступа для SharePoint, выпущенного службой контроля доступа, составляла 12 часов, но это могло измениться.) Ниже указаны основные **функции кода в надстройке SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="3d87e-p106">In the low-trust authorization system, the access tokens are created by Azure ACS and sent to the remote component of your SharePoint Add-in. (When this article was written, ACS-issued access tokens for SharePoint had a life span of 12 hours, but that could change.) The main  **things that the code in your SharePoint Add-in needs to do** are:</span></span>
 

 

-  <span data-ttu-id="3d87e-p107">**Запрос маркера доступа** из Azure ACS. В зависимости от используемого потока OAuth для отправки запроса надстройка использует код авторизации или сведения, извлеченные из маркера контекста.</span><span class="sxs-lookup"><span data-stu-id="3d87e-p107">**Request an access token** from Azure ACS. Depending on which OAuth flow is being used, the add-in uses either an authorization code or information it extracts from a context token to make the request.</span></span>
    
 
-  <span data-ttu-id="3d87e-p108">**Включение маркера в каждый HTTP-запрос в SharePoint.** Маркер добавляется в запрос в качестве заголовка **Authorization** со значением в таком виде: слово Bearer, пробел, маркер доступа с кодировкой Base64.</span><span class="sxs-lookup"><span data-stu-id="3d87e-p108">**Include the token in every HTTP request to SharePoint.** The token is added as an **Authorization** header to the request. The value of the header is the word "Bearer", followed by a space, followed by the base 64 encoded access token.</span></span>
    
 
- <span data-ttu-id="3d87e-127">**Кэширование маркера доступа** для повторного использования в последующих запросах (необязательно, но рекомендуется).</span><span class="sxs-lookup"><span data-stu-id="3d87e-127">Optionally (but recommended),  **cache the access token** for reuse on subsequent requests.</span></span>
    
 
- <span data-ttu-id="3d87e-128">Пересылка маркера доступа в серверные системы, чтобы они могли получать прямой доступ к SharePoint (необязательно).</span><span class="sxs-lookup"><span data-stu-id="3d87e-128">Optionally, forward the access token to back end systems so they can directly access SharePoint.</span></span>
    
 
<span data-ttu-id="3d87e-p109">Эти задачи необходимо выполнять с помощью серверного кода. Если вы используете управляемый код, пример кода для некоторых задач находится в файлах SharePointContext и TokenHelper (с расширением CS или VB), которые входят в Инструменты разработчика Microsoft Office для Visual Studio. Пример кода PHP, который выполняет часть этих задач, см. в статье  [Знакомство с REST-интерфейсом SharePoint и его использование](http://msdn.microsoft.com/en-us/magazine/dn198245.aspx).</span><span class="sxs-lookup"><span data-stu-id="3d87e-p109">These tasks must be done with server-side code. If you are using managed code, sample code for some of these tasks is in the SharePointContext.cs (or .vb) and TokenHelper.cs (or .vb) files that are part of Microsoft Office Developer Tools for Visual Studio. For an example of PHP code that carries out some of these tasks, see  [Understanding and Using the SharePoint REST Interface](http://msdn.microsoft.com/en-us/magazine/dn198245.aspx).</span></span>
 

 

### <a name="cache-the-access-token"></a><span data-ttu-id="3d87e-132">Кэширование маркера доступа</span><span class="sxs-lookup"><span data-stu-id="3d87e-132">Cache the access token</span></span>
<span data-ttu-id="3d87e-133"><a name="CacheAccessToken"> </a></span><span class="sxs-lookup"><span data-stu-id="3d87e-133"></span></span>

<span data-ttu-id="3d87e-134">В зависимости от архитектуры надстройки SharePoint и платформы размещения существует несколько **способов кэширования маркеров доступа** на сервере.</span><span class="sxs-lookup"><span data-stu-id="3d87e-134">Depending on your SharePoint Add-in's architecture and the hosting platform, there are several  **ways to cache the access token** on the server.</span></span>
 

 

- <span data-ttu-id="3d87e-135">В состоянии сеанса.</span><span class="sxs-lookup"><span data-stu-id="3d87e-135">In session state</span></span>
    
 
- <span data-ttu-id="3d87e-136">В состоянии приложения.</span><span class="sxs-lookup"><span data-stu-id="3d87e-136">In application state</span></span>
    
 
- <span data-ttu-id="3d87e-137">В [службе кэширования Windows Server AppFabric](http://msdn.microsoft.com/library/8aef3f5d-2a77-46d9-b951-0768fedd31a1%28Office.15%29.aspx) или ее эквиваленте в ОС, отличных от ОС Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="3d87e-137">In  [Windows Server AppFabric Caching](http://msdn.microsoft.com/library/8aef3f5d-2a77-46d9-b951-0768fedd31a1%28Office.15%29.aspx) or its equivalent in a non-Microsoft OS.</span></span>
    
 
- <span data-ttu-id="3d87e-138">В [службе кэширования Microsoft Azure](http://msdn.microsoft.com/library/7c679300-07cc-4ba1-b8fa-39421b570d56%28Office.15%29.aspx) или ее эквиваленте в облачных службах, отличных от облачных служб Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="3d87e-138">In the  [Microsoft Azure Caching Service](http://msdn.microsoft.com/library/7c679300-07cc-4ba1-b8fa-39421b570d56%28Office.15%29.aspx) or its equivalent in a non-Microsoft cloud service.</span></span>
    
 
- <span data-ttu-id="3d87e-139">В базе данных.</span><span class="sxs-lookup"><span data-stu-id="3d87e-139">In a database</span></span>
    
 
- <span data-ttu-id="3d87e-140">В системе [memcached](http://www.memcached.org/).</span><span class="sxs-lookup"><span data-stu-id="3d87e-140">In a  [memcached](http://www.memcached.org/) system</span></span>
    
 

 <span data-ttu-id="3d87e-p110">**Примечание.** В большинстве сценариев вы не сможете использовать простые термины, например AccessToken, в качестве ключа кэширования, так как надстройке необходимо хранить уникальные маркеры для каждого пользователя и фермы либо тенантности клиента SharePoint. Если надстройка использует [поток маркера контекста](creating-sharepoint-add-ins-that-use-low-trust-authorization.md#Flows), SharePoint предоставляет специальный ключ **CacheKey**, который можно использовать, чтобы различать кэшированные маркеры. В этом разделе описаны проблемы, возникающие, если надстройка не использует поток маркера контекста, и способы их решения.</span><span class="sxs-lookup"><span data-stu-id="3d87e-p110">**Note**  In most scenarios, you won't be able to use terms as simple as "AccessToken" as the caching key because your add-in must keep the tokens for different users and SharePoint farms/tenancies distinct. If your add-in uses the  [Context Token flow](creating-sharepoint-add-ins-that-use-low-trust-authorization.md#Flows), there is special  **CacheKey** provided by SharePoint that can be used to distinguish cached tokens. This section explains what the issues are and what to do when your application is not using the Context Token flow.</span></span>
 

<span data-ttu-id="3d87e-p111">Кэширование маркера доступа в состоянии сеанса подходит для большинства сценариев. Если удаленное веб-приложение получает доступ к другим службам, использующим протокол OAuth (в дополнение к SharePoint), и кэширует различные маркеры доступа в состоянии сеанса, используйте различные ключи кэша для маркеров. Например, вместо AccessToken используйте SharePoint_AccessToken, Facebook_AccessToken, SAP_Gateway_AccessToken. (Если вы не используете состояние сеанса или другой способ кэширования, который автоматически разделяет кэши всех пользователей, понадобится также соотнести ключи с каждым пользователем.)</span><span class="sxs-lookup"><span data-stu-id="3d87e-p111">Caching the access token in session state is fine for most scenarios. If the remote web application is accessing other services that use OAuth (in addition to SharePoint) and it is caching the various access tokens in session state, be sure to use distinct cache keys for the tokens; for example, instead of "AccessToken", use "SharePoint_AccessToken", "Facebook_AccessToken", "SAP_Gateway_AccessToken", etc. . (If you are not using session state or some other caching that automatically separates each user's cache, you would need also to relativize your keys for user.)</span></span>
 

 
<span data-ttu-id="3d87e-p112">Если приложение получает доступ к нескольким фермам SharePoint или тенантностям в Интернете, вы можете использовать домен SharePoint в первичном ключе кэширования приложения (SharePoint_*<mydomain>*.sharepoint.com_AccessToken") либо использовать ферму или область тенантности ("SharePoint_*<realmGUID>*_AccessToken"). И одно, и другое можно считать из маркера доступа. (Чтобы прочитать маркер, ваш код должен выполнить обратное кодирование Base 64 для маркера. В управляемом коде в файле TokenHelper.cs или VB-файле есть пример кода для этой цели. В нем используются классы из пространств имен **Microsoft.IdentityModel.S2S.Tokens** и **System.IdentityModel.Tokens**.) Доступен еще один вариант, когда приложение использует поток маркера контекста, как описано в следующем абзаце.</span><span class="sxs-lookup"><span data-stu-id="3d87e-p112">If the application accesses more than one SharePoint farm or online tenancy, you can use the SharePoint domain as part of the application's primary caching key ("SharePoint_ *<mydomain>*  .sharepoint.com_AccessToken") or use the farm/tenancy's realm ("SharePoint_ *<realmGUID>*  _AccessToken"), both of which can be read from the access token. (Your code needs to reverse the Base 64 encoding of the token to read it. In managed code, the TokenHelper.cs, or .vb, file has sample code for this purpose that uses classes from the **Microsoft.IdentityModel.S2S.Tokens** and **System.IdentityModel.Tokens** namespaces.) There is another option available when the application is using the Context Token flow as described in the next paragraph.</span></span>
 

 
<span data-ttu-id="3d87e-p113">В некоторых сценариях приложению может потребоваться кэшировать маркер доступа в расположении, доступном этому приложению во время сеансов или после их завершения. Например, в приложении может быть доступна возможность планировать действия, выполняющиеся после его закрытия. Если такие действия связаны с доступом к SharePoint, надстройке нужно получить маркер доступа. В таких сценариях **приложение должно хранить уникальные маркеры для каждого пользователя**. Для этого в маркере контекста (если используется поток маркера контекста), который SharePoint передает удаленному компоненту надстройки SharePoint при запуске надстройки, указывается строка ключа кэша. Подробнее об этом **специальном ключе кэша** и его использовании можно узнать в разделе [Общие сведения о ключе кэша](#CacheKey). Эту строку можно также использовать в сценарии, описанном в предыдущем абзаце. В системе планирования предусмотрены некоторые средства для хранения необходимых данных конфигурации, например о времени выполнения запланированной работы и ее сути. Держите ключ кэша для маркера доступа в этом хранилище.</span><span class="sxs-lookup"><span data-stu-id="3d87e-p113">There are some scenarios in which in which your application will need to cache the access token someplace that is available to the application across sessions or after a session ends. For example, the application may be designed to enable users to schedule actions to occur after the user has closed the application. If those actions include accessing SharePoint, then the add-in will need to retrieve the access token. In this kind of scenario,  **your application must keep the access tokens of different users distinct**. If you are using the Context Token flow, a cache key string is provided for this purpose in the context token that SharePoint passes to the remote component of your SharePoint Add-in when the add-in is launched. For more information about this **special cache key** and how to use it, see [Understand the cache key](#CacheKey). You can also use this string for the scenario described in the previous paragraph. The scheduling system will have some means of storing configuration data that it will need, such as when the scheduled work will execute and what it should do. Use this storage to hold the cache key for the access token.</span></span>
 

 
<span data-ttu-id="3d87e-p114">Если межсеансовый кэш, который используете вы, также используют несколько приложений, ключи кэша нужно соотнести с приложениями, пользователями и областями SharePoint. Ключ кэша, предоставленный в маркере контекста, уникален для каждого приложения, пользователя и области SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3d87e-p114">If the cross-session cache you use is also shared by multiple applications, then the cache keys will have to be relativized to applications as well as to users and to SharePoint realms. The cache key that is provided in the context token is unique to applications as well as users and SharePoint realm.</span></span>
 

 
 <span data-ttu-id="3d87e-p115">**Если приложение использует поток кода авторизации**, маркера контекста нет, и потому нет и специально созданного ключа кэша. В таком сценарии **вам нужно создать собственную систему ключей для кэшированных данных**. Такие ключи соотносятся с одним или несколькими пользователями, областями SharePoint и приложениями в зависимости от потенциальных конфликтов имен, которые могут возникнуть при использовании приложения. Чтобы создать такую систему, используйте утверждения из маркера доступа (например, **nameId** и **aud**, как показано в таблицах ниже). Ваш код может просто собирать строки или использовать их для создания уникального хэша, выполняющего роль ключа кэша.</span><span class="sxs-lookup"><span data-stu-id="3d87e-p115">**If your application is using the Authorization Code flow**, then there is no context token and, hence, no specially made cache key. In that scenario, **you will need to create your own system of keys for cached data** that are relativized to one or more of the following depending on what potential name clashes might occur given the use cases of your application: the user, the SharePoint realm, and the application. You can use the claims inside the access token for this purpose; for example, the **nameId** and the **aud** (see the tables below). Your code can simply concatenate the strings or use them as seeds to create a unique hash that can serve as the cache key.</span></span>
 

 
<span data-ttu-id="3d87e-p116">Наконец, если ваша надстройка выполняет вызовы SharePoint как с проверкой разрешений приложения, так и с проверкой разрешений пользователя и надстройки, у него будет два разных маркера доступа. Потому понадобятся разные ключи кэша. Определив основной ключ кэша, просто добавьте к нему "_add-in-only" (только надстройка) или "_add-in+user" (надстройка и пользователь).</span><span class="sxs-lookup"><span data-stu-id="3d87e-p116">Finally, if your application makes both add-in-only and user+add-in calls to SharePoint, then it will have two different access tokens. So, you will need distinct cache keys. Once you have decided on a basic cache key, just append "_add-in-only" or "_add-in+user" to it.</span></span>
 

 

 <span data-ttu-id="3d87e-p117">**Внимание!**   **Хранить маркер доступа в файле cookie небезопасно.** Лучше избегать передачи маркера доступа через браузер.</span><span class="sxs-lookup"><span data-stu-id="3d87e-p117">**Caution**   **It is not a secure practice to store the access token in a cookie.** It is usually a good practice to avoid having the access token pass through the browser.</span></span>
 


### <a name="forward-the-access-token-to-backend-systems"></a><span data-ttu-id="3d87e-169">Пересылка маркера доступа в серверные системы</span><span class="sxs-lookup"><span data-stu-id="3d87e-169">Forward the access token to backend systems</span></span>
<span data-ttu-id="3d87e-170"><a name="ForwardTokenToBackend"> </a></span><span class="sxs-lookup"><span data-stu-id="3d87e-170"></span></span>

<span data-ttu-id="3d87e-p118">Внутренние серверы Надстройка SharePoint и удаленное веб-приложение могут быть размещены на разных доменах. Если внутреннему серверу необходимо выполнить операции CRUD (создание, считывание, обновление или удаление) в SharePoint, надстройка работает быстрее, если эти операции поступают напрямую из серверной системы в SharePoint. Домен важен, только если приложение получает маркер доступа из службы контроля доступа. После этого оно может передать такой маркер внутренним службам, которые с его помощью выполнят вызов SharePoint. Код в этих системах нужен для обработки маркеров доступа с истекшим сроком действия и отправки запросов на получение новых родительскому веб-приложению, зарегистрированному с помощью службы контроля доступа. См. раздел  [Обработка маркеров доступа с истекшим сроком действия](#Expired). Этот способ подходит для собственных внутренних серверов приложения, а не для внешних веб-служб. Используя его, подумайте о создании внутренних служб, чтобы по возможности выполнялись вызовы с проверкой разрешений только надстроек.</span><span class="sxs-lookup"><span data-stu-id="3d87e-p118">a SharePoint Add-in may have backend servers that are not hosted in the same domain as the remote web application. When a backend server needs to perform CRUD operations on SharePoint, the add-in performs faster if these operations can go directly from the backend system to SharePoint. Fortunately, domain is only important when your application is getting an access token from ACS. After it has the token, it can forward it to the backend services and they can call SharePoint by using it. Code in these systems will need to handle expired access tokens and send a request for a new one back to the parent web application that is actually registered with ACS. See  [Handle expired access tokens](#Expired). This technique should only be used for your application's own backend servers, not to external web services. Also, if you are using this technique, consider designing the backend services to use add-in-only calls whenever possible.</span></span>
 

 

### <a name="handle-expired-access-tokens"></a><span data-ttu-id="3d87e-179">Обработка маркеров доступа с истекшим сроком действия</span><span class="sxs-lookup"><span data-stu-id="3d87e-179">Handle expired access tokens</span></span>
<span data-ttu-id="3d87e-180"><a name="Expired"> </a></span><span class="sxs-lookup"><span data-stu-id="3d87e-180"></span></span>

<span data-ttu-id="3d87e-p119">Срок действия маркера доступа истекает через несколько часов с момента выпуска маркера (на момент написания данной статьи срок действия был равен 12 часам, но это могло измениться). Если после этого приложение пытается получить доступ к SharePoint, первый запрос к SharePoint возвращает ошибку **401 Unauthorized**. Ваш код должен обработать этот ответ или проверить срок действия маркера доступа перед его использованием. **Код получает другой маркер доступа от службы контроля доступа, используя маркер обновления.** Если используется поток маркера контекста, маркер обновления будет включен в маркер контекста, который надстройка получает из SharePoint в начале первого сеанса с SharePoint. Если используется поток кода авторизации, маркер обновления будет передан приложению вместе с первым маркером доступа. Чтобы маркер обновления был доступен при необходимости, код должен кэшировать его. Этот маркер активен в течение нескольких месяцев. Его можно хранить в файле cookie или серверном хранилище. Дополнительные сведения см. в разделе [Общие сведения об обработке и кэшировании маркеров обновления](#RefreshTokens).</span><span class="sxs-lookup"><span data-stu-id="3d87e-p119">An access token expires after a few hours (twelve hours as of the time this article was written, but that can change). If the application is still accessing SharePoint after the access token expires, then the first request to SharePoint after the expiration results in a  **401 Unauthorized** error. Your code has to handle this response. Alternatively, the code can test the expiration time of the access token before it is used. **Your code uses the refresh token to obtain another access token from ACS.** In the Context Token flow, the refresh token is included in the context token that your add-in receives from SharePoint at the start of its first session with SharePoint. In the Authorization Code flow, it is passed to the application along with the first access token. Your code must cache it so it is available when needed. The refresh token lasts a few months and can be persisted in a cookie or in server-side storage. For more information, see [Understand the handling and caching of refresh tokens](#RefreshTokens).</span></span>
 

 

### <a name="see-examples-of-access-tokens"></a><span data-ttu-id="3d87e-191">Примеры маркеров доступа</span><span class="sxs-lookup"><span data-stu-id="3d87e-191">See examples of access tokens</span></span>
<span data-ttu-id="3d87e-192"><a name="ExampleAccessTokens"> </a></span><span class="sxs-lookup"><span data-stu-id="3d87e-192"></span></span>

<span data-ttu-id="3d87e-193">В этом разделе описаны (с примерами) маркеры доступа и показано, как они отличаются в зависимости от используемой политики авторизации.</span><span class="sxs-lookup"><span data-stu-id="3d87e-193">This section describes, with examples, access tokens and shows how they differ depending on the authorization policy that is being used.</span></span>
 

 

#### <a name="see-access-tokens-for-the-low-trust-authorization-system"></a><span data-ttu-id="3d87e-194">Маркеры доступа для систем авторизации с низким уровнем доверия</span><span class="sxs-lookup"><span data-stu-id="3d87e-194">See access tokens for the low-trust authorization system</span></span>

 <span data-ttu-id="3d87e-195">**Политика "Пользователь и надстройка"**</span><span class="sxs-lookup"><span data-stu-id="3d87e-195">**User+add-in Policy**</span></span>
 

 
<span data-ttu-id="3d87e-p120">Ниже представлен расшифрованный **пример маркера доступа для пользователя и надстройки, созданного службой контроля доступа**. Этот маркер предназначен для выполнения вызовов SharePoint с помощью [политики "Пользователь и надстройка"](add-in-authorization-policy-types-in-sharepoint.md). Пробел добавлен для удобства чтения. Маркер соответствует протоколу [JWT (JSON Web Token)](http://datatracker.ietf.org/doc/draft-ietf-oauth-json-web-token/?include_text=1). Объект JSON в маркере представляет собой набор утверждений. Его свойства описаны в табл. 1. Обратите внимание, что во всех значениях необходимо использовать только строчные буквы. (Маркеры доступа "Пользователь и надстройка" одинаковые в [потоке маркера контекста](creating-sharepoint-add-ins-that-use-low-trust-authorization.md#Flows) и [потоке кода авторизации](creating-sharepoint-add-ins-that-use-low-trust-authorization.md#Flows).)</span><span class="sxs-lookup"><span data-stu-id="3d87e-p120">The following is a decoded  **example of a user+add-in access token generated by ACS** to be used for calls to SharePoint using the [user+add-in policy](add-in-authorization-policy-types-in-sharepoint.md). White space has been added for readability. The token complies with the  [JSON Web Token](http://datatracker.ietf.org/doc/draft-ietf-oauth-json-web-token/?include_text=1) protocol. The JavaScript Object Notation (JSON) object in the token is called theclaim set See table 1 for details about the properties in the claim set. Note that all the values must be lower-case. (User+add-in access tokens are the same in the [Context Token flow](creating-sharepoint-add-ins-that-use-low-trust-authorization.md#Flows) and the [Authorization Code flow](creating-sharepoint-add-ins-that-use-low-trust-authorization.md#Flows).)</span></span>
 

 



```
{
 "aud": "00000003-0000-0ff1-ce00-000000000000/company.sharepoint.com@040f2415-e6e3-4480-96ce-26ef73275f73",
 "iss": "00000001-0000-0000-c000-000000000000@040f2415-e6e3-4480-96ce-26ef73275f73",
 "nbf": 1377549246,
 "exp": 1377592446,
 "nameid": "2303000085ff9abc",
 "actor": "964de6ad-6d28-4dc7-8e05-3acd8006e5c9@040f2415-e6e3-4480-96ce-26ef73275f73",
 "identityprovider": "urn:federation:microsoftonline"
}
```


<span data-ttu-id="3d87e-202">**Табл. 1. Требования маркеров доступа "Пользователь и надстройка", изданные службой контроля доступа**</span><span class="sxs-lookup"><span data-stu-id="3d87e-202">**Table 1: ACS-issued user+add-in access token claims**</span></span>


|<span data-ttu-id="3d87e-203">**Утверждение**</span><span class="sxs-lookup"><span data-stu-id="3d87e-203">**Claim**</span></span>|<span data-ttu-id="3d87e-204">**Описание**</span><span class="sxs-lookup"><span data-stu-id="3d87e-204">**Description**</span></span>|<span data-ttu-id="3d87e-205">**Соответствующее значение в примере маркера доступа**</span><span class="sxs-lookup"><span data-stu-id="3d87e-205">**Corresponding value in the sample access token**</span></span>|
|:-----|:-----|:-----|
| `aud`|<span data-ttu-id="3d87e-p121">Сокращение для слова "аудитория". Обозначает субъект, для которого предназначен маркер. Используемый формат: _идентификатор субъекта аудитории_/ _домен SharePoint_@ _область SharePoint_, где _идентификатор субъекта аудитории_ — постоянный код субъекта безопасности для SharePoint. (См. статью [Константы субъектов приложения продукта Майкрософт](http://msdn.microsoft.com/en-us/library/hh629982%28v=office.12%29.aspx).) _Область SharePoint_ — это GUID тенантности SharePoint Online или локальной фермы SharePoint, для доступа к которым создан маркер доступа. Этот GUID функционирует как идентификатор области для издателя маркера (в этом случае Azure ACS).</span><span class="sxs-lookup"><span data-stu-id="3d87e-p121">Short for "audience", meaning the principal for which the token is intended. The format is  _audience principal ID_/ _SharePoint domain_@ _SharePoint realm_, where  _audience principal ID_ is a permanent security principal ID for SharePoint. (See [Microsoft Product Application Principal Constants](http://msdn.microsoft.com/en-us/library/hh629982%28v=office.12%29.aspx).). _SharePoint realm_ is the GUID of the SharePoint Online tenancy, or the on-premise SharePoint farm, that the access token is used to access. This GUID functions as the realm's ID for the token issuer, in this case Azure ACS.</span></span>|<span data-ttu-id="3d87e-211">00000003-0000-0ff1-ce00-000000000000/company.sharepoint.com@040f2415-e6e3-4480-96ce-26ef73275f73</span><span class="sxs-lookup"><span data-stu-id="3d87e-211">00000003-0000-0ff1-ce00-000000000000/company.sharepoint.com@040f2415-e6e3-4480-96ce-26ef73275f73</span></span>|
| `iss`|<span data-ttu-id="3d87e-p122">Сокращение для слова "издатель". Представляет субъект, создавший маркер. Используется следующий формат: _GUID издателя_@ _GUID области SharePoint_. В системах авторизации с низким уровнем доверия издателем является Azure ACS с GUID **00000001-0000-0000-c000-000000000000**.</span><span class="sxs-lookup"><span data-stu-id="3d87e-p122">Short for "issuer". It represents the principal that created the token. The format is  _Issuer GUID_@ _SharePoint realm GUID_.In the low-trust authorization system, the issuer is Azure ACS and it's GUID is  **00000001-0000-0000-c000-000000000000**.</span></span>|<span data-ttu-id="3d87e-215">00000001-0000-0000-c000-000000000000@040f2415-e6e3-4480-96ce-26ef73275f73</span><span class="sxs-lookup"><span data-stu-id="3d87e-215">00000001-0000-0000-c000-000000000000@040f2415-e6e3-4480-96ce-26ef73275f73</span></span>|
| `nbf`|<span data-ttu-id="3d87e-p123">Сокращение от "not before" (не ранее). Представляет время  *начала*  действия маркера (указывается в секундах, отсчет ведется с полуночи 1 января 1970 г.). По умолчанию это момент создания маркера. Дополнительные сведения см. в разделе [Работа со значениями времени JWT](#JWTtimes).  </span><span class="sxs-lookup"><span data-stu-id="3d87e-p123">Short for "not before". It represents the time at which the token  *starts*  being valid, in seconds since midnight, January 1, 1970. By default, it is set to the moment the token is created. See [Work with JWT time values](#JWTtimes) for more information.</span></span>|<span data-ttu-id="3d87e-220">1377549246</span><span class="sxs-lookup"><span data-stu-id="3d87e-220">1377549246</span></span>|
| `exp`|<span data-ttu-id="3d87e-p124">Сокращение для слова "истечение срока действия". Представляет время истечения срока действия маркера. По умолчанию срок действия равен 12 часам после времени **nbf**. Дополнительные сведения см. в статье [Работа со значениями времени JWT](#JWTtimes).</span><span class="sxs-lookup"><span data-stu-id="3d87e-p124">Short for "expiration". It represents the time the token expires. By default, this is 12 hours after the  **nbf** time. See [Work with JWT time values](#JWTtimes) for more information.</span></span>|<span data-ttu-id="3d87e-225">1377592446</span><span class="sxs-lookup"><span data-stu-id="3d87e-225">1377592446</span></span>|
| `nameid`|<span data-ttu-id="3d87e-p125">Уникальный идентификатор пользователя, для которого выпущен маркер. Формат зависит от поставщика удостоверений. В этом примере поставщик Microsoft Online. Если бы это была служба Active Directory, ИД выглядел бы так: "s-1-5-21-2127521184-1604012920-1887927527-415149".</span><span class="sxs-lookup"><span data-stu-id="3d87e-p125">A unique identifier for the user for whom the token is issued. The format varies depending on the identity provider. In this example, the provider is Microsoft Online, but if it was Active Directory, the ID would look like "s-1-5-21-2127521184-1604012920-1887927527-415149".</span></span>|<span data-ttu-id="3d87e-229">2303000085ff9abc</span><span class="sxs-lookup"><span data-stu-id="3d87e-229">2303000085ff9abc</span></span>|
| `actor`|<span data-ttu-id="3d87e-p126">Субъект, который ищет доступ к ферме или тенантности SharePoint. Он имеет следующую форму: _Идентификатор клиента приложения_@ _Область SharePoint_.</span><span class="sxs-lookup"><span data-stu-id="3d87e-p126">The principal that seeks access to the SharePoint farm or tenancy. It has the form  _Client ID of Application_@ _SharePoint realm_.</span></span>|<span data-ttu-id="3d87e-232">964de6ad-6d28-4dc7-8e05-3acd8006e5c9@040f2415-e6e3-4480-96ce-26ef73275f73</span><span class="sxs-lookup"><span data-stu-id="3d87e-232">964de6ad-6d28-4dc7-8e05-3acd8006e5c9@040f2415-e6e3-4480-96ce-26ef73275f73</span></span>|
| `identityprovider`|<span data-ttu-id="3d87e-p127">Уникальное имя поставщика удостоверений, зарегистрированное в Internet Assigned Numbers Authority (IANA). Для надстройки, установленной в SharePoint Online, это значение обычно такое же, как в примере. Для надстройки, установленной в локальной ферме, обычно используется локальный поставщик удостоверений, например urn:office:idp:activedirectory.</span><span class="sxs-lookup"><span data-stu-id="3d87e-p127">The unique name of the identity provider as registered with the Internet Assigned Numbers Authority (IANA).For an add-in that is installed to SharePoint Online, the value is usually the same as in this example. For an add-in that is installed to an on-premise farm, it would typically be an on-premise identity provider, such as "urn:office:idp:activedirectory".</span></span>|<span data-ttu-id="3d87e-235">urn:federation:microsoftonline</span><span class="sxs-lookup"><span data-stu-id="3d87e-235">urn:federation:microsoftonline</span></span>|
 <span data-ttu-id="3d87e-236">**Политика "Только надстройка"**</span><span class="sxs-lookup"><span data-stu-id="3d87e-236">**add-in-only Policy**</span></span>
 

 
<span data-ttu-id="3d87e-p128">Ниже представлен расшифрованный **пример маркера доступа только для надстройки, изданного службой контроля доступа**. Этот маркер предназначен для выполнения вызовов SharePoint с помощью [политики "Только надстройка"](add-in-authorization-policy-types-in-sharepoint.md). Пробел добавлен для удобства чтения. Маркер соответствует протоколу [JWT (JSON Web Token)](http://datatracker.ietf.org/doc/draft-ietf-oauth-json-web-token/?include_text=1). Свойства в наборе требований описаны в табл. 2. Политика "Только надстройка" недоступна для надстроек, в которых используется [поток кода авторизации](creating-sharepoint-add-ins-that-use-low-trust-authorization.md#Flows). Это объясняется тем, что у них нет файла манифеста надстройки, и они не могут запрашивать разрешение на использованием вызовов "Только надстройка".</span><span class="sxs-lookup"><span data-stu-id="3d87e-p128">The following is a decoded  **example of an add-in-only access token generated by ACS** to be used for calls to SharePoint using the [add-in-only policy](add-in-authorization-policy-types-in-sharepoint.md). White space has been added for readability. The token complies with the  [JSON Web Token](http://datatracker.ietf.org/doc/draft-ietf-oauth-json-web-token/?include_text=1) protocol. See table 2 for details about the properties in the claim set. (The add-in-only policy is not available for applications that use the [Authorization Code flow](creating-sharepoint-add-ins-that-use-low-trust-authorization.md#Flows), because they do not have an add-in manifest file and, thus, cannot request permission to use add-in-only calls.)</span></span>
 

 



```
{
 "aud":"00000003-0000-0ff1-ce00-000000000000/company.sharepoint.com@040f2415-e6e3-4480-96ce-26ef73275f73",
 "iss":"00000001-0000-0000-c000-000000000000@040f2415-e6e3-4480-96ce-26ef73275f73",
 "nbf":1403304705,
 "exp":1403347905,
 "nameid":"c76da14e-07fd-4638-a723-1ff60ce70d63@040f2415-e6e3-4480-96ce-26ef73275f73",
 "sub":"1d47ac31-498b-4988-8aac-85fc9bd2e1ce",
 "oid":"1d47ac31-498b-4988-8aac-85fc9bd2e1ce",
 "trustedfordelegation":"false",
 "identityprovider":"00000001-0000-0000-c000-000000000000@040f2415-e6e3-4480-96ce-26ef73275f73"
}
```


<span data-ttu-id="3d87e-242">**Табл. 2. Требования маркеров доступа "Только надстройка", изданные службой контроля доступа**</span><span class="sxs-lookup"><span data-stu-id="3d87e-242">**Table 2: ACS-issued add-in-only access token claims**</span></span>


|<span data-ttu-id="3d87e-243">**Утверждение**</span><span class="sxs-lookup"><span data-stu-id="3d87e-243">**Claim**</span></span>|<span data-ttu-id="3d87e-244">**Описание**</span><span class="sxs-lookup"><span data-stu-id="3d87e-244">**Description**</span></span>|<span data-ttu-id="3d87e-245">**Соответствующее значение в примере маркера доступа**</span><span class="sxs-lookup"><span data-stu-id="3d87e-245">**Corresponding value in the sample access token**</span></span>|
|:-----|:-----|:-----|
| `aud`|<span data-ttu-id="3d87e-246">То же, что и для описанного выше маркера "Пользователь и надстройка".</span><span class="sxs-lookup"><span data-stu-id="3d87e-246">Same as the user+add-in token above.</span></span>|<span data-ttu-id="3d87e-247">00000003-0000-0ff1-ce00-000000000000/company.sharepoint.com@040f2415-e6e3-4480-96ce-26ef73275f73</span><span class="sxs-lookup"><span data-stu-id="3d87e-247">00000003-0000-0ff1-ce00-000000000000/company.sharepoint.com@040f2415-e6e3-4480-96ce-26ef73275f73</span></span>|
| `iss`|<span data-ttu-id="3d87e-248">См. маркер для пользователя и надстройки выше.</span><span class="sxs-lookup"><span data-stu-id="3d87e-248">Same as the user+add-in token above.</span></span>|<span data-ttu-id="3d87e-249">00000001-0000-0000-c000-000000000000@040f2415-e6e3-4480-96ce-26ef73275f73</span><span class="sxs-lookup"><span data-stu-id="3d87e-249">00000001-0000-0000-c000-000000000000@040f2415-e6e3-4480-96ce-26ef73275f73</span></span>|
| `nbf`|<span data-ttu-id="3d87e-250">См. маркер для пользователя и надстройки выше.</span><span class="sxs-lookup"><span data-stu-id="3d87e-250">Same as the user+add-in token above.</span></span>|<span data-ttu-id="3d87e-251">1403304705</span><span class="sxs-lookup"><span data-stu-id="3d87e-251">1403304705</span></span>|
| `exp`|<span data-ttu-id="3d87e-252">См. маркер для пользователя и надстройки выше.</span><span class="sxs-lookup"><span data-stu-id="3d87e-252">Same as the user+add-in token above.</span></span>|<span data-ttu-id="3d87e-253">1403347905</span><span class="sxs-lookup"><span data-stu-id="3d87e-253">1403347905</span></span>|
| `nameid`|<span data-ttu-id="3d87e-p129">Уникальный идентификатор надстройки, а не пользователя, так как идентификатор пользователя не важен в политике только для надстройки. Формат:  _ИД клиента_@ _область SharePoint_.  </span><span class="sxs-lookup"><span data-stu-id="3d87e-p129">A unique identifier for the add-in, instead of the user, since the user's identity doesn't matter with the add-in-only policy. The format is  _client ID_@ _SharePoint realm_.</span></span>|<span data-ttu-id="3d87e-256">c76da14e-07fd-4638-a723-1ff60ce70d63@040f2415-e6e3-4480-96ce-26ef73275f73</span><span class="sxs-lookup"><span data-stu-id="3d87e-256">c76da14e-07fd-4638-a723-1ff60ce70d63@040f2415-e6e3-4480-96ce-26ef73275f73</span></span>|
| `sub`|<span data-ttu-id="3d87e-p130">Сокращение для слова "субъект". Это субъект маркера, который пытается получить доступ к SharePoint (в данном случае он представляет собой удаленное веб-приложение). В качестве значения используется идентификатор объекта. См. требование **oid** ниже.</span><span class="sxs-lookup"><span data-stu-id="3d87e-p130">Short for "subject". It is the subject of the token, which is the principal that is seeking access to SharePoint; in this case, the remote web application. The object ID is used for the value. See the  **oid** claim below.</span></span>|<span data-ttu-id="3d87e-261">1d47ac31-498b-4988-8aac-85fc9bd2e1ce</span><span class="sxs-lookup"><span data-stu-id="3d87e-261">1d47ac31-498b-4988-8aac-85fc9bd2e1ce</span></span>|
| `oid`|<span data-ttu-id="3d87e-p131">Сокращение от "object ID" (ИД объекта). Это ИД объекта в службе Azure Active Directory для удаленного веб-приложения. В маркере доступа только для надстройки субъект (с утверждением "sub") и ИД объекта имеют одинаковое значение.</span><span class="sxs-lookup"><span data-stu-id="3d87e-p131">Short for "object ID". It is the object ID in Azure Active Directory for the remote web application. In an add-in-only access token, the subject and object ID are the same value.</span></span>|<span data-ttu-id="3d87e-265">1d47ac31-498b-4988-8aac-85fc9bd2e1ce</span><span class="sxs-lookup"><span data-stu-id="3d87e-265">1d47ac31-498b-4988-8aac-85fc9bd2e1ce</span></span>|
| `trustedfordelegation`|<span data-ttu-id="3d87e-p132">Логическое значение, которое указывает, должна ли служба SharePoint доверять Надстройка SharePoint при аутентификации и авторизации пользователя. В вызовах с проверкой разрешений только для надстройки имеет значение false, так как идентификатор пользователя не важен.</span><span class="sxs-lookup"><span data-stu-id="3d87e-p132">A Boolean value that specifies whether SharePoint should trust the SharePoint Add-in to authenticate and authorize the user. It is false in add-in-only calls because the user identity doesn't matter.</span></span>|<span data-ttu-id="3d87e-268">false</span><span class="sxs-lookup"><span data-stu-id="3d87e-268">false</span></span>|
| `identityprovider`|<span data-ttu-id="3d87e-p133">Уникальное имя поставщика удостоверений. Так как предоставляется удостоверение надстройки, а не пользователя, поставщиком выступает служба контроля доступа. Формат:  _GUID службы контроля доступа_@ _область SharePoint_.  </span><span class="sxs-lookup"><span data-stu-id="3d87e-p133">The unique name of the identity provider. Since it is the add-in, rather than a user, whose identity is being provided, ACS is the identity provider. The format is  _ACS GUID_@ _SharePoint realm_.</span></span>|<span data-ttu-id="3d87e-272">00000001-0000-0000-c000-000000000000@040f2415-e6e3-4480-96ce-26ef73275f73</span><span class="sxs-lookup"><span data-stu-id="3d87e-272">00000001-0000-0000-c000-000000000000@040f2415-e6e3-4480-96ce-26ef73275f73</span></span>|

## <a name="understand-the-structure-and-handling-of-context-tokens"></a><span data-ttu-id="3d87e-273">Общие сведения о структуре и обработке маркеров контекста</span><span class="sxs-lookup"><span data-stu-id="3d87e-273">Understand the structure and handling of context tokens</span></span>
<span data-ttu-id="3d87e-274"><a name="ContextTokens"> </a></span><span class="sxs-lookup"><span data-stu-id="3d87e-274"></span></span>

<span data-ttu-id="3d87e-p134">Маркер контекста используется только в  [потоке маркера контекста](creating-sharepoint-add-ins-that-use-low-trust-authorization.md#Flows) системы авторизации с низким уровнем доверия. **Когда выполняется запуск Надстройка SharePoint в SharePoint, служба SharePoint отправляет службе Azure ACS запрос на создание маркера контекста. Затем SharePoint передает этот маркер удаленному компоненту Надстройка SharePoint.** Маркер контекста передается в виде скрытого параметра формы ( **SPAppToken**) в запросе от SharePoint для начальной страницы удаленного компонента. Этот маркер подписан с использованием секрета клиента, который знают только служба контроля доступа и Надстройка SharePoint. **Маркер контекста содержит маркер обновления, который надстройка использует** вместе с другими данными из маркера контекста, чтобы **запросить маркер доступа** у службы контроля доступа. (Во время написания этой статьи продолжительность существования маркера доступа, выпущенного службой контроля доступа для SharePoint, составляла 12 часов, но это могло измениться.) **Основные задачи кода в Надстройка SharePoint**:</span><span class="sxs-lookup"><span data-stu-id="3d87e-p134">A context token is used only in the  [Context Token flow](creating-sharepoint-add-ins-that-use-low-trust-authorization.md#Flows) of the low-trust authorization system. **When the SharePoint Add-in is launched in SharePoint, SharePoint requests that Azure ACS create a context token that SharePoint then passes on to the remote component of the SharePoint Add-in.** The token is passed as a hidden form parameter called **SPAppToken** in a request from SharePoint for the start page of the remote component. The token is signed with a client secret known only to ACS and the SharePoint Add-in. The **context token includes a refresh token that the add-in uses**, along with other information from the context token, **to request an access token** from ACS. (When this article was written, ACS-issued context tokens for SharePoint had a life span of 12 hours, but that could change.) The **main tasks for the code in the SharePoint Add-in** are the following:</span></span>
 

 

- <span data-ttu-id="3d87e-281">**Проверка маркера контекста** с помощью секрета клиента надстройки.</span><span class="sxs-lookup"><span data-stu-id="3d87e-281">Use the client secret of the add-in to  **validate the context token**.</span></span>
    
 
-  <span data-ttu-id="3d87e-282">**Кэширование маркера контекста** или извлечение и отдельное кэширование маркера обновления и некоторых других элементов из него.</span><span class="sxs-lookup"><span data-stu-id="3d87e-282">**Cache the context token** or extract, and separately cache, the refresh token and certain other items from inside it.</span></span>
    
 
- <span data-ttu-id="3d87e-283">Использование маркера обновления и других сведений для **запроса маркера доступа** в службе контроля доступа и последующего его кэширования.</span><span class="sxs-lookup"><span data-stu-id="3d87e-283">Use the refresh token and other information to  **request an access token** from ACS (which is itself then cached).</span></span>
    
 
-  <span data-ttu-id="3d87e-284">**Кэширование CacheKey** на основе маркера контекста.</span><span class="sxs-lookup"><span data-stu-id="3d87e-284">**Cache the CacheKey** from the context token.</span></span>
    
 

 <span data-ttu-id="3d87e-p135">**Важно!** Первые две задачи необходимо выполнить, прежде чем пользователь перейдет на другую страницу или обновит текущую, иначе маркер будет потерян. Например, в приложении веб-форм ASP.NET эти задачи следует выполнять с помощью метода **Page_Load** (в коде условия он представлен блоком, который выполняется, если запрос не передается обратно). В приложении MVC ASP.NET эти задачи следует выполнять с помощью метода контроллера, используемого по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="3d87e-p135">**Important**  The first two tasks must occur before the user navigates to another page or refreshes the page or the token is lost. For example, in an ASP.NET web forms application, consider doing those tasks in the  **Page_Load** method (in a conditional code block that runs only when the request is not a postback). In an ASP.NET MVC application, consider doing these tasks in the default controller method.</span></span>
 

<span data-ttu-id="3d87e-p136">Если вы используете управляемый код, пример кода для некоторых задач представлен в файлах SharePointContext и TokenHelper (с расширением CS или VB), которые входят в Инструменты разработчика Microsoft Office для Visual Studio. Вам нужно только выполнить простые вызовы членов класса TokenHelper. Например, ваш код может справиться с первой задачей с помощью такой одной строки:</span><span class="sxs-lookup"><span data-stu-id="3d87e-p136">If you are using managed code, sample code for some of these tasks is in the SharePointContext.cs (or .vb) and TokenHelper.cs (or .vb) files that are included in Microsoft Office Developer Tools for Visual Studio. You just need to make simple calls to the members of the TokenHelper class. For example, your code can do the first task with the following single line of code:</span></span>
 

 



```C#
SharePointContextToken contextToken =
    TokenHelper.ReadAndValidateContextToken(contextTokenString, 
    Request.Url.Authority);
```

<span data-ttu-id="3d87e-291">Примеры выполнения некоторых задач с помощью PHP см. в статье  [SharePoint: выполнение операций в библиотеке документов SharePoint на сайте, созданном с использованием PHP](https://code.msdn.microsoft.com/SharePoint-Perform-8a78b8ef).</span><span class="sxs-lookup"><span data-stu-id="3d87e-291">For an example of how to do some of these tasks with PHP, see the sample  [SharePoint: Perform operations on SharePoint Document Library from PHP site](https://code.msdn.microsoft.com/SharePoint-Perform-8a78b8ef).</span></span>
 

 

### <a name="cache-the-context-token-or-parts-of-it"></a><span data-ttu-id="3d87e-292">Кэширование маркера контекста или его частей</span><span class="sxs-lookup"><span data-stu-id="3d87e-292">Cache the context token or parts of it</span></span>
<span data-ttu-id="3d87e-293"><a name="CacheContextToken"> </a></span><span class="sxs-lookup"><span data-stu-id="3d87e-293"></span></span>

<span data-ttu-id="3d87e-p137">Вы можете **кэшировать** весь маркер контекста либо только маркер обновления и ряд других элементов в нем, которые ваш код использует для получения маркеров доступа **в серверном или клиентском хранилище**. Для простоты в этой статье подразумевается, что вы кэшируете весь маркер контекста.</span><span class="sxs-lookup"><span data-stu-id="3d87e-p137">You can  **cache** whole context token, or just the refresh token and certain other items that are inside it that your code uses to get access tokens, **in either server-side or client-side storage**. For simplicity, this article assumes that you cache the context token as a unit.</span></span>
 

 

 <span data-ttu-id="3d87e-p138">**Важно!** Напомним еще раз, так как это очень важно: не используйте кэширование на стороне клиента для маркера *доступа*. Его можно безопасно использовать только для маркера контекста.</span><span class="sxs-lookup"><span data-stu-id="3d87e-p138">**Important**  We remind you one more time because it's really important: do not use client-side caching for the  *access*  token. It is safe to use it only for the context token.</span></span>
 

<span data-ttu-id="3d87e-p139">[Варианты кэширования на стороне сервера](#CacheAccessToken) такие же, как и перечисленные выше для маркера доступа. Варианты на стороне клиента также включают файл cookie и скрытое поле формы на HTML-странице. Кроме того, можно хранить маркер контекста в кэше сеанса, а ключ **CacheKey**, полученный из него, на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="3d87e-p139">You have the same  [server-side caching options](#CacheAccessToken) for as are listed above for the access token. Client-side options include a cookie and a hidden form field on an HTML page. Another option is to store the context token in the session cache, but store the **CacheKey** obtained from inside it on the client.</span></span>
 

 
<span data-ttu-id="3d87e-p140">Если ваша надстройка получает доступ к SharePoint после завершения сеанса, вам не удастся использовать ни кэширование сеанса, ни кэширование на стороне клиента. Это объясняется тем, что у надстройки должен быть доступ к маркеру обновления на случай если истечет срок действия исходного маркера доступа при выполнении работы после сеанса. В этом сценарии нужен устойчивый (межсеансовый) кэш, который совместно используют несколько пользователей, областей SharePoint или надстроек. Потому код должен использовать ключи кэша, в которых различаются пользователи, области SharePoint и надстройки, как описано выше в разделе [Кэширование маркера доступа](#CacheAccessToken). Для этого можно **использовать специальный ключ кэша** из маркера контекста так же, как и для маркера доступа. (См. раздел [Общие сведения о ключе кэша](#CacheKey) ниже.)</span><span class="sxs-lookup"><span data-stu-id="3d87e-p140">If your application accesses SharePoint after a session is ended, then neither session-caching nor client-side caching is an option, because the refresh token must be available to the application in case the original access token has expired when the post-session work executes. In this scenario, you need a durable (cross-session) cache that is shared by multiple users and/or SharePoint realms and/or applications. So, your code has to use cache keys that distinguish user, SharePoint realm, and/or application as explained above in  [Cache the access token](#CacheAccessToken). You can  **use the special cache key** that is inside the context token for this purpose just as you used it for the access token. (See [Understand the cache key](#CacheKey) below.)</span></span>
 

 

#### <a name="understand-the-cache-key"></a><span data-ttu-id="3d87e-306">Общие сведения о ключе кэша</span><span class="sxs-lookup"><span data-stu-id="3d87e-306">Understand the cache key</span></span>
<span data-ttu-id="3d87e-307"><a name="CacheKey"> </a></span><span class="sxs-lookup"><span data-stu-id="3d87e-307"></span></span>

 <span data-ttu-id="3d87e-p141">**Ключ кэша непрозрачная строка, которая уникальна для комбинации пользователя, издателя имени пользователя, надстройки и фермы SharePoint или клиента SharePoint Online.** Ниже приведена его форма до шифрования, где _область_ это GUID локальной фермы SharePoint или области клиента SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="3d87e-p141">**The cache key is an opaque string that is unique to the combination of user, user name issuer, add-in, and SharePoint farm or SharePoint Online tenant.** Before it is encrypted, it has the following form, where _Realm_ is the GUID of the on-premise SharePoint farm or the SharePoint Online tenancy.</span></span>
 

 
 <span data-ttu-id="3d87e-310">_UserNameId_ + "," + _UserNameIdIssuer_ + "," + _ApplicationId_ + "," + _Realm_</span><span class="sxs-lookup"><span data-stu-id="3d87e-310">_UserNameId_ + "," + _UserNameIdIssuer_ + "," + _ApplicationId_ + "," + _Realm_</span></span>
 

 
<span data-ttu-id="3d87e-p142">Ключ кэша не содержит сведений об URL-адресе сайта. У каждого клиента SharePoint Online (или локальной фермы SharePoint) есть уникальная область, и потому ключ кэша уникален для каждой комбинации имени пользователя, его издателя, приложения и фермы. В приведенном ниже примере маркера контекста значение зашифрованного ключа кэша выглядит так:</span><span class="sxs-lookup"><span data-stu-id="3d87e-p142">The cache key does not contain site URL information. Each SharePoint Online tenant (or on-premise SharePoint farm) has a unique realm, so, the cache key is unique for each combination of user name, user name issuer, application, and farm. In the example context token below, the encrypted cache key value is:</span></span>
 

 
 `KQAIUpDUD0sm5Tr83U+jZGYVuPPCPu8BGwoWiAACqNw=`
 

 
<span data-ttu-id="3d87e-p143">Так как с помощью одного ключа кэша надстройка может кэшировать несколько элементов в одном кэше, например маркер доступа и маркер контекста, **ключ кэша следует использовать в качестве основы**. При необходимости в его начало или конец можно добавить определенную строку, например AccessToken или ContextToken, чтобы сформировать полный ключ кэша. **Еще один вариант — создать класс** со свойствами для различных элементов, которые необходимо кэшировать, а затем кэшировать объект такого типа. Есть и **третий вариант** на случай если вы **используете базу данных** в качестве кэша. Он подразумевает использование таблицы со столбцом CacheKey и дополнительными столбцами для кэшированных элементов (AccessToken, ContextToken и т. д.).</span><span class="sxs-lookup"><span data-stu-id="3d87e-p143">Since your application may be caching multiple items, such as both the access token and the context token in the same cache with the same cache key,  **consider using the cache key as a stem** and either appending or prepending a specific string such as "AccessToken" or "ContextToken" to it as needed to form a complete cache key. **Another option is to create a class** with properties for the various things you want to cache and then cache an object of that type. A **third option**, if you are **using a database** as a cache, is to use a table with a CacheKey column and additional columns for the cached items (AccessToken, ContextToken, etc.).</span></span>
 

 
<span data-ttu-id="3d87e-p144">Конечно, приложение не должно использовать один кэш для всех операций кэширования. Обычно маркер доступа кэшируют в кэше сеанса, маркер контекста (или маркер обновления из него) в базе данных, а ключ CacheKey в файле cookie.</span><span class="sxs-lookup"><span data-stu-id="3d87e-p144">Your application does not have to use the same cache for everything it is caching, of course. A common pattern is to cache the access token in session cache, the context token (or the refresh token from inside it) in a database, and the CacheKey in a cookie.</span></span>
 

 

### <a name="use-the-context-token-to-get-an-access-token"></a><span data-ttu-id="3d87e-319">Получение маркера доступа с помощью маркера контекста</span><span class="sxs-lookup"><span data-stu-id="3d87e-319">Use the context token to get an access token</span></span>
<span data-ttu-id="3d87e-320"><a name="UseContextTokenToGetAccessToken"> </a></span><span class="sxs-lookup"><span data-stu-id="3d87e-320"></span></span>

 <span data-ttu-id="3d87e-p145">**Чтобы получить маркер доступа, приложение отправляет запрос напрямую в службу контроля доступа.** Запрос включает три части данных, извлеченные из маркера контекста, а также другую информацию:</span><span class="sxs-lookup"><span data-stu-id="3d87e-p145">**To get an access token, your application sends a request directly to ACS.** The request includes three pieces of information that are extracted from the context token (and other information):</span></span>
 

 

- <span data-ttu-id="3d87e-323">Маркер обновления</span><span class="sxs-lookup"><span data-stu-id="3d87e-323">The refresh token</span></span>
    
 
- <span data-ttu-id="3d87e-324">GUID субъекта приложения в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3d87e-324">The application principal GUID of SharePoint.</span></span>
    
 
- <span data-ttu-id="3d87e-325">GUID области фермы SharePoint или тенантности SharePoint Online, доступ к которой ищет надстройка.</span><span class="sxs-lookup"><span data-stu-id="3d87e-325">The realm GUID of the SharePoint farm or SharePoint Online tenancy to which the add-in is seeking access.</span></span>
    
 
<span data-ttu-id="3d87e-p146">Файл TokenHelper (с расширением CS или VB) содержит код, который создает этот запрос. Пример такого кода PHP см. в статье  [SharePoint: выполнение операций в библиотеке документов SharePoint на сайте, созданном с использованием PHP](http://code.msdn.microsoft.com/office/SharePoint-Perform-8a78b8ef/sourcecode?fileId=117521&amp;pathId=1932320454).</span><span class="sxs-lookup"><span data-stu-id="3d87e-p146">The TokenHelper.cs (or .vb) file has code that creates this request. For an example of PHP code that does this, see  [SharePoint: Perform operations on SharePoint Document Library from PHP site](http://code.msdn.microsoft.com/office/SharePoint-Perform-8a78b8ef/sourcecode?fileId=117521&amp;pathId=1932320454).</span></span>
 

 
<span data-ttu-id="3d87e-p147">Приложение может получить область клиента или фермы SharePoint в среде выполнения вместо ее извлечения из маркера контекста. Если вы используете управляемый код, для получения области существует метод  `TokenHelper.GetRealmFromTargetUrl`. Значение необходимо кэшировать, чтобы код не выполнял повторный вызов по сети для его получения.</span><span class="sxs-lookup"><span data-stu-id="3d87e-p147">The application can get the realm of the SharePoint tenancy or farm at runtime as an alternative to parsing it from the context token. If you are using managed code, there is a  `TokenHelper.GetRealmFromTargetUrl` method to get the realm. Be sure to cache the value so that your code does not make another network call to get it again.</span></span>
 

 

### <a name="get-a-new-context-token"></a><span data-ttu-id="3d87e-331">Получение нового маркера контекста</span><span class="sxs-lookup"><span data-stu-id="3d87e-331">Get a new context token</span></span>
<span data-ttu-id="3d87e-332"><a name="GetNewContextToken"> </a></span><span class="sxs-lookup"><span data-stu-id="3d87e-332"></span></span>

 <span data-ttu-id="3d87e-p148">**Если нужен новый маркер контекста** (обычно это происходит из-за истечения срока действия маркера обновления, который он содержит), **код может получить его, переадресовав браузер на специальную страницу на любом веб-сайте SharePoint** AppRedirect.aspx. К URL-адресу этой страницы необходимо добавить два параметра запроса:</span><span class="sxs-lookup"><span data-stu-id="3d87e-p148">**If you need a new context token**, typically because the refresh token (which are contained in context tokens) has expired, **your code can get a new one by redirecting the browser to a special page in every SharePoint website** -- AppRedirect.aspx. Two query parameters have to be attached to the URL of this page:</span></span>
 

 

-  <span data-ttu-id="3d87e-335">`client_id`: идентификатор клиента надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3d87e-335">`client_id`: The client ID of your SharePoint Add-in.</span></span>
    
 
-  <span data-ttu-id="3d87e-p149">`redirect_uri`. URI, на который необходимо перенаправить браузер после получения нового маркера контекста. Служба SharePoint передаст по методу POST маркер контекста в этот URI. Обычно это страница, метод контроллера или веб-службы, запросившие новый маркер контекста. Значение должно быть закодировано как URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="3d87e-p149">`redirect_uri`: The URI to which you want the browser redirected after the new context token is obtained. SharePoint will POST the context token to this URI. Typically, this is the same page, controller method, or web service method that requested the new context token. The value must be URL-encoded.</span></span>
    
 
<span data-ttu-id="3d87e-340">Ниже показана структура URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="3d87e-340">The following shows the structure of the URL:</span></span>
 

 



```
https://<SharePointDomain> /_layouts/15/appredirect.aspx?client_id=<app_client_GUID> &amp;redirect_uri=<URL-encoded_redirect_URI>
```

<span data-ttu-id="3d87e-341">Пример запроса в ASP.NET с помощью файла TokenHelper:</span><span class="sxs-lookup"><span data-stu-id="3d87e-341">The following is an example of making the request in ASP.NET that uses the TokenHelper file:</span></span>
 

 



```
Response.Redirect(TokenHelper.GetAppContextTokenRequestUrl(sharePointUrl, Server.UrlEncode(Request.Url.ToString())));
```


### <a name="see-an-example-of-a-context-token"></a><span data-ttu-id="3d87e-342">Пример маркера контекста</span><span class="sxs-lookup"><span data-stu-id="3d87e-342">See an example of a context token</span></span>
<span data-ttu-id="3d87e-343"><a name="ExampleContextToken"> </a></span><span class="sxs-lookup"><span data-stu-id="3d87e-343"></span></span>

<span data-ttu-id="3d87e-p150">Ниже показан пример маркера контекста. Маленький объект JSON в начале содержит метаданные о маркере. Эти свойства такие же, как и в маркерах доступа (см. выше). Значение свойства **alg** — это имя алгоритма, используемого для создания подписи, которую служба контроля доступа добавляет к маркеру. Сведения о свойствах в данных маркера см. в табл. 3. Обратите внимание, что все значения должны быть написаны строчными буквами. (Пробел добавлен для удобства чтения.)</span><span class="sxs-lookup"><span data-stu-id="3d87e-p150">The following is an example of a context token. The small JavaScript Object Notation (JSON) object at the top contains metadata about the token. These properties are the same as in access tokens (see above). The value of the  **alg** property is the name of the algorithm that is used to generate the signature that ACS appends to the token. See table 3 for details about the properties in the payload of the token. Note that all the values must be lower-case. (White space has been added for readability.)</span></span>
 

 

```
{"typ":"JWT","alg":"HS256"}
.
{
 "aud":"a044e184-7de2-4d05-aacf-52118008c44e/fabrikam.com@040f2415-e6e3-4480-96ce-26ef73275f73",
 "iss":"00000001-0000-0000-c000-000000000000@040f2415-e6e3-4480-96ce-26ef73275f73",
 "nbf":"1335822895",
 "exp":"1335866095",
 "appctxsender":"00000003-0000-0ff1-ce00-000000000000@040f2415-e6e3-4480-96ce-26ef73275f73",
 "appctx":"{
            \"CacheKey\":\"KQAIUpDUD0sm5Tr83U+jZGYVuPPCPu8BGwoWiAACqNw=\",
            \"SecurityTokenServiceUri\":\"https://accounts.accesscontrol.windows-int-sn1-004.accesscontrol.aadint.windows-int.net/tokens/OAuth/2\"
           }",
 "refreshtoken":"IAAAAC1Lv5w0OrcFAmJx0xk6aaBdhgsw3VPnPzNEDAWypTHtCYytZ2/dBBUKj+HLK8YB3IUCUfDxYpAque
NHKtgs4rYJJ5AegQpNMOJR1yYK8ngivQx0oetj7aSPuGVb+k6at6G0Kx5LZ5vhxkAq8iUSwu8p4L2cvNMzDF1mDKfMivqxgrIZkr2nbf9as0SJFL6VG5hZnDE4HKq
xJnejSW3umatKM4fsfY1MClVCxrkXb2EQ8H/TmwaJc388YW063GEVUS/3BTSgSIRBKQUmXJuJ6BZY7WTm84LaGrx3mIjnUTM/jnqPoPG55JbCC9sS/MeGNPtzPPCDg
6Vv7dVhQ1Dq5Y3fQ65e9LpJ580jCgzYYvpIFT+Wx5V+17mjY2T8wug04K2ts87Znsr+GfFCorf7NS/lj5HjoxRAQ2tva/8dwguSLwxcUwi/Q9MbpR0NNtlpwVazqi9O
hJ4Df7gVhUDdJ0Dtc6aFCPbl5ZLDDRs42xK2", 
 "isbrowserhostedapp": "true"
}
```

<span data-ttu-id="3d87e-p151">Требования **aud**, **iss**, **nbf** и **exp** такие же, как и в маркере доступа, как описано выше. Требования **appctxsender**, **appctx**, **CacheKey**, **SecurityTokenServiceUri**, **refreshtoken** и **isbrowserhostedapp** описаны в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="3d87e-p151">The  **aud**, **iss**, **nbf**, and **exp** claims are exactly the same as in an access token as described above. The **appctxsender**, **appctx**, **CacheKey**, **SecurityTokenServiceUri**, **refreshtoken**, and **isbrowserhostedapp** claims are described in the following table.</span></span>
 

 

<span data-ttu-id="3d87e-353">**Табл. 3. Требования и сведения маркера контекста**</span><span class="sxs-lookup"><span data-stu-id="3d87e-353">**Table 3. Context token claims and information**</span></span>


|<span data-ttu-id="3d87e-354">** **Требование****</span><span class="sxs-lookup"><span data-stu-id="3d87e-354">** **Claim****</span></span>|<span data-ttu-id="3d87e-355">** **Описание****</span><span class="sxs-lookup"><span data-stu-id="3d87e-355">** **Description****</span></span>|<span data-ttu-id="3d87e-356">** **Соответствующее значение в примере маркера контекста****</span><span class="sxs-lookup"><span data-stu-id="3d87e-356">** **Corresponding value in sample context token****</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="3d87e-357">aud</span><span class="sxs-lookup"><span data-stu-id="3d87e-357">aud</span></span>||<span data-ttu-id="3d87e-358">a044e184-7de2-4d05-aacf-52118008c44e/fabrikam.com@040f2415-e6e3-4480-96ce-26ef73275f73</span><span class="sxs-lookup"><span data-stu-id="3d87e-358">a044e184-7de2-4d05-aacf-52118008c44e/fabrikam.com@040f2415-e6e3-4480-96ce-26ef73275f73</span></span>|
|<span data-ttu-id="3d87e-359">iss</span><span class="sxs-lookup"><span data-stu-id="3d87e-359">iss</span></span>||<span data-ttu-id="3d87e-360">00000001-0000-0000-c000-000000000000@040f2415-e6e3-4480-96ce-26ef73275f73</span><span class="sxs-lookup"><span data-stu-id="3d87e-360">00000001-0000-0000-c000-000000000000@040f2415-e6e3-4480-96ce-26ef73275f73</span></span>|
|<span data-ttu-id="3d87e-361">nbf</span><span class="sxs-lookup"><span data-stu-id="3d87e-361">nbf</span></span>||<span data-ttu-id="3d87e-362">1335822895</span><span class="sxs-lookup"><span data-stu-id="3d87e-362">1335822895</span></span>|
|<span data-ttu-id="3d87e-363">exp</span><span class="sxs-lookup"><span data-stu-id="3d87e-363">exp</span></span>||<span data-ttu-id="3d87e-364">1335866095</span><span class="sxs-lookup"><span data-stu-id="3d87e-364">1335866095</span></span>|
|<span data-ttu-id="3d87e-365">appctxsender</span><span class="sxs-lookup"><span data-stu-id="3d87e-365">appctxsender</span></span>|<span data-ttu-id="3d87e-p152">Сокращение для выражения "отправитель контекста приложения". Представляет приложение, отправившее маркер контекста в надстройку SharePoint. Оно имеет следующую форму: _GUID субъекта_@ _Область SharePoint_, где _GUID субъекта_ — это постоянный идентификатор субъекта приложения (SharePoint, Exchange 2013, Lync 2013 или рабочий процесс).</span><span class="sxs-lookup"><span data-stu-id="3d87e-p152">Short for "application context sender". It represents the application that sent the context token to the SharePoint Add-in.It has the form  _GUID of principal_@ _SharePoint realm_, where  _GUID of principal_ is the constant ID of the application principal; either SharePoint, Exchange 2013, Lync 2013, or Workflow.</span></span>|<span data-ttu-id="3d87e-368">00000003-0000-0ff1-ce00-000000000000@040f2415-e6e3-4480-96ce-26ef73275f73</span><span class="sxs-lookup"><span data-stu-id="3d87e-368">00000003-0000-0ff1-ce00-000000000000@040f2415-e6e3-4480-96ce-26ef73275f73</span></span>|
|<span data-ttu-id="3d87e-369">appctx</span><span class="sxs-lookup"><span data-stu-id="3d87e-369">appctx</span></span>|<span data-ttu-id="3d87e-p153">Сокращение для выражения "контекст надстройки". Это объект JSON, который содержит элементы **CacheKey** и **SecurityTokenServiceURI**. </span><span class="sxs-lookup"><span data-stu-id="3d87e-p153">Short for "add-in context". It is a JSON object that contains the  **CacheKey** and **SecurityTokenServiceURI**.</span></span>|<span data-ttu-id="3d87e-372">\"CacheKey\":\"KQAIUpDUD0sm5Tr83U+jZGYVuPPCPu8BGwoWiAACqNw=\", \"SecurityTokenServiceUri\":\"https://accounts.accesscontrol.windows-int-sn1-004.accesscontrol.aadint.windows-int.net/tokens/OAuth/2\"</span><span class="sxs-lookup"><span data-stu-id="3d87e-372">\"CacheKey\":\"KQAIUpDUD0sm5Tr83U+jZGYVuPPCPu8BGwoWiAACqNw=\", \"SecurityTokenServiceUri\":\"https://accounts.accesscontrol.windows-int-sn1-004.accesscontrol.aadint.windows-int.net/tokens/OAuth/2\"</span></span>|
|<span data-ttu-id="3d87e-373">CacheKey</span><span class="sxs-lookup"><span data-stu-id="3d87e-373">CacheKey</span></span>|<span data-ttu-id="3d87e-p154">Уникальное значение, которое можно использовать в качестве ключа в кэше со структурой "ключ-значение" для хранения и получения маркера контекста. Его также можно использовать как значение столбца ключа в строке базы данных.</span><span class="sxs-lookup"><span data-stu-id="3d87e-p154">A unique value that can be used as the key in any key/value structured cache to store and retrieve the context token. It could also be used as the value of a key column in a row of a database.</span></span>|<span data-ttu-id="3d87e-376">KQAIUpDUD0sm5Tr83U+jZGYVuPPCPu8BGwoWiAACqNw=</span><span class="sxs-lookup"><span data-stu-id="3d87e-376">KQAIUpDUD0sm5Tr83U+jZGYVuPPCPu8BGwoWiAACqNw=</span></span>|
|<span data-ttu-id="3d87e-377">SecurityTokenServiceURI</span><span class="sxs-lookup"><span data-stu-id="3d87e-377">SecurityTokenServiceURI</span></span>|<span data-ttu-id="3d87e-378">URI службы, издавшей маркер.</span><span class="sxs-lookup"><span data-stu-id="3d87e-378">The URI of the token issuing service.</span></span>|<span data-ttu-id="3d87e-379">https://accounts.accesscontrol.windows-int-sn1-004.accesscontrol.aadint.windows-int.net/tokens/OAuth/2</span><span class="sxs-lookup"><span data-stu-id="3d87e-379">https://accounts.accesscontrol.windows-int-sn1-004.accesscontrol.aadint.windows-int.net/tokens/OAuth/2</span></span>|
|<span data-ttu-id="3d87e-380">refreshtoken</span><span class="sxs-lookup"><span data-stu-id="3d87e-380">refreshtoken</span></span>|<span data-ttu-id="3d87e-381">Маркер обновления для надстройки.</span><span class="sxs-lookup"><span data-stu-id="3d87e-381">The refresh token for the add-in.</span></span>|<span data-ttu-id="3d87e-382">IAAAAC1Lv5w0OrcFAmJx0xk6???</span><span class="sxs-lookup"><span data-stu-id="3d87e-382">IAAAAC1Lv5w0OrcFAmJx0xk6???</span></span>|
|<span data-ttu-id="3d87e-383">isbrowserhostedapp</span><span class="sxs-lookup"><span data-stu-id="3d87e-383">isbrowserhostedapp</span></span>|<span data-ttu-id="3d87e-384">Поле типа **Boolean**, которое указывает, откуда поступил запрос в надстройку с маркером контекста: из браузера (true) или из удаленного приемника событий (false).</span><span class="sxs-lookup"><span data-stu-id="3d87e-384">A  **Boolean** field that specifies whether the request to the add-in that contains the context token is coming from a browser (true) or from a remote event receiver (false).</span></span>|<span data-ttu-id="3d87e-385">true</span><span class="sxs-lookup"><span data-stu-id="3d87e-385">true</span></span>|

### <a name="use-the-context-token-to-limit-access-to-only-sharepoint-users"></a><span data-ttu-id="3d87e-386">Использование маркера контекста для предоставления доступа только пользователям SharePoint</span><span class="sxs-lookup"><span data-stu-id="3d87e-386">Use the context token to limit access to only SharePoint users</span></span>
<span data-ttu-id="3d87e-387"><a name="UseContextTokenToLimitAccess"> </a></span><span class="sxs-lookup"><span data-stu-id="3d87e-387"></span></span>

<span data-ttu-id="3d87e-p155">Если вам нужно ограничить доступ к удаленному компоненту (например, к службе WCF) для пользователей SharePoint, код может просто проверить маркер контекста в HTTP-запросе. (Если вы используете управляемый код, достаточно вызова **TokenHelper.ReadAndValidateContextToken()**.) Код может проверить, начинается ли утверждение субъекта маркера с **00000003-0000-0ff1-ce00-000000000000**. Так вы убедитесь, что это SharePoint (а не Exchange 2013, Lync 2013 или рабочий процесс, например). Чтобы выполнить дополнительную проверку, для которой нужен обратный вызов SharePoint, например в случае ограничения доступа для пользователей с определенной ролью в SharePoint, вы можете кэшировать сведения о выполнении такой проверки для определенного пользователя. Для этого используется ключ **CacheKey** маркера контекста. Такой способ позволяет выполнять проверку только один раз.</span><span class="sxs-lookup"><span data-stu-id="3d87e-p155">If you want to limit access to your remote component, such as a WCF service, to SharePoint users, your code can simply validate the context token in the HTTP Request. (If you are using managed code, you can just call  **TokenHelper.ReadAndValidateContextToken()**). Your code can verify that the actor claim of the token starts with  **00000003-0000-0ff1-ce00-000000000000**, if you want to make sure that it is SharePoint (and not, for example, Exchange 2013, Lync 2013, or Workflow). If you want to do additional validation that requires a call back to SharePoint, such as limiting access to users with a certain role in SharePoint, you can cache the fact that you have done this validation for a particular user (by using the context token's **CacheKey**) so that you have to do this only once.</span></span>
 

 

## <a name="understand-the-handling-and-caching-of-refresh-tokens"></a><span data-ttu-id="3d87e-392">Общие сведения об обработке и кэшировании маркеров обновления</span><span class="sxs-lookup"><span data-stu-id="3d87e-392">Understand the handling and caching of refresh tokens</span></span>
<span data-ttu-id="3d87e-393"><a name="RefreshTokens"> </a></span><span class="sxs-lookup"><span data-stu-id="3d87e-393"></span></span>

 <span data-ttu-id="3d87e-p156">**Маркер обновления включен в маркер контекста, который служба SharePoint публикует в веб-приложении при его запуске.** Маркер обновления зашифрован, и Надстройка SharePoint не может его расшифровать. **Код использует его** и другие данные **для получения нового маркера доступа после истечения срока действия текущего**. С его помощью также можно получить *первый*  маркер доступа в [потоке маркера контекста](creating-sharepoint-add-ins-that-use-low-trust-authorization.md#Flows). (Во время написания этой статьи продолжительность существования маркера обновления, выпущенного службой контроля доступа для SharePoint, составляла 6 месяцев, но это могло измениться.)</span><span class="sxs-lookup"><span data-stu-id="3d87e-p156">**A refresh token is included in the context token that SharePoint posts to your web application when it is launched.** The refresh token is an encrypted token that your SharePoint Add-in cannot unencrypt. **Your code uses it**, along with other information, **to get a new access token when the current access token expires**. It is also used to get the *first*  access token in the [Context Token flow](creating-sharepoint-add-ins-that-use-low-trust-authorization.md#Flows). (When this article was written, ACS-issued refresh tokens for SharePoint had a life span of 6 months, but that could change.)</span></span>
 

 
<span data-ttu-id="3d87e-399">Так как маркер доступа действует только несколько часов (сейчас 12) и пользователь получает новый при каждом запуске Надстройка SharePoint в SharePoint, маркер обновления нужен только в таких сценариях:</span><span class="sxs-lookup"><span data-stu-id="3d87e-399">Since an access token lasts hours (currently 12) and an end user gets a new one each time he launches your SharePoint Add-in from SharePoint, you only need the refresh token in one of these scenarios:</span></span>
 

 

- <span data-ttu-id="3d87e-400">Пользователи открыли продолжительные сеансы надстройки, в которых она выполняет вызовы SharePoint в течение нескольких часов (более 12) после запуска.</span><span class="sxs-lookup"><span data-stu-id="3d87e-400">Users have long running sessions with your add-in in which the add-in makes calls to SharePoint many hours (currently more than 12) after it is launched.</span></span>
    
 
- <span data-ttu-id="3d87e-401">Конструкция надстройки дает пользователям возможность планировать доступ надстройки к SharePoint после окончания сеанса.</span><span class="sxs-lookup"><span data-stu-id="3d87e-401">The add-in's design enables users to schedule the add-in to access SharePoint sometime after the session ends.</span></span>
    
 
<span data-ttu-id="3d87e-p157">В обоих **сценариях надстройка должна кэшировать маркер обновления**, а во втором также нужен кэш на стороне сервера, устойчивый на протяжении всех сеансов. Варианты кэширования такие же, как и для [маркера доступа](#CacheAccessToken), а в потоке маркера контекста можно использовать [ключ кэша в маркере контекста](#CacheKey). В потоке маркера контекста вы обычно кэшируете маркер контекста. Он содержит маркер обновления и другие данные, необходимые для получения нового маркера доступа. В [потоке кода авторизации](creating-sharepoint-add-ins-that-use-low-trust-authorization.md#Flows) маркера контекста нет, потому вы кэшируете сам маркер обновления.</span><span class="sxs-lookup"><span data-stu-id="3d87e-p157">Both  **scenarios require your add-in to cache the refresh token**, and second scenario requires a server-side cache that is durable across sessions. Your caching options are the same as those for the [access token](#CacheAccessToken) and, in the Context Token flow, you can use [the cache key in the context token](#CacheKey). (In the Context Token flow, you usually just cache the context token. It contains the refresh token and other information you need to get a new access token. In the  [Authorization Code flow](creating-sharepoint-add-ins-that-use-low-trust-authorization.md#Flows), there is no context token, so you cache the refresh token itself.)</span></span>
 

 
<span data-ttu-id="3d87e-p158">Если вы кэшируете маркер обновления в хранилище, которое существует во всех сеансах надстройки, открытых определенным пользователем, замените его самым новым маркером обновления. Пользователь получает новый маркер обновления при каждом запуске надстройки как в случае потока с облачным размещением, так и потока кода авторизации.</span><span class="sxs-lookup"><span data-stu-id="3d87e-p158">If you are caching the refresh token in a storage that persists across a specific user's sessions with your add-in, be sure to replace it with the newest refresh token. In both the Cloud-hosted and Authorization Code flows, the user gets a new refresh token each time he or she launches the add-in.</span></span>
 

 
<span data-ttu-id="3d87e-p159">Если истек срок действия маркера обновления, запрос на получение нового маркера доступа в службу контроля доступа возвращает ошибку **401 Unauthorized**. В ответ на нее надстройка должна получить новый маркер обновления, а с его помощью новый маркер доступа. (Так как маркер обновления зашифрован, код не может проверить срок его действия перед использованием.) В потоке маркера контекста надстройка получает новый маркер обновления, [получив новый маркер контекста](#GetNewContextToken). Чтобы получить маркер обновления в потоке кода авторизации, надстройка перезапускает поток. В частности, в ответ на ошибку код должен перенаправить пользователя на страницу OAuthAuthorize.aspx в SharePoint (см. раздел [Общие сведения о потоке OAuth для надстроек, запрашивающих разрешение в динамическом режиме](authorization-code-oauth-flow-for-sharepoint-add-ins.md#Flow)).</span><span class="sxs-lookup"><span data-stu-id="3d87e-p159">If the refresh token is expired, a request to ACS for a new access token will result in a  **401 Unauthorized** error. Your add-in should respond to this error by getting a new refresh token and using it to get a new access token. (Since the refresh token is encrypted, your code cannot check its expiration before using it.) In the Context Token flow, your add-in gets a new refresh token by [getting a new context token](#GetNewContextToken). In the Authorization Code flow, your add-in gets a new refresh token by restarting the flow. Specifically, your code should respond to the error by redirecting the user to the SharePoint OAuthAuthorize.aspx page as explained in  [Understand the OAuth flow for add-ins that request permissions on the fly](authorization-code-oauth-flow-for-sharepoint-add-ins.md#Flow).</span></span>
 

 

## <a name="understanding-the-handling-authorization-codes"></a><span data-ttu-id="3d87e-414">Общие сведения об обработке кодов авторизации</span><span class="sxs-lookup"><span data-stu-id="3d87e-414">Understanding the handling authorization codes</span></span>
<span data-ttu-id="3d87e-415"><a name="Authcodes"> </a></span><span class="sxs-lookup"><span data-stu-id="3d87e-415"></span></span>

 <span data-ttu-id="3d87e-p160">**Процесс авторизации в потоке кода авторизации начинается с того, что служба контроля доступа при получении запроса из службы SharePoint выпускает код авторизации. После этого SharePoint передает его удаленному приложению** в качестве параметра запроса. Код авторизации уникален для каждой пары пользователя и удаленного приложения. (Во время написания этой статьи код авторизации, выпущенный службой контроля доступа для SharePoint, действовал в течение 5 минут, но это могло измениться.) Код **приложения должен получить код авторизации из параметра запроса и с его помощью запросить маркер доступа из службы контроля доступа**. Если вы используете управляемый код, пример кода для создания маркера находится в файле TokenHelper (с расширением CS или VB). Пример кода для чтения параметра запроса можно найти в разделе [Пример кода программной части страницы, обращающейся к SharePoint](authorization-code-oauth-flow-for-sharepoint-add-ins.md#Default). Служба контроля доступа делает код авторизации недействительным сразу после выпуска маркера доступа, потому его можно использовать только один раз. Кэшировать его бессмысленно.</span><span class="sxs-lookup"><span data-stu-id="3d87e-p160">**In the Authorization Code flow, the authorization process begins with an authorization code that ACS issues, at the request of SharePoint, and which SharePoint then passes to the remote application** as a query parameter. The authorization code is unique to each pair of user and remote application. (When this article was written, ACS-issued authorization codes for SharePoint had a life span of 5 minutes, but that could change.) The logic in **your application must get the authorization code from the query parameter and use it in a request to ACS for an access token**. If you are using managed code, sample code for creating the token is in the TokenHelper.cs (and .vb) file. Sample code for reading the query parameter is in [Get sample code behind for a page that accesses SharePoint](authorization-code-oauth-flow-for-sharepoint-add-ins.md#Default). ACS invalidates the authorization code immediately after issuing the access token, so it can only be used once and there is no point in caching it.</span></span>
 

 

## <a name="work-with-jwt-time-values"></a><span data-ttu-id="3d87e-422">Работа со значениями времени JWT</span><span class="sxs-lookup"><span data-stu-id="3d87e-422">Work with JWT time values</span></span>
<span data-ttu-id="3d87e-423"><a name="JWTtimes"> </a></span><span class="sxs-lookup"><span data-stu-id="3d87e-423"></span></span>

<span data-ttu-id="3d87e-p161">Формат требований **nbf** и **exp** определен в [спецификации JWT](http://self-issued.info/docs/draft-goland-json-web-token-00l). Это количество секунд, отсчет которых ведется с 1 января 1970 г. На языке C# эти значения можно преобразовать с помощью приведенного ниже кода, где _jWTTimeStamp_ — это значение из маркера, например 1335822895.</span><span class="sxs-lookup"><span data-stu-id="3d87e-p161">The  **nbf** and **exp** claims are in the format specified by the [JWT specification](http://self-issued.info/docs/draft-goland-json-web-token-00l). They are written as the number of seconds since Jan 1, 1970. In C#, you can translate these values with the following code, where  _jWTTimeStamp_ is the value from the token, such as 1335822895.</span></span>
 

 

```C#
DateTime exp = new DateTime(1970,1,1).AddSeconds(jWTTimeStamp);

```


## <a name="troubleshooting-token-handling"></a><span data-ttu-id="3d87e-427">Устранение неполадок при обработке маркеров</span><span class="sxs-lookup"><span data-stu-id="3d87e-427">Troubleshooting token handling</span></span>
<span data-ttu-id="3d87e-428"><a name="Troubleshooting"> </a></span><span class="sxs-lookup"><span data-stu-id="3d87e-428"></span></span>

<span data-ttu-id="3d87e-p162">HTTP-запросы, которые удаленный компонент надстройки отправляет в SharePoint, можно перехватывать с помощью бесплатного  [средства Fiddler](http://www.telerik.com/fiddler). Для него также есть  [бесплатное расширение](https://github.com/andrewconnell/SPOAuthFiddlerExt), которое автоматически декодирует маркеры в запросах.</span><span class="sxs-lookup"><span data-stu-id="3d87e-p162">The free  [Fiddler tool](http://www.telerik.com/fiddler) can be used to capture the HTTP Requests sent by the remote component of your add-in to SharePoint. There is a [free extension to the tool](https://github.com/andrewconnell/SPOAuthFiddlerExt) that automatically decodes the tokens in the requests.</span></span>
 

 

## <a name="additional-resources"></a><span data-ttu-id="3d87e-431">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="3d87e-431">Additional resources</span></span>
<span data-ttu-id="3d87e-432"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="3d87e-432"></span></span>


-  [<span data-ttu-id="3d87e-433">Создание надстроек SharePoint, использующих авторизацию с низким уровнем доверия</span><span class="sxs-lookup"><span data-stu-id="3d87e-433">Creating SharePoint Add-ins that use low-trust authorization</span></span>](creating-sharepoint-add-ins-that-use-low-trust-authorization.md)
    
 
- <span data-ttu-id="3d87e-434">Примеры кода, в которых используются управляемый код и TokenHelper, см. в статьях [SharePoint: удаленная надстройка Hello World, использующая CSOM](http://code.msdn.microsoft.com/SharePoint-Hello-0fd15fbf) и [Пакет примеров надстроек SharePoint](http://code.msdn.microsoft.com/office/Apps-for-SharePoint-sample-64c80184).</span><span class="sxs-lookup"><span data-stu-id="3d87e-434">For code samples that use managed code and TokenHelper, see  [SharePoint: Hello World remote add-in using CSOM](http://code.msdn.microsoft.com/SharePoint-Hello-0fd15fbf) and [SharePoint Add-ins sample pack](http://code.msdn.microsoft.com/office/Apps-for-SharePoint-sample-64c80184)</span></span>
    
 
- <span data-ttu-id="3d87e-435">Пример кода, в котором используются вызовы REST из надстройки PHP: [SharePoint: выполнение операций над библиотекой документов SharePoint с сайта PHP](https://code.msdn.microsoft.com/SharePoint-Perform-8a78b8ef)</span><span class="sxs-lookup"><span data-stu-id="3d87e-435">For a code sample that uses REST calls from a PHP add-in:  [SharePoint: Perform operations on SharePoint Document Library from PHP site](https://code.msdn.microsoft.com/SharePoint-Perform-8a78b8ef)</span></span>
    
 

