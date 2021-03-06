
# <a name="url-strings-and-tokens-in-sharepoint-add-ins"></a>Токены и строки URL-адресов в надстройках SharePoint
Узнайте, какие маркеры URL-адресов доступны для использования в надстройках SharePoint.
 

 **Примечание.** Название "приложения для SharePoint" меняется на "надстройки SharePoint". Пока изменения не будут внесены полностью, в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio по-прежнему может встречаться термин "приложение". Дополнительные сведения см. в разделе [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).
 


 **Важно!** Общие сведения о составлении URL-адресов в SharePoint и использовании маркеров в этих URL-адресах см. в статье [URL-адреса и маркеры в SharePoint](http://msdn.microsoft.com/library/161418d7-8123-4c4e-91a1-97e43c17f0e6%28Office.15%29.aspx). В этой статье описываются маркеры, доступные в надстройках SharePoint.
 


## 
<a name="URLtokens"> </a>

В приведенных ниже таблицах перечислены маркеры, поддерживаемые для использования в надстройках SharePoint.
 

 
Маркеры, перечисленные в таблицах в этом разделе, можно использовать в URL-адресах во множестве ситуаций в ходе разработки надстроек SharePoint, например в дополнительных действиях и ссылках на пользовательские страницы. Некоторые из этих маркеров невозможно использовать в определенных контекстах. Для начальных страниц надстроек, дополнительных действий на хост-сайтах и свойства **Src** веб-частей надстроек можно использовать только некоторые из доступных маркеров. Эти случаи вынесены в отдельные столбцы, * **но они не представляют собой исчерпывающий список областей применения маркеров.*** 
 

 
В столбце **StartPage** указано, можно ли использовать маркер в элементе **StartPage** манифеста надстройки. В столбце **Дополнительное действие** указано, можно ли использовать маркер в URL-адресе дополнительного действия на хост-сайте. В столбце **Веб-часть надстройки** указано, можно ли использовать маркер в свойстве **Src** веб-части надстройки.
 

 

**Маркеры, которые можно использовать в начале URL-адреса надстройки SharePoint**


|**Маркер**|**Во что разрешается**|**StartPage**|**Дополнительное действие**|**Веб-часть надстройки**|**Замечания**|
|:-----|:-----|:-----|:-----|:-----|:-----|
|~appWebUrl|URL-адрес сайта надстройки для Надстройка SharePoint.|Да|Да|Да|Этот маркер следует использовать только вне сайта надстройки. На самом сайте надстройки используйте для его URL-адреса маркер **~site**.|
|~controlTemplates|URL-адрес виртуальной папки ControlTemplates для текущего веб-сайта.|Нет|Нет|Нет||
|~hostUrl|URL-адрес хост-сайта.|Нет|НЕТ|Да||
|~hostLogoUrl|URL-адрес логотипа хост-сайта.|Нет|Нет|Нет||
|~layouts|URL-адрес виртуальной папки Layouts для текущего веб-сайта.|Нет|Нет|Нет||
|~remoteAppUrl|URL-адрес удаленного веб-приложения в Надстройка SharePoint.|Да|Да для хост-сайтов. Нет для сайтов надстроек.|Да|Если при разработке надстройки SharePoint не используются Инструменты разработчика Microsoft Office для Visual Studio, то маркер **~remoteAppUrl** невозможно использовать в URL-адресах **StartPage**. Однако если используются Visual Studio и инструменты разработчика, то этот маркер можно использовать для всех размещаемых у поставщика надстроек, и он разрешается, когда Visual Studio упаковывает надстройку. В этом случае он является скорее маркером Visual Studio, чем маркером SharePoint. Вне манифеста надстройки этот маркер можно использовать, даже если Инструменты разработчика Microsoft Office для Visual Studio не используются.|
|~site|URL-адрес текущего веб-сайта.|Нет|НЕТ|Да||
|~sitecollection|URL-адрес родительского семейства сайтов для текущего веб-сайта.|Нет|НЕТ|Да||
Если не указано обратное, перечисленные в следующей таблице маркеры можно использовать в части  *path*  свойства веб-части надстройки **Src** . Столбец **Веб-часть надстройки** относится к их использованию в части значения *query string*  .
 

 

**Маркеры, которые можно использовать в URL-адресе**


|**Маркер**|**Во что разрешается**|**StartPage**|**Дополнительное действие**|**Веб-часть надстройки**|**Замечания**|
|:-----|:-----|:-----|:-----|:-----|:-----|
|{AppContextToken}|Маркер контекста OAuth для надстройки.|Нет|Нет|Нет||
|{AppWebUrl}|URL-адрес сайта надстройки в Надстройка SharePoint.|Да|Да|Да|Этот маркер следует использовать только вне сайта надстройки. На самом сайте надстройки используйте для его URL-адреса маркер **{Site}**.|
|{ClientTag}|Контрольный номер кэша клиента (метка клиента) для текущего веб-сайта.|Да|Да|Да||
|{HostLogoUrl}|Эмблема для хост-сайта Надстройка SharePoint.|Да|Да|Да||
|{HostTitle}|Название хост-сайта Надстройка SharePoint.|Да|Да|Да||
|{HostUrl}|URL-адрес хост-сайта Надстройка SharePoint.|Да|Да|Да||
|{ItemId}|Идентификатор элемента в списке или библиотеке (целое значение).|Нет|ДА|Нет||
|{ItemUrl}|URL-адрес элемента, с которым выполняется действие. |Нет|ДА|Нет||
|{Language}|Текущий язык и региональные параметры хост-сайта Надстройка SharePoint.|Да|Да|Да||
|{ListId}|Идентификатор текущего списка (GUID).|Нет|ДА|Нет||
|{ProductNumber}|Полный номер версии фермы SharePoint.|Да|Да|Да|Пример значения: "15.0.4433.1011".|
|{RecurrenceId}|Индекс повторения повторяющегося события.|Нет|ДА|Нет|Этот маркер не поддерживается для контекстных меню элементов списков.|
|{RemoteAppUrl}|URL-адрес удаленного веб-приложения в Надстройка SharePoint.|Да|Да|Да||
|{Site}|URL-адрес текущего веб-сайта.|Нет|ДА|Да||
|{SiteCollection}|URL-адрес родительского сайта для текущего веб-сайта.|Нет|ДА|Да||
|{SiteUrl}|URL-адрес текущего веб-сайта.|Нет|ДА|Нет||
|{Source}|URL-адрес HTTP-запроса.|Нет|ДА|Нет||
|{StandardTokens}|См. раздел "Замечания".|Да|Да|Да|Этот маркер составлен из пяти других маркеров. Сначала он разрешается в  `SPHostUrl={HostUrl}&amp;SPAppWebUrl={AppWebUrl}&amp;SPLanguage={Language}&amp;SPClientTag={ClientTag}&amp;SPProductNumber={ProductNumber}`. Затем разрешается каждый из этих маркеров. Если сайт надстройки отсутствует, то отсутствует и часть  `&amp;SPAppWebUrl={AppWebUrl}`.  |

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="SP15URLstrings_bk_addlresources"> </a>


-  [Расширенная поддержка экстрасети](http://msdn.microsoft.com/library/21d67796-23c5-4339-8f0e-124208d21ab2%28Office.15%29.aspx)
    
 
-  [Получение ссылок на сайты, веб-приложения и другие ключевые объекты](http://msdn.microsoft.com/library/8623ef1d-e3cc-426c-84a3-6379e0ae284f%28Office.15%29.aspx)
    
 
-  [Работа с объектами List и коллекциями](http://msdn.microsoft.com/library/d4167b10-6f1e-49f1-8b22-16ce20012a27%28Office.15%29.aspx)
    
 
-  [Базовые задачи объектной модели](http://msdn.microsoft.com/library/94d6898d-6a0f-43a7-ad06-1b27ec6916ea%28Office.15%29.aspx)
    
 

