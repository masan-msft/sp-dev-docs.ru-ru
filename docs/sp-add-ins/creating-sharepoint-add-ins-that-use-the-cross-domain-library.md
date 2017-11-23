# <a name="creating-sharepoint-add-ins-that-use-the-cross-domain-library"></a><span data-ttu-id="e956a-101">Создание надстроек SharePoint, использующих междоменную библиотеку</span><span class="sxs-lookup"><span data-stu-id="e956a-101">Creating SharePoint Add-ins that use the cross-domain library</span></span>
<span data-ttu-id="e956a-102">Сведения о междоменной библиотеке JavaScript в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="e956a-102">Learn about the SharePoint cross-domain JavaScript library.</span></span>
 

 <span data-ttu-id="e956a-p101">**Примечание.** Название "приложения для SharePoint" меняется на "надстройки SharePoint". Пока изменения не будут внесены полностью, в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio по-прежнему может встречаться термин "приложение". Дополнительные сведения см. в разделе [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="e956a-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

<span data-ttu-id="e956a-p102">В некоторых сценариях надстройка SharePoint не может использовать ни систему авторизации с низким уровнем доверия, ни систему авторизации с высоким уровнем доверия. В некоторых случаях такие системы лучше не использовать как единственное средство авторизации для доступа надстройки к ресурсам SharePoint. Примеры представлены ниже.</span><span class="sxs-lookup"><span data-stu-id="e956a-p102">Learn about the SharePoint cross-domain JavaScript library. There are some scenarios in which neither the low-trust nor the high-trust authorization systems can be used by a SharePoint Add-in, or they are not a good choice as the only means for the add-in to gain authorization to SharePoint resources. Examples:</span></span>
 

- <span data-ttu-id="e956a-108">Удаленные компоненты надстройки SharePoint находятся не в локальной среде, но корпоративный брандмауэр блокирует межсерверное взаимодействие между SharePoint и ACS, тем самым не позволяя использовать систему с низким уровнем доверия.</span><span class="sxs-lookup"><span data-stu-id="e956a-108">The remote components of the SharePoint Add-in are not on-premise, but a corporate firewall blocks server-to-server communication between SharePoint and ACS, thereby preventing the use of the low-trust system.</span></span>
    
 
- <span data-ttu-id="e956a-109">Надстройка SharePoint это одностраничное веб-приложение, использующее клиентский код JavaScript для выполнения операций с данными в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="e956a-109">The SharePoint Add-in is designed as a single-page web application that relies on client-side JavaScript for data operations with SharePoint.</span></span>
    
 
- <span data-ttu-id="e956a-p103">Надстройка SharePoint в основном использует межсерверные вызовы для доступа к данным SharePoint (и авторизуется системами с низким или высоким уровнем доверия), но его необходимо дополнить вызовами JavaScript. Например, страница с интенсивным использованием графики может применять JavaScript, чтобы вносить небольшие изменения в отображаемые данные без перегрузки всей страницы.</span><span class="sxs-lookup"><span data-stu-id="e956a-p103">The SharePoint Add-in relies mainly on server-to-server calls to access SharePoint data (and is authorized by either the low-trust or high-trust systems), but it needs to be supplemented with some JavaScript calls. For example, a graphics-heavy page can use JavaScript to make minor updates to displayed data without having to reload the entire page.</span></span>
    
 
<span data-ttu-id="e956a-p104">Однако в  [целях безопасности](http://msdn.microsoft.com/ru-ru/library%28d=robot%29/cc709423(d=robot,l=en-us,v=vs.85).aspx) браузеры не разрешают коду JavaScript, размещенному в одном домене, получать доступ к ресурсам в другом домене. Поэтому необходимо использовать специальную методику, чтобы предоставить удаленному коду JavaScript доступ к ресурсам SharePoint. Междоменная библиотека JavaScriptSharePoint упрощает использование этого метода в веб-приложениях.</span><span class="sxs-lookup"><span data-stu-id="e956a-p104">However,  [for security](http://msdn.microsoft.com/ru-ru/library%28d=robot%29/cc709423(d=robot,l=en-us,v=vs.85).aspx), browsers do not allow JavaScript that is hosted on one domain to access resources on another domain, so a special technique is required to allow the remote JavaScript to access SharePoint resources. The SharePoint cross-domain JavaScript library makes it easy for your remote web application to use the technique.</span></span>
 

 <span data-ttu-id="e956a-p105">**Примечание.** Междоменная библиотека также используется для предоставления доступа к данным в обратном направлении (т. е. чтобы разрешить коду JavaScript на странице SharePoint получать доступ к данным на удаленном домене). Дополнительные сведения см. в разделе [Доступ к удаленным данным со страницы SharePoint](#ReverseDirection).</span><span class="sxs-lookup"><span data-stu-id="e956a-p105">**Note** The cross-domain library is also used to allow access to data in the reverse direction; that is, to allow JavaScript on a SharePoint page to access data in a remote domain. See  [Access remote data from a SharePoint page](#ReverseDirection) for more information.</span></span>
 


## <a name="understand-the-architecture-of-the-cross-domain-library"></a><span data-ttu-id="e956a-116">Общие сведения об архитектуре междоменной библиотеки</span><span class="sxs-lookup"><span data-stu-id="e956a-116">Understand the architecture of the cross-domain library</span></span>

<span data-ttu-id="e956a-p106">Междоменная библиотека SharePoint содержится в файле SP.RequestExecutor.js, который расположен в виртуальной папке /_layouts/15/ каждого веб-сайта SharePoint. Скрипты в этом файле используют известный способ обхода ограничения междоменных скриптов браузера: iFrame может взаимодействовать с родительской страницей с помощью функции  `window.postMessage()`, даже если страница в iFrame находится в другом домене. Поэтому запросы данных и ответы передаются между домена с помощью функции  `postMessage()`.</span><span class="sxs-lookup"><span data-stu-id="e956a-p106">The SharePoint cross-domain library is contained in the file SP.RequestExecutor.js which is located in the /_layouts/15/ virtual folder of every SharePoint website. The scripts in this file encapsulate a secure well-known technique for overcoming the browser's restriction on cross-domain scripting: An iFrame can communicate with its parent page by means of the  `window.postMessage()` function, even if the page in the iFrame is in a different domain. So data requests and responses are passed over the domain boundary by using calls to `postMessage()`.</span></span>
 

 

 <span data-ttu-id="e956a-120">**Внимание!** Функция `postMessage()` работает только в браузерах, поддерживающих HTML 5, поэтому надстройки SharePoint, использующие междоменную библиотеку, не будут работать в старых браузерах.</span><span class="sxs-lookup"><span data-stu-id="e956a-120">**Caution** The  `postMessage()` function works only on browsers that support HTML 5, so SharePoint Add-ins that use the cross-domain library will not work on older browsers.</span></span>
 

<span data-ttu-id="e956a-p107">Для SharePoint междоменная библиотека загружается на странице удаленного веб-приложения, где создается скрытый iFrame, в котором размещается специальная прокси-страница из домена SharePoint. Прокси-страница уже существует на каждом веб-сайте SharePoint. С помощью библиотеки создается объект Нотация объектов JavaScript (JSON), содержащий все сведения, необходимые для CRUD-вызова к API-интерфейсам REST SharePoint. Объект JSON передается прокси-странице с помощью функции  `postMessage()`. На прокси-странице, где также загружается библиотека, объект JSON анализируется и преобразуется в REST-вызов SharePoint. Так как прокси-страница находится в домене SharePoint, браузер разрешает вызов.</span><span class="sxs-lookup"><span data-stu-id="e956a-p107">For SharePoint, the cross-domain library is loaded on a page of the remote web application where it creates a hidden iFrame that hosts a special proxy page from the SharePoint domain. The proxy page already exists on every SharePoint website. The library is used to create a JavaScript Object Notation (JSON) object which contains all the information needed to make a CRUD call to the REST APIs of SharePoint. The JSON object is passed to the proxy page by using  `postMessage()`. On the proxy page, where the library is also loaded, the JSON object is parsed and reconstructed as a REST call to SharePoint. Since the proxy page is in the SharePoint domain, the browser allows the call.</span></span>
 

 
<span data-ttu-id="e956a-p108">Конечно, у удаленных компонентов надстройки SharePoint по-прежнему должен быть авторизованный доступ к ресурсам SharePoint. Для этого существует два способа:</span><span class="sxs-lookup"><span data-stu-id="e956a-p108">Of course, the remote components of the SharePoint Add-in still have to have authorized access to the SharePoint resources. There are two ways to do this:</span></span>
 

 

- <span data-ttu-id="e956a-p109">Задайте для надстройки тип субъекта **RemoteWebApplication** (значение по умолчанию для надстроек с размещением у поставщика) в манифесте надстройки. При регистрации надстройки в службе ACS указывается домен удаленного веб-приложения. SharePoint доверяет доменам, зарегистрированным в ACS, хотя в этом сценарии не используются потоки передачи маркеров, применяемые в серверной системе с низким уровнем доверия. Подробные сведения о регистрации надстроек см. в статье [Регистрация надстроек SharePoint 2013](register-sharepoint-add-ins-2013).</span><span class="sxs-lookup"><span data-stu-id="e956a-p109">Set the add-in principal type to **RemoteWebApplication** (the default for provider-hosted apps) in the add-in manifest. When the add-in is registered with ACS, the registration includes the domain of the remote web application. SharePoint trusts domains that are registered with ACS, even though it is not, in this scenario, using any of the token passing flows that are part of the server-side low-trust system. For detailed information about registering add-ins, see [Register SharePoint Add-ins 2013](register-sharepoint-add-ins-2013).</span></span> 
    
 
- <span data-ttu-id="e956a-p110">В надстройке, размещенной в SharePoint, можно оставить тип субъекта надстройки по умолчанию, т. е. **Internal**. Задайте в атрибуте **AllowedRemoteHostUrl** элемента **Internal** URL-адрес удаленного приложения, как показано в приведенном ниже примере.</span><span class="sxs-lookup"><span data-stu-id="e956a-p110">In a SharePoint-hosted add-in, you can leave the add-in principal type set to its default, which is **Internal**. Then set the **AllowedRemoteHostUrl** attribute of the **Internal** element to the URL of the remote web application, as in the following example.</span></span>
    
```
  <AppPrincipal>
  <Internal AllowedRemoteHostUrl="https://example.com/Home.html" />
</AppPrincipal>
```


 <span data-ttu-id="e956a-p111">**Примечание.** Если вы используете второй вариант (субъект надстройки **Internal**), то для доступа к SharePoint можно использовать только JavaScript и междоменную библиотеку. Клиентская объектная модель SharePoint заблокирована для надстроек SharePoint с атрибутом **Internal**, поэтому невозможно создать двойную систему авторизации, которая допускает применение как междоменной библиотеки, так и системы с низким или высоким уровнем доверия.</span><span class="sxs-lookup"><span data-stu-id="e956a-p111">**Note** If you use the second option (an **Internal** add-in principal), then you can use only JavaScript and the cross-domain library to access SharePoint. The SharePoint client object model is blocked for **Internal**SharePoint Add-ins, so you cannot have a dual authorization system that uses both the cross-domain library and either the low-trust or high-trust systems.</span></span>
 

<span data-ttu-id="e956a-137">Сведения о том, как использовать библиотеку, см. в статье [Обращение к данным SharePoint из надстроек с помощью междоменной библиотеки](access-sharepoint-2013-data-from-add-ins-using-the-cross-domain-library).</span><span class="sxs-lookup"><span data-stu-id="e956a-137">For details on how to use the library, see  [Access SharePoint data from add-ins using the cross-domain library](access-sharepoint-2013-data-from-add-ins-using-the-cross-domain-library).</span></span>
 

 

## <a name="access-remote-data-from-a-sharepoint-page"></a><span data-ttu-id="e956a-138">Доступ к удаленным данным со страницы SharePoint</span><span class="sxs-lookup"><span data-stu-id="e956a-138">Access remote data from a SharePoint page</span></span>
<span data-ttu-id="e956a-139"><a name="ReverseDirection"> </a></span><span class="sxs-lookup"><span data-stu-id="e956a-139"></span></span>

<span data-ttu-id="e956a-p112">Междоменную библиотеку SharePoint также можно использовать в обратном направлении, т. е. JavaScript на странице SharePoint может с помощью библиотеки получить данные из удаленных компонентов надстройки. Для этого междоменная архитектура меняется на обратную: вы создаете прокси-страницу в удаленном веб-приложении. Библиотека вызывается со страницы SharePoint, где она создает iFrame для размещения прокси-страницы. Дополнительные сведения о таком применении библиотеки см. в статье  [Создание пользовательской прокси-страницы для междоменной библиотеки в SharePoint](create-a-custom-proxy-page-for-the-cross-domain-library-in-sharepoint-2013).</span><span class="sxs-lookup"><span data-stu-id="e956a-p112">The SharePoint cross-domain library can also be used in the reverse direction; that is, JavaScript on a SharePoint page can use the library to get data from the remote components of the add-in. To do this, you reverse the cross-domain architecture: you create a proxy page in the remote web application. The library is called from a SharePoint page where it creates an iFrame to host the proxy page. For details on how to use the library in this way, see  [Create a custom proxy page for the cross-domain library in SharePoint](create-a-custom-proxy-page-for-the-cross-domain-library-in-sharepoint-2013).</span></span>
 

 

## <a name="in-this-section"></a><span data-ttu-id="e956a-144">В этом разделе:</span><span class="sxs-lookup"><span data-stu-id="e956a-144">In this section</span></span>
<span data-ttu-id="e956a-145"><a name="ReverseDirection"> </a></span><span class="sxs-lookup"><span data-stu-id="e956a-145"></span></span>


-  [<span data-ttu-id="e956a-146">Обращение к данным SharePoint из надстроек с помощью междоменной библиотеки</span><span class="sxs-lookup"><span data-stu-id="e956a-146">Access SharePoint data from add-ins using the cross-domain library</span></span>](access-sharepoint-2013-data-from-add-ins-using-the-cross-domain-library)
    
 
-  [<span data-ttu-id="e956a-147">Работа с междоменной библиотекой в различных зонах безопасности Internet Explorer в надстройках SharePoint</span><span class="sxs-lookup"><span data-stu-id="e956a-147">Work with the cross-domain library across different Internet Explorer security zones in SharePoint Add-ins</span></span>](work-with-the-cross-domain-library-across-different-internet-explorer-security-zones-in-sharepoint-add-ins)
    
 

## <a name="additional-resources"></a><span data-ttu-id="e956a-148">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="e956a-148">Additional resources</span></span>
<span data-ttu-id="e956a-149"><a name="ReverseDirection"> </a></span><span class="sxs-lookup"><span data-stu-id="e956a-149"></span></span>


-  [<span data-ttu-id="e956a-150">Исправление междоменных проблем в надстройках SharePoint</span><span class="sxs-lookup"><span data-stu-id="e956a-150">Solving cross-domain problems in SharePoint Add-ins</span></span>](http://blogs.msdn.com/b/officeapps/archive/2012/11/29/solving-cross-domain-problems-in-apps-for-sharepoint.aspx)
    
 

