---
title: "Навигация по структуре данных SharePoint, представленной в службе REST"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: f4cd8be2a34150e72c476194956dd3e8527ab8a9
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="navigate-the-sharepoint-data-structure-represented-in-the-rest-service"></a><span data-ttu-id="ab64b-102">Навигация по структуре данных SharePoint, представленной в службе REST</span><span class="sxs-lookup"><span data-stu-id="ab64b-102">Navigate the SharePoint data structure represented in the REST service</span></span>
<span data-ttu-id="ab64b-103">Узнайте, как с помощью конечной точки REST в элементе SharePoint получить доступ к связанным элементам, например родительским сайтам или структуре библиотеки, в которой находится этот элемент.</span><span class="sxs-lookup"><span data-stu-id="ab64b-103">Learn how to start from a REST endpoint for a given SharePoint item, and navigate to and access related items, such as parent sites or the library structure where that item resides.</span></span> 
 
## <a name="navigate-from-a-given-url-to-reach-other-sharepoint-resources"></a><span data-ttu-id="ab64b-104">Переход от заданного URL-адреса к другим ресурсам SharePoint</span><span class="sxs-lookup"><span data-stu-id="ab64b-104">Navigate from a given URL to reach other SharePoint resources</span></span>
<span data-ttu-id="ab64b-p101">При работе со службой REST SharePoint вы часто начинаете с того, что узнаете URL-адрес определенного элемента SharePoint, но хотите получить доступ к связанным элементам, например папке или структуре библиотеки, в которой находится элемент. Предположим, что вы создаете надстройку, где пользователь вводит URL-адрес документа в библиотеке SharePoint. Ваша надстройка должна затем разбить этот URL-адрес, чтобы вычислить фактический URL-адрес сайта SharePoint. После этого надстройка может отправлять больше запросов от имени пользователя, например для создания, обновления или удаления связанных элементов или ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ab64b-p101">When you're working with the SharePoint REST service, you'll often start out knowing the URL of a specific SharePoint item, but want to access related items, such as the folder or library structure where that item resides. For example, suppose you create an add-in where your user enters the URL of a document in a SharePoint library. Your add-in must then break down that URL to figure out the actual SharePoint site URL. Once it's done that, the add-in can then make more requests from the site on the user's behalf, such as to create, update, or delete related items or resources.</span></span> 
 
<span data-ttu-id="ab64b-109">Для этого надстройка должна запросить у SharePoint следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="ab64b-109">To do this, your add-in needs to query SharePoint for the following information:</span></span>
 
- <span data-ttu-id="ab64b-110">URL-адреса относительно сервера для сайта и семейства веб-сайтов, содержащих ресурс.</span><span class="sxs-lookup"><span data-stu-id="ab64b-110">The server relative URLs of the site and site collection containing the resource</span></span>   
 
- <span data-ttu-id="ab64b-111">Дайджест формы, позволяющий выполнять запросы, меняющие состояние ресурса, например **POST**, **PUT**, **MERGE** и **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="ab64b-111">A form digest to enable you to perform requests that change the state of the resource, such as  **POST**,  **PUT**,  **MERGE**, and  **DELETE**</span></span>
    
<span data-ttu-id="ab64b-112">Базовый процесс:</span><span class="sxs-lookup"><span data-stu-id="ab64b-112">The basic process:</span></span>

1. <span data-ttu-id="ab64b-p102">Используйте оператор `/contextinfo` с заданным URL-адресом для доступа к сайту и семейству веб-сайтов, а также дайджестом формы. Используйте оператор `/contextinfo` в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="ab64b-p102">Use the  `/contextinfo` operator with the given URL to access the site and site collection addresses, and the form digest. Use the `/contextinfo` operator in the following format:</span></span>
    
     `http://server/web/doclib/forms/_api/contextinfo`
    
    <span data-ttu-id="ab64b-115">Чтобы усилить защиту от межсайтовых сценариев, оператор `/contextinfo` принимает только запросы **POST**.</span><span class="sxs-lookup"><span data-stu-id="ab64b-115">To increase security against cross-site scripting attempts, the  `/contextinfo` operator accepts only **POST** requests.</span></span>
    
 
2. <span data-ttu-id="ab64b-116">Используйте [свойства объекта SPContextWebInformation](#bk_props), возвращаемые оператором `/contextinfo`, для доступа к дополнительным ресурсам по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="ab64b-116">Use the  [SPContextWebInformation object properties](#bk_props) that the `/contextinfo` operator returns to access additional resources as desired.</span></span>
    
 
 <span data-ttu-id="ab64b-117">**Попробуйте сами**</span><span class="sxs-lookup"><span data-stu-id="ab64b-117">**Try it**</span></span>
 

1. <span data-ttu-id="ab64b-p103">Начните с URL-адреса определенного элемента SharePoint. Например:</span><span class="sxs-lookup"><span data-stu-id="ab64b-p103">Start with a URL to a given SharePoint item. For example:</span></span>
    
     `http://site/web/doclib/myDocument.docx`
     
2. <span data-ttu-id="ab64b-p104">Удалите имя ресурса в конце URL-адреса таким образом, чтобы URL-адрес указывал на библиотеку документа, папку или список. В данном случае:</span><span class="sxs-lookup"><span data-stu-id="ab64b-p104">Remove the name of the specific resource from the end of the URL, so that the URL points to a document library, folder, or list. IN this case:</span></span>
    
     `http://site/web/doclib/`
    
3. <span data-ttu-id="ab64b-122">Добавьте указатель службы REST и оператор `/contextinfo` к URL-адресу:</span><span class="sxs-lookup"><span data-stu-id="ab64b-122">Append the REST service pointer and the  `/contextinfo` operator to the URL:</span></span>
    
     `http://site/web/doclib/_api/contextinfo`
    
4. <span data-ttu-id="ab64b-123">Прочитайте дайджест формы и свойства **webFullUrl** из отклика.</span><span class="sxs-lookup"><span data-stu-id="ab64b-123">Read the form digest and  **webFullUrl** properties from the response.</span></span>
    
5. <span data-ttu-id="ab64b-124">Добавьте указатель службы REST `_api` в конец URL-адреса веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="ab64b-124">Append the REST service pointer  `_api` to the web URL</span></span>
    
6. <span data-ttu-id="ab64b-125">Используйте полученный URL-адрес и дайджест формы для отправки запросов о других нужных ресурсах.</span><span class="sxs-lookup"><span data-stu-id="ab64b-125">Use the resulting URL and the form digest to make requests for other resources you need.</span></span>
    
<span data-ttu-id="ab64b-126">При отправке запросов **GET** или отправке запросов с использованием проверенного маркера OAuth передавать дайджест формы не требуется.</span><span class="sxs-lookup"><span data-stu-id="ab64b-126">You don't have to pass the form digest if you're making  **GET** requests, or making requests using a validated OAuth token.</span></span>
 
## <a name="navigate-parent-and-child-sites"></a><span data-ttu-id="ab64b-127">Навигация по родительским и дочерним сайтам</span><span class="sxs-lookup"><span data-stu-id="ab64b-127">Navigate parent and child sites</span></span>
<span data-ttu-id="ab64b-128"><a name="bk_sites"> </a> При навигации по структуре сайтов с помощью серверной объектной модели SharePoint используются свойства **SPWeb.ParentWeb** и **SPWeb.Webs** для доступа к объектам, представляющим родительские и дочерние сайты.</span><span class="sxs-lookup"><span data-stu-id="ab64b-128"><a name="bk_sites"> </a> When you navigate your site structure using the SharePoint server object model, you use the  **SPWeb.ParentWeb** and **SPWeb.Webs** properties to access objects that represent parent and child sites.</span></span>

<span data-ttu-id="ab64b-p105">Соответствующие ресурсы REST — `web/parentweb` и `web/webs` — не возвращают объекты, представляющие сайты. Это вызвано тем, что служба REST соответствует стандартам OData, а возврат готовых представлений сайтов сделал бы такие запросы неэффективными. Вместо этого они возвращают [объект WebInfo](#bk_webinfo), содержащий скалярные свойства сайта, но без связанных наборов сущностей, таких как коллекции или семейства полей.</span><span class="sxs-lookup"><span data-stu-id="ab64b-p105">The corresponding REST resources— `web/parentweb` and `web/webs`—don't return objects that represent sites. This is because the REST service conforms to OData standards, and returning complete site representations would make such requests inefficient. Instead, they return a  [WebInfo object ](#bk_webinfo) that contains the site's scalar properties, but without related entity sets such as like collections or field collections.</span></span>
  
<span data-ttu-id="ab64b-p106">Чтобы перейти к определенному родительскому или дочернему сайту, составьте подходящий URL-адрес REST этого сайта с помощью свойства **Id** или **Title**. После этого вы можете получить доступ к наборам сущностей, связанным с этим сайтом.</span><span class="sxs-lookup"><span data-stu-id="ab64b-p106">To navigate to a specific parent or child site, construct the appropriate REST URL to that site using the  **Id** or **Title** property to. From there, you can access that site's related entity sets.</span></span>
 
## <a name="navigating-folder-structure"></a><span data-ttu-id="ab64b-134">Навигация по структуре папок</span><span class="sxs-lookup"><span data-stu-id="ab64b-134">Navigating folder structure</span></span>
<span data-ttu-id="ab64b-135"><a name="bk_folders"> </a> Служба REST SharePoint не поддерживает переход по иерархии папок сайта путем составления URL-адресов.</span><span class="sxs-lookup"><span data-stu-id="ab64b-135"><a name="bk_folders"> </a> The SharePoint REST service does not support traversing the folder hierarchy of a site through the URL construction.</span></span> <span data-ttu-id="ab64b-136">Вместо этого можно использовать аналог метода **Web.GetFolderByServerRelativeUrl** в службе REST.</span><span class="sxs-lookup"><span data-stu-id="ab64b-136">Instead, use the REST equivalent of the  **Web.GetFolderByServerRelativeUrl** method.</span></span> <span data-ttu-id="ab64b-137">Пример:</span><span class="sxs-lookup"><span data-stu-id="ab64b-137">For example:</span></span>
 
 <span data-ttu-id="ab64b-138">*Навигация, не поддерживаемая в службе REST:*</span><span class="sxs-lookup"><span data-stu-id="ab64b-138">*Navigation not supported through the REST service:*</span></span> 
  
 `/_vti_bin/client.svc/web/lists/SharedDocuments/folder1/stuff/things/Recycle`
 
<span data-ttu-id="ab64b-139">Навигация, поддерживаемая в службе REST:</span><span class="sxs-lookup"><span data-stu-id="ab64b-139">Navigation that is supported by the REST service:</span></span> 
 
 <span data-ttu-id="ab64b-140">`/_vti_bin/client.svc/web/GetFolderByServerRelativeUrl('SharedDocuments/folder1/stuff/things')/Recycle`.</span><span class="sxs-lookup"><span data-stu-id="ab64b-140">`/_vti_bin/client.svc/web/GetFolderByServerRelativeUrl('SharedDocuments/folder1/stuff/things')/Recycle`.</span></span>
 

## <a name="spcontextwebinformation-object-properties"></a><span data-ttu-id="ab64b-141">Свойства объекта SPContextWebInformation</span><span class="sxs-lookup"><span data-stu-id="ab64b-141">SPContextWebInformation object properties</span></span>
<span data-ttu-id="ab64b-142"><a name="bk_props"> </a></span><span class="sxs-lookup"><span data-stu-id="ab64b-142"><a name="bk_props"> </a></span></span>

|<span data-ttu-id="ab64b-143">**Свойство SPContextWebInformation**</span><span class="sxs-lookup"><span data-stu-id="ab64b-143">**SPContextWebInformation Property**</span></span>|<span data-ttu-id="ab64b-144">**Описание**</span><span class="sxs-lookup"><span data-stu-id="ab64b-144">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="ab64b-145">**webFullUrl**</span><span class="sxs-lookup"><span data-stu-id="ab64b-145">**webFullUrl**</span></span>|<span data-ttu-id="ab64b-146">Возвращает URL-адрес относительно сервера для ближайшего сайта.</span><span class="sxs-lookup"><span data-stu-id="ab64b-146">Gets the server-relative URL of the nearest site.</span></span>|
|<span data-ttu-id="ab64b-147">**siteFullUrl**</span><span class="sxs-lookup"><span data-stu-id="ab64b-147">**siteFullUrl**</span></span>|<span data-ttu-id="ab64b-148">Возвращает URL-адрес относительно сервера для корня семейства веб-сайтов, включающего текущий сайт. Если ближайший веб-сайт является корнем семейства веб-сайтов, значение свойства **webFullUrl** будет совпадать со значением свойства **siteFullUrl**.</span><span class="sxs-lookup"><span data-stu-id="ab64b-148">Gets the server-relative URL of the root of the site collection that the site is contained within.If the nearest web is the root of a site collection, then the value of the  **webFullUrl** property is equal to the **siteFullUrl** property.</span></span>|
|<span data-ttu-id="ab64b-149">**formDigestValue**</span><span class="sxs-lookup"><span data-stu-id="ab64b-149">**formDigestValue**</span></span>|<span data-ttu-id="ab64b-150">Возвращает дайджест формы запроса сервера.</span><span class="sxs-lookup"><span data-stu-id="ab64b-150">Gets the server's request form digest.</span></span>|
|<span data-ttu-id="ab64b-151">**LibraryVersion**</span><span class="sxs-lookup"><span data-stu-id="ab64b-151">**LibraryVersion**</span></span>|<span data-ttu-id="ab64b-152">Возвращает текущую версию библиотеки REST.</span><span class="sxs-lookup"><span data-stu-id="ab64b-152">Gets the current version of the REST library.</span></span>|
|<span data-ttu-id="ab64b-153">**SupportedSchemaVersions**</span><span class="sxs-lookup"><span data-stu-id="ab64b-153">**SupportedSchemaVersions**</span></span>|<span data-ttu-id="ab64b-154">Получает поддерживаемые версии схемы библиотеки REST/CSOM.</span><span class="sxs-lookup"><span data-stu-id="ab64b-154">Gets the versions of the schema of the REST/CSOM library that are supported.</span></span>|

## <a name="webinfo-object"></a><span data-ttu-id="ab64b-155">Объект WebInfo</span><span class="sxs-lookup"><span data-stu-id="ab64b-155">WebInfo object</span></span>
<span data-ttu-id="ab64b-156"><a name="bk_webinfo"> </a></span><span class="sxs-lookup"><span data-stu-id="ab64b-156"><a name="bk_webinfo"> </a></span></span>

|<span data-ttu-id="ab64b-157">**Свойство WebInfo**</span><span class="sxs-lookup"><span data-stu-id="ab64b-157">**WebInfo property**</span></span>|<span data-ttu-id="ab64b-158">**Описание**</span><span class="sxs-lookup"><span data-stu-id="ab64b-158">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="ab64b-159">**Created**</span><span class="sxs-lookup"><span data-stu-id="ab64b-159">**Created**</span></span>|<span data-ttu-id="ab64b-160">Возвращает значение, определяющее, когда был создан сайт.</span><span class="sxs-lookup"><span data-stu-id="ab64b-160">Gets a value that specifies when the site was created.</span></span>|
|<span data-ttu-id="ab64b-161">**Description**</span><span class="sxs-lookup"><span data-stu-id="ab64b-161">**Description**</span></span>|<span data-ttu-id="ab64b-162">Возвращает или задает описание сайта.</span><span class="sxs-lookup"><span data-stu-id="ab64b-162">Gets or sets the description for the site.</span></span>|
|<span data-ttu-id="ab64b-163">**Id**</span><span class="sxs-lookup"><span data-stu-id="ab64b-163">**Id**</span></span>|<span data-ttu-id="ab64b-164">Возвращает значение, указывающее идентификатор сайта.</span><span class="sxs-lookup"><span data-stu-id="ab64b-164">Gets a value that specifies the site identifier.</span></span>|
|<span data-ttu-id="ab64b-165">**Language**</span><span class="sxs-lookup"><span data-stu-id="ab64b-165">**Language**</span></span>|<span data-ttu-id="ab64b-166">Возвращает значение, указывающее код языка, используемого на сайте.</span><span class="sxs-lookup"><span data-stu-id="ab64b-166">Gets a value that specifies the locale ID (LCID) for the language that is used on the site.</span></span>|
|<span data-ttu-id="ab64b-167">**LastItemModifiedDate**</span><span class="sxs-lookup"><span data-stu-id="ab64b-167">**LastItemModifiedDate**</span></span>|<span data-ttu-id="ab64b-168">Возвращает значение, определяющее, когда в последний раз был изменен элемент на сайте.</span><span class="sxs-lookup"><span data-stu-id="ab64b-168">Gets a value that specifies when an item was last modified in the site.</span></span>|
|<span data-ttu-id="ab64b-169">**Title**</span><span class="sxs-lookup"><span data-stu-id="ab64b-169">**Title**</span></span>|<span data-ttu-id="ab64b-170">Получает или задает название сайта.</span><span class="sxs-lookup"><span data-stu-id="ab64b-170">Gets or sets the title for the site.</span></span>|
|<span data-ttu-id="ab64b-171">**WebTemplateId**</span><span class="sxs-lookup"><span data-stu-id="ab64b-171">**WebTemplateId**</span></span>|<span data-ttu-id="ab64b-172">Получает идентификатор шаблона сайта.</span><span class="sxs-lookup"><span data-stu-id="ab64b-172">Gets the identifier of the site template.</span></span>|

## <a name="see-also"></a><span data-ttu-id="ab64b-173">См. также</span><span class="sxs-lookup"><span data-stu-id="ab64b-173">See also</span></span>
<span data-ttu-id="ab64b-174"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="ab64b-174"><a name="bk_addresources"> </a></span></span>

-  [<span data-ttu-id="ab64b-175">Знакомство со службой REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="ab64b-175">Get to know the SharePoint REST service</span></span>](get-to-know-the-sharepoint-rest-service.md)
-  [<span data-ttu-id="ab64b-176">Выполнение базовых операций с использованием конечных точек SharePoint REST</span><span class="sxs-lookup"><span data-stu-id="ab64b-176">Complete basic operations using SharePoint REST endpoints</span></span>](complete-basic-operations-using-sharepoint-rest-endpoints.md)
-  [<span data-ttu-id="ab64b-177">Работа со списками и элементами списков в интерфейсе REST</span><span class="sxs-lookup"><span data-stu-id="ab64b-177">Working with lists and list items with REST</span></span>](working-with-lists-and-list-items-with-rest.md)
-  [<span data-ttu-id="ab64b-178">Работа с папками и файлами в службе REST</span><span class="sxs-lookup"><span data-stu-id="ab64b-178">Working with folders and files with REST</span></span>](working-with-folders-and-files-with-rest.md)
-  [<span data-ttu-id="ab64b-179">Определение URI для конечных точек службы REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="ab64b-179">Determine SharePoint REST service endpoint URIs</span></span>](determine-sharepoint-rest-service-endpoint-uris.md)
-  [<span data-ttu-id="ab64b-180">Использование операций запросов OData в запросах REST SharePoint</span><span class="sxs-lookup"><span data-stu-id="ab64b-180">Use OData query operations in SharePoint REST requests</span></span>](use-odata-query-operations-in-sharepoint-rest-requests.md)
-  [<span data-ttu-id="ab64b-181">Справочные материалы и примеры по REST API</span><span class="sxs-lookup"><span data-stu-id="ab64b-181">REST API reference and samples</span></span>](http://msdn.microsoft.com/library/02128c70-9d27-4388-9374-a11bce68fdb8%28Office.15%29.aspx)
-  [<span data-ttu-id="ab64b-182">Синхронизация элементов SharePoint с помощью службы REST</span><span class="sxs-lookup"><span data-stu-id="ab64b-182">Synchronize SharePoint items using the REST service</span></span>](synchronize-sharepoint-items-using-the-rest-service.md)
-  [<span data-ttu-id="ab64b-183">Получение версий элементов списков и документов с помощью значений ETag в службе REST</span><span class="sxs-lookup"><span data-stu-id="ab64b-183">Use ETag values through the REST service to get document list item versioning</span></span>](http://msdn.microsoft.com/library/use-etag-values-through-the-rest-service-to-get-document-list-item-versioning%28Office.15%29.aspx)
    
 

 

 

