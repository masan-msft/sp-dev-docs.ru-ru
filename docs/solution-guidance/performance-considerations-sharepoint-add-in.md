---
title: "Рекомендации по производительности в объектная модель SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 1a7313fd7b8c783268b54ef1ecb06f2e06fb8b44
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
<a name="performance-considerations-in-the-sharepoint-add-in-model"></a>Рекомендации по производительности в объектная модель SharePoint
=========================================================

<a name="summary"></a>Summary
-------

Подходы потребоваться убедитесь, что оптимальной производительности с помощью SharePoint отличается в новой модели надстройки SharePoint не был с кодом полного доверия. В типичных полного доверия кода (FTC) / сценарий решения фермы большинство операций кода выполнялись в объектной модели SharePoint серверного кода.

В SharePoint надстройки модели сценарии объектную модель SharePoint на стороне клиента (CSOM) и/или интерфейса API REST SharePoint используются для выполнения кода.

Основное различие между двумя моделями — серверный код и код на стороне клиента. В модели надстройки SharePoint так как код выполняется с помощью клиентов, возникает дополнительные сетевого трафика.  Минимизации количества вызов API циклами на сервере SharePoint будет повышения производительности из вашего SharePoint надстройки и сократить объем ресурсов, затрачиваемых сайта SharePoint.

Кроме того в модели надстройки SharePoint, так как код выполняется с помощью клиентов может быть задержки перед получен ответ. Кэширование данных для длительной операции (например, API профилей пользователей) могут сократить время, необходимое для возврата информации или получения подтверждения процесс завершен.

<a name="high-level-guidelines"></a>Рекомендации по высокого уровня
---------------------

Как правило эскиз мы предлагаем для обеспечения высокого уровня следующие рекомендации для обеспечения оптимальной производительности с помощью SharePoint в новой модели надстройки SharePoint.

- Минимизация вызовов API со стороны клиента к серверу SharePoint.
- Используйте методы кэширования на сервере и со стороны клиента для хранения сведений.
- Не рекомендуется хранить clientIDs clientSecrets, имена пользователей, пароли, маркеры и другие конфиденциальные данные в кэш.

<a name="options-to-ensure-optimal-performance-with-sharepoint"></a>Параметры, чтобы гарантировать их оптимальную работу с SharePoint
-----------------------------------------------------
У вас есть две возможности для обеспечения оптимальной производительности с помощью SharePoint.

- Используйте кэширование на стороне клиента 
- Используйте кэширование на сервере 

<a name="use-client-side-caching"></a>Используйте кэширование на стороне клиента 
-----------------------
В этом шаблоне методы кэширования со стороны клиента, такие как HTML5 LocalStorage и файлы cookie используются для кэширования данных. Данные, хранящиеся в этих расположениях используется для определения, если это необходимо выполнять вызовы API SharePoint server.

- Этот шаблон хранит данные, возвращаемые из вызовов SharePoint API в кэш со стороны клиента.
- Этот шаблон используется код на стороне клиента (JavaScript) для оценки данных, хранящихся в кэш со стороны клиента.
- Файлы cookie не более хранения 4095 объем данных в байтах.
    + Файлы cookie имеют механизм истечение срока действия встроенных данных.
- HTML5 LocalStorage не более 5 МБ данных.
    - HTML5 LocalStorage не имеет механизм истечение срока действия встроенных данных. Тем не менее такой механизм истечение срока действия может быть быстро и легко реализованы в JavaScript.
    
        В разделе функции **setLocalStorageKeyExpiry** и **isLocalStorageExpired** в [файл App.js JavaScript](https://github.com/SharePoint/PnP/blob/master/Samples/Performance.Caching/Performance.LocalStorage/Scripts/App.js) в [Performance.LocalStorage (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Performance.Caching/Performance.LocalStorage) в качестве примера.

        **Установка ключа истечение срока действия в LocalStorage:**

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

        **Проверьте, если ключ истечение срока действия срока действия в LocalStorage:**
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

**Когда это подходит?**

Когда следует использовать API модели объектов SharePoint ECMA со стороны клиента (sp.js) и оценить данные со стороны клиента, чтобы определить необходимо осуществлять вызовы API.

**Приступая к работе**

[Performance.Caching (PnP образец O365)](https://github.com/SharePoint/PnP/tree/master/Samples/Performance.Caching) демонстрируется, как реализовать LocalStorage и на основе файлов cookie со стороны клиента, кэширование в модели надстройки и предоставляет ссылки на другие статьи и примеры.

<a name="use-server-side-caching"></a>Используйте кэширование на сервере 
-----------------------
В этом шаблоне методы кэширования на сервере, такие как оценки файла cookie сеанса и на сервере используются для доступа к кэшированным данным. Данные, хранящиеся в этих расположениях используется для определения, если это необходимо выполнять вызовы API SharePoint server.

- Этот шаблон хранит данные, возвращаемые из вызовов SharePoint API в кэш на сервере.    
- Этот шаблон используется код на стороне сервера для оценки данных, сохраненных в расположений на сервере.
    + Расположений на сервере могут содержать данных на основе сеанса, хранимые в оперативной памяти или других сторонних производителей на стороне сервера кэширования технологий кэшируется на сервере.
- Этот шаблон используется код на стороне сервера для оценки данных, сохраненных в файлах cookie.
- Файлы cookie не более хранения 4095 объем данных в байтах.
    + Файлы cookie имеют механизм истечение срока действия встроенных данных.
    
    В разделе **CookieCheckSkip** метода в [Класс Customizer.aspx.cs](https://github.com/SharePoint/PnP/blob/master/Solutions/OD4B.Configuration.Async/OD4B.Configuration.AsyncWeb/Pages/Customizer.aspx.cs) в [OD4B. Configuration.Async (PnP образец O365)](https://github.com/SharePoint/PnP/tree/master/Solutions/OD4B.Configuration.Async) для просмотра кода на стороне сервера используется для оценки файлы cookie.

**Реализация уровень кэша «атаки третьего»** В некоторых случаях имеет смысл создать собственный уровень пользовательского кэша. Хороший пример — Если вам необходимо получить сведения из профиля пользователя. API-интерфейсы профилей пользователей в некоторых случаях уйти много времени на выполнение. Чтобы предоставить конечным пользователям быстро пользовательский интерфейс, можно создать задания таймера удаленного для запроса службы профилей пользователей и сохранения данных в различных хранилищ данных. Затем можно создать службы обеспечивает возможность запроса хранит данные через JavaScript вызовы из SharePoint надстройки.  

Azure доступно множество различных механизмов хранения, которые могут использоваться для хранения сведений, многие из которых очень быстро выполнять как хранение таблицы и хранилища больших двоичных объектов. Azure также можно создать веб-приложение для размещения службы и обеспечения безопасности, все данные и службы с помощью одной Azure Active Directory как клиента Office 365 SharePoint или даже среде SharePoint в локальной с поддержкой DirSync.

**Когда это подходит?**

- Когда следует использовать API модели объектов SharePoint управляемого кода на стороне клиента (Microsoft.SharePoint.Client.dll) и оценки данных на сервере или файлы cookie, чтобы определить необходимо осуществлять вызовы API.
- При наличии длительных операций, таких как Azure Web задания, которое должно быть инициирована только один раз в заданном интервал времени, независимо от того, как количество раз пользователь пытается инициировать операцию.  
    + Применение настроенной OneDrive для бизнеса конфигураций являются хорошим примером такого сценария.

**Приступая к работе**

[Performance.Caching (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Performance.Caching) описывается, как реализовать LocalStorage и на основе файлов cookie со стороны клиента, кэширование в модели надстройки и предоставляет ссылки на другие статьи и примеры.

<a name="related-links"></a>Ссылки по теме
=============
- Руководств по [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Руководств")
- Справочные материалы в библиотеке MSDN по [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Справочные материалы в библиотеке MSDN")
- Видеозаписи по [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "видео")

<a name="related-pnp-samples"></a>Примеры связанных с ними PnP
===================

- Примеры и содержимое в [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)

<a name="applies-to"></a>Применимо к
==========
- Office 365 нескольких клиентов (MT)
- Office 365 выделенных (D)
- SharePoint 2013 в локальной
