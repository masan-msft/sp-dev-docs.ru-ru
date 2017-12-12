---
title: "Документ библиотеки шаблонов пример надстройки для SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 405e5863bbbfdb7740a93e33f9ed8b80f136d39b
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="document-library-templates-sample-add-in-for-sharepoint"></a><span data-ttu-id="664ac-102">Документ библиотеки шаблонов пример надстройки для SharePoint</span><span class="sxs-lookup"><span data-stu-id="664ac-102">Document library templates sample add-in for SharePoint</span></span>

<span data-ttu-id="664ac-103">В рамках стратегии Enterprise содержимое Management (ECM) можно реализовать шаблон библиотеки пользовательских документов и настраивать столбцы сайта, типы контента сайта, поля таксономии, параметры версии и типа контента документа по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="664ac-103">As part of your Enterprise Content Management (ECM) strategy, you can implement a custom document library template, and customize site columns, site content types, taxonomy fields, version settings, and the default document content type.</span></span>
    
<span data-ttu-id="664ac-104">_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="664ac-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="664ac-105">[ECM. DocumentLibraries](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.DocumentLibraries) примере показано, как использовать размещение у поставщика в надстройке для создания списка или библиотеки документов, назначить типу контента и удаление типа контента по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="664ac-105">The [ECM.DocumentLibraries](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.DocumentLibraries) sample shows you how to use a provider-hosted add-in to create a list or document library, assign a content type to it, and remove the default content type.</span></span> <span data-ttu-id="664ac-106">Если вы хотите используйте этого решения:</span><span class="sxs-lookup"><span data-stu-id="664ac-106">Use this solution if you want to:</span></span>    

- <span data-ttu-id="664ac-107">Создание списка или библиотеки документов и применение типа контента по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="664ac-107">Create a list or document library and apply a default content type.</span></span>
    
- <span data-ttu-id="664ac-108">Утверждаете контролировать добавление, обслуживания или реализации локализованных версий настраиваемых полей.</span><span class="sxs-lookup"><span data-stu-id="664ac-108">Assert greater control over the addition, maintenance, or implementation of localized versions of your custom fields.</span></span>
    
- <span data-ttu-id="664ac-109">Удаление типа контента по умолчанию для списка или библиотеки.</span><span class="sxs-lookup"><span data-stu-id="664ac-109">Remove the default content type on a list or library.</span></span>
    
- <span data-ttu-id="664ac-110">Применить параметры конфигурации библиотеки для создания списка или библиотеки.</span><span class="sxs-lookup"><span data-stu-id="664ac-110">Apply library configuration settings when you create a list or library.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="664ac-111">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="664ac-111">Before you begin</span></span>
<span data-ttu-id="664ac-112"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="664ac-112"></span></span>

<span data-ttu-id="664ac-113">Чтобы начать работу, загрузите [ECM. DocumentLibraries](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.DocumentLibraries) пример надстройки из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.</span><span class="sxs-lookup"><span data-stu-id="664ac-113">To get started, download the  [ECM.DocumentLibraries](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.DocumentLibraries) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

<span data-ttu-id="664ac-114">Пользователи, обращающиеся к ECM. Надстройка DocumentLibraries необходимо иметь разрешения на управление списками.</span><span class="sxs-lookup"><span data-stu-id="664ac-114">Users accessing the ECM.DocumentLibraries add-in must have permissions to manage lists.</span></span> <span data-ttu-id="664ac-115">Метод **DoesUserHavePermission** в файле Default.aspx.cs проверяет разрешения пользователя чтобы убедиться, что они могут управлять списками.</span><span class="sxs-lookup"><span data-stu-id="664ac-115">The  **DoesUserHavePermission** method in Default.aspx.cs checks the user's permissions to ensure they can manage lists.</span></span> <span data-ttu-id="664ac-116">Если пользователь не имеет разрешения на управление списками, надстройка представляет сообщение об ошибке пользователю.</span><span class="sxs-lookup"><span data-stu-id="664ac-116">If the user does not have permissions to manage lists, the add-in presents an error message to the user.</span></span>

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

## <a name="using-the-ecmdocumentlibraries-sample-add-in"></a><span data-ttu-id="664ac-117">С помощью ECM. DocumentLibraries пример надстройки</span><span class="sxs-lookup"><span data-stu-id="664ac-117">Using the ECM.DocumentLibraries sample add-in</span></span> 
<span data-ttu-id="664ac-118"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="664ac-118"></span></span>

<span data-ttu-id="664ac-119">При запуске этой надстройки начальной страницы отображается как показано на рисунке 1.</span><span class="sxs-lookup"><span data-stu-id="664ac-119">When you start this add-in , the start page displays as shown in Figure 1.</span></span> <span data-ttu-id="664ac-120">ECM. DocumentLibraries запуск страницы выглядит страницу, чтобы добавить новую библиотеку документов, когда вы выбираете **Контент сайта** > **Добавление приложения** > **Библиотеки документов** > **Дополнительные параметры** - с одной различие.</span><span class="sxs-lookup"><span data-stu-id="664ac-120">The ECM.DocumentLibraries start page looks like the page to add a new document library when you select  **Site Contents** > **add an app** > **Document Library** > **Advanced Options** - with one difference.</span></span> <span data-ttu-id="664ac-121">При запуске надстройки, в раскрывающемся списке шаблона документа отображает шаблон библиотеки пользовательских документов, ИТ и документы Contoso.</span><span class="sxs-lookup"><span data-stu-id="664ac-121">When you start the add-in , the Document Template dropdown list displays custom document library template, IT Document and Contoso Document.</span></span> <span data-ttu-id="664ac-122">При выборе **создания**новой библиотеки документов назначается выбранного типа содержимого.</span><span class="sxs-lookup"><span data-stu-id="664ac-122">When the user chooses **Create**, the selected custom content type is assigned to the new document library.</span></span> 

<span data-ttu-id="664ac-123">** На рисунке 1.</span><span class="sxs-lookup"><span data-stu-id="664ac-123">**Figure 1.</span></span> <span data-ttu-id="664ac-124">Начальная страница ECM. Надстройка DocumentLibraries **</span><span class="sxs-lookup"><span data-stu-id="664ac-124">Start page of the ECM.DocumentLibraries add-in **</span></span>

![Снимок экрана, показывающий ECM. DocumentLibraries надстройки "Запуск" с полем раскрывающегося списка шаблона документа, в котором приведены ИТ документ как выбор.](media/d58b9d12-808e-4f2b-9065-31e6d735dbaa.png)

<span data-ttu-id="664ac-126">Когда пользователи выберите **Создать**, с помощью метода **CreateLibrary_Click** в файле Default.aspx.cs проверяет шаблон выбранные по умолчанию и вызывает метод либо **CreateITDocumentLibrary** , либо **CreateContosoDocumentLibrary** в ContentTypeManager.cs, как показано в следующем коде.</span><span class="sxs-lookup"><span data-stu-id="664ac-126">When users choose  **Create**, the  **CreateLibrary_Click** method in Default.aspx.cs checks the selected default template and makes calls to either the **CreateITDocumentLibrary** or **CreateContosoDocumentLibrary** method in ContentTypeManager.cs, as shown in the following code.</span></span>
    
> [!NOTE] 
> <span data-ttu-id="664ac-127">Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.</span><span class="sxs-lookup"><span data-stu-id="664ac-127">The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

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

<span data-ttu-id="664ac-128">Метод **CreateContosoDocumentLibrary** выполняет следующие задачи, как показано в следующем примере кода:</span><span class="sxs-lookup"><span data-stu-id="664ac-128">The  **CreateContosoDocumentLibrary** method then performs the following tasks, as shown in the next code example:</span></span>

1. <span data-ttu-id="664ac-129">Создание настраиваемых полей в службы управляемых метаданных.</span><span class="sxs-lookup"><span data-stu-id="664ac-129">Creates custom fields in the Managed Metadata Service.</span></span>
    
2. <span data-ttu-id="664ac-130">Создание типа контента.</span><span class="sxs-lookup"><span data-stu-id="664ac-130">Creates a content type.</span></span> 
    
3. <span data-ttu-id="664ac-131">Связывает настраиваемые поля с типами контента.</span><span class="sxs-lookup"><span data-stu-id="664ac-131">Associates the custom fields with the content types.</span></span>
    
4. <span data-ttu-id="664ac-132">Создание библиотеки документов с типом контента.</span><span class="sxs-lookup"><span data-stu-id="664ac-132">Creates the document library with the content type.</span></span>

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

<span data-ttu-id="664ac-133">**CreateContosoDocumentLibrary** вызывает метод **CreateTaxonomyField** , который является частью OfficeDevPnP.Core.</span><span class="sxs-lookup"><span data-stu-id="664ac-133">**CreateContosoDocumentLibrary** calls the **CreateTaxonomyField** method, which is part of the OfficeDevPnP.Core.</span></span> <span data-ttu-id="664ac-134">**CreateTaxonomyField** создает поле в службе управляемых метаданных из надстройки размещением у поставщика.</span><span class="sxs-lookup"><span data-stu-id="664ac-134">**CreateTaxonomyField** creates a field in the managed metadata service from the provider-hosted add-in .</span></span>

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

<span data-ttu-id="664ac-135">**CreateContosoDocumentLibrary** вызывает метод **CreateContentType** , который является частью OfficeDevPnP.Core.</span><span class="sxs-lookup"><span data-stu-id="664ac-135">**CreateContosoDocumentLibrary** calls the **CreateContentType** method which is part of OfficeDevPnP.Core.</span></span> <span data-ttu-id="664ac-136">**CreateContentType** создает новый тип контента.</span><span class="sxs-lookup"><span data-stu-id="664ac-136">**CreateContentType** creates a new content type.</span></span>

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

<span data-ttu-id="664ac-137">**CreateContosoDocumentLibrary** вызывает метод **AddFieldToContentTypeById** , который является частью OfficeDevPnP.Core.</span><span class="sxs-lookup"><span data-stu-id="664ac-137">**CreateContosoDocumentLibrary** calls the **AddFieldToContentTypeById** method, which is part of OfficeDevPnP.Core.</span></span> <span data-ttu-id="664ac-138">**AddFieldToContentTypeById** связывает поле с типом контента.</span><span class="sxs-lookup"><span data-stu-id="664ac-138">**AddFieldToContentTypeById** associates a field with a content type.</span></span>

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

<span data-ttu-id="664ac-139">**CreateContosoDocumentLibrary** вызывает метод **CreateLibrary** ContentTypeManager.cs для создания библиотеки документов.</span><span class="sxs-lookup"><span data-stu-id="664ac-139">**CreateContosoDocumentLibrary** calls the **CreateLibrary** method in ContentTypeManager.cs to create the document library.</span></span> <span data-ttu-id="664ac-140">Метод **CreateLibrary** назначает параметры библиотеки, такие как описание библиотеки документов, управление версиями документов и связанных типов контента.</span><span class="sxs-lookup"><span data-stu-id="664ac-140">The **CreateLibrary** method assigns library settings such as the document library's description, document versioning, and associated content types.</span></span>

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

<span data-ttu-id="664ac-141">**CreateLibrary** вызывает **RemoveContentTypeByName** ListExtensions.cs, которая является частью OfficeDevPnP.Core.</span><span class="sxs-lookup"><span data-stu-id="664ac-141">**CreateLibrary** calls **RemoveContentTypeByName** in ListExtensions.cs, which is part of OfficeDevPnP.Core.</span></span> <span data-ttu-id="664ac-142">**RemoveContentTypeByName** Удаляет тип контента по умолчанию в библиотеке документов.</span><span class="sxs-lookup"><span data-stu-id="664ac-142">**RemoveContentTypeByName** removes the default content type on the document library.</span></span>

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

<span data-ttu-id="664ac-143">После создания библиотеки документов, перейдите в раздел **Параметры библиотеки** в библиотеку документов для просмотра имя, описание, параметры управления версиями документов, тип контента и настраиваемые поля надстройки, назначенные в библиотеку документов.</span><span class="sxs-lookup"><span data-stu-id="664ac-143">After you create the document library, go to the  **Library settings** on your document library to review the name, description, document versioning setting, content type, and custom fields the add-in assigned to your document library.</span></span>

<span data-ttu-id="664ac-144">** На рисунке 2.</span><span class="sxs-lookup"><span data-stu-id="664ac-144">**Figure 2.</span></span> <span data-ttu-id="664ac-145">Библиотека параметров, применяемых с помощью надстройки в **</span><span class="sxs-lookup"><span data-stu-id="664ac-145">Library settings applied by the add-in **</span></span>

![Снимок экрана на странице Параметры библиотеки документов, с помощью поля имя, веб-адрес и описание с выделением.](media/aedf5107-bacb-4872-8ad4-8e66b1afead8.png)

## <a name="see-also"></a><span data-ttu-id="664ac-147">См. также</span><span class="sxs-lookup"><span data-stu-id="664ac-147">See also</span></span>
<span data-ttu-id="664ac-148"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="664ac-148"></span></span>

-  [<span data-ttu-id="664ac-149">Управление корпоративным информационным содержимым решений для SharePoint 2013 и SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="664ac-149">Enterprise Content Management solutions for SharePoint 2013 and SharePoint Online</span></span>](Enterprise-Content-Management-solutions-for-SharePoint-2013-and-SharePoint-Online.md)
    
-  [<span data-ttu-id="664ac-150">ECM. Пример приложения Autotagging</span><span class="sxs-lookup"><span data-stu-id="664ac-150">ECM.Autotagging sample app</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.Autotagging)
