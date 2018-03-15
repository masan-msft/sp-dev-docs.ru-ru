---
title: "Навигация по структуре данных SharePoint, представленной в службе REST"
description: "Узнайте, как с помощью конечной точки REST в элементе SharePoint получить доступ к связанным элементам, например родительским сайтам или структуре библиотеки, в которой находится этот элемент."
ms.date: 12/14/2017
ms.prod: sharepoint
ms.openlocfilehash: 30d64635d404e49d5aab5857146e1c2ea192f359
ms.sourcegitcommit: 202dd467c8e5b62c6469808226ad334061f70aa2
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/15/2017
---
# <a name="navigate-the-sharepoint-data-structure-represented-in-the-rest-service"></a><span data-ttu-id="675b0-103">Навигация по структуре данных SharePoint, представленной в службе REST</span><span class="sxs-lookup"><span data-stu-id="675b0-103">Navigate the SharePoint data structure represented in the REST service</span></span>

<span data-ttu-id="675b0-104">При работе со службой REST SharePoint часто возникает ситуация, когда вам известен URL-адрес определенного элемента SharePoint, но требуется получить доступ к связанным элементам, например структуре папок и библиотек, в которой находится элемент.</span><span class="sxs-lookup"><span data-stu-id="675b0-104">When you're working with the SharePoint REST service, you'll often start out knowing the URL of a specific SharePoint item, but want to access related items, such as the folder or library structure where that item resides.</span></span> <span data-ttu-id="675b0-105">Допустим, вы создаете надстройку, в которой пользователь вводит URL-адрес документа в библиотеке SharePoint.</span><span class="sxs-lookup"><span data-stu-id="675b0-105">For example, suppose you create an add-in where your user enters the URL of a document in a SharePoint library.</span></span> <span data-ttu-id="675b0-106">После этого надстройка должна разобрать этот URL-адрес и определить фактический URL-адрес сайта SharePoint.</span><span class="sxs-lookup"><span data-stu-id="675b0-106">Your add-in must then break down that URL to figure out the actual SharePoint site URL.</span></span> <span data-ttu-id="675b0-107">После этого надстройка сможет отправлять с сайта дальнейшие запросы от имени пользователя, например на создание, обновление или удаление связанных элементов или ресурсов.</span><span class="sxs-lookup"><span data-stu-id="675b0-107">After it's done that, the add-in can then make more requests from the site on the user's behalf, such as to create, update, or delete related items or resources.</span></span> 

<span data-ttu-id="675b0-108">Для этого надстройка должна запросить у SharePoint следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="675b0-108">To do this, your add-in needs to query SharePoint for the following information:</span></span>

- <span data-ttu-id="675b0-109">Относительные URL-адреса сайта и семейства веб-сайтов, содержащих ресурс.</span><span class="sxs-lookup"><span data-stu-id="675b0-109">The server relative URLs of the site and site collection containing the resource</span></span>
- <span data-ttu-id="675b0-110">Дайджест формы, позволяющий выполнять запросы, меняющие состояние ресурса, например **POST**, **PUT**, **MERGE** и **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="675b0-110">A form digest to enable you to perform requests that change the state of the resource, such as  **POST**,  **PUT**,  **MERGE**, and  **DELETE**</span></span>

### <a name="the-basic-process"></a><span data-ttu-id="675b0-111">Простой процесс:</span><span class="sxs-lookup"><span data-stu-id="675b0-111">The basic process:</span></span>

1. <span data-ttu-id="675b0-112">Используйте оператор `/contextinfo` с заданным URL-адресом для доступа к сайту и семейству веб-сайтов, а также дайджестом формы.</span><span class="sxs-lookup"><span data-stu-id="675b0-112">Use the  `/contextinfo` operator with the given URL to access the site and site collection addresses, and the form digest. Use the  operator in the following format:</span></span> <span data-ttu-id="675b0-113">Используйте оператор `/contextinfo` в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="675b0-113">Use the `/contextinfo` operator in the following format:</span></span>
    
    `http://server/web/doclib/forms/_api/contextinfo`
    
    <span data-ttu-id="675b0-114">Чтобы усилить защиту от межсайтовых сценариев, оператор `/contextinfo` принимает только запросы **POST**.</span><span class="sxs-lookup"><span data-stu-id="675b0-114">To increase security against cross-site scripting attempts, the  `/contextinfo` operator accepts only **POST** requests.</span></span>
    
2. <span data-ttu-id="675b0-115">Используйте [свойства объекта SPContextWebInformation](#bk_props), возвращаемые оператором `/contextinfo`, для доступа к дополнительным ресурсам по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="675b0-115">Use the  [SPContextWebInformation object properties](#bk_props) that the `/contextinfo` operator returns to access additional resources as desired.</span></span>
    
 
### <a name="try-it"></a><span data-ttu-id="675b0-116">Попробуйте</span><span class="sxs-lookup"><span data-stu-id="675b0-116">Try it</span></span>

1. <span data-ttu-id="675b0-p103">Начните с URL-адреса определенного элемента SharePoint. Пример:</span><span class="sxs-lookup"><span data-stu-id="675b0-p103">Start with a URL to a given SharePoint item. For example:</span></span>
    
    `http://site/web/doclib/myDocument.docx`
    
2. <span data-ttu-id="675b0-119">Удалите имя ресурса в конце URL-адреса так, чтобы URL-адрес указывал на библиотеку документа, папку или список.</span><span class="sxs-lookup"><span data-stu-id="675b0-119">Remove the name of the specific resource from the end of the URL, so that the URL points to a document library, folder, or list. IN this case:</span></span> <span data-ttu-id="675b0-120">В этом случае:</span><span class="sxs-lookup"><span data-stu-id="675b0-120">In this case:</span></span>
    
    `http://site/web/doclib/`
    
3. <span data-ttu-id="675b0-121">Добавьте указатель службы REST и оператор `/contextinfo` к URL-адресу:</span><span class="sxs-lookup"><span data-stu-id="675b0-121">Append the REST service pointer and the  `/contextinfo` operator to the URL:</span></span>
    
    `http://site/web/doclib/_api/contextinfo`
    
4. <span data-ttu-id="675b0-122">Прочитайте дайджест формы и свойства **webFullUrl** из отклика.</span><span class="sxs-lookup"><span data-stu-id="675b0-122">Read the form digest and **webFullUrl** properties from the response.</span></span>
 
5. <span data-ttu-id="675b0-123">Добавьте указатель службы REST `_api` в конец URL-адреса веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="675b0-123">Append the REST service pointer  `_api` to the web URL</span></span>

6. <span data-ttu-id="675b0-124">Используйте полученный URL-адрес и дайджест формы для отправки запросов о других нужных ресурсах.</span><span class="sxs-lookup"><span data-stu-id="675b0-124">Use the resulting URL and the form digest to make requests for other resources you need.</span></span>

<span data-ttu-id="675b0-125">При отправке запросов **GET** или отправке запросов с использованием проверенного маркера OAuth передавать дайджест формы не требуется.</span><span class="sxs-lookup"><span data-stu-id="675b0-125">You don't have to pass the form digest if you're making **GET** requests, or making requests using a validated OAuth token.</span></span>

<span data-ttu-id="675b0-126"><a name="bk_sites"> </a></span><span class="sxs-lookup"><span data-stu-id="675b0-126"></span></span> 

## <a name="navigate-parent-and-child-sites"></a><span data-ttu-id="675b0-127">Навигация по родительским и дочерним сайтам</span><span class="sxs-lookup"><span data-stu-id="675b0-127">Navigate parent and child sites</span></span>

<span data-ttu-id="675b0-128">При навигации по структуре сайтов с помощью серверной объектной модели SharePoint используются свойства **SPWeb.ParentWeb** и **SPWeb.Webs** для доступа к объектам, представляющим родительские и дочерние сайты.</span><span class="sxs-lookup"><span data-stu-id="675b0-128"> When you navigate your site structure using the SharePoint server object model, you use the  **SPWeb.ParentWeb** and **SPWeb.Webs** properties to access objects that represent parent and child sites.</span></span>

<span data-ttu-id="675b0-p105">Соответствующие ресурсы REST — `web/parentweb` и `web/webs` — не возвращают объекты, представляющие сайты. Это вызвано тем, что служба REST соответствует стандартам OData, а возврат готовых представлений сайтов сделал бы такие запросы неэффективными. Вместо этого они возвращают [объект WebInfo](#bk_webinfo), содержащий скалярные свойства сайта, но без связанных наборов сущностей, таких как коллекции или семейства полей.</span><span class="sxs-lookup"><span data-stu-id="675b0-p105">The corresponding REST resources— `web/parentweb` and `web/webs`—don't return objects that represent sites. This is because the REST service conforms to OData standards, and returning complete site representations would make such requests inefficient. Instead, they return a  [WebInfo object ](#bk_webinfo) that contains the site's scalar properties, but without related entity sets such as like collections or field collections.</span></span>

<span data-ttu-id="675b0-p106">Чтобы перейти к определенному родительскому или дочернему сайту, составьте подходящий URL-адрес REST этого сайта с помощью свойства **Id** или **Title**. После этого вы можете получить доступ к наборам сущностей, связанным с этим сайтом.</span><span class="sxs-lookup"><span data-stu-id="675b0-p106">To navigate to a specific parent or child site, construct the appropriate REST URL to that site using the  **Id** or **Title** property to. From there, you can access that site's related entity sets.</span></span>

<span data-ttu-id="675b0-134"><a name="bk_folders"> </a></span><span class="sxs-lookup"><span data-stu-id="675b0-134"></span></span> 

## <a name="navigate-folder-structure"></a><span data-ttu-id="675b0-135">Навигация по структуре папок</span><span class="sxs-lookup"><span data-stu-id="675b0-135">Navigate folder structure</span></span>

<span data-ttu-id="675b0-136">Служба REST SharePoint не поддерживает обход иерархии папок сайта путем составления URL-адресов.</span><span class="sxs-lookup"><span data-stu-id="675b0-136">The SharePoint REST service does not support traversing the folder hierarchy of a site through the URL construction.</span></span> <span data-ttu-id="675b0-137">Вместо этого можно использовать аналог метода **Web.GetFolderByServerRelativeUrl** в службе REST.</span><span class="sxs-lookup"><span data-stu-id="675b0-137">Instead, use the REST equivalent of the  **Web.GetFolderByServerRelativeUrl** method.</span></span> <span data-ttu-id="675b0-138">Пример:</span><span class="sxs-lookup"><span data-stu-id="675b0-138">For example:</span></span>

<span data-ttu-id="675b0-139">*Навигация, не поддерживаемая в службе REST:*</span><span class="sxs-lookup"><span data-stu-id="675b0-139">*Navigation not supported through the REST service:*</span></span> 

`/_vti_bin/client.svc/web/lists/SharedDocuments/folder1/stuff/things/Recycle`
 
<span data-ttu-id="675b0-140">*Навигация, поддерживаемая в службе REST:*</span><span class="sxs-lookup"><span data-stu-id="675b0-140">*Navigation that is supported by the REST service:*</span></span> 
 
`/_vti_bin/client.svc/web/GetFolderByServerRelativeUrl('SharedDocuments/folder1/stuff/things')/Recycle`
 

<span data-ttu-id="675b0-141"><a name="bk_props"> </a></span><span class="sxs-lookup"><span data-stu-id="675b0-141"></span></span>

## <a name="spcontextwebinformation-object-properties"></a><span data-ttu-id="675b0-142">Свойства объекта SPContextWebInformation</span><span class="sxs-lookup"><span data-stu-id="675b0-142">SPContextWebInformation object properties</span></span>

|<span data-ttu-id="675b0-143">**Свойство SPContextWebInformation**</span><span class="sxs-lookup"><span data-stu-id="675b0-143">**SPContextWebInformation Property**</span></span>|<span data-ttu-id="675b0-144">**Описание**</span><span class="sxs-lookup"><span data-stu-id="675b0-144">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="675b0-145">**webFullUrl**</span><span class="sxs-lookup"><span data-stu-id="675b0-145">**webFullUrl**</span></span>|<span data-ttu-id="675b0-146">Возвращает URL-адрес относительно сервера для ближайшего сайта.</span><span class="sxs-lookup"><span data-stu-id="675b0-146">Gets the server-relative URL of the nearest site.</span></span>|
|<span data-ttu-id="675b0-147">**siteFullUrl**</span><span class="sxs-lookup"><span data-stu-id="675b0-147">**siteFullUrl**</span></span>|<span data-ttu-id="675b0-148">Получает относительный URL-адрес корневого веб-сайта семейства, в котором содержится сайт.</span><span class="sxs-lookup"><span data-stu-id="675b0-148">Gets the server-relative URL of the root of the site collection that the site is contained within.</span></span><br/><span data-ttu-id="675b0-149">Если ближайшим веб-сайтом является корневой сайт семейства веб-сайтов, значения свойств **webFullUrl** и **siteFullUrl** одинаковы.</span><span class="sxs-lookup"><span data-stu-id="675b0-149">If the nearest web is the root of a site collection, then the value of the **webFullUrl** property is equal to the **siteFullUrl** property.</span></span>|
|<span data-ttu-id="675b0-150">**formDigestValue**</span><span class="sxs-lookup"><span data-stu-id="675b0-150">**formDigestValue**</span></span>|<span data-ttu-id="675b0-151">Возвращает дайджест формы запроса сервера.</span><span class="sxs-lookup"><span data-stu-id="675b0-151">Gets the server's request form digest.</span></span>|
|<span data-ttu-id="675b0-152">**LibraryVersion**</span><span class="sxs-lookup"><span data-stu-id="675b0-152">**LibraryVersion**</span></span>|<span data-ttu-id="675b0-153">Возвращает текущую версию библиотеки REST.</span><span class="sxs-lookup"><span data-stu-id="675b0-153">Gets the current version of the REST library.</span></span>|
|<span data-ttu-id="675b0-154">**SupportedSchemaVersions**</span><span class="sxs-lookup"><span data-stu-id="675b0-154">**SupportedSchemaVersions**</span></span>|<span data-ttu-id="675b0-155">Получает поддерживаемые версии схемы библиотеки REST/CSOM.</span><span class="sxs-lookup"><span data-stu-id="675b0-155">Gets the versions of the schema of the REST/CSOM library that are supported.</span></span>|

<span data-ttu-id="675b0-156"><a name="bk_webinfo"> </a></span><span class="sxs-lookup"><span data-stu-id="675b0-156"><a name="bk_webinfo"> </a></span></span>

## <a name="webinfo-object"></a><span data-ttu-id="675b0-157">Объект WebInfo</span><span class="sxs-lookup"><span data-stu-id="675b0-157">WebInfo object</span></span>

|<span data-ttu-id="675b0-158">**Свойство WebInfo**</span><span class="sxs-lookup"><span data-stu-id="675b0-158">**WebInfo property**</span></span>|<span data-ttu-id="675b0-159">**Описание**</span><span class="sxs-lookup"><span data-stu-id="675b0-159">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="675b0-160">**Created**</span><span class="sxs-lookup"><span data-stu-id="675b0-160">**Created**</span></span>|<span data-ttu-id="675b0-161">Возвращает значение, определяющее, когда был создан сайт.</span><span class="sxs-lookup"><span data-stu-id="675b0-161">Gets a value that specifies when the site was created.</span></span>|
|<span data-ttu-id="675b0-162">**Description**</span><span class="sxs-lookup"><span data-stu-id="675b0-162">**Description**</span></span>|<span data-ttu-id="675b0-163">Возвращает или задает описание сайта.</span><span class="sxs-lookup"><span data-stu-id="675b0-163">Gets or sets the description for the site.</span></span>|
|<span data-ttu-id="675b0-164">**Id**</span><span class="sxs-lookup"><span data-stu-id="675b0-164">**Id**</span></span>|<span data-ttu-id="675b0-165">Возвращает значение, указывающее идентификатор сайта.</span><span class="sxs-lookup"><span data-stu-id="675b0-165">Gets a value that specifies the site identifier.</span></span>|
|<span data-ttu-id="675b0-166">**Language**</span><span class="sxs-lookup"><span data-stu-id="675b0-166">**Language**</span></span>|<span data-ttu-id="675b0-167">Возвращает значение, указывающее код языка, используемого на сайте.</span><span class="sxs-lookup"><span data-stu-id="675b0-167">Gets a value that specifies the locale ID (LCID) for the language that is used on the site.</span></span>|
|<span data-ttu-id="675b0-168">**LastItemModifiedDate**</span><span class="sxs-lookup"><span data-stu-id="675b0-168">**LastItemModifiedDate**</span></span>|<span data-ttu-id="675b0-169">Возвращает значение, определяющее, когда в последний раз был изменен элемент на сайте.</span><span class="sxs-lookup"><span data-stu-id="675b0-169">Gets a value that specifies when an item was last modified in the site.</span></span>|
|<span data-ttu-id="675b0-170">**Title**</span><span class="sxs-lookup"><span data-stu-id="675b0-170">**Title**</span></span>|<span data-ttu-id="675b0-171">Получает или задает название сайта.</span><span class="sxs-lookup"><span data-stu-id="675b0-171">Gets or sets the title for the site.</span></span>|
|<span data-ttu-id="675b0-172">**WebTemplateId**</span><span class="sxs-lookup"><span data-stu-id="675b0-172">**WebTemplateId**</span></span>|<span data-ttu-id="675b0-173">Получает идентификатор шаблона сайта.</span><span class="sxs-lookup"><span data-stu-id="675b0-173">Gets the identifier of the site template.</span></span>|

## <a name="see-also"></a><span data-ttu-id="675b0-174">См. также</span><span class="sxs-lookup"><span data-stu-id="675b0-174">See also</span></span>
<span data-ttu-id="675b0-175"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="675b0-175"></span></span>

- [<span data-ttu-id="675b0-176">Знакомство со службой REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="675b0-176">Get to know the SharePoint REST service</span></span>](get-to-know-the-sharepoint-rest-service.md)
- [<span data-ttu-id="675b0-177">Справочные материалы по REST API и примеры</span><span class="sxs-lookup"><span data-stu-id="675b0-177">REST API reference and samples</span></span>](https://msdn.microsoft.com/library)
- [<span data-ttu-id="675b0-178">Получение версий списков документов с помощью значений ETag в службе REST</span><span class="sxs-lookup"><span data-stu-id="675b0-178">Use ETag values through the REST service to get document list item versioning</span></span>](working-with-lists-and-list-items-with-rest.md#using-etag-values-to-determine-document-and-list-item-versioning)
- [<span data-ttu-id="675b0-179">Материалы по OData</span><span class="sxs-lookup"><span data-stu-id="675b0-179">OData resources</span></span>](get-to-know-the-sharepoint-rest-service.md#odata-resources)
- [<span data-ttu-id="675b0-180">Разработка надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="675b0-180">Develop SharePoint Add-ins</span></span>](develop-sharepoint-add-ins.md)
    
 

 

 

