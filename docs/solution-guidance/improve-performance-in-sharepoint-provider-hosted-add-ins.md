---
title: "Улучшения производительности в SharePoint размещение у поставщика в надстройках"
ms.date: 11/03/2017
ms.openlocfilehash: d876d0a14eebdcef940c6d22997f96182b51af28
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="improve-performance-in-sharepoint-provider-hosted-add-ins"></a>Улучшения производительности в SharePoint размещение у поставщика в надстройках

Повышение быстродействия SharePoint размещение у поставщика в надстройке, ограничив число удаленных вызовов.

_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_

Можно повысить производительность SharePoint размещение у поставщика в надстройке, ограничение числа и частоту удаленных вызовов в SharePoint. Слишком большого числа звонков на сайт узла снижает производительность. Чтобы ограничить количество удаленных вызовов, вы можете реализовать файлы cookie HTTP или локальное хранилище HTML5.

Пример [Performance.Caching](https://github.com/SharePoint/PnP/tree/dev/Samples/Performance.Caching) показано, как использовать файлы cookie HTTP и локальное хранилище HTML5 для кэширования данных. Пример включает два размещением у поставщика надстроек, которые позволяют просматривать **Сведения обо мне** разделе своего профиля пользователя, добавление данных и сохраните его для более поздней версии. Надстройка не обновляет сведения о профилях пользователей; он кэширует его, чтобы можно было использовать более поздней версии. Один пример использует файлы cookie HTTP для кэширования данных, а другое локальное хранилище HTML5.

## <a name="use-http-cookies-for-caching"></a>Использование файлов cookie HTTP для кэширования

Начальной странице пример cookie HTTP сведения из раздела **Сведения обо мне** своего профиля пользователя в текстовом поле. Вторым текстовым полем вы найдете ли был создан новый файл cookie и истечения срока действия существующего файла cookie. Данные, хранящиеся в файлах cookie не должен превышать 4095 байт.

**На рисунке 1. В файл cookie HTTP, кэширование образца данных**

![В файл cookie HTTP, кэширование образца данных](media/improve-performance-in-sharepoint-provider-hosted-add-ins/c9427295-4242-48df-9aa8-392b58d7f4c6.png)

Файл app.js, который находится в папке Scripts веб-проекта, определяет поведение кнопки **Сохранить для последующих операций** . Код сначала проверяет, что файлы Cookie включены в браузере, задав cookie тестовых. Если включены файлы cookie, код определяет ли сведения о профиле пользователя уже хранятся в файлах cookie. В противном случае используется JSON для поиска сведений **Обо мне** , сохраните ее в файле cookie и затем отобразить сведения в браузере.

Следующая функция задает файл cookie и его срок действия.

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

## <a name="use-html5-local-storage-for-caching"></a>Использовать локальное хранилище HTML5 для кэширования

Начальной странице пример локальное хранилище HTML5 сведения из раздела **Сведения обо мне** сведений профиля пользователя о кэшированных данных. Текстовое поле отображает эти сведения, а также время истечения срока действия (при его наличии) кэшированные данные.

**На рисунке 2. Данные, отображаемые в локальном хранилище HTML 5, кэширование пример** файл app.js, который находится в папке Scripts веб-проекта, определяет поведение кнопки **Сохранить для последующих операций** . Надстройка сначала проверяет, что локальное хранилище включено, используя следующую функцию.

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

Если поддерживается локальное хранилище, функция определяет, будет ли сведения о профиле пользователя уже имеется. В противном случае JSOM используется для поиска **Сведения обо мне** информации, для хранения локально, а затем для отображения информации в браузере. Приведенный ниже код хранятся сведения **Обо мне** в раздел с именем «aboutMeValue».

```c#
var aboutMeValue = personProperties.get_userProfileProperties()['AboutMe'];
    $('#aboutMeText').val(aboutMeValue);

    // Add to local storage.
    localStorage.setItem("aboutMeValue", aboutMeValue);
    setLocalStorageKeyExpiry("aboutMeValue");

    cachingStatus += "\n" + "Populated local storage with profile properties...";
    $('#status').val(cachingStatus);

```

Кнопка **Очистить кэш** удаляет этого ключа, ищет сведения **Обо мне** в профиле пользователя и создает ключ новым дискового пространства для хранения этих сведений. Надстройка не ограничен сроком действия по умолчанию значение, но файл app.js содержит следующие функции, которая задает срок действия кэширования данных.

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

Прежде чем ищете информацию, содержащуюся в ключ локального хранилища, используется код, **isKeyExpired** работать определить истек срок действия ключа. Дополнительные сведения содержатся в разделе [Настройка пользовательского интерфейса с помощью SharePoint у поставщика надстроек](customize-the-ux-by-using-sharepoint-provider-hosted-add-ins.md).

## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>

- [Компоненты взаимодействия с пользователями в SharePoint 2013 и SharePoint Online](ux-components-in-sharepoint-2013-and-sharepoint-online.md)
    
- [Настройка интерфейса пользователя с помощью SharePoint у поставщика надстроек](customize-the-ux-by-using-sharepoint-provider-hosted-add-ins.md)
    
- [Branding.UIElementPersonalization](https://github.com/SharePoint/PnP/tree/dev/Samples/Branding.UIElementPersonalization)
    
- [Performance.Caching](https://github.com/SharePoint/PnP/tree/dev/Samples/Performance.Caching)
