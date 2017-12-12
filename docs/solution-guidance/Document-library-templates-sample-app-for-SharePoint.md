---
title: "Документ библиотеки шаблонов пример надстройки для SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 405e5863bbbfdb7740a93e33f9ed8b80f136d39b
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="document-library-templates-sample-add-in-for-sharepoint"></a>Документ библиотеки шаблонов пример надстройки для SharePoint

В рамках стратегии Enterprise содержимое Management (ECM) можно реализовать шаблон библиотеки пользовательских документов и настраивать столбцы сайта, типы контента сайта, поля таксономии, параметры версии и типа контента документа по умолчанию.
    
_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_

[ECM. DocumentLibraries](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.DocumentLibraries) примере показано, как использовать размещение у поставщика в надстройке для создания списка или библиотеки документов, назначить типу контента и удаление типа контента по умолчанию. Если вы хотите используйте этого решения:    

- Создание списка или библиотеки документов и применение типа контента по умолчанию.
    
- Утверждаете контролировать добавление, обслуживания или реализации локализованных версий настраиваемых полей.
    
- Удаление типа контента по умолчанию для списка или библиотеки.
    
- Применить параметры конфигурации библиотеки для создания списка или библиотеки.

## <a name="before-you-begin"></a>Перед началом работы
<a name="sectionSection0"> </a>

Чтобы начать работу, загрузите [ECM. DocumentLibraries](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.DocumentLibraries) пример надстройки из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.

Пользователи, обращающиеся к ECM. Надстройка DocumentLibraries необходимо иметь разрешения на управление списками. Метод **DoesUserHavePermission** в файле Default.aspx.cs проверяет разрешения пользователя чтобы убедиться, что они могут управлять списками. Если пользователь не имеет разрешения на управление списками, надстройка представляет сообщение об ошибке пользователю.

```C#
private bool DoesUserHavePermission()
        {
            var spContext = SharePointContextProvider.Current.GetSharePointContext(Context);
            using (var ctx = spContext.CreateUserClientContextForSPHost())
            {
                BasePermissions perms = new BasePermissions();
                perms.Set(PermissionKind.ManageLists);
                ClientResult<bool> _permResult = ctx.Web.DoesUserHavePermissions(perms);
                ctx.ExecuteQuery();
                return _permResult.Value;
            }
        }

```

## <a name="using-the-ecmdocumentlibraries-sample-add-in"></a>С помощью ECM. DocumentLibraries пример надстройки 
<a name="sectionSection1"> </a>

При запуске этой надстройки начальной страницы отображается как показано на рисунке 1. ECM. DocumentLibraries запуск страницы выглядит страницу, чтобы добавить новую библиотеку документов, когда вы выбираете **Контент сайта** > **Добавление приложения** > **Библиотеки документов** > **Дополнительные параметры** - с одной различие. При запуске надстройки, в раскрывающемся списке шаблона документа отображает шаблон библиотеки пользовательских документов, ИТ и документы Contoso. При выборе **создания**новой библиотеки документов назначается выбранного типа содержимого. 

** На рисунке 1. Начальная страница ECM. Надстройка DocumentLibraries **

![Снимок экрана, показывающий ECM. DocumentLibraries надстройки "Запуск" с полем раскрывающегося списка шаблона документа, в котором приведены ИТ документ как выбор.](media/d58b9d12-808e-4f2b-9065-31e6d735dbaa.png)

Когда пользователи выберите **Создать**, с помощью метода **CreateLibrary_Click** в файле Default.aspx.cs проверяет шаблон выбранные по умолчанию и вызывает метод либо **CreateITDocumentLibrary** , либо **CreateContosoDocumentLibrary** в ContentTypeManager.cs, как показано в следующем коде.
    
> [!NOTE] 
> Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.

```C#
protected void CreateLibrary_Click(object sender, EventArgs e)
        {
            try
            {
                var _spContext = SharePointContextProvider.Current.GetSharePointContext(Context);
                var _templateSelectedItem = this.DocumentTemplateType.Value;
                var _libraryToCreate = this.GetLibraryToCreate();
                using (var _ctx = _spContext.CreateUserClientContextForSPHost())
                {
                    
                    _ctx.ApplicationName = "AMS ECM.DocumentLibraries";
                    ContentTypeManager _manager = new ContentTypeManager();
                    switch(_templateSelectedItem)
                    {
                        case "IT Document":
                            _manager.CreateITDocumentLibrary(_ctx, _libraryToCreate);
                            break;
                        case "Contoso Document":
                            _manager.CreateContosoDocumentLibrary(_ctx, _libraryToCreate);
                            break;
                    }
                 }

                Response.Redirect(this.Url.Value);
            }
            catch (Exception _ex)
            {
                throw;
            }
        }

```

Метод **CreateContosoDocumentLibrary** выполняет следующие задачи, как показано в следующем примере кода:

1. Создание настраиваемых полей в службы управляемых метаданных.
    
2. Создание типа контента. 
    
3. Связывает настраиваемые поля с типами контента.
    
4. Создание библиотеки документов с типом контента.

```C#
        public void CreateContosoDocumentLibrary(ClientContext ctx, Library library)
        {
            // Check the fields.
            if (!ctx.Web.FieldExistsById(FLD_CLASSIFICATION_ID)){
                ctx.Web.CreateTaxonomyField(FLD_CLASSIFICATION_ID, 
                                            FLD_CLASSIFICATION_INTERNAL_NAME, 
                                            FLD_CLASSIFICATION_DISPLAY_NAME, 
                                            FIELDS_GROUP_NAME, 
                                            TAXONOMY_GROUP, 
                                            TAXONOMY_TERMSET_CLASSIFICATION_NAME);
            }
            
            // Check the content type.
            if (!ctx.Web.ContentTypeExistsById(CONTOSODOCUMENT_CT_ID)){
                ctx.Web.CreateContentType(CONTOSODOCUMENT_CT_NAME, 
                                          CT_DESC, CONTOSODOCUMENT_CT_ID, 
                                          CT_GROUP);
            }

            // Associate fields to content types.
            if (!ctx.Web.FieldExistsByNameInContentType(CONTOSODOCUMENT_CT_NAME, FLD_CLASSIFICATION_INTERNAL_NAME)){
                ctx.Web.AddFieldToContentTypeById(CONTOSODOCUMENT_CT_ID, 
                                                  FLD_CLASSIFICATION_ID.ToString(), 
                                                  false);
            }
            CreateLibrary(ctx, library, CONTOSODOCUMENT_CT_ID);
          
        }

```

**CreateContosoDocumentLibrary** вызывает метод **CreateTaxonomyField** , который является частью OfficeDevPnP.Core. **CreateTaxonomyField** создает поле в службе управляемых метаданных из надстройки размещением у поставщика.

```C#
public static Field CreateTaxonomyField(this Web web, Guid id, string internalName, string displayName, string group, TermSet termSet, bool multiValue = false)
        {
            internalName.ValidateNotNullOrEmpty("internalName");
            displayName.ValidateNotNullOrEmpty("displayName");
            termSet.ValidateNotNullOrEmpty("termSet");

            try
            {
                var _field = web.CreateField(id, internalName, multiValue ? "TaxonomyFieldTypeMulti" : "TaxonomyFieldType", true, displayName, group, "ShowField=\"Term1033\"");

                WireUpTaxonomyField(web, _field, termSet, multiValue);
                _field.Update();

                web.Context.ExecuteQuery();

                return _field;
            }
            catch (Exception)
            {
                /// If there is an exception, the hidden field might be present.
                FieldCollection _fields = web.Fields;
                web.Context.Load(_fields, fc => fc.Include(f => f.Id, f => f.InternalName));
                web.Context.ExecuteQuery();
                var _hiddenField = id.ToString().Replace("-", "");

                var _field = _fields.FirstOrDefault(f => f.InternalName == _hiddenField);
                if (_field != null)
                {
                    _field.DeleteObject();
                    web.Context.ExecuteQuery();
                }
                throw;

            }
        }
```

**CreateContosoDocumentLibrary** вызывает метод **CreateContentType** , который является частью OfficeDevPnP.Core. **CreateContentType** создает новый тип контента.

```C#
public static ContentType CreateContentType(this Web web, string name, string description, string id, string group, ContentType parentContentType = null)
        {
            LoggingUtility.Internal.TraceInformation((int)EventId.CreateContentType, CoreResources.FieldAndContentTypeExtensions_CreateContentType01, name, id);

            // Load the current collection of content types.
            ContentTypeCollection contentTypes = web.ContentTypes;
            web.Context.Load(contentTypes);
            web.Context.ExecuteQuery();
            ContentTypeCreationInformation newCt = new ContentTypeCreationInformation();

            // Set the properties for the content type.
            newCt.Name = name;
            newCt.Id = id;
            newCt.Description = description;
            newCt.Group = group;
            newCt.ParentContentType = parentContentType;
            ContentType myContentType = contentTypes.Add(newCt);
            web.Context.ExecuteQuery();

            // Return the content type object.
            return myContentType;
        }

```

**CreateContosoDocumentLibrary** вызывает метод **AddFieldToContentTypeById** , который является частью OfficeDevPnP.Core. **AddFieldToContentTypeById** связывает поле с типом контента.

```C#
public static void AddFieldToContentTypeById(this Web web, string contentTypeID, string fieldID, bool required = false, bool hidden = false)
        {
            // Get content type.
            ContentType ct = web.GetContentTypeById(contentTypeID);
            web.Context.Load(ct);
            web.Context.Load(ct.FieldLinks);
            web.Context.ExecuteQuery();

            // Get field.
            Field fld = web.Fields.GetById(new Guid(fieldID));

            // Add field association to content type.
            AddFieldToContentType(web, ct, fld, required, hidden);
        }
```

**CreateContosoDocumentLibrary** вызывает метод **CreateLibrary** ContentTypeManager.cs для создания библиотеки документов. Метод **CreateLibrary** назначает параметры библиотеки, такие как описание библиотеки документов, управление версиями документов и связанных типов контента.

```C#
private void CreateLibrary(ClientContext ctx, Library library, string associateContentTypeID)
        {
            if (!ctx.Web.ListExists(library.Title))
            {
                ctx.Web.AddList(ListTemplateType.DocumentLibrary, library.Title, false);
                List _list = ctx.Web.GetListByTitle(library.Title);
                if(!string.IsNullOrEmpty(library.Description)) {
                    _list.Description = library.Description;
                }

                if(library.VerisioningEnabled) {
                    _list.EnableVersioning = true;
                }

                _list.ContentTypesEnabled = true;
                _list.Update();
                ctx.Web.AddContentTypeToListById(library.Title, associateContentTypeID, true);
                // Remove the default Document Content Type.
                _list.RemoveContentTypeByName(ContentTypeManager.DEFAULT_DOCUMENT_CT_NAME);
                ctx.Web.Context.ExecuteQuery();
            }
            else
            {
                throw new Exception("A list, survey, discussion board, or document library with the specified title already exists in this Web site.  Please choose another title.");
            }
        }
```

**CreateLibrary** вызывает **RemoveContentTypeByName** ListExtensions.cs, которая является частью OfficeDevPnP.Core. **RemoveContentTypeByName** Удаляет тип контента по умолчанию в библиотеке документов.

```C#
        public static void RemoveContentTypeByName(this List list, string contentTypeName)
        {
            if (string.IsNullOrEmpty(contentTypeName))
            {
                throw (contentTypeName == null)
                  ? new ArgumentNullException("contentTypeName")
                  : new ArgumentException(CoreResources.Exception_Message_EmptyString_Arg, "contentTypeName");
            }

            ContentTypeCollection _cts = list.ContentTypes;
            list.Context.Load(_cts);

            IEnumerable<ContentType> _results = list.Context.LoadQuery<ContentType>(_cts.Where(item => item.Name == contentTypeName));
            list.Context.ExecuteQuery();

            ContentType _ct = _results.FirstOrDefault();
            if (_ct != null)
            {
                _ct.DeleteObject();
                list.Update();
                list.Context.ExecuteQuery();
            }
        }
```

После создания библиотеки документов, перейдите в раздел **Параметры библиотеки** в библиотеку документов для просмотра имя, описание, параметры управления версиями документов, тип контента и настраиваемые поля надстройки, назначенные в библиотеку документов.

** На рисунке 2. Библиотека параметров, применяемых с помощью надстройки в **

![Снимок экрана на странице Параметры библиотеки документов, с помощью поля имя, веб-адрес и описание с выделением.](media/aedf5107-bacb-4872-8ad4-8e66b1afead8.png)

## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>

-  [Управление корпоративным информационным содержимым решений для SharePoint 2013 и SharePoint Online](Enterprise-Content-Management-solutions-for-SharePoint-2013-and-SharePoint-Online.md)
    
-  [ECM. Пример приложения Autotagging](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.Autotagging)
