---
title: "Улучшения производительности в SharePoint размещение у поставщика в надстройках"
ms.date: 11/03/2017
ms.openlocfilehash: d876d0a14eebdcef940c6d22997f96182b51af28
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="improve-performance-in-sharepoint-provider-hosted-add-ins"></a><span data-ttu-id="384c3-102">Улучшения производительности в SharePoint размещение у поставщика в надстройках</span><span class="sxs-lookup"><span data-stu-id="384c3-102">Improve performance in SharePoint provider-hosted add-ins</span></span>

<span data-ttu-id="384c3-103">Повышение быстродействия SharePoint размещение у поставщика в надстройке, ограничив число удаленных вызовов.</span><span class="sxs-lookup"><span data-stu-id="384c3-103">Improve the performance of your SharePoint provider-hosted add-in by limiting remote calls.</span></span>

<span data-ttu-id="384c3-104">_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="384c3-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="384c3-105">Можно повысить производительность SharePoint размещение у поставщика в надстройке, ограничение числа и частоту удаленных вызовов в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="384c3-105">You can improve the performance of your SharePoint provider-hosted add-in by limiting the number and frequency of remote calls to SharePoint.</span></span> <span data-ttu-id="384c3-106">Слишком большого числа звонков на сайт узла снижает производительность.</span><span class="sxs-lookup"><span data-stu-id="384c3-106">Too many calls to the host site degrades performance.</span></span> <span data-ttu-id="384c3-107">Чтобы ограничить количество удаленных вызовов, вы можете реализовать файлы cookie HTTP или локальное хранилище HTML5.</span><span class="sxs-lookup"><span data-stu-id="384c3-107">To limit the number of remote calls, you can implement either HTTP cookies or HTML5 local storage.</span></span>

<span data-ttu-id="384c3-108">Пример [Performance.Caching](https://github.com/SharePoint/PnP/tree/dev/Samples/Performance.Caching) показано, как использовать файлы cookie HTTP и локальное хранилище HTML5 для кэширования данных.</span><span class="sxs-lookup"><span data-stu-id="384c3-108">The [Performance.Caching](https://github.com/SharePoint/PnP/tree/dev/Samples/Performance.Caching) sample shows you how to use HTTP cookies and HTML5 local storage to cache data.</span></span> <span data-ttu-id="384c3-109">Пример включает два размещением у поставщика надстроек, которые позволяют просматривать **Сведения обо мне** разделе своего профиля пользователя, добавление данных и сохраните его для более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="384c3-109">The sample includes two provider-hosted add-ins that allow you to view the **About Me** section of your user profile, add data, and save it for later.</span></span> <span data-ttu-id="384c3-110">Надстройка не обновляет сведения о профилях пользователей; он кэширует его, чтобы можно было использовать более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="384c3-110">The add-in does not update user profile information; it caches it so that it can be used later.</span></span> <span data-ttu-id="384c3-111">Один пример использует файлы cookie HTTP для кэширования данных, а другое локальное хранилище HTML5.</span><span class="sxs-lookup"><span data-stu-id="384c3-111">One sample uses HTTP cookies to cache the data, and the other uses HTML5 local storage.</span></span>

## <a name="use-http-cookies-for-caching"></a><span data-ttu-id="384c3-112">Использование файлов cookie HTTP для кэширования</span><span class="sxs-lookup"><span data-stu-id="384c3-112">Use HTTP cookies for caching</span></span>

<span data-ttu-id="384c3-113">Начальной странице пример cookie HTTP сведения из раздела **Сведения обо мне** своего профиля пользователя в текстовом поле.</span><span class="sxs-lookup"><span data-stu-id="384c3-113">The start page of the HTTP cookie sample displays information from the  **About Me** section of your user profile in a text box.</span></span> <span data-ttu-id="384c3-114">Вторым текстовым полем вы найдете ли был создан новый файл cookie и истечения срока действия существующего файла cookie.</span><span class="sxs-lookup"><span data-stu-id="384c3-114">A second text box tells you whether a new cookie was created and when the existing cookie will expire.</span></span> <span data-ttu-id="384c3-115">Данные, хранящиеся в файлах cookie не должен превышать 4095 байт.</span><span class="sxs-lookup"><span data-stu-id="384c3-115">The information stored in cookies can't be larger than 4095 bytes.</span></span>

<span data-ttu-id="384c3-116">**На рисунке 1. В файл cookie HTTP, кэширование образца данных**</span><span class="sxs-lookup"><span data-stu-id="384c3-116">**Figure 1. Data rendered in the HTTP cookie caching sample**</span></span>

![В файл cookie HTTP, кэширование образца данных](media/improve-performance-in-sharepoint-provider-hosted-add-ins/c9427295-4242-48df-9aa8-392b58d7f4c6.png)

<span data-ttu-id="384c3-118">Файл app.js, который находится в папке Scripts веб-проекта, определяет поведение кнопки **Сохранить для последующих операций** .</span><span class="sxs-lookup"><span data-stu-id="384c3-118">The app.js file, which is located in the Scripts folder of the web project, defines the behavior of the  **Save for later** button.</span></span> <span data-ttu-id="384c3-119">Код сначала проверяет, что файлы Cookie включены в браузере, задав cookie тестовых.</span><span class="sxs-lookup"><span data-stu-id="384c3-119">The code first verifies that cookies are enabled in the browser by setting a test cookie.</span></span> <span data-ttu-id="384c3-120">Если включены файлы cookie, код определяет ли сведения о профиле пользователя уже хранятся в файлах cookie.</span><span class="sxs-lookup"><span data-stu-id="384c3-120">If cookies are enabled, the code determines whether the user profile information is already stored in a cookie.</span></span> <span data-ttu-id="384c3-121">В противном случае используется JSON для поиска сведений **Обо мне** , сохраните ее в файле cookie и затем отобразить сведения в браузере.</span><span class="sxs-lookup"><span data-stu-id="384c3-121">If it isn't, it uses JSON to look up the **About Me** information, store it in a cookie, and then display the information in the browser.</span></span>

<span data-ttu-id="384c3-122">Следующая функция задает файл cookie и его срок действия.</span><span class="sxs-lookup"><span data-stu-id="384c3-122">The following function sets the cookie and its expiration date.</span></span>

```c#
function setCookie(key, value, expiry, path, domain, secure) {
    var todaysDate = new Date();
    todaysDate.setTime(todaysDate.getTime());

    if (expiry == "") { expiry = "1"; }

    // The following line sets for n number of days. For hours, remove * 24. For minutes, remove * 60 * 24.
    if (expiry) {
        expiry = expiry * 1000 * 60 * 60 * 24;
    }

    var newExpiry = new Date(todaysDate.getTime() + (expiry));

    document.cookie = key + "=" + escape(value) +
        ( ( expiry ) ? ";expires=" + newExpiry : "" ) +
        ( ( path ) ? ";path=" + path : "" ) +
        ( ( domain ) ? ";domain=" + domain : "" ) +
        ((secure) ? ";secure" : "");

    cachingStatus += "\n" + "Creating http cookie for AboutMe data...";
    cachingStatus += "\n" + "Cookie will expire " + newExpiry;
    $('#status').text(cachingStatus);
}

```

## <a name="use-html5-local-storage-for-caching"></a><span data-ttu-id="384c3-123">Использовать локальное хранилище HTML5 для кэширования</span><span class="sxs-lookup"><span data-stu-id="384c3-123">Use HTML5 local storage for caching</span></span>

<span data-ttu-id="384c3-124">Начальной странице пример локальное хранилище HTML5 сведения из раздела **Сведения обо мне** сведений профиля пользователя о кэшированных данных.</span><span class="sxs-lookup"><span data-stu-id="384c3-124">The start page of the HTML5 local storage sample displays information from the  **About Me** section of your user profile information about the cached data.</span></span> <span data-ttu-id="384c3-125">Текстовое поле отображает эти сведения, а также время истечения срока действия (при его наличии) кэшированные данные.</span><span class="sxs-lookup"><span data-stu-id="384c3-125">The text box displays this information as well as the expiration time (if any) of the cached information.</span></span>

<span data-ttu-id="384c3-126">**На рисунке 2. Данные, отображаемые в локальном хранилище HTML 5, кэширование пример** файл app.js, который находится в папке Scripts веб-проекта, определяет поведение кнопки **Сохранить для последующих операций** .</span><span class="sxs-lookup"><span data-stu-id="384c3-126">**Figure 2. Data rendered in the HTML 5 local storage caching sample** The app.js file, which is located in the Scripts folder of the web project, defines the behavior of the  **Save for later** button.</span></span> <span data-ttu-id="384c3-127">Надстройка сначала проверяет, что локальное хранилище включено, используя следующую функцию.</span><span class="sxs-lookup"><span data-stu-id="384c3-127">The add-in first verifies that local storage is enabled by using the following function.</span></span>

```c#
isHtml5StorageSupported = function () {
    try {
        return 'localStorage' in window &amp;&amp; window['localStorage'] !== null;
    } catch (e) {
        return false;
    }
    return false;
}

```

<span data-ttu-id="384c3-128">Если поддерживается локальное хранилище, функция определяет, будет ли сведения о профиле пользователя уже имеется.</span><span class="sxs-lookup"><span data-stu-id="384c3-128">If local storage is supported, the function determines whether the user profile information is already stored there.</span></span> <span data-ttu-id="384c3-129">В противном случае JSOM используется для поиска **Сведения обо мне** информации, для хранения локально, а затем для отображения информации в браузере.</span><span class="sxs-lookup"><span data-stu-id="384c3-129">If it isn't, it uses JSOM to look up the  **About Me** information, to store it locally, and then to display the information in the browser.</span></span> <span data-ttu-id="384c3-130">Приведенный ниже код хранятся сведения **Обо мне** в раздел с именем «aboutMeValue».</span><span class="sxs-lookup"><span data-stu-id="384c3-130">The following code stores the **About Me** information in a key named "aboutMeValue".</span></span>

```c#
var aboutMeValue = personProperties.get_userProfileProperties()['AboutMe'];
    $('#aboutMeText').val(aboutMeValue);

    // Add to local storage.
    localStorage.setItem("aboutMeValue", aboutMeValue);
    setLocalStorageKeyExpiry("aboutMeValue");

    cachingStatus += "\n" + "Populated local storage with profile properties...";
    $('#status').val(cachingStatus);

```

<span data-ttu-id="384c3-131">Кнопка **Очистить кэш** удаляет этого ключа, ищет сведения **Обо мне** в профиле пользователя и создает ключ новым дискового пространства для хранения этих сведений.</span><span class="sxs-lookup"><span data-stu-id="384c3-131">The  **Clear the cache** button removes that key, looks up the **About Me** information in your user profile, and creates a fresh local storage key to store that information.</span></span> <span data-ttu-id="384c3-132">Надстройка не ограничен сроком действия по умолчанию значение, но файл app.js содержит следующие функции, которая задает срок действия кэширования данных.</span><span class="sxs-lookup"><span data-stu-id="384c3-132">The add-in doesn't set an expiration time by default, but the app.js file does contain the following function, which sets an expiration time for the cached data.</span></span>

```c#
function setLocalStorageKeyExpiry(key) {

    // Check for expiration config values.
    var expiryConfig = localStorage.getItem(expiryConfigKey);
    
    // Check for existing expiration stamp.
    var existingStamp = localStorage.getItem(key + expiryKeySuffix);    

    // Override cached setting if a user has entered a value that is different than what is stored.
    if (expiryConfig != null) {
                
        var currentTime = Math.floor((new Date().getTime()) / 1000);
        expiryConfig = parseInt(expiryConfig);
        
        var newStamp = Math.floor((currentTime + expiryConfig));
        localStorage.setItem(key + expiryKeySuffix, newStamp);
        
        // Log status to window.        
        cachingStatus += "\n" + "Setting expiration for the " + key + " key...";
        $('#status').val(cachingStatus);
    }    
    else {
       
    }
}

```

<span data-ttu-id="384c3-133">Прежде чем ищете информацию, содержащуюся в ключ локального хранилища, используется код, **isKeyExpired** работать определить истек срок действия ключа.</span><span class="sxs-lookup"><span data-stu-id="384c3-133">Before looking for the information stored in the local storage key, the code uses the  **isKeyExpired** function to determine whether the key is expired.</span></span> <span data-ttu-id="384c3-134">Дополнительные сведения содержатся в разделе [Настройка пользовательского интерфейса с помощью SharePoint у поставщика надстроек](customize-the-ux-by-using-sharepoint-provider-hosted-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="384c3-134">For more information, see [Customize the UX by using SharePoint provider-hosted add-ins](customize-the-ux-by-using-sharepoint-provider-hosted-add-ins.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="384c3-135">См. также</span><span class="sxs-lookup"><span data-stu-id="384c3-135">See also</span></span>
<span data-ttu-id="384c3-136"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="384c3-136"></span></span>

- [<span data-ttu-id="384c3-137">Компоненты взаимодействия с пользователями в SharePoint 2013 и SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="384c3-137">UX Components in SharePoint 2013 and SharePoint Online</span></span>](ux-components-in-sharepoint-2013-and-sharepoint-online.md)
    
- [<span data-ttu-id="384c3-138">Настройка интерфейса пользователя с помощью SharePoint у поставщика надстроек</span><span class="sxs-lookup"><span data-stu-id="384c3-138">Customize the UX by using SharePoint provider-hosted add-ins</span></span>](customize-the-ux-by-using-sharepoint-provider-hosted-add-ins.md)
    
- [<span data-ttu-id="384c3-139">Branding.UIElementPersonalization</span><span class="sxs-lookup"><span data-stu-id="384c3-139">Branding.UIElementPersonalization</span></span>](https://github.com/SharePoint/PnP/tree/dev/Samples/Branding.UIElementPersonalization)
    
- [<span data-ttu-id="384c3-140">Performance.Caching</span><span class="sxs-lookup"><span data-stu-id="384c3-140">Performance.Caching</span></span>](https://github.com/SharePoint/PnP/tree/dev/Samples/Performance.Caching)
