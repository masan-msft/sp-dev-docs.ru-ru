
# <a name="navigate-the-sharepoint-data-structure-represented-in-the-rest-service"></a><span data-ttu-id="b51ba-101">Навигация по структуре данных SharePoint, представленной в службе REST</span><span class="sxs-lookup"><span data-stu-id="b51ba-101">Navigate the SharePoint data structure represented in the REST service</span></span>
<span data-ttu-id="b51ba-102">Узнайте, как с помощью конечной точки REST в элементе SharePoint получить доступ к связанным элементам, например родительским сайтам или структуре библиотеки, в которой находится этот элемент.</span><span class="sxs-lookup"><span data-stu-id="b51ba-102">Learn how to start from a REST endpoint for a given SharePoint item, and navigate to and access related items, such as parent sites or the library structure where that item resides.</span></span> 
 

 <span data-ttu-id="b51ba-p101">**Примечание.** Название "приложения для SharePoint" меняется на "надстройки SharePoint". Пока изменения не будут внесены полностью, в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio по-прежнему может встречаться термин "приложение". Дополнительные сведения см. в разделе [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="b51ba-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 


## <a name="navigate-from-a-given-url-to-reach-other-sharepoint-resources"></a><span data-ttu-id="b51ba-106">Переход от заданного URL-адреса к другим ресурсам SharePoint</span><span class="sxs-lookup"><span data-stu-id="b51ba-106">Navigate from a given URL to reach other SharePoint resources</span></span>

<span data-ttu-id="b51ba-p102">При работе со службой REST SharePoint вы часто начинаете с того, что узнаете URL-адрес определенного элемента SharePoint, но хотите получить доступ к связанным элементам, например папке или структуре библиотеки, в которой находится элемент. Предположим, что вы создаете надстройку, где пользователь вводит URL-адрес документа в библиотеке SharePoint. Ваша надстройка должна затем разбить этот URL-адрес, чтобы вычислить фактический URL-адрес сайта SharePoint. После этого надстройка может отправлять больше запросов от имени пользователя, например для создания, обновления или удаления связанных элементов или ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b51ba-p102">When you're working with the SharePoint REST service, you'll often start out knowing the URL of a specific SharePoint item, but want to access related items, such as the folder or library structure where that item resides. For example, suppose you create an add-in where your user enters the URL of a document in a SharePoint library. Your add-in must then break down that URL to figure out the actual SharePoint site URL. Once it's done that, the add-in can then make more requests from the site on the user's behalf, such as to create, update, or delete related items or resources.</span></span> 
 

 
<span data-ttu-id="b51ba-111">Для этого надстройка должна запросить у SharePoint следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="b51ba-111">To do this, your add-in needs to query SharePoint for the following information:</span></span>
 

 

- <span data-ttu-id="b51ba-112">URL-адреса относительно сервера для сайта и семейства веб-сайтов, содержащих ресурс.</span><span class="sxs-lookup"><span data-stu-id="b51ba-112">The server relative URLs of the site and site collection containing the resource</span></span>
    
 
- <span data-ttu-id="b51ba-113">Дайджест формы, позволяющий выполнять запросы, меняющие состояние ресурса, например **POST**, **PUT**, **MERGE** и **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="b51ba-113">A form digest to enable you to perform requests that change the state of the resource, such as  **POST**,  **PUT**,  **MERGE**, and  **DELETE**</span></span>
    
 
<span data-ttu-id="b51ba-114">Базовый процесс:</span><span class="sxs-lookup"><span data-stu-id="b51ba-114">The basic process:</span></span>
 

 

1. <span data-ttu-id="b51ba-p103">Используйте оператор `/contextinfo` с заданным URL-адресом для доступа к сайту и семейству веб-сайтов, а также дайджестом формы. Используйте оператор `/contextinfo` в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="b51ba-p103">Use the  `/contextinfo` operator with the given URL to access the site and site collection addresses, and the form digest. Use the `/contextinfo` operator in the following format:</span></span>
    
     `http://server/web/doclib/forms/_api/contextinfo`
    
    <span data-ttu-id="b51ba-117">Чтобы усилить защиту от межсайтовых сценариев, оператор `/contextinfo` принимает только запросы **POST**.</span><span class="sxs-lookup"><span data-stu-id="b51ba-117">To increase security against cross-site scripting attempts, the  `/contextinfo` operator accepts only **POST** requests.</span></span>
    
 
2. <span data-ttu-id="b51ba-118">Используйте [свойства объекта SPContextWebInformation](#bk_props), возвращаемые оператором `/contextinfo`, для доступа к дополнительным ресурсам по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="b51ba-118">Use the  [SPContextWebInformation object properties](#bk_props) that the `/contextinfo` operator returns to access additional resources as desired.</span></span>
    
 
 <span data-ttu-id="b51ba-119">**Попробуйте сами**</span><span class="sxs-lookup"><span data-stu-id="b51ba-119">**Try it**</span></span>
 

 

1. <span data-ttu-id="b51ba-p104">Начните с URL-адреса определенного элемента SharePoint. Например:</span><span class="sxs-lookup"><span data-stu-id="b51ba-p104">Start with a URL to a given SharePoint item. For example:</span></span>
    
     `http://site/web/doclib/myDocument.docx`
    
 
2. <span data-ttu-id="b51ba-p105">Удалите имя ресурса в конце URL-адреса таким образом, чтобы URL-адрес указывал на библиотеку документа, папку или список. В данном случае:</span><span class="sxs-lookup"><span data-stu-id="b51ba-p105">Remove the name of the specific resource from the end of the URL, so that the URL points to a document library, folder, or list. IN this case:</span></span>
    
     `http://site/web/doclib/`
    
 
3. <span data-ttu-id="b51ba-124">Добавьте указатель службы REST и оператор `/contextinfo` к URL-адресу:</span><span class="sxs-lookup"><span data-stu-id="b51ba-124">Append the REST service pointer and the  `/contextinfo` operator to the URL:</span></span>
    
     `http://site/web/doclib/_api/contextinfo`
    
 
4. <span data-ttu-id="b51ba-125">Прочитайте дайджест формы и свойства **webFullUrl** из отклика.</span><span class="sxs-lookup"><span data-stu-id="b51ba-125">Read the form digest and  **webFullUrl** properties from the response.</span></span>
    
 
5. <span data-ttu-id="b51ba-126">Добавьте указатель службы REST `_api` в конец URL-адреса веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="b51ba-126">Append the REST service pointer  `_api` to the web URL</span></span>
    
 
6. <span data-ttu-id="b51ba-127">Используйте полученный URL-адрес и дайджест формы для отправки запросов о других нужных ресурсах.</span><span class="sxs-lookup"><span data-stu-id="b51ba-127">Use the resulting URL and the form digest to make requests for other resources you need.</span></span>
    
 
<span data-ttu-id="b51ba-128">При отправке запросов **GET** или отправке запросов с использованием проверенного маркера OAuth передавать дайджест формы не требуется.</span><span class="sxs-lookup"><span data-stu-id="b51ba-128">You don't have to pass the form digest if you're making  **GET** requests, or making requests using a validated OAuth token.</span></span>
 

 

## <a name="navigate-parent-and-child-sites"></a><span data-ttu-id="b51ba-129">Навигация по родительским и дочерним сайтам</span><span class="sxs-lookup"><span data-stu-id="b51ba-129">Navigate parent and child sites</span></span>
<span data-ttu-id="b51ba-130"><a name="bk_sites"> </a></span><span class="sxs-lookup"><span data-stu-id="b51ba-130"></span></span>

<span data-ttu-id="b51ba-131"> При навигации по структуре сайтов с помощью серверной объектной модели SharePoint используются свойства **SPWeb.ParentWeb** и **SPWeb.Webs** для доступа к объектам, представляющим родительские и дочерние сайты.</span><span class="sxs-lookup"><span data-stu-id="b51ba-131">When you navigate your site structure using the SharePoint server object model, you use the  **SPWeb.ParentWeb** and **SPWeb.Webs** properties to access objects that represent parent and child sites.</span></span>
 

 
<span data-ttu-id="b51ba-p106">Соответствующие ресурсы REST — `web/parentweb` и `web/webs` — не возвращают объекты, представляющие сайты. Это вызвано тем, что служба REST соответствует стандартам OData, а возврат готовых представлений сайтов сделал бы такие запросы неэффективными. Вместо этого они возвращают [объект WebInfo](#bk_webinfo), содержащий скалярные свойства сайта, но без связанных наборов сущностей, таких как коллекции или семейства полей.</span><span class="sxs-lookup"><span data-stu-id="b51ba-p106">The corresponding REST resources— `web/parentweb` and `web/webs`—don't return objects that represent sites. This is because the REST service conforms to OData standards, and returning complete site representations would make such requests inefficient. Instead, they return a  [WebInfo object ](#bk_webinfo) that contains the site's scalar properties, but without related entity sets such as like collections or field collections.</span></span>
 

 
<span data-ttu-id="b51ba-p107">Чтобы перейти к определенному родительскому или дочернему сайту, составьте подходящий URL-адрес REST этого сайта с помощью свойства **Id** или **Title**. После этого вы можете получить доступ к наборам сущностей, связанным с этим сайтом.</span><span class="sxs-lookup"><span data-stu-id="b51ba-p107">To navigate to a specific parent or child site, construct the appropriate REST URL to that site using the  **Id** or **Title** property to. From there, you can access that site's related entity sets.</span></span>
 

 

## <a name="navigating-folder-structure"></a><span data-ttu-id="b51ba-137">Навигация по структуре папок</span><span class="sxs-lookup"><span data-stu-id="b51ba-137">Navigating folder structure</span></span>
<span data-ttu-id="b51ba-138"><a name="bk_folders"> </a></span><span class="sxs-lookup"><span data-stu-id="b51ba-138"></span></span>

<span data-ttu-id="b51ba-p108"> Служба REST SharePoint не поддерживает переход по иерархии папок сайта путем составления URL-адресов. Вместо этого можно использовать аналог метода **Web.GetFolderByServerRelativeUrl** в службе REST. Например:</span><span class="sxs-lookup"><span data-stu-id="b51ba-p108">The SharePoint REST service does not support traversing the folder hierarchy of a site through the URL construction. Instead, use the REST equivalent of the  **Web.GetFolderByServerRelativeUrl** method. For example:</span></span>
 

 
 <span data-ttu-id="b51ba-142">*Функции навигации, не поддерживаемые в службе REST:*</span><span class="sxs-lookup"><span data-stu-id="b51ba-142">*Navigation not supported through the REST service:*</span></span> 
 

 
 `/_vti_bin/client.svc/web/lists/SharedDocuments/folder1/stuff/things/Recycle`
 

 
<span data-ttu-id="b51ba-143">Навигация, поддерживаемая в службе REST:</span><span class="sxs-lookup"><span data-stu-id="b51ba-143">Navigation that is supported by the REST service:</span></span> 
 

 
 <span data-ttu-id="b51ba-144">`/_vti_bin/client.svc/web/GetFolderByServerRelativeUrl('SharedDocuments/folder1/stuff/things')/Recycle`.</span><span class="sxs-lookup"><span data-stu-id="b51ba-144"></span></span>
 

 

## <a name="spcontextwebinformation-object-properties"></a><span data-ttu-id="b51ba-145">Свойства объекта SPContextWebInformation</span><span class="sxs-lookup"><span data-stu-id="b51ba-145">SPContextWebInformation object properties</span></span>
<span data-ttu-id="b51ba-146"><a name="bk_props"> </a></span><span class="sxs-lookup"><span data-stu-id="b51ba-146"></span></span>



|<span data-ttu-id="b51ba-147">**Свойство SPContextWebInformation**</span><span class="sxs-lookup"><span data-stu-id="b51ba-147">**SPContextWebInformation Property**</span></span>|<span data-ttu-id="b51ba-148">**Описание**</span><span class="sxs-lookup"><span data-stu-id="b51ba-148">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="b51ba-149">**webFullUrl**</span><span class="sxs-lookup"><span data-stu-id="b51ba-149">**webFullUrl**</span></span>|<span data-ttu-id="b51ba-150">Возвращает URL-адрес относительно сервера для ближайшего сайта.</span><span class="sxs-lookup"><span data-stu-id="b51ba-150">Gets the server-relative URL of the nearest site.</span></span>|
|<span data-ttu-id="b51ba-151">**siteFullUrl**</span><span class="sxs-lookup"><span data-stu-id="b51ba-151">**siteFullUrl**</span></span>|<span data-ttu-id="b51ba-152">Возвращает URL-адрес относительно сервера для корня семейства веб-сайтов, включающего текущий сайт. Если ближайший веб-сайт является корнем семейства веб-сайтов, значение свойства **webFullUrl** будет совпадать со значением свойства **siteFullUrl**.</span><span class="sxs-lookup"><span data-stu-id="b51ba-152">Gets the server-relative URL of the root of the site collection that the site is contained within.If the nearest web is the root of a site collection, then the value of the  **webFullUrl** property is equal to the **siteFullUrl** property.</span></span>|
|<span data-ttu-id="b51ba-153">**formDigestValue**</span><span class="sxs-lookup"><span data-stu-id="b51ba-153">**formDigestValue**</span></span>|<span data-ttu-id="b51ba-154">Возвращает дайджест формы запроса сервера.</span><span class="sxs-lookup"><span data-stu-id="b51ba-154">Gets the server's request form digest.</span></span>|
|<span data-ttu-id="b51ba-155">**LibraryVersion**</span><span class="sxs-lookup"><span data-stu-id="b51ba-155">**LibraryVersion**</span></span>|<span data-ttu-id="b51ba-156">Возвращает текущую версию библиотеки REST.</span><span class="sxs-lookup"><span data-stu-id="b51ba-156">Gets the current version of the REST library.</span></span>|
|<span data-ttu-id="b51ba-157">**SupportedSchemaVersions**</span><span class="sxs-lookup"><span data-stu-id="b51ba-157">**SupportedSchemaVersions**</span></span>|<span data-ttu-id="b51ba-158">Получает поддерживаемые версии схемы библиотеки REST/CSOM.</span><span class="sxs-lookup"><span data-stu-id="b51ba-158">Gets the versions of the schema of the REST/CSOM library that are supported.</span></span>|

## <a name="webinfo-object"></a><span data-ttu-id="b51ba-159">Объект WebInfo</span><span class="sxs-lookup"><span data-stu-id="b51ba-159">WebInfo object</span></span>
<span data-ttu-id="b51ba-160"><a name="bk_webinfo"> </a></span><span class="sxs-lookup"><span data-stu-id="b51ba-160"></span></span>



|<span data-ttu-id="b51ba-161">**Свойство WebInfo**</span><span class="sxs-lookup"><span data-stu-id="b51ba-161">**WebInfo property**</span></span>|<span data-ttu-id="b51ba-162">**Описание**</span><span class="sxs-lookup"><span data-stu-id="b51ba-162">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="b51ba-163">**Created**</span><span class="sxs-lookup"><span data-stu-id="b51ba-163">**Created**</span></span>|<span data-ttu-id="b51ba-164">Возвращает значение, определяющее, когда был создан сайт.</span><span class="sxs-lookup"><span data-stu-id="b51ba-164">Gets a value that specifies when the site was created.</span></span>|
|<span data-ttu-id="b51ba-165">**Description**</span><span class="sxs-lookup"><span data-stu-id="b51ba-165">**Description**</span></span>|<span data-ttu-id="b51ba-166">Возвращает или задает описание сайта.</span><span class="sxs-lookup"><span data-stu-id="b51ba-166">Gets or sets the description for the site.</span></span>|
|<span data-ttu-id="b51ba-167">**Id**</span><span class="sxs-lookup"><span data-stu-id="b51ba-167">**Id**</span></span>|<span data-ttu-id="b51ba-168">Возвращает значение, указывающее идентификатор сайта.</span><span class="sxs-lookup"><span data-stu-id="b51ba-168">Gets a value that specifies the site identifier.</span></span>|
|<span data-ttu-id="b51ba-169">**Language**</span><span class="sxs-lookup"><span data-stu-id="b51ba-169">**Language**</span></span>|<span data-ttu-id="b51ba-170">Возвращает значение, указывающее код языка, используемого на сайте.</span><span class="sxs-lookup"><span data-stu-id="b51ba-170">Gets a value that specifies the locale ID (LCID) for the language that is used on the site.</span></span>|
|<span data-ttu-id="b51ba-171">**LastItemModifiedDate**</span><span class="sxs-lookup"><span data-stu-id="b51ba-171">**LastItemModifiedDate**</span></span>|<span data-ttu-id="b51ba-172">Возвращает значение, определяющее, когда в последний раз был изменен элемент на сайте.</span><span class="sxs-lookup"><span data-stu-id="b51ba-172">Gets a value that specifies when an item was last modified in the site.</span></span>|
|<span data-ttu-id="b51ba-173">**Title**</span><span class="sxs-lookup"><span data-stu-id="b51ba-173">**Title**</span></span>|<span data-ttu-id="b51ba-174">Получает или задает название сайта.</span><span class="sxs-lookup"><span data-stu-id="b51ba-174">Gets or sets the title for the site.</span></span>|
|<span data-ttu-id="b51ba-175">**WebTemplateId**</span><span class="sxs-lookup"><span data-stu-id="b51ba-175">**WebTemplateId**</span></span>|<span data-ttu-id="b51ba-176">Получает идентификатор шаблона сайта.</span><span class="sxs-lookup"><span data-stu-id="b51ba-176">Gets the identifier of the site template.</span></span>|

## <a name="additional-resources"></a><span data-ttu-id="b51ba-177">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b51ba-177">Additional resources</span></span>
<span data-ttu-id="b51ba-178"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="b51ba-178"></span></span>


-  [<span data-ttu-id="b51ba-179">Знакомство со службой REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="b51ba-179">Get to know the SharePoint REST service</span></span>](get-to-know-the-sharepoint-2013-rest-service)
    
 
-  [<span data-ttu-id="b51ba-180">Выполнение базовых операций с использованием конечных точек SharePoint REST</span><span class="sxs-lookup"><span data-stu-id="b51ba-180">Complete basic operations using SharePoint REST endpoints</span></span>](complete-basic-operations-using-sharepoint-2013-rest-endpoints)
    
 
-  [<span data-ttu-id="b51ba-181">Работа со списками и элементами списков в интерфейсе REST</span><span class="sxs-lookup"><span data-stu-id="b51ba-181">Working with lists and list items with REST</span></span>](working-with-lists-and-list-items-with-rest)
    
 
-  [<span data-ttu-id="b51ba-182">Работа с папками и файлами в службе REST</span><span class="sxs-lookup"><span data-stu-id="b51ba-182">Working with folders and files with REST</span></span>](working-with-folders-and-files-with-rest)
    
 
-  [<span data-ttu-id="b51ba-183">Определение URI для конечных точек службы REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="b51ba-183">Determine SharePoint REST service endpoint URIs</span></span>](determine-sharepoint-rest-service-endpoint-uris)
    
 
-  [<span data-ttu-id="b51ba-184">Использование операций запросов OData в запросах REST SharePoint</span><span class="sxs-lookup"><span data-stu-id="b51ba-184">Use OData query operations in SharePoint REST requests</span></span>](use-odata-query-operations-in-sharepoint-rest-requests)
    
 
-  [<span data-ttu-id="b51ba-185">Справочные материалы и примеры по REST API</span><span class="sxs-lookup"><span data-stu-id="b51ba-185">REST API reference and samples</span></span>](http://msdn.microsoft.com/library/rest-api-reference-and-samples%28Office.15%29.aspx)
    
 
-  [<span data-ttu-id="b51ba-186">Синхронизация элементов SharePoint с помощью службы REST</span><span class="sxs-lookup"><span data-stu-id="b51ba-186">Synchronize SharePoint items using the REST service</span></span>](synchronize-sharepoint-items-using-the-rest-service)
    
 
-  [<span data-ttu-id="b51ba-187">Получение версий элементов списков и документов с помощью значений ETag в службе REST</span><span class="sxs-lookup"><span data-stu-id="b51ba-187">Use ETag values through the REST service to get document list item versioning</span></span>](http://msdn.microsoft.com/library/5f7e0579-46b7-44ab-b3b4-cdbc622dcd98%28Office.15%29.aspx)
    
 

 

 

