# <a name="creating-sharepoint-add-ins-that-use-the-cross-domain-library"></a>Создание надстроек SharePoint, использующих междоменную библиотеку
Сведения о междоменной библиотеке JavaScript в SharePoint.
 

 **Примечание.** Название "приложения для SharePoint" меняется на "надстройки SharePoint". Пока изменения не будут внесены полностью, в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio по-прежнему может встречаться термин "приложение". Дополнительные сведения см. в разделе [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).
 

В некоторых сценариях надстройка SharePoint не может использовать ни систему авторизации с низким уровнем доверия, ни систему авторизации с высоким уровнем доверия. В некоторых случаях такие системы лучше не использовать как единственное средство авторизации для доступа надстройки к ресурсам SharePoint. Примеры представлены ниже.
 

- Удаленные компоненты надстройки SharePoint находятся не в локальной среде, но корпоративный брандмауэр блокирует межсерверное взаимодействие между SharePoint и ACS, тем самым не позволяя использовать систему с низким уровнем доверия.
    
 
- Надстройка SharePoint это одностраничное веб-приложение, использующее клиентский код JavaScript для выполнения операций с данными в SharePoint.
    
 
- Надстройка SharePoint в основном использует межсерверные вызовы для доступа к данным SharePoint (и авторизуется системами с низким или высоким уровнем доверия), но его необходимо дополнить вызовами JavaScript. Например, страница с интенсивным использованием графики может применять JavaScript, чтобы вносить небольшие изменения в отображаемые данные без перегрузки всей страницы.
    
 
Однако в  [целях безопасности](http://msdn.microsoft.com/en-us/library%28d=robot%29/cc709423(d=robot,l=en-us,v=vs.85).aspx) браузеры не разрешают коду JavaScript, размещенному в одном домене, получать доступ к ресурсам в другом домене. Поэтому необходимо использовать специальную методику, чтобы предоставить удаленному коду JavaScript доступ к ресурсам SharePoint. Междоменная библиотека JavaScriptSharePoint упрощает использование этого метода в веб-приложениях.
 

 **Примечание.** Междоменная библиотека также используется для предоставления доступа к данным в обратном направлении (т. е. чтобы разрешить коду JavaScript на странице SharePoint получать доступ к данным на удаленном домене). Дополнительные сведения см. в разделе [Доступ к удаленным данным со страницы SharePoint](#ReverseDirection).
 


## <a name="understand-the-architecture-of-the-cross-domain-library"></a>Общие сведения об архитектуре междоменной библиотеки

Междоменная библиотека SharePoint содержится в файле SP.RequestExecutor.js, который расположен в виртуальной папке /_layouts/15/ каждого веб-сайта SharePoint. Скрипты в этом файле используют известный способ обхода ограничения междоменных скриптов браузера: iFrame может взаимодействовать с родительской страницей с помощью функции  `window.postMessage()`, даже если страница в iFrame находится в другом домене. Поэтому запросы данных и ответы передаются между домена с помощью функции  `postMessage()`.
 

 

 **Внимание!** Функция `postMessage()` работает только в браузерах, поддерживающих HTML 5, поэтому надстройки SharePoint, использующие междоменную библиотеку, не будут работать в старых браузерах.
 

Для SharePoint междоменная библиотека загружается на странице удаленного веб-приложения, где создается скрытый iFrame, в котором размещается специальная прокси-страница из домена SharePoint. Прокси-страница уже существует на каждом веб-сайте SharePoint. С помощью библиотеки создается объект Нотация объектов JavaScript (JSON), содержащий все сведения, необходимые для CRUD-вызова к API-интерфейсам REST SharePoint. Объект JSON передается прокси-странице с помощью функции  `postMessage()`. На прокси-странице, где также загружается библиотека, объект JSON анализируется и преобразуется в REST-вызов SharePoint. Так как прокси-страница находится в домене SharePoint, браузер разрешает вызов.
 

 
Конечно, у удаленных компонентов надстройки SharePoint по-прежнему должен быть авторизованный доступ к ресурсам SharePoint. Для этого существует два способа:
 

 

- Задайте для надстройки тип субъекта **RemoteWebApplication** (значение по умолчанию для надстроек с размещением у поставщика) в манифесте надстройки. При регистрации надстройки в службе ACS указывается домен удаленного веб-приложения. SharePoint доверяет доменам, зарегистрированным в ACS, хотя в этом сценарии не используются потоки передачи маркеров, применяемые в серверной системе с низким уровнем доверия. Подробные сведения о регистрации надстроек см. в статье [Регистрация надстроек SharePoint 2013](register-sharepoint-add-ins-2013). 
    
 
- В надстройке, размещенной в SharePoint, можно оставить тип субъекта надстройки по умолчанию, т. е. **Internal**. Задайте в атрибуте **AllowedRemoteHostUrl** элемента **Internal** URL-адрес удаленного приложения, как показано в приведенном ниже примере.
    
```
  <AppPrincipal>
  <Internal AllowedRemoteHostUrl="https://example.com/Home.html" />
</AppPrincipal>
```


 **Примечание.** Если вы используете второй вариант (субъект надстройки **Internal**), то для доступа к SharePoint можно использовать только JavaScript и междоменную библиотеку. Клиентская объектная модель SharePoint заблокирована для надстроек SharePoint с атрибутом **Internal**, поэтому невозможно создать двойную систему авторизации, которая допускает применение как междоменной библиотеки, так и системы с низким или высоким уровнем доверия.
 

Сведения о том, как использовать библиотеку, см. в статье [Обращение к данным SharePoint из надстроек с помощью междоменной библиотеки](access-sharepoint-2013-data-from-add-ins-using-the-cross-domain-library).
 

 

## <a name="access-remote-data-from-a-sharepoint-page"></a>Доступ к удаленным данным со страницы SharePoint
<a name="ReverseDirection"> </a>

Междоменную библиотеку SharePoint также можно использовать в обратном направлении, т. е. JavaScript на странице SharePoint может с помощью библиотеки получить данные из удаленных компонентов надстройки. Для этого междоменная архитектура меняется на обратную: вы создаете прокси-страницу в удаленном веб-приложении. Библиотека вызывается со страницы SharePoint, где она создает iFrame для размещения прокси-страницы. Дополнительные сведения о таком применении библиотеки см. в статье  [Создание пользовательской прокси-страницы для междоменной библиотеки в SharePoint](create-a-custom-proxy-page-for-the-cross-domain-library-in-sharepoint-2013).
 

 

## <a name="in-this-section"></a>В этом разделе:
<a name="ReverseDirection"> </a>


-  [Обращение к данным SharePoint из надстроек с помощью междоменной библиотеки](access-sharepoint-2013-data-from-add-ins-using-the-cross-domain-library)
    
 
-  [Работа с междоменной библиотекой в различных зонах безопасности Internet Explorer в надстройках SharePoint](work-with-the-cross-domain-library-across-different-internet-explorer-security-zones-in-sharepoint-add-ins)
    
 

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="ReverseDirection"> </a>


-  [Исправление междоменных проблем в надстройках SharePoint](http://blogs.msdn.com/b/officeapps/archive/2012/11/29/solving-cross-domain-problems-in-apps-for-sharepoint.aspx)
    
 
