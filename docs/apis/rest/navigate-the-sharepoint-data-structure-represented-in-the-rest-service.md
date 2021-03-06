# <a name="navigate-the-sharepoint-data-structure-represented-in-the-rest-service"></a>Навигация по структуре данных SharePoint, представленной в службе REST
Узнайте, как с помощью конечной точки REST в элементе SharePoint получить доступ к связанным элементам, например родительским сайтам или структуре библиотеки, в которой находится этот элемент. 
 
## <a name="navigate-from-a-given-url-to-reach-other-sharepoint-resources"></a>Переход от заданного URL-адреса к другим ресурсам SharePoint
При работе со службой REST SharePoint вы часто начинаете с того, что узнаете URL-адрес определенного элемента SharePoint, но хотите получить доступ к связанным элементам, например папке или структуре библиотеки, в которой находится элемент. Предположим, что вы создаете надстройку, где пользователь вводит URL-адрес документа в библиотеке SharePoint. Ваша надстройка должна затем разбить этот URL-адрес, чтобы вычислить фактический URL-адрес сайта SharePoint. После этого надстройка может отправлять больше запросов от имени пользователя, например для создания, обновления или удаления связанных элементов или ресурсов. 
 
Для этого надстройка должна запросить у SharePoint следующие сведения:
 
- URL-адреса относительно сервера для сайта и семейства веб-сайтов, содержащих ресурс.   
 
- Дайджест формы, позволяющий выполнять запросы, меняющие состояние ресурса, например **POST**, **PUT**, **MERGE** и **DELETE**.
    
Базовый процесс:

1. Используйте оператор `/contextinfo` с заданным URL-адресом для доступа к сайту и семейству веб-сайтов, а также дайджестом формы. Используйте оператор `/contextinfo` в следующем формате:
    
     `http://server/web/doclib/forms/_api/contextinfo`
    
    Чтобы усилить защиту от межсайтовых сценариев, оператор `/contextinfo` принимает только запросы **POST**.
    
 
2. Используйте [свойства объекта SPContextWebInformation](#bk_props), возвращаемые оператором `/contextinfo`, для доступа к дополнительным ресурсам по мере необходимости.
    
 
 **Попробуйте сами**
 

1. Начните с URL-адреса определенного элемента SharePoint. Например:
    
     `http://site/web/doclib/myDocument.docx`
     
2. Удалите имя ресурса в конце URL-адреса таким образом, чтобы URL-адрес указывал на библиотеку документа, папку или список. В данном случае:
    
     `http://site/web/doclib/`
    
3. Добавьте указатель службы REST и оператор `/contextinfo` к URL-адресу:
    
     `http://site/web/doclib/_api/contextinfo`
    
4. Прочитайте дайджест формы и свойства **webFullUrl** из отклика.
    
5. Добавьте указатель службы REST `_api` в конец URL-адреса веб-сайта.
    
6. Используйте полученный URL-адрес и дайджест формы для отправки запросов о других нужных ресурсах.
    
При отправке запросов **GET** или отправке запросов с использованием проверенного маркера OAuth передавать дайджест формы не требуется.
 
## <a name="navigate-parent-and-child-sites"></a>Навигация по родительским и дочерним сайтам
<a name="bk_sites"> </a> При навигации по структуре сайтов с помощью серверной объектной модели SharePoint используются свойства **SPWeb.ParentWeb** и **SPWeb.Webs** для доступа к объектам, представляющим родительские и дочерние сайты.

Соответствующие ресурсы REST — `web/parentweb` и `web/webs` — не возвращают объекты, представляющие сайты. Это вызвано тем, что служба REST соответствует стандартам OData, а возврат готовых представлений сайтов сделал бы такие запросы неэффективными. Вместо этого они возвращают [объект WebInfo](#bk_webinfo), содержащий скалярные свойства сайта, но без связанных наборов сущностей, таких как коллекции или семейства полей.
  
Чтобы перейти к определенному родительскому или дочернему сайту, составьте подходящий URL-адрес REST этого сайта с помощью свойства **Id** или **Title**. После этого вы можете получить доступ к наборам сущностей, связанным с этим сайтом.
 
## <a name="navigating-folder-structure"></a>Навигация по структуре папок
<a name="bk_folders"> </a> Служба REST SharePoint не поддерживает переход по иерархии папок сайта путем составления URL-адресов. Вместо этого можно использовать аналог метода **Web.GetFolderByServerRelativeUrl** в службе REST. Например:
 
 *Навигация, не поддерживаемая в службе REST:* 
  
 `/_vti_bin/client.svc/web/lists/SharedDocuments/folder1/stuff/things/Recycle`
 
Навигация, поддерживаемая в службе REST: 
 
 `/_vti_bin/client.svc/web/GetFolderByServerRelativeUrl('SharedDocuments/folder1/stuff/things')/Recycle`.
 

## <a name="spcontextwebinformation-object-properties"></a>Свойства объекта SPContextWebInformation
<a name="bk_props"> </a>

|**Свойство SPContextWebInformation**|**Описание**|
|:-----|:-----|
|**webFullUrl**|Возвращает URL-адрес относительно сервера для ближайшего сайта.|
|**siteFullUrl**|Возвращает URL-адрес относительно сервера для корня семейства веб-сайтов, включающего текущий сайт. Если ближайший веб-сайт является корнем семейства веб-сайтов, значение свойства **webFullUrl** будет совпадать со значением свойства **siteFullUrl**.|
|**formDigestValue**|Возвращает дайджест формы запроса сервера.|
|**LibraryVersion**|Возвращает текущую версию библиотеки REST.|
|**SupportedSchemaVersions**|Получает поддерживаемые версии схемы библиотеки REST/CSOM.|

## <a name="webinfo-object"></a>Объект WebInfo
<a name="bk_webinfo"> </a>

|**Свойство WebInfo**|**Описание**|
|:-----|:-----|
|**Created**|Возвращает значение, определяющее, когда был создан сайт.|
|**Description**|Возвращает или задает описание сайта.|
|**Id**|Возвращает значение, указывающее идентификатор сайта.|
|**Language**|Возвращает значение, указывающее код языка, используемого на сайте.|
|**LastItemModifiedDate**|Возвращает значение, определяющее, когда в последний раз был изменен элемент на сайте.|
|**Title**|Получает или задает название сайта.|
|**WebTemplateId**|Получает идентификатор шаблона сайта.|

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>

-  [Знакомство со службой REST в SharePoint](get-to-know-the-sharepoint-rest-service.md)
-  [Выполнение базовых операций с использованием конечных точек SharePoint REST](complete-basic-operations-using-sharepoint-rest-endpoints.md)
-  [Работа со списками и элементами списков в интерфейсе REST](working-with-lists-and-list-items-with-rest.md)
-  [Работа с папками и файлами в службе REST](working-with-folders-and-files-with-rest.md)
-  [Определение URI для конечных точек службы REST в SharePoint](determine-sharepoint-rest-service-endpoint-uris.md)
-  [Использование операций запросов OData в запросах REST SharePoint](use-odata-query-operations-in-sharepoint-rest-requests.md)
-  [Справочные материалы и примеры по REST API](http://msdn.microsoft.com/library/02128c70-9d27-4388-9374-a11bce68fdb8%28Office.15%29.aspx)
-  [Синхронизация элементов SharePoint с помощью службы REST](synchronize-sharepoint-items-using-the-rest-service.md)
-  [Получение версий элементов списков и документов с помощью значений ETag в службе REST](http://msdn.microsoft.com/library/use-etag-values-through-the-rest-service-to-get-document-list-item-versioning%28Office.15%29.aspx)
    
 

 

 

