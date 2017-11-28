---
title: "Экземпляр списка в объектная модель SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 5bfe9697dfbd75b389f974801add3ed399507ed4
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
<a name="list-instance-in-the-sharepoint-add-in-model"></a>Экземпляр списка в объектная модель SharePoint
============================================

<a name="summary"></a>Summary
-------

Подхода, можно создавать экземпляры списка отличается в новой модели надстройки SharePoint не был с кодом полного доверия. В типичных полного доверия кода (FTC) / сценарий решения фермы экземпляры списков были созданы с помощью декларативного кода и развернуты через решений SharePoint. 

В модели сценарий надстройки SharePoint удаленного подготовки шаблон используется для создания экземпляров списка.

<a name="high-level-guidelines"></a>Рекомендации по высокого уровня
---------------------

Как правило эскиз мы предлагаем для обеспечения высокого уровня следующие рекомендации для создания экземпляров списка.

- Использование удаленных подготовки шаблон для создания экземпляров списка.
- Не используйте декларативный код (elements.xml) для создания экземпляров списка.

**Приступая к работе**

Следующий пример кода PnP O365 и видео показано, как создать надстройки SharePoint, который предоставляет пользовательский интерфейс, который позволяет конечным пользователям создавать новые библиотеки документов. Также демонстрируется создание библиотеки документов с определенным конфигурации, которые совместно представляют шаблона. В этом примере вы найдете код, который создает экземпляр списка.

- [ECM. DocumentLibraries (образец кода PnP O365)](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.DocumentLibraries)

Следующем видеоролике описывается пример кода.

- [Шаблоны документов и списков с моделью приложений (O365 PnP видео)](http://channel9.msdn.com/blogs/OfficeDevPnP/Document-and-list-templates-with-app-model)

Используйте метод AddList в SharePoint CSOM для создания экземпляра списка с помощью удаленного подготовки шаблон. Следующий код, взяты из [ECM. DocumentLibraries (O365 PnP образец кода)](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.DocumentLibraries) показано, как это сделать.

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

В следующем примере кода показано, как создать экземпляр списка с использованием интерфейса API REST SharePoint.  В этом примере извлекаются из [списков и справочник по API -Интерфейс REST элементов списка (статья MSDN)](https://msdn.microsoft.com/en-us/library/office/dn531433.aspx)

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

<a name="related-links"></a>Ссылки по теме
=============
- [Списки и справочник по API-Интерфейс REST элементов списка (статья MSDN)](https://msdn.microsoft.com/en-us/library/office/dn531433.aspx)
- [Список определений или шаблонов списков (добавить в SharePoint модель набора команд)](list-definition-template-sharepoint-add-in.md)
- [Шаблоны документов и списков с моделью приложений (O365 PnP видео)](http://channel9.msdn.com/blogs/OfficeDevPnP/Document-and-list-templates-with-app-model)
- Руководств по [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Руководств")
- Справочные материалы в библиотеке MSDN по [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Справочные материалы в библиотеке MSDN")
- Видеозаписи по [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "видео")

<a name="related-pnp-samples"></a>Примеры связанных с ними PnP
===================

- [ECM. DocumentLibraries (образец кода PnP O365)](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.DocumentLibraries)
- Примеры и содержимое в [https://github.com/SharePoint/PnP](https://github.com/SharePoint/PnP)

<a name="applies-to"></a>Применимо к
==========
- Office 365 нескольких клиентов (MT)
- Office 365 выделенных (D) *частично*
- SharePoint 2013 в локальной — *частично*

*Шаблоны для выделенных и локальной идентичны с помощью надстройки SharePoint методики модели, но возможных технологий, которые могут использоваться отличаются.*
