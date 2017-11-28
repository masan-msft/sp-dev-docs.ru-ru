---
title: "Экземпляр списка в объектная модель SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 5bfe9697dfbd75b389f974801add3ed399507ed4
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
<a name="list-instance-in-the-sharepoint-add-in-model"></a><span data-ttu-id="9f0f0-102">Экземпляр списка в объектная модель SharePoint</span><span class="sxs-lookup"><span data-stu-id="9f0f0-102">List instance in the SharePoint add-in model</span></span>
============================================

<a name="summary"></a><span data-ttu-id="9f0f0-103">Summary</span><span class="sxs-lookup"><span data-stu-id="9f0f0-103">Summary</span></span>
-------

<span data-ttu-id="9f0f0-104">Подхода, можно создавать экземпляры списка отличается в новой модели надстройки SharePoint не был с кодом полного доверия.</span><span class="sxs-lookup"><span data-stu-id="9f0f0-104">The approach you take to create list instances is different in the new SharePoint Add-in model than it was with Full Trust Code.</span></span> <span data-ttu-id="9f0f0-105">В типичных полного доверия кода (FTC) / сценарий решения фермы экземпляры списков были созданы с помощью декларативного кода и развернуты через решений SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9f0f0-105">In a typical Full Trust Code (FTC) / Farm Solution scenario, list instances were created with declarative code and deployed via SharePoint Solutions.</span></span> 

<span data-ttu-id="9f0f0-106">В модели сценарий надстройки SharePoint удаленного подготовки шаблон используется для создания экземпляров списка.</span><span class="sxs-lookup"><span data-stu-id="9f0f0-106">In a SharePoint Add-in model scenario, the remote provisioning pattern is used to create list instances.</span></span>

<a name="high-level-guidelines"></a><span data-ttu-id="9f0f0-107">Рекомендации по высокого уровня</span><span class="sxs-lookup"><span data-stu-id="9f0f0-107">High-level guidelines</span></span>
---------------------

<span data-ttu-id="9f0f0-108">Как правило эскиз мы предлагаем для обеспечения высокого уровня следующие рекомендации для создания экземпляров списка.</span><span class="sxs-lookup"><span data-stu-id="9f0f0-108">As a rule of a thumb, we would like to provide the following high-level guidelines to create list instances.</span></span>

- <span data-ttu-id="9f0f0-109">Использование удаленных подготовки шаблон для создания экземпляров списка.</span><span class="sxs-lookup"><span data-stu-id="9f0f0-109">Use the remote provisioning pattern to create list instances.</span></span>
- <span data-ttu-id="9f0f0-110">Не используйте декларативный код (elements.xml) для создания экземпляров списка.</span><span class="sxs-lookup"><span data-stu-id="9f0f0-110">Do not use declarative code (elements.xml) to create list instances.</span></span>

<span data-ttu-id="9f0f0-111">**Приступая к работе**</span><span class="sxs-lookup"><span data-stu-id="9f0f0-111">**Getting started**</span></span>

<span data-ttu-id="9f0f0-112">Следующий пример кода PnP O365 и видео показано, как создать надстройки SharePoint, который предоставляет пользовательский интерфейс, который позволяет конечным пользователям создавать новые библиотеки документов.</span><span class="sxs-lookup"><span data-stu-id="9f0f0-112">The following O365 PnP code sample and video demonstrates how to create a SharePoint Add-in that provides a user interface that allows end users to create new document libraries.</span></span> <span data-ttu-id="9f0f0-113">Также демонстрируется создание библиотеки документов с определенным конфигурации, которые совместно представляют шаблона.</span><span class="sxs-lookup"><span data-stu-id="9f0f0-113">It also demonstrates how to create a document library with specific configurations that collectively represent a template.</span></span> <span data-ttu-id="9f0f0-114">В этом примере вы найдете код, который создает экземпляр списка.</span><span class="sxs-lookup"><span data-stu-id="9f0f0-114">In this sample you will find the code that creates a list instance.</span></span>

- [<span data-ttu-id="9f0f0-115">ECM. DocumentLibraries (образец кода PnP O365)</span><span class="sxs-lookup"><span data-stu-id="9f0f0-115">ECM.DocumentLibraries (O365 PnP Code Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.DocumentLibraries)

<span data-ttu-id="9f0f0-116">Следующем видеоролике описывается пример кода.</span><span class="sxs-lookup"><span data-stu-id="9f0f0-116">The following video walks through the code sample.</span></span>

- [<span data-ttu-id="9f0f0-117">Шаблоны документов и списков с моделью приложений (O365 PnP видео)</span><span class="sxs-lookup"><span data-stu-id="9f0f0-117">Document and list templates with app model (O365 PnP Video)</span></span>](http://channel9.msdn.com/blogs/OfficeDevPnP/Document-and-list-templates-with-app-model)

<span data-ttu-id="9f0f0-118">Используйте метод AddList в SharePoint CSOM для создания экземпляра списка с помощью удаленного подготовки шаблон.</span><span class="sxs-lookup"><span data-stu-id="9f0f0-118">Use the AddList method in the SharePoint CSOM to create a list instance via the remote provisioning pattern.</span></span> <span data-ttu-id="9f0f0-119">Следующий код, взяты из [ECM. DocumentLibraries (O365 PnP образец кода)](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.DocumentLibraries) показано, как это сделать.</span><span class="sxs-lookup"><span data-stu-id="9f0f0-119">The following code taken from the [ECM.DocumentLibraries (O365 PnP Code Sample)](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.DocumentLibraries) illustrates how to do it.</span></span>

    private void CreateLibrary(ClientContext ctx, Library library, string associateContentTypeID) 
    {
        if (!ctx.Web.ListExists(library.Title))
        {
           // Create List Instance
           ctx.Web.AddList(ListTemplateType.DocumentLibrary, library.Title, false);
           List _list = ctx.Web.GetListByTitle(library.Title);
           
           //Set Description
           if(!string.IsNullOrEmpty(library.Description)) 
           {
            _list.Description = library.Description;
           }

           //Turn on versioning 
           if(library.VerisioningEnabled) {
              _list.EnableVersioning = true;
           }
           
            //Turn on Content Types
           _list.ContentTypesEnabled = true;
           _list.Update();

           //Add Content Type to List
           ctx.Web.AddContentTypeToListById(library.Title, associateContentTypeID, true);
    
           //Remove the default Document Content Type
           _list.RemoveContentTypeByName(ContentTypeManager.DEFAULT_DOCUMENT_CT_NAME);

           ctx.Web.Context.ExecuteQuery();
        }
    }

<span data-ttu-id="9f0f0-120">В следующем примере кода показано, как создать экземпляр списка с использованием интерфейса API REST SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9f0f0-120">The following code sample illustrates how to create a list instance with the SharePoint REST API.</span></span>  <span data-ttu-id="9f0f0-121">В этом примере извлекаются из [списков и справочник по API -Интерфейс REST элементов списка (статья MSDN)](https://msdn.microsoft.com/en-us/library/office/dn531433.aspx)</span><span class="sxs-lookup"><span data-stu-id="9f0f0-121">This sample comes from the [Lists and list items REST API reference (MSDN Article)](https://msdn.microsoft.com/en-us/library/office/dn531433.aspx)</span></span>

    executor.executeAsync({
      url: "<app web url>/_api/SP.AppContextSite(@target)/web/lists
        ?@target='<host web url>'",
      method: "POST",
      body: "{ '__metadata': { 'type': 'SP.List' }, 'AllowContentTypes': true, 'BaseTemplate': 100,
        'ContentTypesEnabled': true, 'Description': 'My list description', 'Title': 'Test title' }",
      headers: { "content-type": "application/json;odata=verbose" },
      success: successHandler,
      error: errorHandler
    });

<a name="related-links"></a><span data-ttu-id="9f0f0-122">Ссылки по теме</span><span class="sxs-lookup"><span data-stu-id="9f0f0-122">Related links</span></span>
=============
- [<span data-ttu-id="9f0f0-123">Списки и справочник по API-Интерфейс REST элементов списка (статья MSDN)</span><span class="sxs-lookup"><span data-stu-id="9f0f0-123">Lists and list items REST API reference (MSDN Article)</span></span>](https://msdn.microsoft.com/en-us/library/office/dn531433.aspx)
- [<span data-ttu-id="9f0f0-124">Список определений или шаблонов списков (добавить в SharePoint модель набора команд)</span><span class="sxs-lookup"><span data-stu-id="9f0f0-124">List Definitions / List Templates (SharePoint Add-in model recipe)</span></span>](list-definition-template-sharepoint-add-in.md)
- [<span data-ttu-id="9f0f0-125">Шаблоны документов и списков с моделью приложений (O365 PnP видео)</span><span class="sxs-lookup"><span data-stu-id="9f0f0-125">Document and list templates with app model (O365 PnP Video)</span></span>](http://channel9.msdn.com/blogs/OfficeDevPnP/Document-and-list-templates-with-app-model)
- <span data-ttu-id="9f0f0-126">Руководств по [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Руководств")</span><span class="sxs-lookup"><span data-stu-id="9f0f0-126">Guidance articles at [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Guidance Articles")</span></span>
- <span data-ttu-id="9f0f0-127">Справочные материалы в библиотеке MSDN по [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Справочные материалы в библиотеке MSDN")</span><span class="sxs-lookup"><span data-stu-id="9f0f0-127">References in MSDN at [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "References in MSDN")</span></span>
- <span data-ttu-id="9f0f0-128">Видеозаписи по [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "видео")</span><span class="sxs-lookup"><span data-stu-id="9f0f0-128">Videos at [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span></span>

<a name="related-pnp-samples"></a><span data-ttu-id="9f0f0-129">Примеры связанных с ними PnP</span><span class="sxs-lookup"><span data-stu-id="9f0f0-129">Related PnP samples</span></span>
===================

- [<span data-ttu-id="9f0f0-130">ECM. DocumentLibraries (образец кода PnP O365)</span><span class="sxs-lookup"><span data-stu-id="9f0f0-130">ECM.DocumentLibraries (O365 PnP Code Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.DocumentLibraries)
- <span data-ttu-id="9f0f0-131">Примеры и содержимое в [https://github.com/SharePoint/PnP](https://github.com/SharePoint/PnP)</span><span class="sxs-lookup"><span data-stu-id="9f0f0-131">Samples and content at [https://github.com/SharePoint/PnP](https://github.com/SharePoint/PnP)</span></span>

<a name="applies-to"></a><span data-ttu-id="9f0f0-132">Применимо к</span><span class="sxs-lookup"><span data-stu-id="9f0f0-132">Applies to</span></span>
==========
- <span data-ttu-id="9f0f0-133">Office 365 нескольких клиентов (MT)</span><span class="sxs-lookup"><span data-stu-id="9f0f0-133">Office 365 Multi Tenant (MT)</span></span>
- <span data-ttu-id="9f0f0-134">Office 365 выделенных (D) *частично*</span><span class="sxs-lookup"><span data-stu-id="9f0f0-134">Office 365 Dedicated (D) *partly*</span></span>
- <span data-ttu-id="9f0f0-135">SharePoint 2013 в локальной — *частично*</span><span class="sxs-lookup"><span data-stu-id="9f0f0-135">SharePoint 2013 on-premises – *partly*</span></span>

<span data-ttu-id="9f0f0-136">*Шаблоны для выделенных и локальной идентичны с помощью надстройки SharePoint методики модели, но возможных технологий, которые могут использоваться отличаются.*</span><span class="sxs-lookup"><span data-stu-id="9f0f0-136">*Patterns for dedicated and on-premises are identical with SharePoint Add-in model techniques, but there are differences on the possible technologies that can be used.*</span></span>
