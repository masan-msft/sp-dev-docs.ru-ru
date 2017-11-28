---
title: "Шаблоны JavaScript и производительности"
ms.date: 11/03/2017
ms.openlocfilehash: d9f125657f65da7da770e36e7c1c314759a05c29
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="javascript-patterns-and-performance"></a>Шаблоны JavaScript и производительности

Лет назад ASP.NET мы получили визуализации для элемента управления пользовательского интерфейса на сервере, и была хороший. Тем не менее, что на сервере визуализации, требуется код с полным доверием. Теперь, когда мы выполнившим переход к SharePoint и Office 365, код с полным доверием больше не вариант. Это означает, что отображение элемента управления пользовательского интерфейса на сервере, не будут работать для нас больше.

Еще бизнеса по-прежнему требуются специальные функциональные возможности пользовательского интерфейса для своих веб-сайтов и приложений. Это означает, что пользовательские функции пользовательского интерфейса должны быть перемещены на стороне сервера со стороны клиента. 

JavaScript на стороне клиента теперь является лучшим выбором для отображения элемента управления пользовательского интерфейса.

## <a name="JavaScriptPatterns"></a>Шаблоны JavaScript

Поскольку JavaScript на стороне клиента — это путь, что такое лучшие способы реализации JavaScript на стороне клиента Как одно приступить к работе?

Существует несколько вариантов:

|Параметр|Описание|
|:---|:---|
|Внедрение JavaScript | [Site.UserCustomActions](https://msdn.microsoft.com/EN-US/library/office/microsoft.sharepoint.client.site.usercustomactions.aspx) или [Web.UserCustomActions](https://msdn.microsoft.com/EN-US/library/office/microsoft.sharepoint.client.web.usercustomactions.aspx) разрешить для включения сценария непосредственно в разметке страницы. Используется в [Шаблон загрузчик](#LoaderPattern) , описанные ниже|
|Шаблоны отображения | Применяется для представления и поиска. У вас нет развертывание любого типа приложения или поставщик размещенных кода. Это просто файл JavaScript, которые могут быть загружены в (например) библиотеку стилей для настройки представления. Можно создать любое представление, необходимо с помощью JavaScript|
|Надстройки размещением в SharePoint | С помощью JSOM осуществляющих обратную связь с веб-узла или добавить в веб-сайта. Предоставляет доступ к веб-прокси для кросс-доменнные запросы|
|Надстройки размещением у поставщика | Позволяет создавать сложные приложения в различных стеки технологии - без снижения безопасности интеграции с SharePoint|
|JSLink | Позволяет загрузить один или несколько файлов JavaScript в веб-части OOTB и представлений|
|ScriptEditor веб-части | Включить сценарий напрямую или загрузки через теги скрипта разметку для создания сложных одной страницы приложений, размещенных полностью на сайте SharePoint|

Кажется, что вы фиксируются в эти варианты выбора, если ваш взгляд другой параметр бы лучше подходит для вашей ситуации. 

## <a name="JavaScriptPerformance"></a>Производительность JavaScript

На каждом этапе процесса разработки важно помнить о производительности. Вот несколько вещей, которые делают разница в производительности JavaScript.

|Параметр|Описание|
|:---|:---|
|[Уменьшите количество запросов](#ReduceTheNumberOfRequests) | Меньшее число запросов означает, что меньшего числа обращений к серверу, уменьшение задержки.|
|[Извлечение необходимых данных](#RetrieveOnlyTheDataYouNeed) | Уменьшение объема данных, передаваемых по сети. Также снижает нагрузку на сервер.|
|[Предоставляют возможности нагрузки хороший страницы](#ProvideAGoodUserExperience) | Сохранение пользовательского интерфейса реагирует на пользователя. Например, обновить меню на страницу *до* начала загрузки 100 записей.|
|[Использование асинхронных вызовов и шаблоны, по возможности](#EverythingIsAsynchronous) | Опрос — весом нагрузку на производительность, чем использование асинхронного вызова или обратного вызова.| 
|[Кэширование — ключ](#ClientSideCaching) | При проведении улучшения производительности дальнейшей кэширование сократить расходы на сервере.|
|[Подготовка к более просмотров страниц, чем когда-либо представить](#PriceOfPopularity) | Высокая интенсивность операций данных целевая страница допустимо при наличии нескольких совпадений. Однако при получении тысяч обращений, действительно можно повысить производительность.|

## <a name="WhatIsMyCodeDoing"></a>Каким образом код

Для повышения производительности важно знать, каким образом кода в любой момент. Это позволяет определить способы повышения эффективности работы. Ниже приведены несколько способов хороший делать это.

### <a name="ReduceTheNumberOfRequests"></a>Уменьшите количество запросов

Всегда позволяют наименьшее и наименьшее запросов. Каждого запроса, то исключить сократить расходы производительности на сервере и на клиенте. И запрашивать доступ меньшего размера дальнейшей снижает нагрузку производительности.

Существует несколько способов сократить количество запросов и уменьшения размера запроса.

- Максимальное число файлов JavaScript в рабочей среде. Отделение файлов JavaScript работает подходят для разработки, но не так и для рабочей среды. Объединение файлов JavaScript в единый файл JavaScript, а также некоторые файлы JavaScript, как.
- Уменьшить размеры файлов. Минимизация файлов JavaScript рабочей путем удаления разрывов, пробелов и комментарии. Существует несколько JavaScript minify программы и веб-сайты, которые можно использовать для значительно уменьшает размер файлов JavaScript.
- Используйте кэширование файлов браузера, чтобы уменьшить запросов. Обновленный [Шаблон загрузчик](#LoaderPattern) ниже — это удобный способ разверните узел при этом представление.

### < имя «RetrieveOnlyTheDataYouNeed» ></a> извлечения только необходимых данных

При запросе данных, не забудьте специализация запросов на самом деле требуется. Загрузка всей статьи для получения заголовок, например, приведет к снижению производительности довольно.

- Используйте фильтрацию сервера, выберите и ограничения для сведения к минимуму трафика по сети.
- Не запрашивать все статьи, если необходимо использовать только первые пять, в качестве другого примера.
- Больше не задавать для контейнера всей свойств, если вы хотите, чтобы только одно свойство. В один пример сценария требуется только одно свойство, но запрошено контейнер всей свойств, которая оказалась 800 КБ. Также следует помните, что размер объекта могут изменяться, так что такое только несколько килобайт теперь могут стать МБ далее в жизненном цикле продукта. 

### <a name="DontRequestDataYouWillDiscard"></a>Не запрашивать данные, что будут потеряны неиспользуемых

При извлечении данных, можно было использовать речь идет о возможность лучше фильтрации исходного запроса. 

- Запросите поля, которые как имя и адрес, а не всю запись.
- Сделать определенные, тщательного запросов фильтра. К примеру Если вы хотите перечислены доступные статьи, получите заголовок, PublishingDate и автор. Оставьте для остальных полей из строки запроса.

### <a name="ProvideAGoodUserExperience"></a>Предоставление удобства работы пользователей

Рывками, неправильное пользовательских интерфейсов влиять не просто производительности, а также производительности. Написание кода таким образом, чтобы предоставить повышения качества связи.

- Чтобы указать, что действия загрузке или время используйте счетчик.
- Понять порядок выполнения кода и фигуры для работы пользователей. Например если планируется извлечение большого объема данных с сервера, и вы планируете изменить пользовательский интерфейс путем скрытия меню, скройте меню сначала. Которая позволит по ширине пользовательский интерфейс для пользователя.

## <a name="EverythingIsAsynchronous"></a>Все, что является асинхронное

Каждые действие code в браузере должен считаться асинхронный. Файлы загрузки в некотором порядке, необходимо дождаться DOM для загрузки и запросы на SharePoint будут завершены на различные скорости. 

- Понимаете, как код работает в времени.
- События использования и обратных вызовов вместо опроса.
- Использование обязательства. В jQuery они называются объектами **Отложенный** . Существуют аналогичные понятия Q, WinJS и ES6.
- Используйте асинхронные вызовы пользу не асинхронного вызова.
- Используйте асинхронный каждый раз, когда может быть задержку:
    - Во время выполнения запроса AJAX.
    - Во время любого значительные DOM выполнение различных операций.

Шаблоны асинхронного повышения производительности и скорости ответа и разрешить для эффективной цепочки зависимые действия.

## <a name="ClientSideCaching"></a>Кэширование на стороне клиента

Кэширование на стороне клиента — это один из большинства улучшения часто пропущенных производительности, которые можно добавить в код.

Существует три различных местах, можно кэшировать данные.

|Параметр|Описание|
|:---|:---|
|Сеанс хранилища|Хранит данные в виде пары ключ значение на стороне клиента. Причина этого заключается в хранилище сеанса, которое всегда хранится в виде строки. <br /> JSON.stringify() преобразует объектов JavaScript строк, которые приводятся рекомендации для хранения объектов.
|Локальное хранилище|<p>Хранит данные в виде пары ключ значение на стороне клиента. Это сохраняемого между сеансами, которые всегда хранится в виде строки.</p><p>JSON.stringify() преобразует объектов JavaScript строк, которые приводятся рекомендации для хранения объектов.</p>|
|Локальной базы данных|Сохранение реляционные данные на стороне клиента. В качестве ядро базы данных, часто используется средство упрощенного SQL.<br>Локальное хранилище базы данных не всегда доступны во всех браузерах&mdash;проверьте конечного поддержки браузеров

При кэшировании, имейте в виду ограничений хранилища, доступные для вас и актуальность данных. 
- Если производится доступ в конец дискового пространства, стоит удалить старые или менее важных кэшированные данные. 
- Различные типы данных можно устарели быстрее, чем другие. Список статей новостей может быть устаревших в 5-10 минут, однако имя профиля пользователя можно часто безопасно кэшировать 24 часов и более. 

Локальный и хранение сеанса не имеет встроенных истечение срока действия, но файлов cookie. Можно привязать хранимых данных в файл cookie для добавления истечение срока действия в вашей локальной и хранение сеанса. Также можно создавать оболочкой хранилища, который включает в себя дату окончания срока действия и проверить в коде.

## <a name="PriceOfPopularity"></a>Цена популярности

Как часто отображаются на странице? В сценарии с классической корпоративной домашней страницы задано как страница запуска всех браузеров в организации. Затем получите внезапно гораздо большее число трафика, чем когда-либо представить. Каждый байт контента внезапно увеличивается на производительность сервера и пропускной способности, которые принимают домашней страницы.

Решение: перейдите light на домашней странице и ссылка на другой контент.

Высокая интенсивность операций данных панелей мониторинга, также кандидата для приложения с размещением у поставщика, который можно масштабировать независимо друг от друга.

## <a name="LoaderPattern"></a>Загрузчик шаблон

Цель шаблон загрузчик — укажите способ внедрения неизвестное число удаленных скрипты в сайт без необходимости обновления сайта. Обновления можно выполнить на удаленных CDN и обновит все сайты.

Шаблон загрузчик создает URL-адрес с Отметка даты и времени в конце, чтобы файл не будут кэшироваться. Он устанавливает jQuery в качестве зависимость от файла загрузчик, а затем выполняет функцию в загрузчик. Это гарантирует, что настраиваемый JavaScript будет загружен после завершения загрузки jQuery.

PnP-dev\Samples\Core.JavaScript\Core.JavaScript.Embedder\Program.cs:

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

`SP.SOD.registerSodDep('pnp-loader.js', 'pnp-jquery.js');` Выполняет настройку зависимостей, и `SP.SOD.executeFunc('pnp-loader.js', null, function() {});` принудительно jQuery загрузится полностью перед загрузкой настраиваемый JavaScript.

`newLink.ScriptBlock = script2;` И `newLink.Location = "ScriptLink";` основные части Добавление в действие клиента пользователя.

Файл pnp loader.js загружает список файлов JavaScript, с помощью резервирования, который может выполняться при загрузке каждого файла.

PnP-dev\Samples\Core.JavaScript\Core.JavaScript.CDN\js\pnp-loader.js:

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

Файл pnp loader.js не кэш, который хорошо подходит для среды разработки. Заменяет файл pnp загрузчик cached.js `$.getScript` работать с `$.ajax` функция, которая позволяет для браузера кэширования файлов и лучше подходит для рабочей среды.

Из PnP-dev\Samples\Core.JavaScript\Core.JavaScript.CDN\js\pnp-loader.js

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

Этот шаблон облегчает развертывание и обновление на сайты. Особенно полезен при развертывании или обновление на тысячи семейств веб-сайтов.

## <a name="CachingCurrentUserInfo"></a>Кэширование текущего пользователя

Если пользователь уже кэширования, эта функция получает данные из кэша сеанса. Если сведения о пользователе хранится в кэше, получает данные определенного пользователя мы должны и сохраняет его в кэше.

Это также использует отложенный (версия jQuery promise). Если мы получить данные из кэша или с сервера, отложенный решена. Если ошибка, отложенный отклоняется.

Из PnP-dev\Samples\Core.JavaScript\Core.JavaScript.CDN\js\pnp-core.js:

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

## <a name="CachingPatternUsingAsynchronousAndDeferred"></a>С помощью асинхронной и отложенная кэширования шаблона

Другой шаблон кэширования можно найти в storageTest pnp clientcache.js, который берет файлы из modernizer storageTest. Он содержит функции для add, get, удаление и getOrAdd, который возвращает кэшированные данные, если он находится в кэше, или получение данных с сервера и добавить его в кэш, если он не в кэше, что позволяет экономить написание повторяющиеся кода в вызывающей функции. get используется JSON.parse для проверки истечения срока действия с момента истечение срока действия не является компонентом в локальном хранилище. _createPersistable хранит объект JavaScript в кэше локального хранилища.

Из PnP-dev\Samples\Core.JavaScript\Core.JavaScript.CDN\js\pnp-clientcache.js:

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

Для более сложного использования асинхронных и отложенный можно ссылаться на панели мониторинга разработчика в pnp clientcache.js

## <a name="Resources"></a>Ресурсы

### <a name="see-also"></a>См. также:
- [JavaScript — шаблоны и об использовании](http://dev.office.com/blogs/javascript-development-patterns-with-sharepoint)
- [JavaScript — рекомендации по производительности](http://dev.office.com/blogs/javascript-performance-considerations-with-sharepoint)
- [Выполнение базовых операций с использованием кода библиотеки JavaScript в SharePoint 2013](https://msdn.microsoft.com/EN-US/library/office/jj163201.aspx)
- [Примеры кода обработки на стороне клиента (JS ссылка)](https://code.msdn.microsoft.com/office/Client-side-rendering-JS-2ed3538a)
- [Внедрение JavaScript (Настройка сайта SharePoint пользовательского интерфейса с помощью JavaScript)](https://msdn.microsoft.com/EN-US/library/dn913116.aspx)
- [Настройки поиска для SharePoint](https://msdn.microsoft.com/EN-US/library/mt210901.aspx)
- [Надстройка SharePoint набора команд — тип настраиваемого поля (с помощью отображения со стороны клиента)](custom-field-type-sharepoint-add-in.md)

### <a name="samples"></a>Примеры

- [Performance.Caching](https://github.com/SharePoint/PnP/tree/master/Samples/Performance.Caching)
- [Core.JavaScript](https://github.com/SharePoint/Pnp/tree/master/Samples/Core.JavaScript)
