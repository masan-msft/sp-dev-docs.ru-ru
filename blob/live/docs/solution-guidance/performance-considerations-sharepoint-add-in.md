---
title: "Рекомендации по производительности в объектная модель SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 1a7313fd7b8c783268b54ef1ecb06f2e06fb8b44
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
<a name="performance-considerations-in-the-sharepoint-add-in-model"></a><span data-ttu-id="8e4c4-102">Рекомендации по производительности в объектная модель SharePoint</span><span class="sxs-lookup"><span data-stu-id="8e4c4-102">Performance considerations in the SharePoint add-in model</span></span>
=========================================================

<a name="summary"></a><span data-ttu-id="8e4c4-103">Summary</span><span class="sxs-lookup"><span data-stu-id="8e4c4-103">Summary</span></span>
-------

<span data-ttu-id="8e4c4-104">Подходы потребоваться убедитесь, что оптимальной производительности с помощью SharePoint отличается в новой модели надстройки SharePoint не был с кодом полного доверия.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-104">The approaches you take to ensure optimal performance with SharePoint is different in the new SharePoint Add-in model than it was with Full Trust Code.</span></span> <span data-ttu-id="8e4c4-105">В типичных полного доверия кода (FTC) / сценарий решения фермы большинство операций кода выполнялись в объектной модели SharePoint серверного кода.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-105">In a typical Full Trust Code (FTC) / Farm Solution scenario most code operations took place in the SharePoint Server-side Object Model code.</span></span>

<span data-ttu-id="8e4c4-106">В SharePoint надстройки модели сценарии объектную модель SharePoint на стороне клиента (CSOM) и/или интерфейса API REST SharePoint используются для выполнения кода.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-106">In an SharePoint Add-in model scenario, the SharePoint Client-side Object Model (CSOM) and/or the SharePoint REST API are used to execute code.</span></span>

<span data-ttu-id="8e4c4-107">Основное различие между двумя моделями — серверный код и код на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-107">The major difference between the two models is server-side code versus client-side code.</span></span> <span data-ttu-id="8e4c4-108">В модели надстройки SharePoint так как код выполняется с помощью клиентов, возникает дополнительные сетевого трафика.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-108">In the SharePoint Add-in model, because code is executed via clients, additional network traffic occurs.</span></span>  <span data-ttu-id="8e4c4-109">Минимизации количества вызов API циклами на сервере SharePoint будет повышения производительности из вашего SharePoint надстройки и сократить объем ресурсов, затрачиваемых сайта SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-109">Minimizing the number of API call round trips to the SharePoint server will increase the performance of your SharePoint Add-ins and reduce the amount of resources consumed by your SharePoint site.</span></span>

<span data-ttu-id="8e4c4-110">Кроме того в модели надстройки SharePoint, так как код выполняется с помощью клиентов может быть задержки перед получен ответ.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-110">Additionally, in the SharePoint Add-in model, because code is executed via clients there could be long delays before a response is received.</span></span> <span data-ttu-id="8e4c4-111">Кэширование данных для длительной операции (например, API профилей пользователей) могут сократить время, необходимое для возврата информации или получения подтверждения процесс завершен.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-111">Caching data for long running operations (like the User Profile APIs) can reduce the amount of time it takes to return information or receive confirmation a process is complete.</span></span>

<a name="high-level-guidelines"></a><span data-ttu-id="8e4c4-112">Рекомендации по высокого уровня</span><span class="sxs-lookup"><span data-stu-id="8e4c4-112">High-level guidelines</span></span>
---------------------

<span data-ttu-id="8e4c4-113">Как правило эскиз мы предлагаем для обеспечения высокого уровня следующие рекомендации для обеспечения оптимальной производительности с помощью SharePoint в новой модели надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-113">As a rule of a thumb, we would like to provide the following high-level guidelines to ensure optimal performance with SharePoint in the new SharePoint Add-in model.</span></span>

- <span data-ttu-id="8e4c4-114">Минимизация вызовов API со стороны клиента к серверу SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-114">Minimize client-side API calls to the SharePoint server.</span></span>
- <span data-ttu-id="8e4c4-115">Используйте методы кэширования на сервере и со стороны клиента для хранения сведений.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-115">Use server-side and client-side caching techniques to store information.</span></span>
- <span data-ttu-id="8e4c4-116">Не рекомендуется хранить clientIDs clientSecrets, имена пользователей, пароли, маркеры и другие конфиденциальные данные в кэш.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-116">It is not recommended that you store clientIDs, clientSecrets, usernames, passwords, tokens, or other sensitive security information in caches.</span></span>

<a name="options-to-ensure-optimal-performance-with-sharepoint"></a><span data-ttu-id="8e4c4-117">Параметры, чтобы гарантировать их оптимальную работу с SharePoint</span><span class="sxs-lookup"><span data-stu-id="8e4c4-117">Options to ensure optimal performance with SharePoint</span></span>
-----------------------------------------------------
<span data-ttu-id="8e4c4-118">У вас есть две возможности для обеспечения оптимальной производительности с помощью SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-118">You have a couple of options to ensure optimal performance with SharePoint.</span></span>

- <span data-ttu-id="8e4c4-119">Используйте кэширование на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="8e4c4-119">Use client-side caching</span></span> 
- <span data-ttu-id="8e4c4-120">Используйте кэширование на сервере</span><span class="sxs-lookup"><span data-stu-id="8e4c4-120">Use server-side caching</span></span> 

<a name="use-client-side-caching"></a><span data-ttu-id="8e4c4-121">Используйте кэширование на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="8e4c4-121">Use client-side caching</span></span> 
-----------------------
<span data-ttu-id="8e4c4-122">В этом шаблоне методы кэширования со стороны клиента, такие как HTML5 LocalStorage и файлы cookie используются для кэширования данных.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-122">In this pattern, client-side caching techniques such as HTML5 LocalStorage and cookies are used to cache data.</span></span> <span data-ttu-id="8e4c4-123">Данные, хранящиеся в этих расположениях используется для определения, если это необходимо выполнять вызовы API SharePoint server.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-123">Information stored in these locations is used to determine if it is necessary to make API calls to a SharePoint server.</span></span>

- <span data-ttu-id="8e4c4-124">Этот шаблон хранит данные, возвращаемые из вызовов SharePoint API в кэш со стороны клиента.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-124">This pattern stores data returned from SharePoint API calls in client-side caches.</span></span>
- <span data-ttu-id="8e4c4-125">Этот шаблон используется код на стороне клиента (JavaScript) для оценки данных, хранящихся в кэш со стороны клиента.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-125">This pattern uses client-side code (JavaScript) to evaluate data stored in client-side caches.</span></span>
- <span data-ttu-id="8e4c4-126">Файлы cookie не более хранения 4095 объем данных в байтах.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-126">Cookies are limited to storing 4095 bytes of data.</span></span>
    + <span data-ttu-id="8e4c4-127">Файлы cookie имеют механизм истечение срока действия встроенных данных.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-127">Cookies have a built-in data expiration mechanism.</span></span>
- <span data-ttu-id="8e4c4-128">HTML5 LocalStorage не более 5 МБ данных.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-128">HTML5 LocalStorage is limited to 5MB of data.</span></span>
    - <span data-ttu-id="8e4c4-129">HTML5 LocalStorage не имеет механизм истечение срока действия встроенных данных.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-129">HTML5 LocalStorage does not have a built-in data expiration mechanism.</span></span> <span data-ttu-id="8e4c4-130">Тем не менее такой механизм истечение срока действия может быть быстро и легко реализованы в JavaScript.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-130">However, such an expiration mechanism may be quickly and easily implemented in JavaScript.</span></span>
    
        <span data-ttu-id="8e4c4-131">В разделе функции **setLocalStorageKeyExpiry** и **isLocalStorageExpired** в [файл App.js JavaScript](https://github.com/SharePoint/PnP/blob/master/Samples/Performance.Caching/Performance.LocalStorage/Scripts/App.js) в [Performance.LocalStorage (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Performance.Caching/Performance.LocalStorage) в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-131">See the **setLocalStorageKeyExpiry** and **isLocalStorageExpired** functions in the [App.js JavaScript file](https://github.com/SharePoint/PnP/blob/master/Samples/Performance.Caching/Performance.LocalStorage/Scripts/App.js) in the [Performance.LocalStorage (O365 PnP Sample)](https://github.com/SharePoint/PnP/tree/master/Samples/Performance.Caching/Performance.LocalStorage) for an example.</span></span>

        <span data-ttu-id="8e4c4-132">**Установка ключа истечение срока действия в LocalStorage:**</span><span class="sxs-lookup"><span data-stu-id="8e4c4-132">**Setting an expiration key in LocalStorage:**</span></span>

        ```
        function setLocalStorageKeyExpiry(key) 
        {       
            // Check for expiration config values
            var expiryConfig = localStorage.getItem(expiryConfigKey);
            
            // Check for existing expiration stamp
            var existingStamp = localStorage.getItem(key + expiryKeySuffix);    
        
            // Override cached setting if a user has entered a value that is different than what is stored
            if (expiryConfig != null) 
            {                       
                var currentTime = Math.floor((new Date().getTime()) / 1000);
                expiryConfig = parseInt(expiryConfig);
                
                var newStamp = Math.floor((currentTime + expiryConfig));
                localStorage.setItem(key + expiryKeySuffix, newStamp);
                
                // Log status to window        
                cachingStatus += "\n" + "Setting expiration for the " + key + " key...";
                $('#status').val(cachingStatus);
            }    
            else 
            {
               
            }
        }
        ```

        <span data-ttu-id="8e4c4-133">**Проверьте, если ключ истечение срока действия срока действия в LocalStorage:**</span><span class="sxs-lookup"><span data-stu-id="8e4c4-133">**Check to see if the expiration key is expired in LocalStorage:**</span></span>
        ```
        function isLocalStorageExpired(key, keyTimeStampName) 
        {
            // Retrieve the example setting for expiration in seconds
            var expiryConfig = localStorage.getItem(expiryConfigKey);
            
            // Retrieve the example setting for expiration in seconds
            var expiryStamp = localStorage.getItem(keyTimeStampName);
        
            if (expiryStamp != null && expiryConfig != null) {
        
                // Retrieve the expiration stamp and compare against specified settings to see if it is expired
                var currentTime = Math.floor((new Date().getTime()) / 1000);
        
                if (currentTime - parseInt(expiryStamp) > parseInt(expiryConfig)) {
                    cachingStatus += "\n" + "The " + key + " key time stamp has expired...";
                    $('#status').val(cachingStatus);
                    return true;
                }
                else 
                {
                    var estimatedSeconds = parseInt(expiryStamp) - currentTime;
                    cachingStatus += "\n" + "The " + key + " time stamp expires in " + estimatedSeconds + " seconds...";
                    $('#status').val(cachingStatus);
                    return false;
                }
            }
            else 
            {
                //default
                return true;
            }
        }
        ```

<span data-ttu-id="8e4c4-134">**Когда это подходит?**</span><span class="sxs-lookup"><span data-stu-id="8e4c4-134">**When is it a good fit?**</span></span>

<span data-ttu-id="8e4c4-135">Когда следует использовать API модели объектов SharePoint ECMA со стороны клиента (sp.js) и оценить данные со стороны клиента, чтобы определить необходимо осуществлять вызовы API.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-135">When you need to use the SharePoint ECMA Client-side Object Model API (sp.js) and evaluate client-side data to determine if the API calls need to be made.</span></span>

<span data-ttu-id="8e4c4-136">**Приступая к работе**</span><span class="sxs-lookup"><span data-stu-id="8e4c4-136">**Getting started**</span></span>

<span data-ttu-id="8e4c4-137">[Performance.Caching (PnP образец O365)](https://github.com/SharePoint/PnP/tree/master/Samples/Performance.Caching) демонстрируется, как реализовать LocalStorage и на основе файлов cookie со стороны клиента, кэширование в модели надстройки и предоставляет ссылки на другие статьи и примеры.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-137">The [Performance.Caching (O365 PnP Sample)](https://github.com/SharePoint/PnP/tree/master/Samples/Performance.Caching) demonstrates how to implement both LocalStorage and cookie-based client-side caching in the Add-in model and provides links to several samples and articles.</span></span>

<a name="use-server-side-caching"></a><span data-ttu-id="8e4c4-138">Используйте кэширование на сервере</span><span class="sxs-lookup"><span data-stu-id="8e4c4-138">Use server-side caching</span></span> 
-----------------------
<span data-ttu-id="8e4c4-139">В этом шаблоне методы кэширования на сервере, такие как оценки файла cookie сеанса и на сервере используются для доступа к кэшированным данным.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-139">In this pattern, server-side caching techniques such as session and server-side cookie evaluation are used to access cached data.</span></span> <span data-ttu-id="8e4c4-140">Данные, хранящиеся в этих расположениях используется для определения, если это необходимо выполнять вызовы API SharePoint server.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-140">Information stored in these locations is used to determine if it is necessary to make API calls to a SharePoint server.</span></span>

- <span data-ttu-id="8e4c4-141">Этот шаблон хранит данные, возвращаемые из вызовов SharePoint API в кэш на сервере.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-141">This pattern stores data returned from SharePoint API calls in server-side caches.</span></span>    
- <span data-ttu-id="8e4c4-142">Этот шаблон используется код на стороне сервера для оценки данных, сохраненных в расположений на сервере.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-142">This pattern uses server-side code to evaluate data stored in server-side locations.</span></span>
    + <span data-ttu-id="8e4c4-143">Расположений на сервере могут содержать данных на основе сеанса, хранимые в оперативной памяти или других сторонних производителей на стороне сервера кэширования технологий кэшируется на сервере.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-143">Server-side locations may include session-based data, server-side caches stored in RAM, or other third-party server-based caching technologies.</span></span>
- <span data-ttu-id="8e4c4-144">Этот шаблон используется код на стороне сервера для оценки данных, сохраненных в файлах cookie.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-144">This pattern uses server-side code to evaluate data stored in cookies.</span></span>
- <span data-ttu-id="8e4c4-145">Файлы cookie не более хранения 4095 объем данных в байтах.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-145">Cookies are limited to storing 4095 bytes of data.</span></span>
    + <span data-ttu-id="8e4c4-146">Файлы cookie имеют механизм истечение срока действия встроенных данных.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-146">Cookies have a built-in data expiration mechanism.</span></span>
    
    <span data-ttu-id="8e4c4-147">В разделе **CookieCheckSkip** метода в [Класс Customizer.aspx.cs](https://github.com/SharePoint/PnP/blob/master/Solutions/OD4B.Configuration.Async/OD4B.Configuration.AsyncWeb/Pages/Customizer.aspx.cs) в [OD4B. Configuration.Async (PnP образец O365)](https://github.com/SharePoint/PnP/tree/master/Solutions/OD4B.Configuration.Async) для просмотра кода на стороне сервера используется для оценки файлы cookie.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-147">See the **CookieCheckSkip** method in the [Customizer.aspx.cs Class](https://github.com/SharePoint/PnP/blob/master/Solutions/OD4B.Configuration.Async/OD4B.Configuration.AsyncWeb/Pages/Customizer.aspx.cs) in the [OD4B.Configuration.Async (O365 PnP Sample)](https://github.com/SharePoint/PnP/tree/master/Solutions/OD4B.Configuration.Async) to see how server-side code is used to evaluate cookies.</span></span>

<span data-ttu-id="8e4c4-148">**Реализация уровень кэша «атаки третьего»** В некоторых случаях имеет смысл создать собственный уровень пользовательского кэша.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-148">**Implementing your own 'man-in-the-middle' cache layer** Sometimes, it makes sense to create your own custom cache layer.</span></span> <span data-ttu-id="8e4c4-149">Хороший пример — Если вам необходимо получить сведения из профиля пользователя.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-149">A good example is when you need to return information from a user's profile.</span></span> <span data-ttu-id="8e4c4-150">API-интерфейсы профилей пользователей в некоторых случаях уйти много времени на выполнение.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-150">The User Profile APIs sometimes take a long time to execute.</span></span> <span data-ttu-id="8e4c4-151">Чтобы предоставить конечным пользователям быстро пользовательский интерфейс, можно создать задания таймера удаленного для запроса службы профилей пользователей и сохранения данных в различных хранилищ данных.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-151">To provide end users with a fast user interface experience, you can create a remote timer job to query the user profile service and store the information in a variety of data stores.</span></span> <span data-ttu-id="8e4c4-152">Затем можно создать службы обеспечивает возможность запроса хранит данные через JavaScript вызовы из SharePoint надстройки.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-152">Then, you can create a service to allow you to query the data stores via JavaScript calls from SharePoint Add-ins.</span></span>  

<span data-ttu-id="8e4c4-153">Azure доступно множество различных механизмов хранения, которые могут использоваться для хранения сведений, многие из которых очень быстро выполнять как хранение таблицы и хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-153">Azure has many different storage mechanisms that may be used to store information, many of which perform extremely fast, like Table storage and Blob storage.</span></span> <span data-ttu-id="8e4c4-154">Azure также можно создать веб-приложение для размещения службы и обеспечения безопасности, все данные и службы с помощью одной Azure Active Directory как клиента Office 365 SharePoint или даже среде SharePoint в локальной с поддержкой DirSync.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-154">Azure also allows you to create a web app to host the service and secure all of the data and the service with the same Azure Active Directory as an Office 365 SharePoint tenancy, or even an on-premises SharePoint environment with DirSync enabled.</span></span>

<span data-ttu-id="8e4c4-155">**Когда это подходит?**</span><span class="sxs-lookup"><span data-stu-id="8e4c4-155">**When is it a good fit?**</span></span>

- <span data-ttu-id="8e4c4-156">Когда следует использовать API модели объектов SharePoint управляемого кода на стороне клиента (Microsoft.SharePoint.Client.dll) и оценки данных на сервере или файлы cookie, чтобы определить необходимо осуществлять вызовы API.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-156">When you need to use the SharePoint Managed Code Client-side Object Model API (Microsoft.SharePoint.Client.dll) and evaluate server-side data or cookies to determine if the API calls need to be made.</span></span>
- <span data-ttu-id="8e4c4-157">При наличии длительных операций, таких как Azure Web задания, которое должно быть инициирована только один раз в заданном интервал времени, независимо от того, как количество раз пользователь пытается инициировать операцию.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-157">When you have long-running operations, such as an Azure Web Job, that should only be initiated once per given time frame, no matter how many times a user tries to initiate an operation.</span></span>  
    + <span data-ttu-id="8e4c4-158">Применение настроенной OneDrive для бизнеса конфигураций являются хорошим примером такого сценария.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-158">Applying customized OneDrive for Business configurations are a good example of such a scenario.</span></span>

<span data-ttu-id="8e4c4-159">**Приступая к работе**</span><span class="sxs-lookup"><span data-stu-id="8e4c4-159">**Getting started**</span></span>

<span data-ttu-id="8e4c4-160">[Performance.Caching (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Performance.Caching) описывается, как реализовать LocalStorage и на основе файлов cookie со стороны клиента, кэширование в модели надстройки и предоставляет ссылки на другие статьи и примеры.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-160">The [Performance.Caching (O365 PnP Sample)](https://github.com/SharePoint/PnP/tree/master/Samples/Performance.Caching) describes how to implement both LocalStorage and cookie-based client-side caching in the Add-in model and provides links to several samples and articles.</span></span>

<a name="related-links"></a><span data-ttu-id="8e4c4-161">Ссылки по теме</span><span class="sxs-lookup"><span data-stu-id="8e4c4-161">Related links</span></span>
=============
- <span data-ttu-id="8e4c4-162">Руководств по [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Руководств")</span><span class="sxs-lookup"><span data-stu-id="8e4c4-162">Guidance articles at [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Guidance Articles")</span></span>
- <span data-ttu-id="8e4c4-163">Справочные материалы в библиотеке MSDN по [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Справочные материалы в библиотеке MSDN")</span><span class="sxs-lookup"><span data-stu-id="8e4c4-163">References in MSDN at [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "References in MSDN")</span></span>
- <span data-ttu-id="8e4c4-164">Видеозаписи по [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "видео")</span><span class="sxs-lookup"><span data-stu-id="8e4c4-164">Videos at [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span></span>

<a name="related-pnp-samples"></a><span data-ttu-id="8e4c4-165">Примеры связанных с ними PnP</span><span class="sxs-lookup"><span data-stu-id="8e4c4-165">Related PnP samples</span></span>
===================

- <span data-ttu-id="8e4c4-166">Примеры и содержимое в [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span><span class="sxs-lookup"><span data-stu-id="8e4c4-166">Samples and content at [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span></span>

<a name="applies-to"></a><span data-ttu-id="8e4c4-167">Применимо к</span><span class="sxs-lookup"><span data-stu-id="8e4c4-167">Applies to</span></span>
==========
- <span data-ttu-id="8e4c4-168">Office 365 нескольких клиентов (MT)</span><span class="sxs-lookup"><span data-stu-id="8e4c4-168">Office 365 Multi Tenant (MT)</span></span>
- <span data-ttu-id="8e4c4-169">Office 365 выделенных (D)</span><span class="sxs-lookup"><span data-stu-id="8e4c4-169">Office 365 Dedicated (D)</span></span>
- <span data-ttu-id="8e4c4-170">SharePoint 2013 в локальной</span><span class="sxs-lookup"><span data-stu-id="8e4c4-170">SharePoint 2013 on-premises</span></span>
