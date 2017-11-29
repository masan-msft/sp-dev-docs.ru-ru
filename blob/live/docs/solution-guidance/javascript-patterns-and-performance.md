---
title: "Шаблоны JavaScript и производительности"
ms.date: 11/03/2017
ms.openlocfilehash: d9f125657f65da7da770e36e7c1c314759a05c29
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="javascript-patterns-and-performance"></a><span data-ttu-id="e7b99-102">Шаблоны JavaScript и производительности</span><span class="sxs-lookup"><span data-stu-id="e7b99-102">JavaScript Patterns and Performance</span></span>

<span data-ttu-id="e7b99-103">Лет назад ASP.NET мы получили визуализации для элемента управления пользовательского интерфейса на сервере, и была хороший.</span><span class="sxs-lookup"><span data-stu-id="e7b99-103">Years ago, ASP.NET gave us server-side UI control rendering, and it was good.</span></span> <span data-ttu-id="e7b99-104">Тем не менее, что на сервере визуализации, требуется код с полным доверием.</span><span class="sxs-lookup"><span data-stu-id="e7b99-104">That server-side rendering, however, requires full-trust code.</span></span> <span data-ttu-id="e7b99-105">Теперь, когда мы выполнившим переход к SharePoint и Office 365, код с полным доверием больше не вариант.</span><span class="sxs-lookup"><span data-stu-id="e7b99-105">Now that we have transitioned to SharePoint and Office 365, full-trust code is no longer an option.</span></span> <span data-ttu-id="e7b99-106">Это означает, что отображение элемента управления пользовательского интерфейса на сервере, не будут работать для нас больше.</span><span class="sxs-lookup"><span data-stu-id="e7b99-106">That means server-side UI control rendering won't work for us any more.</span></span>

<span data-ttu-id="e7b99-107">Еще бизнеса по-прежнему требуются специальные функциональные возможности пользовательского интерфейса для своих веб-сайтов и приложений.</span><span class="sxs-lookup"><span data-stu-id="e7b99-107">Yet, businesses still need custom UI functionality for their websites and apps.</span></span> <span data-ttu-id="e7b99-108">Это означает, что пользовательские функции пользовательского интерфейса должны быть перемещены на стороне сервера со стороны клиента.</span><span class="sxs-lookup"><span data-stu-id="e7b99-108">That means custom UI functionality must be moved from the server-side to the client-side.</span></span> 

<span data-ttu-id="e7b99-109">JavaScript на стороне клиента теперь является лучшим выбором для отображения элемента управления пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="e7b99-109">Client-side JavaScript is now the way to go for UI control rendering.</span></span>

## <span data-ttu-id="e7b99-110"><a name="JavaScriptPatterns"></a>Шаблоны JavaScript</span><span class="sxs-lookup"><span data-stu-id="e7b99-110"><a name="JavaScriptPatterns"></a> JavaScript Patterns</span></span>

<span data-ttu-id="e7b99-111">Поскольку JavaScript на стороне клиента — это путь, что такое лучшие способы реализации JavaScript на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="e7b99-111">Since client-side JavaScript is the path, what are the best ways to implement client-side JavaScript?</span></span> <span data-ttu-id="e7b99-112">Как одно приступить к работе?</span><span class="sxs-lookup"><span data-stu-id="e7b99-112">How does one get started?</span></span>

<span data-ttu-id="e7b99-113">Существует несколько вариантов:</span><span class="sxs-lookup"><span data-stu-id="e7b99-113">There are several options:</span></span>

|<span data-ttu-id="e7b99-114">Параметр</span><span class="sxs-lookup"><span data-stu-id="e7b99-114">Option</span></span>|<span data-ttu-id="e7b99-115">Описание</span><span class="sxs-lookup"><span data-stu-id="e7b99-115">Description</span></span>|
|:---|:---|
|<span data-ttu-id="e7b99-116">Внедрение JavaScript</span><span class="sxs-lookup"><span data-stu-id="e7b99-116">JavaScript Embedding</span></span> | <span data-ttu-id="e7b99-117">[Site.UserCustomActions](https://msdn.microsoft.com/EN-US/library/office/microsoft.sharepoint.client.site.usercustomactions.aspx) или [Web.UserCustomActions](https://msdn.microsoft.com/EN-US/library/office/microsoft.sharepoint.client.web.usercustomactions.aspx) разрешить для включения сценария непосредственно в разметке страницы.</span><span class="sxs-lookup"><span data-stu-id="e7b99-117">[Site.UserCustomActions](https://msdn.microsoft.com/EN-US/library/office/microsoft.sharepoint.client.site.usercustomactions.aspx) or [Web.UserCustomActions](https://msdn.microsoft.com/EN-US/library/office/microsoft.sharepoint.client.web.usercustomactions.aspx) allow for the inclusion of script directly into the page markup.</span></span> <span data-ttu-id="e7b99-118">Используется в [Шаблон загрузчик](#LoaderPattern) , описанные ниже</span><span class="sxs-lookup"><span data-stu-id="e7b99-118">This is used in the [Loader Pattern](#LoaderPattern) discussed below</span></span>|
|<span data-ttu-id="e7b99-119">Шаблоны отображения</span><span class="sxs-lookup"><span data-stu-id="e7b99-119">Display Templates</span></span> | <span data-ttu-id="e7b99-120">Применяется для представления и поиска.</span><span class="sxs-lookup"><span data-stu-id="e7b99-120">Applies to Views and Search.</span></span> <span data-ttu-id="e7b99-121">У вас нет развертывание любого типа приложения или поставщик размещенных кода.</span><span class="sxs-lookup"><span data-stu-id="e7b99-121">You don't have to deploy any kind of an app or provider hosted code.</span></span> <span data-ttu-id="e7b99-122">Это просто файл JavaScript, которые могут быть загружены в (например) библиотеку стилей для настройки представления.</span><span class="sxs-lookup"><span data-stu-id="e7b99-122">It's simply a JavaScript file that can be uploaded to (for example) the style library to customize views.</span></span> <span data-ttu-id="e7b99-123">Можно создать любое представление, необходимо с помощью JavaScript</span><span class="sxs-lookup"><span data-stu-id="e7b99-123">You can create any view required by using JavaScript</span></span>|
|<span data-ttu-id="e7b99-124">Надстройки размещением в SharePoint</span><span class="sxs-lookup"><span data-stu-id="e7b99-124">SharePoint Hosted Add-Ins</span></span> | <span data-ttu-id="e7b99-125">С помощью JSOM осуществляющих обратную связь с веб-узла или добавить в веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="e7b99-125">Uses JSOM to communicate back to the host web or the add-in web.</span></span> <span data-ttu-id="e7b99-126">Предоставляет доступ к веб-прокси для кросс-доменнные запросы</span><span class="sxs-lookup"><span data-stu-id="e7b99-126">It gives access to the Web Proxy for cross domain calls</span></span>|
|<span data-ttu-id="e7b99-127">Надстройки размещением у поставщика</span><span class="sxs-lookup"><span data-stu-id="e7b99-127">Provider Hosted Add-Ins</span></span> | <span data-ttu-id="e7b99-128">Позволяет создавать сложные приложения в различных стеки технологии - без снижения безопасности интеграции с SharePoint</span><span class="sxs-lookup"><span data-stu-id="e7b99-128">Enables the creation of complex applications across a variety of technology stacks - while maintaining secure integration with SharePoint</span></span>|
|<span data-ttu-id="e7b99-129">JSLink</span><span class="sxs-lookup"><span data-stu-id="e7b99-129">JSLink</span></span> | <span data-ttu-id="e7b99-130">Позволяет загрузить один или несколько файлов JavaScript в веб-части OOTB и представлений</span><span class="sxs-lookup"><span data-stu-id="e7b99-130">Allows you to load one or more JavaScript files in many OOTB web parts and views</span></span>|
|<span data-ttu-id="e7b99-131">ScriptEditor веб-части</span><span class="sxs-lookup"><span data-stu-id="e7b99-131">ScriptEditor Webpart</span></span> | <span data-ttu-id="e7b99-132">Включить сценарий напрямую или загрузки через теги скрипта разметку для создания сложных одной страницы приложений, размещенных полностью на сайте SharePoint</span><span class="sxs-lookup"><span data-stu-id="e7b99-132">Include script directly or loaded through script tags with markup to create complex single page applications hosted entirely within the SharePoint site</span></span>|

<span data-ttu-id="e7b99-133">Кажется, что вы фиксируются в эти варианты выбора, если ваш взгляд другой параметр бы лучше подходит для вашей ситуации.</span><span class="sxs-lookup"><span data-stu-id="e7b99-133">Don't think you are locked into these choices if you feel a different option would be better for your situation.</span></span> 

## <span data-ttu-id="e7b99-134"><a name="JavaScriptPerformance"></a>Производительность JavaScript</span><span class="sxs-lookup"><span data-stu-id="e7b99-134"><a name="JavaScriptPerformance"></a> JavaScript Performance</span></span>

<span data-ttu-id="e7b99-135">На каждом этапе процесса разработки важно помнить о производительности.</span><span class="sxs-lookup"><span data-stu-id="e7b99-135">At each step of the development process, it's important to keep performance in mind.</span></span> <span data-ttu-id="e7b99-136">Вот несколько вещей, которые делают разница в производительности JavaScript.</span><span class="sxs-lookup"><span data-stu-id="e7b99-136">Here are a few things that make a big difference in JavaScript performance:</span></span>

|<span data-ttu-id="e7b99-137">Параметр</span><span class="sxs-lookup"><span data-stu-id="e7b99-137">Option</span></span>|<span data-ttu-id="e7b99-138">Описание</span><span class="sxs-lookup"><span data-stu-id="e7b99-138">Description</span></span>|
|:---|:---|
|[<span data-ttu-id="e7b99-139">Уменьшите количество запросов</span><span class="sxs-lookup"><span data-stu-id="e7b99-139">Reduce the number of requests</span></span>](#ReduceTheNumberOfRequests) | <span data-ttu-id="e7b99-140">Меньшее число запросов означает, что меньшего числа обращений к серверу, уменьшение задержки.</span><span class="sxs-lookup"><span data-stu-id="e7b99-140">Fewer requests means fewer round-trips to the server, reducing latency.</span></span>|
|[<span data-ttu-id="e7b99-141">Извлечение необходимых данных</span><span class="sxs-lookup"><span data-stu-id="e7b99-141">Retrieve only the data you need</span></span>](#RetrieveOnlyTheDataYouNeed) | <span data-ttu-id="e7b99-142">Уменьшение объема данных, передаваемых по сети.</span><span class="sxs-lookup"><span data-stu-id="e7b99-142">Reduce the amount of data sent over the wire.</span></span> <span data-ttu-id="e7b99-143">Также снижает нагрузку на сервер.</span><span class="sxs-lookup"><span data-stu-id="e7b99-143">Also reduces server load.</span></span>|
|[<span data-ttu-id="e7b99-144">Предоставляют возможности нагрузки хороший страницы</span><span class="sxs-lookup"><span data-stu-id="e7b99-144">Provide a good page load experience</span></span>](#ProvideAGoodUserExperience) | <span data-ttu-id="e7b99-145">Сохранение пользовательского интерфейса реагирует на пользователя.</span><span class="sxs-lookup"><span data-stu-id="e7b99-145">Keep your UI responsive to the user.</span></span> <span data-ttu-id="e7b99-146">Например, обновить меню на страницу *до* начала загрузки 100 записей.</span><span class="sxs-lookup"><span data-stu-id="e7b99-146">For example, update the menus on the page *before* you start the download of 100+ records.</span></span>|
|[<span data-ttu-id="e7b99-147">Использование асинхронных вызовов и шаблоны, по возможности</span><span class="sxs-lookup"><span data-stu-id="e7b99-147">Use asynchronous calls and patterns whenever possible</span></span>](#EverythingIsAsynchronous) | <span data-ttu-id="e7b99-148">Опрос — весом нагрузку на производительность, чем использование асинхронного вызова или обратного вызова.</span><span class="sxs-lookup"><span data-stu-id="e7b99-148">Polling is a heavier burden on performance than using an asynchronous call or callback.</span></span>| 
|[<span data-ttu-id="e7b99-149">Кэширование — ключ</span><span class="sxs-lookup"><span data-stu-id="e7b99-149">Caching is key</span></span>](#ClientSideCaching) | <span data-ttu-id="e7b99-150">При проведении улучшения производительности дальнейшей кэширование сократить расходы на сервере.</span><span class="sxs-lookup"><span data-stu-id="e7b99-150">Caching further reduces the burden on the server while giving immediate performance improvement.</span></span>|
|[<span data-ttu-id="e7b99-151">Подготовка к более просмотров страниц, чем когда-либо представить</span><span class="sxs-lookup"><span data-stu-id="e7b99-151">Prepare for more page views than you ever imagined</span></span>](#PriceOfPopularity) | <span data-ttu-id="e7b99-152">Высокая интенсивность операций данных целевая страница допустимо при наличии нескольких совпадений.</span><span class="sxs-lookup"><span data-stu-id="e7b99-152">A data-heavy landing page is okay when you only have a few hits.</span></span> <span data-ttu-id="e7b99-153">Однако при получении тысяч обращений, действительно можно повысить производительность.</span><span class="sxs-lookup"><span data-stu-id="e7b99-153">But if you get thousands of hits, that can really impact performance.</span></span>|

## <span data-ttu-id="e7b99-154"><a name="WhatIsMyCodeDoing"></a>Каким образом код</span><span class="sxs-lookup"><span data-stu-id="e7b99-154"><a name="WhatIsMyCodeDoing"></a> What is my code doing</span></span>

<span data-ttu-id="e7b99-155">Для повышения производительности важно знать, каким образом кода в любой момент.</span><span class="sxs-lookup"><span data-stu-id="e7b99-155">For performance, it's important to know what your code is doing at any point.</span></span> <span data-ttu-id="e7b99-156">Это позволяет определить способы повышения эффективности работы.</span><span class="sxs-lookup"><span data-stu-id="e7b99-156">This lets you identify ways to improve efficiency.</span></span> <span data-ttu-id="e7b99-157">Ниже приведены несколько способов хороший делать это.</span><span class="sxs-lookup"><span data-stu-id="e7b99-157">Below are a few good ways to do just that.</span></span>

### <span data-ttu-id="e7b99-158"><a name="ReduceTheNumberOfRequests"></a>Уменьшите количество запросов</span><span class="sxs-lookup"><span data-stu-id="e7b99-158"><a name="ReduceTheNumberOfRequests"></a> Reduce the number of requests</span></span>

<span data-ttu-id="e7b99-159">Всегда позволяют наименьшее и наименьшее запросов.</span><span class="sxs-lookup"><span data-stu-id="e7b99-159">Always make the fewest and smallest requests possible.</span></span> <span data-ttu-id="e7b99-160">Каждого запроса, то исключить сократить расходы производительности на сервере и на клиенте.</span><span class="sxs-lookup"><span data-stu-id="e7b99-160">Each request you eliminate reduces the performance burden on the server and on the client.</span></span> <span data-ttu-id="e7b99-161">И запрашивать доступ меньшего размера дальнейшей снижает нагрузку производительности.</span><span class="sxs-lookup"><span data-stu-id="e7b99-161">And making smaller requests further reduces the performance burden.</span></span>

<span data-ttu-id="e7b99-162">Существует несколько способов сократить количество запросов и уменьшения размера запроса.</span><span class="sxs-lookup"><span data-stu-id="e7b99-162">There are several ways to reduce requests and reduce request size.</span></span>

- <span data-ttu-id="e7b99-163">Максимальное число файлов JavaScript в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="e7b99-163">Limit the number of JavaScript files in production.</span></span> <span data-ttu-id="e7b99-164">Отделение файлов JavaScript работает подходят для разработки, но не так и для рабочей среды.</span><span class="sxs-lookup"><span data-stu-id="e7b99-164">Separating your JavaScript files works well for development, but not so well for production.</span></span> <span data-ttu-id="e7b99-165">Объединение файлов JavaScript в единый файл JavaScript, а также некоторые файлы JavaScript, как.</span><span class="sxs-lookup"><span data-stu-id="e7b99-165">Combine your JavaScript files into a single JavaScript file, or as few JavaScript files as you can.</span></span>
- <span data-ttu-id="e7b99-166">Уменьшить размеры файлов.</span><span class="sxs-lookup"><span data-stu-id="e7b99-166">Shrink file sizes.</span></span> <span data-ttu-id="e7b99-167">Минимизация файлов JavaScript рабочей путем удаления разрывов, пробелов и комментарии.</span><span class="sxs-lookup"><span data-stu-id="e7b99-167">Minimize your production JavaScript files by removing line breaks, white space, and comments.</span></span> <span data-ttu-id="e7b99-168">Существует несколько JavaScript minify программы и веб-сайты, которые можно использовать для значительно уменьшает размер файлов JavaScript.</span><span class="sxs-lookup"><span data-stu-id="e7b99-168">There are several JavaScript minify programs and websites that you can use to greatly reduce your JavaScript file sizes.</span></span>
- <span data-ttu-id="e7b99-169">Используйте кэширование файлов браузера, чтобы уменьшить запросов.</span><span class="sxs-lookup"><span data-stu-id="e7b99-169">Use browser file caching to reduce requests.</span></span> <span data-ttu-id="e7b99-170">Обновленный [Шаблон загрузчик](#LoaderPattern) ниже — это удобный способ разверните узел при этом представление.</span><span class="sxs-lookup"><span data-stu-id="e7b99-170">The updated [Loader Pattern](#LoaderPattern) below is a good way to expand upon this idea.</span></span>

### <span data-ttu-id="e7b99-171">< имя «RetrieveOnlyTheDataYouNeed» ></a> извлечения только необходимых данных</span><span class="sxs-lookup"><span data-stu-id="e7b99-171"><a name"RetrieveOnlyTheDataYouNeed"></a> Retrieve only the data you need</span></span>

<span data-ttu-id="e7b99-172">При запросе данных, не забудьте специализация запросов на самом деле требуется.</span><span class="sxs-lookup"><span data-stu-id="e7b99-172">When requesting data, remember to focus your requests to what you actually need.</span></span> <span data-ttu-id="e7b99-173">Загрузка всей статьи для получения заголовок, например, приведет к снижению производительности довольно.</span><span class="sxs-lookup"><span data-stu-id="e7b99-173">Downloading an entire article to obtain the title, for example, will reduce performance quite a bit.</span></span>

- <span data-ttu-id="e7b99-174">Используйте фильтрацию сервера, выберите и ограничения для сведения к минимуму трафика по сети.</span><span class="sxs-lookup"><span data-stu-id="e7b99-174">Use server filtering, select, and limits to minimize traffic over the wire.</span></span>
- <span data-ttu-id="e7b99-175">Не запрашивать все статьи, если необходимо использовать только первые пять, в качестве другого примера.</span><span class="sxs-lookup"><span data-stu-id="e7b99-175">Don't request all articles when you want only the first five, as another example.</span></span>
- <span data-ttu-id="e7b99-176">Больше не задавать для контейнера всей свойств, если вы хотите, чтобы только одно свойство.</span><span class="sxs-lookup"><span data-stu-id="e7b99-176">Don't ask for the entire property bag if you want only one property.</span></span> <span data-ttu-id="e7b99-177">В один пример сценария требуется только одно свойство, но запрошено контейнер всей свойств, которая оказалась 800 КБ.</span><span class="sxs-lookup"><span data-stu-id="e7b99-177">In one example, a script needed only one property, but requested the entire property bag, which turned out to be 800 KB.</span></span> <span data-ttu-id="e7b99-178">Также следует помните, что размер объекта могут изменяться, так что такое только несколько килобайт теперь могут стать МБ далее в жизненном цикле продукта.</span><span class="sxs-lookup"><span data-stu-id="e7b99-178">Also remember that the size of an object can change over time, so what is only a few kilobytes now can become megabytes in size later in the product lifecycle.</span></span> 

### <span data-ttu-id="e7b99-179"><a name="DontRequestDataYouWillDiscard"></a>Не запрашивать данные, что будут потеряны неиспользуемых</span><span class="sxs-lookup"><span data-stu-id="e7b99-179"><a name="DontRequestDataYouWillDiscard"></a> Don't request data that you will discard unused</span></span>

<span data-ttu-id="e7b99-180">При извлечении данных, можно было использовать речь идет о возможность лучше фильтрации исходного запроса.</span><span class="sxs-lookup"><span data-stu-id="e7b99-180">If you retrieve more data than you actually use, think of it as an opportunity to better filter your initial query.</span></span> 

- <span data-ttu-id="e7b99-181">Запросите поля, которые как имя и адрес, а не всю запись.</span><span class="sxs-lookup"><span data-stu-id="e7b99-181">Request only the fields you need, like Name and Address, not the entire record.</span></span>
- <span data-ttu-id="e7b99-182">Сделать определенные, тщательного запросов фильтра.</span><span class="sxs-lookup"><span data-stu-id="e7b99-182">Make specific, deliberate filter requests.</span></span> <span data-ttu-id="e7b99-183">К примеру Если вы хотите перечислены доступные статьи, получите заголовок, PublishingDate и автор.</span><span class="sxs-lookup"><span data-stu-id="e7b99-183">For example, if you want to list the available articles, get the Title, PublishingDate, and Author.</span></span> <span data-ttu-id="e7b99-184">Оставьте для остальных полей из строки запроса.</span><span class="sxs-lookup"><span data-stu-id="e7b99-184">Leave the rest of the fields out of the request.</span></span>

### <span data-ttu-id="e7b99-185"><a name="ProvideAGoodUserExperience"></a>Предоставление удобства работы пользователей</span><span class="sxs-lookup"><span data-stu-id="e7b99-185"><a name="ProvideAGoodUserExperience"></a> Provide a good user experience</span></span>

<span data-ttu-id="e7b99-186">Рывками, неправильное пользовательских интерфейсов влиять не просто производительности, а также производительности.</span><span class="sxs-lookup"><span data-stu-id="e7b99-186">Jerky, inconsistent user interfaces impact not just performance, but also perceived performance.</span></span> <span data-ttu-id="e7b99-187">Написание кода таким образом, чтобы предоставить повышения качества связи.</span><span class="sxs-lookup"><span data-stu-id="e7b99-187">Write your code in such a way as to give a smooth experience.</span></span>

- <span data-ttu-id="e7b99-188">Чтобы указать, что действия загрузке или время используйте счетчик.</span><span class="sxs-lookup"><span data-stu-id="e7b99-188">Use a spinner to indicate that things are loading or taking time.</span></span>
- <span data-ttu-id="e7b99-189">Понять порядок выполнения кода и фигуры для работы пользователей.</span><span class="sxs-lookup"><span data-stu-id="e7b99-189">Understand the order of execution for your code, and shape it for the best user experience.</span></span> <span data-ttu-id="e7b99-190">Например если планируется извлечение большого объема данных с сервера, и вы планируете изменить пользовательский интерфейс путем скрытия меню, скройте меню сначала.</span><span class="sxs-lookup"><span data-stu-id="e7b99-190">For example, if you plan to retrieve a lot of data from the server, and you plan to change the user interface by hiding a menu, hide the menu first.</span></span> <span data-ttu-id="e7b99-191">Которая позволит по ширине пользовательский интерфейс для пользователя.</span><span class="sxs-lookup"><span data-stu-id="e7b99-191">That will prevent a staggered UI experience for the user.</span></span>

## <span data-ttu-id="e7b99-192"><a name="EverythingIsAsynchronous"></a>Все, что является асинхронное</span><span class="sxs-lookup"><span data-stu-id="e7b99-192"><a name="EverythingIsAsynchronous"></a> Everything is Asynchronous</span></span>

<span data-ttu-id="e7b99-193">Каждые действие code в браузере должен считаться асинхронный.</span><span class="sxs-lookup"><span data-stu-id="e7b99-193">Every code activity in the browser should be considered asynchronous.</span></span> <span data-ttu-id="e7b99-194">Файлы загрузки в некотором порядке, необходимо дождаться DOM для загрузки и запросы на SharePoint будут завершены на различные скорости.</span><span class="sxs-lookup"><span data-stu-id="e7b99-194">Your files load in some order, you must wait for the DOM to load, and your requests back to SharePoint will complete at different speeds.</span></span> 

- <span data-ttu-id="e7b99-195">Понимаете, как код работает в времени.</span><span class="sxs-lookup"><span data-stu-id="e7b99-195">Understand how your code operates in time.</span></span>
- <span data-ttu-id="e7b99-196">События использования и обратных вызовов вместо опроса.</span><span class="sxs-lookup"><span data-stu-id="e7b99-196">Use events and callbacks instead of polling.</span></span>
- <span data-ttu-id="e7b99-197">Использование обязательства.</span><span class="sxs-lookup"><span data-stu-id="e7b99-197">Use promises.</span></span> <span data-ttu-id="e7b99-198">В jQuery они называются объектами **Отложенный** .</span><span class="sxs-lookup"><span data-stu-id="e7b99-198">In jQuery they're called **Deferred** objects.</span></span> <span data-ttu-id="e7b99-199">Существуют аналогичные понятия Q, WinJS и ES6.</span><span class="sxs-lookup"><span data-stu-id="e7b99-199">There are similar concepts in Q, WinJS, and ES6.</span></span>
- <span data-ttu-id="e7b99-200">Используйте асинхронные вызовы пользу не асинхронного вызова.</span><span class="sxs-lookup"><span data-stu-id="e7b99-200">Use the asynchronous call in favor of the non-asynchronous call.</span></span>
- <span data-ttu-id="e7b99-201">Используйте асинхронный каждый раз, когда может быть задержку:</span><span class="sxs-lookup"><span data-stu-id="e7b99-201">Use asynchronous any time there could be a delay:</span></span>
    - <span data-ttu-id="e7b99-202">Во время выполнения запроса AJAX.</span><span class="sxs-lookup"><span data-stu-id="e7b99-202">During an AJAX request.</span></span>
    - <span data-ttu-id="e7b99-203">Во время любого значительные DOM выполнение различных операций.</span><span class="sxs-lookup"><span data-stu-id="e7b99-203">During any significant DOM manipulation.</span></span>

<span data-ttu-id="e7b99-204">Шаблоны асинхронного повышения производительности и скорости ответа и разрешить для эффективной цепочки зависимые действия.</span><span class="sxs-lookup"><span data-stu-id="e7b99-204">Asynchronous patterns improve performance and responsiveness and allow for the effective chaining of dependent actions.</span></span>

## <span data-ttu-id="e7b99-205"><a name="ClientSideCaching"></a>Кэширование на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="e7b99-205"><a name="ClientSideCaching"></a> Client Side Caching</span></span>

<span data-ttu-id="e7b99-206">Кэширование на стороне клиента — это один из большинства улучшения часто пропущенных производительности, которые можно добавить в код.</span><span class="sxs-lookup"><span data-stu-id="e7b99-206">Client side caching is one of the most often missed performance enhancements you can add to your code.</span></span>

<span data-ttu-id="e7b99-207">Существует три различных местах, можно кэшировать данные.</span><span class="sxs-lookup"><span data-stu-id="e7b99-207">There are three different places you can cache your data:</span></span>

|<span data-ttu-id="e7b99-208">Параметр</span><span class="sxs-lookup"><span data-stu-id="e7b99-208">Option</span></span>|<span data-ttu-id="e7b99-209">Описание</span><span class="sxs-lookup"><span data-stu-id="e7b99-209">Description</span></span>|
|:---|:---|
|<span data-ttu-id="e7b99-210">Сеанс хранилища</span><span class="sxs-lookup"><span data-stu-id="e7b99-210">Session Storage</span></span>|<span data-ttu-id="e7b99-211">Хранит данные в виде пары ключ значение на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="e7b99-211">Stores data as a key/value pair on the client.</span></span> <span data-ttu-id="e7b99-212">Причина этого заключается в хранилище сеанса, которое всегда хранится в виде строки.</span><span class="sxs-lookup"><span data-stu-id="e7b99-212">This is per session storage which is always stored as strings.</span></span> <br /> <span data-ttu-id="e7b99-213">JSON.stringify() преобразует объектов JavaScript строк, которые приводятся рекомендации для хранения объектов.</span><span class="sxs-lookup"><span data-stu-id="e7b99-213">JSON.stringify() will convert your JavaScript objects to strings which helps to store objects.</span></span>
|<span data-ttu-id="e7b99-214">Локальное хранилище</span><span class="sxs-lookup"><span data-stu-id="e7b99-214">Local Storage</span></span>|<p><span data-ttu-id="e7b99-215">Хранит данные в виде пары ключ значение на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="e7b99-215">Stores data as a key/value pair on the client.</span></span> <span data-ttu-id="e7b99-216">Это сохраняемого между сеансами, которые всегда хранится в виде строки.</span><span class="sxs-lookup"><span data-stu-id="e7b99-216">This is persistent across sessions which is always stored as strings.</span></span></p><p><span data-ttu-id="e7b99-217">JSON.stringify() преобразует объектов JavaScript строк, которые приводятся рекомендации для хранения объектов.</span><span class="sxs-lookup"><span data-stu-id="e7b99-217">JSON.stringify() will convert your JavaScript objects to strings which helps to store objects.</span></span></p>|
|<span data-ttu-id="e7b99-218">Локальной базы данных</span><span class="sxs-lookup"><span data-stu-id="e7b99-218">Local Database</span></span>|<span data-ttu-id="e7b99-219">Сохранение реляционные данные на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="e7b99-219">Stores relational data on the client.</span></span> <span data-ttu-id="e7b99-220">В качестве ядро базы данных, часто используется средство упрощенного SQL.</span><span class="sxs-lookup"><span data-stu-id="e7b99-220">Frequently uses SQL-Lite as the database engine.</span></span><br><span data-ttu-id="e7b99-221">Локальное хранилище базы данных не всегда доступны во всех браузерах&mdash;проверьте конечного поддержки браузеров</span><span class="sxs-lookup"><span data-stu-id="e7b99-221">Local Database storage is not always available on all browsers&mdash;Check target browser support</span></span>

<span data-ttu-id="e7b99-222">При кэшировании, имейте в виду ограничений хранилища, доступные для вас и актуальность данных.</span><span class="sxs-lookup"><span data-stu-id="e7b99-222">When caching, keep in mind the storage limits available to you, and the freshness of your data.</span></span> 
- <span data-ttu-id="e7b99-223">Если производится доступ в конец дискового пространства, стоит удалить старые или менее важных кэшированные данные.</span><span class="sxs-lookup"><span data-stu-id="e7b99-223">If you are reaching the end of your storage limits, it might be wise to remove the older or less important cached data.</span></span> 
- <span data-ttu-id="e7b99-224">Различные типы данных можно устарели быстрее, чем другие.</span><span class="sxs-lookup"><span data-stu-id="e7b99-224">Different kinds of data can become stale faster than others.</span></span> <span data-ttu-id="e7b99-225">Список статей новостей может быть устаревших в 5-10 минут, однако имя профиля пользователя можно часто безопасно кэшировать 24 часов и более.</span><span class="sxs-lookup"><span data-stu-id="e7b99-225">A list of news articles can be stale in five to ten minutes, but a user's profile name can often be safely cached for 24 hours or more.</span></span> 

<span data-ttu-id="e7b99-226">Локальный и хранение сеанса не имеет встроенных истечение срока действия, но файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="e7b99-226">Local and session storage doesn't have expiration built-in, but cookies do.</span></span> <span data-ttu-id="e7b99-227">Можно привязать хранимых данных в файл cookie для добавления истечение срока действия в вашей локальной и хранение сеанса.</span><span class="sxs-lookup"><span data-stu-id="e7b99-227">You can tie your stored data to a cookie to add expiration to your local and session storage.</span></span> <span data-ttu-id="e7b99-228">Также можно создавать оболочкой хранилища, который включает в себя дату окончания срока действия и проверить в коде.</span><span class="sxs-lookup"><span data-stu-id="e7b99-228">You can also create a storage wrapper that includes an expiration date and check this in your code.</span></span>

## <span data-ttu-id="e7b99-229"><a name="PriceOfPopularity"></a>Цена популярности</span><span class="sxs-lookup"><span data-stu-id="e7b99-229"><a name="PriceOfPopularity"></a> The Price of Popularity</span></span>

<span data-ttu-id="e7b99-230">Как часто отображаются на странице?</span><span class="sxs-lookup"><span data-stu-id="e7b99-230">How often is your page viewed?</span></span> <span data-ttu-id="e7b99-231">В сценарии с классической корпоративной домашней страницы задано как страница запуска всех браузеров в организации.</span><span class="sxs-lookup"><span data-stu-id="e7b99-231">In the classic scenario, the corporate home page is set as the launch page for all browsers across the organization.</span></span> <span data-ttu-id="e7b99-232">Затем получите внезапно гораздо большее число трафика, чем когда-либо представить.</span><span class="sxs-lookup"><span data-stu-id="e7b99-232">Then you suddenly get far more traffic than you ever imagined.</span></span> <span data-ttu-id="e7b99-233">Каждый байт контента внезапно увеличивается на производительность сервера и пропускной способности, которые принимают домашней страницы.</span><span class="sxs-lookup"><span data-stu-id="e7b99-233">Every byte of content is suddenly magnified in the server performance and bandwidth that your home page consumes.</span></span>

<span data-ttu-id="e7b99-234">Решение: перейдите light на домашней странице и ссылка на другой контент.</span><span class="sxs-lookup"><span data-stu-id="e7b99-234">The solution: Go light on the home page and link to the other content.</span></span>

<span data-ttu-id="e7b99-235">Высокая интенсивность операций данных панелей мониторинга, также кандидата для приложения с размещением у поставщика, который можно масштабировать независимо друг от друга.</span><span class="sxs-lookup"><span data-stu-id="e7b99-235">Data-heavy dashboards are also a candidate for a provider hosted app which can scale independently.</span></span>

## <span data-ttu-id="e7b99-236"><a name="LoaderPattern"></a>Загрузчик шаблон</span><span class="sxs-lookup"><span data-stu-id="e7b99-236"><a name="LoaderPattern"></a> The Loader Pattern</span></span>

<span data-ttu-id="e7b99-237">Цель шаблон загрузчик — укажите способ внедрения неизвестное число удаленных скрипты в сайт без необходимости обновления сайта.</span><span class="sxs-lookup"><span data-stu-id="e7b99-237">The goal of the loader pattern is to provide a way to embed an unknown number of remote scripts into a site without having to update the site.</span></span> <span data-ttu-id="e7b99-238">Обновления можно выполнить на удаленных CDN и обновит все сайты.</span><span class="sxs-lookup"><span data-stu-id="e7b99-238">The updates can be done on the remote CDN and will update all sites.</span></span>

<span data-ttu-id="e7b99-239">Шаблон загрузчик создает URL-адрес с Отметка даты и времени в конце, чтобы файл не будут кэшироваться.</span><span class="sxs-lookup"><span data-stu-id="e7b99-239">The Loader Pattern constructs a URL with date and time stamp at the end so that the file will not be cached.</span></span> <span data-ttu-id="e7b99-240">Он устанавливает jQuery в качестве зависимость от файла загрузчик, а затем выполняет функцию в загрузчик.</span><span class="sxs-lookup"><span data-stu-id="e7b99-240">It sets up jQuery as a dependency on the loader file, then executes a function in the loader.</span></span> <span data-ttu-id="e7b99-241">Это гарантирует, что настраиваемый JavaScript будет загружен после завершения загрузки jQuery.</span><span class="sxs-lookup"><span data-stu-id="e7b99-241">This ensures your custom JavaScript will load after jQuery finishes loading.</span></span>

<span data-ttu-id="e7b99-242">PnP-dev\Samples\Core.JavaScript\Core.JavaScript.Embedder\Program.cs:</span><span class="sxs-lookup"><span data-stu-id="e7b99-242">PnP-dev\Samples\Core.JavaScript\Core.JavaScript.Embedder\Program.cs:</span></span>

```csharp
static void Main(string[] args)
{
    ContextManager.WithContext((context) =>
        // this is the script block that will be embedded into the page
        // in practice this can be done during provisioning of the site/web
        // make sure to include ';' at end to play nice with page embedding
        // using the script on demand feature built into SharePoint we load jQuery, then our remote loader(pnp-loader.js or pnp-loader-cached.js) file using a dependency
        var script = @"(function (loaderFile, nocache) {
                                var url = loaderFile + ((nocache) ? '?' + encodeURIComponent((new Date()).getTime()) : '');
                                SP.SOD.registerSod('pnp-jquery.js', 'https://localhost:44324/js/jquery.js');
                                SP.SOD.registerSod('pnp-loader.js', url);
                                SP.SOD.registerSodDep('pnp-loader.js', 'pnp-jquery.js');
                                SP.SOD.executeFunc('pnp-loader.js', null, function() {});
                        })('https://localhost:44324/pnp-loader.js', true);";


        // this version of the script along with pnp-loaderMDS.js (or pnp-loaderMDS-cached.js) handles pages where the minimum download strategy is active
        var script2 = @"ExecuteOrDelayUntilBodyLoaded(function () {
                            var url = 'https://localhost:44324/js/pnp-loaderMDS.js?' + encodeURIComponent((new Date()).getTime());
                            SP.SOD.registerSod('pnp-jquery.js', 'https://localhost:44324/js/jquery.js');
                            SP.SOD.registerSod('pnp-loader.js', url);
                            SP.SOD.registerSodDep('pnp-loader.js', 'pnp-jquery.js');
                            SP.SOD.executeFunc('pnp-loader.js', null, function () {
                                if (typeof pnpLoadFiles === 'undefined') {
                                    RegisterModuleInit('https://localhost:44324/js/pnp-loaderMDS.js', pnpLoadFiles);
                                } else {
                                    pnpLoadFiles();
                                }
                            });    
                        });";

        // load the collection of existing links
        var links = context.Site.RootWeb.UserCustomActions;
        context.Load(links, ls => ls.Include(l => l.Title));
        context.ExecuteQueryRetry();

        // this block handles deleting previous test custom actions
        var doDelete = false;

        foreach (var link in links.ToArray().Where(l => l.Title.Equals("MyTestCustomAction", StringComparison.OrdinalIgnoreCase)))
        {
            link.DeleteObject();
            doDelete = true;
        }

        if (doDelete)
        {
            context.ExecuteQueryRetry();
        }

        // now we embed our script into the user custom action
        var newLink = context.Site.RootWeb.UserCustomActions.Add();
        newLink.Title = "MyTestCustomAction";
        newLink.Description = "Doing some testing.";
        newLink.ScriptBlock = script2;
        newLink.Location = "ScriptLink";
        newLink.Update();
        context.ExecuteQueryRetry();
    });
}
```

<span data-ttu-id="e7b99-243">`SP.SOD.registerSodDep('pnp-loader.js', 'pnp-jquery.js');` Выполняет настройку зависимостей, и `SP.SOD.executeFunc('pnp-loader.js', null, function() {});` принудительно jQuery загрузится полностью перед загрузкой настраиваемый JavaScript.</span><span class="sxs-lookup"><span data-stu-id="e7b99-243">The `SP.SOD.registerSodDep('pnp-loader.js', 'pnp-jquery.js');` sets up the dependency, and `SP.SOD.executeFunc('pnp-loader.js', null, function() {});` forces jQuery to load completely before loading the custom JavaScript.</span></span>

<span data-ttu-id="e7b99-244">`newLink.ScriptBlock = script2;` И `newLink.Location = "ScriptLink";` основные части Добавление в действие клиента пользователя.</span><span class="sxs-lookup"><span data-stu-id="e7b99-244">The `newLink.ScriptBlock = script2;` and `newLink.Location = "ScriptLink";` are the key parts of adding this into the user customer action.</span></span>

<span data-ttu-id="e7b99-245">Файл pnp loader.js загружает список файлов JavaScript, с помощью резервирования, который может выполняться при загрузке каждого файла.</span><span class="sxs-lookup"><span data-stu-id="e7b99-245">The pnp-loader.js file then loads a list of JavaScript files, with a promise that can be run when each file loads.</span></span>

<span data-ttu-id="e7b99-246">PnP-dev\Samples\Core.JavaScript\Core.JavaScript.CDN\js\pnp-loader.js:</span><span class="sxs-lookup"><span data-stu-id="e7b99-246">PnP-dev\Samples\Core.JavaScript\Core.JavaScript.CDN\js\pnp-loader.js:</span></span>

```javascript
(function () {

    var urlbase = 'https://localhost:44324';
    var files = [
        '/js/pnp-settings.js',
        '/js/pnp-core.js',
        '/js/pnp-clientcache.js',
        '/js/pnp-config.js',
        '/js/pnp-logging.js',
        '/js/pnp-devdashboard.js',
        '/js/pnp-uimods.js'
    ];

    // create a promise
    var promise = $.Deferred();

    // this function will be used to recursively load all the files
    var engine = function () {

        // maintain context
        var self = this;

        // get the next file to load
        var file = self.files.shift();

        var fullPath = urlbase + file;

        // load the remote script file
        $.getScript(fullPath).done(function () {
            if (self.files.length > 0) {
                engine.call(self);
            }
            else {
                self.promise.resolve();
            }
        }).fail(self.promise.reject);
    };

    // create our "this" we will apply to the engine function
    var ctx = {
        files: files,
        promise: promise
    };

    // call the engine with our context
    engine.call(ctx);

    // give back the promise
    return promise.promise();

})().done(function () {
    /* all scripts are loaded and I could take actions here */
}).fail(function () {
    /* something failed, take some action here if needed */
});
```

<span data-ttu-id="e7b99-247">Файл pnp loader.js не кэш, который хорошо подходит для среды разработки.</span><span class="sxs-lookup"><span data-stu-id="e7b99-247">The pnp-loader.js file does not cache, which works well for a development environment.</span></span> <span data-ttu-id="e7b99-248">Заменяет файл pnp загрузчик cached.js `$.getScript` работать с `$.ajax` функция, которая позволяет для браузера кэширования файлов и лучше подходит для рабочей среды.</span><span class="sxs-lookup"><span data-stu-id="e7b99-248">The pnp-loader-cached.js file replaces the `$.getScript` function with an `$.ajax` function which allows for browser caching of the files and is better suited for production.</span></span>

<span data-ttu-id="e7b99-249">Из PnP-dev\Samples\Core.JavaScript\Core.JavaScript.CDN\js\pnp-loader.js</span><span class="sxs-lookup"><span data-stu-id="e7b99-249">From PnP-dev\Samples\Core.JavaScript\Core.JavaScript.CDN\js\pnp-loader.js</span></span>

```javascript
    // load the remote script file
    $.ajax({
        type: 'GET',
        url: fullPath,
        cache: true,
        dataType: 'script'
    }).done(function () {
        if (self.files.length > 0) {
            engine.call(self);
        }
        else {
            self.promise.resolve();
        }
    }).fail(self.promise.reject);
```

<span data-ttu-id="e7b99-250">Этот шаблон облегчает развертывание и обновление на сайты.</span><span class="sxs-lookup"><span data-stu-id="e7b99-250">This pattern eases deployment and updates to sites.</span></span> <span data-ttu-id="e7b99-251">Особенно полезен при развертывании или обновление на тысячи семейств веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="e7b99-251">It is especially useful when deploying or updating across thousands of site collections.</span></span>

## <span data-ttu-id="e7b99-252"><a name="CachingCurrentUserInfo"></a>Кэширование текущего пользователя</span><span class="sxs-lookup"><span data-stu-id="e7b99-252"><a name="CachingCurrentUserInfo"></a> Caching the current user</span></span>

<span data-ttu-id="e7b99-253">Если пользователь уже кэширования, эта функция получает данные из кэша сеанса.</span><span class="sxs-lookup"><span data-stu-id="e7b99-253">If the user info is already cached, this function gets the data from the session cache.</span></span> <span data-ttu-id="e7b99-254">Если сведения о пользователе хранится в кэше, получает данные определенного пользователя мы должны и сохраняет его в кэше.</span><span class="sxs-lookup"><span data-stu-id="e7b99-254">If the user info is not stored in the cache, it gets the specific user info we need and stores it in the cache.</span></span>

<span data-ttu-id="e7b99-255">Это также использует отложенный (версия jQuery promise).</span><span class="sxs-lookup"><span data-stu-id="e7b99-255">This also uses Deferred (jQuery version of promise).</span></span> <span data-ttu-id="e7b99-256">Если мы получить данные из кэша или с сервера, отложенный решена.</span><span class="sxs-lookup"><span data-stu-id="e7b99-256">If we get the data from the cache or from the server, the Deferred is resolved.</span></span> <span data-ttu-id="e7b99-257">Если ошибка, отложенный отклоняется.</span><span class="sxs-lookup"><span data-stu-id="e7b99-257">If there is an error, the Deferred is rejected.</span></span>

<span data-ttu-id="e7b99-258">Из PnP-dev\Samples\Core.JavaScript\Core.JavaScript.CDN\js\pnp-core.js:</span><span class="sxs-lookup"><span data-stu-id="e7b99-258">From PnP-dev\Samples\Core.JavaScript\Core.JavaScript.CDN\js\pnp-core.js:</span></span>

```javascript
    getCurrentUserInfo: function (ctx) {

        var self = this;

        if (self._currentUserInfoPromise == null) {

            self._currentUserInfoPromise = $.Deferred(function (def) {

                var cachingTest = $pnp.session !== 'undefined' && $pnp.session.enabled;

                // if we have the caching module loaded
                if (cachingTest) {
                    var userInfo = $pnp.session.get(self._currentUserInfoCacheKey);
                    if (userInfo !== null) {
                        self._currentUserInfo = userInfo;
                        def.resolveWith(ctx || self._currentUserInfo, [self._currentUserInfo]);
                        return;
                    }
                }

                // send the request and allow caching
                $.ajax({
                    method: 'GET',
                    url: '/_api/SP.UserProfiles.PeopleManager/GetMyProperties?$select=AccountName,DisplayName,Title',
                    headers: { "Accept": "application/json; odata=verbose" },
                    cache: true
                }).done(function (response) {

                    // we also parse and add some custom properties as an example
                    self._currentUserInfo = $.extend(response.d,
                        {
                            ParsedLoginName: $pnp.core.getUserIdFromLogin(response.d.AccountName)
                        });

                    if (cachingTest) {
                        $pnp.session.add(self._currentUserInfoCacheKey, self._currentUserInfo);
                    }

                    def.resolveWith(ctx || self._currentUserInfo, [self._currentUserInfo]);

                }).fail(function (jqXHR, textStatus, errorThrown) {

                    console.error('[PNP]=>[Fatal Error] Could not load current user data data from /_api/SP.UserProfiles.PeopleManager/GetMyProperties. status: ' + textStatus + ', error: ' + errorThrown);
                    def.rejectWith(ctx || null);
                });
            });
        }

        return this._currentUserInfoPromise.promise();
    }
}
```

## <span data-ttu-id="e7b99-259"><a name="CachingPatternUsingAsynchronousAndDeferred"></a>С помощью асинхронной и отложенная кэширования шаблона</span><span class="sxs-lookup"><span data-stu-id="e7b99-259"><a name="CachingPatternUsingAsynchronousAndDeferred"></a> Caching pattern using asynchronous and Deferred</span></span>

<span data-ttu-id="e7b99-260">Другой шаблон кэширования можно найти в storageTest pnp clientcache.js, который берет файлы из modernizer storageTest.</span><span class="sxs-lookup"><span data-stu-id="e7b99-260">Another caching pattern can be found in pnp-clientcache.js storageTest, which is taken from the modernizer storageTest.</span></span> <span data-ttu-id="e7b99-261">Он содержит функции для add, get, удаление и getOrAdd, который возвращает кэшированные данные, если он находится в кэше, или получение данных с сервера и добавить его в кэш, если он не в кэше, что позволяет экономить написание повторяющиеся кода в вызывающей функции.</span><span class="sxs-lookup"><span data-stu-id="e7b99-261">It contains functions for add, get, remove, and getOrAdd which will return the cached data if it's in the cache, or retrieve the data from the server and add it to the cache if it is not in the cache which saves writing repetitive code in the calling function.</span></span> <span data-ttu-id="e7b99-262">get используется JSON.parse для проверки истечения срока действия с момента истечение срока действия не является компонентом в локальном хранилище.</span><span class="sxs-lookup"><span data-stu-id="e7b99-262">get uses JSON.parse to test for expiration since expiration is not a feature in local storage.</span></span> <span data-ttu-id="e7b99-263">_createPersistable хранит объект JavaScript в кэше локального хранилища.</span><span class="sxs-lookup"><span data-stu-id="e7b99-263">_createPersistable stores the JavaScript object in the local storage cache.</span></span>

<span data-ttu-id="e7b99-264">Из PnP-dev\Samples\Core.JavaScript\Core.JavaScript.CDN\js\pnp-clientcache.js:</span><span class="sxs-lookup"><span data-stu-id="e7b99-264">From PnP-dev\Samples\Core.JavaScript\Core.JavaScript.CDN\js\pnp-clientcache.js:</span></span>

```javascript
// adds the client cache capability
caching: {

    // determine if we have local storage once
    enabled: storageTest(),

    add: function (/*string*/ key, /*object*/ value, /*datetime*/ expiration) {

        if (this.enabled) {
            localStorage.setItem(key, this._createPersistable(value, expiration));
        }
    },

    // gets an item from the cache, checking the expiration and removing the object if it is expired
    get: function (/*string*/ key) {

        if (!this.enabled) {
            return null;
        }

        var o = localStorage.getItem(key);

        if (o == null) {
            return o;
        }

        var persistable = JSON.parse(o);

        if (new Date(persistable.expiration) <= new Date()) {

            this.remove(key);
            o = null;

        } else {

            o = persistable.value;
        }

        return o;
    },

    // removes an item from local storage by key
    remove: function (/*string*/ key) {

        if (this.enabled) {
            localStorage.removeItem(key);
        }
    },

    // gets an item from the cache or adds it using the supplied getter function
    getOrAdd: function (/*string*/ key, /*function*/ getter) {

        if (!this.enabled) {
            return getter();
        }

        if (!$.isFunction(getter)) {
            throw 'Function expected for parameter "getter".';
        }

        var o = this.get(key);

        if (o == null) {
            o = getter();
            this.add(key, o);
        }

        return o;
    },

    // creates the persisted object wrapper using the value and the expiration, setting the default expiration if none is applied
    _createPersistable: function (/*object*/ o, /*datetime*/ expiration) {

        if (typeof expiration === 'undefined') {
            expiration = $pnp.core.dateAdd(new Date(), 'minute', $pnp.settings.localStorageDefaultTimeoutMinutes);
        }

        return JSON.stringify({
            value: o,
            expiration: expiration
        });
    }
},
```

<span data-ttu-id="e7b99-265">Для более сложного использования асинхронных и отложенный можно ссылаться на панели мониторинга разработчика в pnp clientcache.js</span><span class="sxs-lookup"><span data-stu-id="e7b99-265">For a more complex usage of asynchronous and Deferred, you can refer to the developer dashboard in pnp-clientcache.js</span></span>

## <span data-ttu-id="e7b99-266"><a name="Resources"></a>Ресурсы</span><span class="sxs-lookup"><span data-stu-id="e7b99-266"><a name="Resources"></a> Resources</span></span>

### <a name="see-also"></a><span data-ttu-id="e7b99-267">См. также:</span><span class="sxs-lookup"><span data-stu-id="e7b99-267">See Also</span></span>
- [<span data-ttu-id="e7b99-268">JavaScript — шаблоны и об использовании</span><span class="sxs-lookup"><span data-stu-id="e7b99-268">JavaScript – Patterns and Usage</span></span>](http://dev.office.com/blogs/javascript-development-patterns-with-sharepoint)
- [<span data-ttu-id="e7b99-269">JavaScript — рекомендации по производительности</span><span class="sxs-lookup"><span data-stu-id="e7b99-269">JavaScript – Performance Considerations</span></span>](http://dev.office.com/blogs/javascript-performance-considerations-with-sharepoint)
- [<span data-ttu-id="e7b99-270">Выполнение базовых операций с использованием кода библиотеки JavaScript в SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="e7b99-270">Complete basic operations using JavaScript library code in SharePoint 2013</span></span>](https://msdn.microsoft.com/EN-US/library/office/jj163201.aspx)
- [<span data-ttu-id="e7b99-271">Примеры кода обработки на стороне клиента (JS ссылка)</span><span class="sxs-lookup"><span data-stu-id="e7b99-271">Client-side rendering (JS Link) code samples</span></span>](https://code.msdn.microsoft.com/office/Client-side-rendering-JS-2ed3538a)
- [<span data-ttu-id="e7b99-272">Внедрение JavaScript (Настройка сайта SharePoint пользовательского интерфейса с помощью JavaScript)</span><span class="sxs-lookup"><span data-stu-id="e7b99-272">JavaScript Embedding (Customize your SharePoint site UI by using JavaScript)</span></span>](https://msdn.microsoft.com/EN-US/library/dn913116.aspx)
- [<span data-ttu-id="e7b99-273">Настройки поиска для SharePoint</span><span class="sxs-lookup"><span data-stu-id="e7b99-273">Search customizations for SharePoint</span></span>](https://msdn.microsoft.com/EN-US/library/mt210901.aspx)
- [<span data-ttu-id="e7b99-274">Надстройка SharePoint набора команд — тип настраиваемого поля (с помощью отображения со стороны клиента)</span><span class="sxs-lookup"><span data-stu-id="e7b99-274">SharePoint Add-in Recipe – Custom field type (by using Client Side Rendering)</span></span>](custom-field-type-sharepoint-add-in.md)

### <a name="samples"></a><span data-ttu-id="e7b99-275">Примеры</span><span class="sxs-lookup"><span data-stu-id="e7b99-275">Samples</span></span>

- [<span data-ttu-id="e7b99-276">Performance.Caching</span><span class="sxs-lookup"><span data-stu-id="e7b99-276">Performance.Caching</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Performance.Caching)
- [<span data-ttu-id="e7b99-277">Core.JavaScript</span><span class="sxs-lookup"><span data-stu-id="e7b99-277">Core.JavaScript</span></span>](https://github.com/SharePoint/Pnp/tree/master/Samples/Core.JavaScript)
