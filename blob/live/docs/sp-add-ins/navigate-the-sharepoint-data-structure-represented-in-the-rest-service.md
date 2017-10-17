---
title: "Навигация по структуре данных SharePoint, представленной в службе REST"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: ef5a5b8056899acfa2f55096111ab24b8fdbf49c
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="navigate-the-sharepoint-data-structure-represented-in-the-rest-service"></a><span data-ttu-id="28db6-102">Навигация по структуре данных SharePoint, представленной в службе REST</span><span class="sxs-lookup"><span data-stu-id="28db6-102">Navigate the SharePoint data structure represented in the REST service</span></span>
<span data-ttu-id="28db6-103">Узнайте, как с помощью конечной точки REST в элементе SharePoint получить доступ к связанным элементам, например родительским сайтам или структуре библиотеки, в которой находится этот элемент.</span><span class="sxs-lookup"><span data-stu-id="28db6-103">Learn how to start from a REST endpoint for a given SharePoint item, and navigate to and access related items, such as parent sites or the library structure where that item resides.</span></span> 
 

 <span data-ttu-id="28db6-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="28db6-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 


## <a name="navigate-from-a-given-url-to-reach-other-sharepoint-resources"></a><span data-ttu-id="28db6-107">Переход от заданного URL-адреса к другим ресурсам SharePoint</span><span class="sxs-lookup"><span data-stu-id="28db6-107">Navigate from a given URL to reach other SharePoint resources</span></span>

<span data-ttu-id="28db6-p102">При работе со службой REST SharePoint вы часто начинаете с того, что узнаете URL-адрес определенного элемента SharePoint, но хотите получить доступ к связанным элементам, например папке или структуре библиотеки, в которой находится элемент. Предположим, что вы создаете надстройку, где пользователь вводит URL-адрес документа в библиотеке SharePoint. Ваша надстройка должна затем разбить этот URL-адрес, чтобы вычислить фактический URL-адрес сайта SharePoint. После этого надстройка может отправлять больше запросов от имени пользователя, например для создания, обновления или удаления связанных элементов или ресурсов.</span><span class="sxs-lookup"><span data-stu-id="28db6-p102">When you're working with the SharePoint REST service, you'll often start out knowing the URL of a specific SharePoint item, but want to access related items, such as the folder or library structure where that item resides. For example, suppose you create an add-in where your user enters the URL of a document in a SharePoint library. Your add-in must then break down that URL to figure out the actual SharePoint site URL. Once it's done that, the add-in can then make more requests from the site on the user's behalf, such as to create, update, or delete related items or resources.</span></span> 
 

 
<span data-ttu-id="28db6-112">Для этого надстройка должна запросить у SharePoint следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="28db6-112">To do this, your add-in needs to query SharePoint for the following information:</span></span>
 

 

- <span data-ttu-id="28db6-113">URL-адреса относительно сервера для сайта и семейства веб-сайтов, содержащих ресурс.</span><span class="sxs-lookup"><span data-stu-id="28db6-113">The server relative URLs of the site and site collection containing the resource</span></span>
    
 
- <span data-ttu-id="28db6-114">Дайджест формы, позволяющий выполнять запросы, меняющие состояние ресурса, например **POST**, **PUT**, **MERGE** и **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="28db6-114">A form digest to enable you to perform requests that change the state of the resource, such as  **POST**,  **PUT**,  **MERGE**, and  **DELETE**</span></span>
    
 
<span data-ttu-id="28db6-115">Базовый процесс:</span><span class="sxs-lookup"><span data-stu-id="28db6-115">The basic process:</span></span>
 

 

1. <span data-ttu-id="28db6-p103">Используйте оператор `/contextinfo` с заданным URL-адресом для доступа к сайту и семейству веб-сайтов, а также дайджестом формы. Используйте оператор `/contextinfo` в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="28db6-p103">Use the  `/contextinfo` operator with the given URL to access the site and site collection addresses, and the form digest. Use the `/contextinfo` operator in the following format:</span></span>
    
     `http://server/web/doclib/forms/_api/contextinfo`
    
    <span data-ttu-id="28db6-118">Чтобы усилить защиту от межсайтовых сценариев, оператор `/contextinfo` принимает только запросы **POST**.</span><span class="sxs-lookup"><span data-stu-id="28db6-118">To increase security against cross-site scripting attempts, the  `/contextinfo` operator accepts only **POST** requests.</span></span>
    
 
2. <span data-ttu-id="28db6-119">Используйте [свойства объекта SPContextWebInformation](#bk_props), возвращаемые оператором `/contextinfo`, для доступа к дополнительным ресурсам по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="28db6-119">Use the  [SPContextWebInformation object properties](#bk_props) that the `/contextinfo` operator returns to access additional resources as desired.</span></span>
    
 
 <span data-ttu-id="28db6-120">**Попробуйте сами**</span><span class="sxs-lookup"><span data-stu-id="28db6-120">**Try it**</span></span>
 

 

1. <span data-ttu-id="28db6-p104">Начните с URL-адреса определенного элемента SharePoint. Например:</span><span class="sxs-lookup"><span data-stu-id="28db6-p104">Start with a URL to a given SharePoint item. For example:</span></span>
    
     `http://site/web/doclib/myDocument.docx`
    
 
2. <span data-ttu-id="28db6-p105">Удалите имя ресурса в конце URL-адреса таким образом, чтобы URL-адрес указывал на библиотеку документа, папку или список. В данном случае:</span><span class="sxs-lookup"><span data-stu-id="28db6-p105">Remove the name of the specific resource from the end of the URL, so that the URL points to a document library, folder, or list. IN this case:</span></span>
    
     `http://site/web/doclib/`
    
 
3. <span data-ttu-id="28db6-125">Добавьте указатель службы REST и оператор `/contextinfo` к URL-адресу:</span><span class="sxs-lookup"><span data-stu-id="28db6-125">Append the REST service pointer and the  `/contextinfo` operator to the URL:</span></span>
    
     `http://site/web/doclib/_api/contextinfo`
    
 
4. <span data-ttu-id="28db6-126">Прочитайте дайджест формы и свойства **webFullUrl** из отклика.</span><span class="sxs-lookup"><span data-stu-id="28db6-126">Read the form digest and  **webFullUrl** properties from the response.</span></span>
    
 
5. <span data-ttu-id="28db6-127">Добавьте указатель службы REST `_api` в конец URL-адреса веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="28db6-127">Append the REST service pointer  `_api` to the web URL</span></span>
    
 
6. <span data-ttu-id="28db6-128">Используйте полученный URL-адрес и дайджест формы для отправки запросов о других нужных ресурсах.</span><span class="sxs-lookup"><span data-stu-id="28db6-128">Use the resulting URL and the form digest to make requests for other resources you need.</span></span>
    
 
<span data-ttu-id="28db6-129">При отправке запросов **GET** или отправке запросов с использованием проверенного маркера OAuth передавать дайджест формы не требуется.</span><span class="sxs-lookup"><span data-stu-id="28db6-129">You don't have to pass the form digest if you're making  **GET** requests, or making requests using a validated OAuth token.</span></span>
 

 

## <a name="navigate-parent-and-child-sites"></a><span data-ttu-id="28db6-130">Навигация по родительским и дочерним сайтам</span><span class="sxs-lookup"><span data-stu-id="28db6-130">Navigate parent and child sites</span></span>
<span data-ttu-id="28db6-131"><a name="bk_sites"> </a></span><span class="sxs-lookup"><span data-stu-id="28db6-131"></span></span>

<span data-ttu-id="28db6-132"> При навигации по структуре сайтов с помощью серверной объектной модели SharePoint используются свойства **SPWeb.ParentWeb** и **SPWeb.Webs** для доступа к объектам, представляющим родительские и дочерние сайты.</span><span class="sxs-lookup"><span data-stu-id="28db6-132">When you navigate your site structure using the SharePoint server object model, you use the  **SPWeb.ParentWeb** and **SPWeb.Webs** properties to access objects that represent parent and child sites.</span></span>
 

 
<span data-ttu-id="28db6-p106">Соответствующие ресурсы REST — `web/parentweb` и `web/webs` — не возвращают объекты, представляющие сайты. Это вызвано тем, что служба REST соответствует стандартам OData, а возврат готовых представлений сайтов сделал бы такие запросы неэффективными. Вместо этого они возвращают [объект WebInfo](#bk_webinfo), содержащий скалярные свойства сайта, но без связанных наборов сущностей, таких как коллекции или семейства полей.</span><span class="sxs-lookup"><span data-stu-id="28db6-p106">The corresponding REST resources— `web/parentweb` and `web/webs`—don't return objects that represent sites. This is because the REST service conforms to OData standards, and returning complete site representations would make such requests inefficient. Instead, they return a  [WebInfo object ](#bk_webinfo) that contains the site's scalar properties, but without related entity sets such as like collections or field collections.</span></span>
 

 
<span data-ttu-id="28db6-p107">Чтобы перейти к определенному родительскому или дочернему сайту, составьте подходящий URL-адрес REST этого сайта с помощью свойства **Id** или **Title**. После этого вы можете получить доступ к наборам сущностей, связанным с этим сайтом.</span><span class="sxs-lookup"><span data-stu-id="28db6-p107">To navigate to a specific parent or child site, construct the appropriate REST URL to that site using the  **Id** or **Title** property to. From there, you can access that site's related entity sets.</span></span>
 

 

## <a name="navigating-folder-structure"></a><span data-ttu-id="28db6-138">Навигация по структуре папок</span><span class="sxs-lookup"><span data-stu-id="28db6-138">Navigating folder structure</span></span>
<span data-ttu-id="28db6-139"><a name="bk_folders"> </a></span><span class="sxs-lookup"><span data-stu-id="28db6-139"></span></span>

<span data-ttu-id="28db6-p108"> Служба REST SharePoint не поддерживает переход по иерархии папок сайта путем составления URL-адресов. Вместо этого можно использовать аналог метода **Web.GetFolderByServerRelativeUrl** в службе REST. Например:</span><span class="sxs-lookup"><span data-stu-id="28db6-p108">The SharePoint REST service does not support traversing the folder hierarchy of a site through the URL construction. Instead, use the REST equivalent of the  **Web.GetFolderByServerRelativeUrl** method. For example:</span></span>
 

 
 <span data-ttu-id="28db6-143">*Функции навигации, не поддерживаемые в службе REST:*</span><span class="sxs-lookup"><span data-stu-id="28db6-143">*Navigation not supported through the REST service:*</span></span> 
 

 
 `/_vti_bin/client.svc/web/lists/SharedDocuments/folder1/stuff/things/Recycle`
 

 
<span data-ttu-id="28db6-144">Навигация, поддерживаемая в службе REST:</span><span class="sxs-lookup"><span data-stu-id="28db6-144">Navigation that is supported by the REST service:</span></span> 
 

 
 <span data-ttu-id="28db6-145">`/_vti_bin/client.svc/web/GetFolderByServerRelativeUrl('SharedDocuments/folder1/stuff/things')/Recycle`.</span><span class="sxs-lookup"><span data-stu-id="28db6-145"></span></span>
 

 

## <a name="spcontextwebinformation-object-properties"></a><span data-ttu-id="28db6-146">Свойства объекта SPContextWebInformation</span><span class="sxs-lookup"><span data-stu-id="28db6-146">SPContextWebInformation object properties</span></span>
<span data-ttu-id="28db6-147"><a name="bk_props"> </a></span><span class="sxs-lookup"><span data-stu-id="28db6-147"></span></span>



|<span data-ttu-id="28db6-148">**Свойство SPContextWebInformation**</span><span class="sxs-lookup"><span data-stu-id="28db6-148">**SPContextWebInformation Property**</span></span>|<span data-ttu-id="28db6-149">**Описание**</span><span class="sxs-lookup"><span data-stu-id="28db6-149">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="28db6-150">**webFullUrl**</span><span class="sxs-lookup"><span data-stu-id="28db6-150">**webFullUrl**</span></span>|<span data-ttu-id="28db6-151">Возвращает URL-адрес относительно сервера для ближайшего сайта.</span><span class="sxs-lookup"><span data-stu-id="28db6-151">Gets the server-relative URL of the nearest site.</span></span>|
|<span data-ttu-id="28db6-152">**siteFullUrl**</span><span class="sxs-lookup"><span data-stu-id="28db6-152">**siteFullUrl**</span></span>|<span data-ttu-id="28db6-153">Возвращает URL-адрес относительно сервера для корня семейства веб-сайтов, включающего текущий сайт. Если ближайший веб-сайт является корнем семейства веб-сайтов, значение свойства **webFullUrl** будет совпадать со значением свойства **siteFullUrl**.</span><span class="sxs-lookup"><span data-stu-id="28db6-153">Gets the server-relative URL of the root of the site collection that the site is contained within.If the nearest web is the root of a site collection, then the value of the  **webFullUrl** property is equal to the **siteFullUrl** property.</span></span>|
|<span data-ttu-id="28db6-154">**formDigestValue**</span><span class="sxs-lookup"><span data-stu-id="28db6-154">**formDigestValue**</span></span>|<span data-ttu-id="28db6-155">Возвращает дайджест формы запроса сервера.</span><span class="sxs-lookup"><span data-stu-id="28db6-155">Gets the server's request form digest.</span></span>|
|<span data-ttu-id="28db6-156">**LibraryVersion**</span><span class="sxs-lookup"><span data-stu-id="28db6-156">**LibraryVersion**</span></span>|<span data-ttu-id="28db6-157">Возвращает текущую версию библиотеки REST.</span><span class="sxs-lookup"><span data-stu-id="28db6-157">Gets the current version of the REST library.</span></span>|
|<span data-ttu-id="28db6-158">**SupportedSchemaVersions**</span><span class="sxs-lookup"><span data-stu-id="28db6-158">**SupportedSchemaVersions**</span></span>|<span data-ttu-id="28db6-159">Получает поддерживаемые версии схемы библиотеки REST/CSOM.</span><span class="sxs-lookup"><span data-stu-id="28db6-159">Gets the versions of the schema of the REST/CSOM library that are supported.</span></span>|

## <a name="webinfo-object"></a><span data-ttu-id="28db6-160">Объект WebInfo</span><span class="sxs-lookup"><span data-stu-id="28db6-160">WebInfo object</span></span>
<span data-ttu-id="28db6-161"><a name="bk_webinfo"> </a></span><span class="sxs-lookup"><span data-stu-id="28db6-161"></span></span>



|<span data-ttu-id="28db6-162">**Свойство WebInfo**</span><span class="sxs-lookup"><span data-stu-id="28db6-162">**WebInfo property**</span></span>|<span data-ttu-id="28db6-163">**Описание**</span><span class="sxs-lookup"><span data-stu-id="28db6-163">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="28db6-164">**Created**</span><span class="sxs-lookup"><span data-stu-id="28db6-164">**Created**</span></span>|<span data-ttu-id="28db6-165">Возвращает значение, определяющее, когда был создан сайт.</span><span class="sxs-lookup"><span data-stu-id="28db6-165">Gets a value that specifies when the site was created.</span></span>|
|<span data-ttu-id="28db6-166">**Description**</span><span class="sxs-lookup"><span data-stu-id="28db6-166">**Description**</span></span>|<span data-ttu-id="28db6-167">Возвращает или задает описание сайта.</span><span class="sxs-lookup"><span data-stu-id="28db6-167">Gets or sets the description for the site.</span></span>|
|<span data-ttu-id="28db6-168">**Id**</span><span class="sxs-lookup"><span data-stu-id="28db6-168">**Id**</span></span>|<span data-ttu-id="28db6-169">Возвращает значение, указывающее идентификатор сайта.</span><span class="sxs-lookup"><span data-stu-id="28db6-169">Gets a value that specifies the site identifier.</span></span>|
|<span data-ttu-id="28db6-170">**Language**</span><span class="sxs-lookup"><span data-stu-id="28db6-170">**Language**</span></span>|<span data-ttu-id="28db6-171">Возвращает значение, указывающее код языка, используемого на сайте.</span><span class="sxs-lookup"><span data-stu-id="28db6-171">Gets a value that specifies the locale ID (LCID) for the language that is used on the site.</span></span>|
|<span data-ttu-id="28db6-172">**LastItemModifiedDate**</span><span class="sxs-lookup"><span data-stu-id="28db6-172">**LastItemModifiedDate**</span></span>|<span data-ttu-id="28db6-173">Возвращает значение, определяющее, когда в последний раз был изменен элемент на сайте.</span><span class="sxs-lookup"><span data-stu-id="28db6-173">Gets a value that specifies when an item was last modified in the site.</span></span>|
|<span data-ttu-id="28db6-174">**Title**</span><span class="sxs-lookup"><span data-stu-id="28db6-174">**Title**</span></span>|<span data-ttu-id="28db6-175">Получает или задает название сайта.</span><span class="sxs-lookup"><span data-stu-id="28db6-175">Gets or sets the title for the site.</span></span>|
|<span data-ttu-id="28db6-176">**WebTemplateId**</span><span class="sxs-lookup"><span data-stu-id="28db6-176">**WebTemplateId**</span></span>|<span data-ttu-id="28db6-177">Получает идентификатор шаблона сайта.</span><span class="sxs-lookup"><span data-stu-id="28db6-177">Gets the identifier of the site template.</span></span>|

## <a name="additional-resources"></a><span data-ttu-id="28db6-178">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="28db6-178">Additional resources</span></span>
<span data-ttu-id="28db6-179"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="28db6-179"></span></span>


-  [<span data-ttu-id="28db6-180">Знакомство со службой REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="28db6-180">Get to know the SharePoint REST service</span></span>](get-to-know-the-sharepoint-rest-service.md)
    
 
-  [<span data-ttu-id="28db6-181">Выполнение базовых операций с использованием конечных точек SharePoint REST</span><span class="sxs-lookup"><span data-stu-id="28db6-181">Complete basic operations using SharePoint REST endpoints</span></span>](complete-basic-operations-using-sharepoint-rest-endpoints.md)
    
 
-  [<span data-ttu-id="28db6-182">Работа со списками и элементами списков в интерфейсе REST</span><span class="sxs-lookup"><span data-stu-id="28db6-182">Working with lists and list items with REST</span></span>](working-with-lists-and-list-items-with-rest.md)
    
 
-  [<span data-ttu-id="28db6-183">Работа с папками и файлами в службе REST</span><span class="sxs-lookup"><span data-stu-id="28db6-183">Working with folders and files with REST</span></span>](working-with-folders-and-files-with-rest.md)
    
 
-  [<span data-ttu-id="28db6-184">Определение URI для конечных точек службы REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="28db6-184">Determine SharePoint REST service endpoint URIs</span></span>](determine-sharepoint-rest-service-endpoint-uris.md)
    
 
-  [<span data-ttu-id="28db6-185">Использование операций запросов OData в запросах REST SharePoint</span><span class="sxs-lookup"><span data-stu-id="28db6-185">Use OData query operations in SharePoint REST requests</span></span>](use-odata-query-operations-in-sharepoint-rest-requests.md)
    
 
-  [<span data-ttu-id="28db6-186">Справочные материалы и примеры по REST API</span><span class="sxs-lookup"><span data-stu-id="28db6-186">REST API reference and samples</span></span>](http://msdn.microsoft.com/library/rest-api-reference-and-samples%28Office.15%29.aspx)
    
 
-  [<span data-ttu-id="28db6-187">Синхронизация элементов SharePoint с помощью службы REST</span><span class="sxs-lookup"><span data-stu-id="28db6-187">Synchronize SharePoint items using the REST service</span></span>](synchronize-sharepoint-items-using-the-rest-service.md)
    
 
-  [<span data-ttu-id="28db6-188">Получение версий элементов списков и документов с помощью значений ETag в службе REST</span><span class="sxs-lookup"><span data-stu-id="28db6-188">Use ETag values through the REST service to get document list item versioning</span></span>](http://msdn.microsoft.com/library/5f7e0579-46b7-44ab-b3b4-cdbc622dcd98%28Office.15%29.aspx)
    
 

 

 

