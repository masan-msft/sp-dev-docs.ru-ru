---
title: "Autotagging пример надстройки для SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 79be82cac67ad11921b4c4477e5773efc98396e7
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="autotagging-sample-add-in-for-sharepoint"></a>Autotagging пример надстройки для SharePoint

В рамках стратегии Enterprise Content Management (ECM) можно автоматически установить метку документы с помощью метаданных при создании или выгрузить в SharePoint. 
    
_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_

[ECM. AutoTagging](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.AutoTagging) примере показано, как использовать у поставщика надстройки с автоматически тег контента добавляется в библиотеку SharePoint с привязкой из свойства профиля в пользовательских данных. Эта надстройка используется удаленных приемников событий, размещенных на нужный Azure веб-сайт, чтобы:   

- Создание поля, типы контента и библиотек документов.
    
- Извлечение значения свойства профиля пользователя.
    
- Установить поля таксономии.
    
Если вы хотите используйте этого решения:

- Реализация приемников событий в SharePoint Online. 
    
- Улучшение результатов поиска с помощью присоединения дополнительных метаданных для содержимого при его создании.
    
- Классификации контента.
    
- Модернизация кода до миграции в новой версии SharePoint и использовании приемников событий в прошлом.
    
## <a name="before-you-begin"></a>Перед началом работы
<a name="sectionSection0"> </a>

Чтобы начать работу, загрузите [ECM. AutoTagging](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.AutoTagging) пример надстройки из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.

Прежде чем запускать эта надстройка, сделайте следующее:

1. Создание веб-сайта Azure и развертывание ECM. Проект AutoTaggingWeb на него.
    
2. Регистрация надстройки на странице Appregnew.aspx в Office 365. 
    
3. Эта надстройка используется только для приложений разрешения. Им необходимо назначить разрешения только для приложений, на странице AppInv.aspx в Office 365. Скопируйте следующий XML-код из файла AppManifest.xml в текстовом поле XML запрашивать разрешения на странице AppInv.aspx как показано на рисунке 1. 

    ``` 
      <AppPermissionRequests AllowAppOnlyPolicy="true">
        <AppPermissionRequest Scope="http://sharepoint/content/tenant" Right="FullControl" />
        <AppPermissionRequest Scope="http://sharepoint/taxonomy" Right="Read" />
        <AppPermissionRequest Scope="http://sharepoint/social/tenant" Right="Read" />
      </AppPermissionRequests>
    ```

    **На рисунке 1. Назначение разрешений только для приложений с помощью страницы AppInv.aspx в Office 365**

    ![Снимок экрана, на странице AppInv.aspx с выделенными полями идентификатор приложения и разрешение запрос XML](media/d733e2b0-55f3-4aee-872b-49e7e2baf470.png)

4. В ECM. AutoTaggingWeb проекта, в файле ReceiverHelper.cs в методе **CreateEventReciever** обновите свойство **ReceiverUrl** , указав URL-адрес вашего веб-сайта Azure.

    ```C#
        public static EventReceiverDefinitionCreationInformation CreateEventReciever(string receiverName, EventReceiverType type)
            {
    
                EventReceiverDefinitionCreationInformation _rer = new EventReceiverDefinitionCreationInformation();
                _rer.EventType = type;
                _rer.ReceiverName = receiverName;
                _rer.ReceiverClass = "ECM.AutoTaggingWeb.Services.AutoTaggingService";
                _rer.ReceiverUrl = "https://<Your domain>.azurewebsites.net/Services/AutoTaggingService.svc";
                _rer.Synchronization = EventReceiverSynchronization.Synchronous;
                return _rer;
            }
    
    ```
5. Упаковка и развертывание надстройки. 
    
При запуске надстройки, начальной странице документа Autotagging размещением у поставщика надстройка дисплеев, как показано на рисунке 2. Начальная страница показаны некоторые дополнительных действий по настройке, которые необходимо выполнить перед назначение и удаление приемников событий. 

**На рисунке 2. Дополнительных действий по настройке выполняется на странице надстройка Пуск в SharePoint**

![Снимок экрана с autotagging добавьте в начало страницы, с три этапа установки с выделением.](media/eb0521b2-11e2-4c57-8026-d7e838c21eae.png)

## <a name="using-the-ecmautotagging-sample-add-in"></a>С помощью ECM. Autotagging пример надстройки 
<a name="sectionSection1"> </a>

В этом примере с помощью удаленного приемника событий автоматически тег (Добавление метаданных в) свойство документы, которые были добавлены в библиотеку документов с данными из настраиваемого пользовательского профиля. На рисунке 3 показана схема процесса autotagging документов с помощью удаленного приемника событий.

**На рисунке 3. Технологическая схема для добавления тегов к работе с документами в библиотеке документов с помощью удаленного приемника событий**

![Иллюстрация процесса для добавления тегов документа в библиотеке. Когда пользователь создает контент, надстройки подключается приемника событий, которое получает доступ к профилю пользователя и отправляет данные в SharePoint.](media/430eee99-5ab9-49d8-8021-71d7cee79a73.png)

Назначение метаданных для только что созданного документа в библиотеке документов с помощью удаленного приемника событий:

1. Пользователь создает или отправляет новое содержимое в библиотеке документов. Удаленный приемник событий назначается для обработки событий **ItemAdding** или **ItemAdded** в эту библиотеку документов.
    
2. Метод **ItemAdding** или **ItemAdded** выполняется вызов приемника событий remove.
    
3. Надстройка размещением у поставщика извлекает значение свойства профиля пользователя, настраиваемых в пользовательского профиля службы SharePoint для этого пользователя. В этот образец надстройки извлекается свойство классификации настраиваемого пользовательского профиля, который был добавлен ранее.
    
4. В удаленный приемник событий обновление метаданных на новый документ со значением свойства профиля пользователя для этого пользователя. 

### <a name="run-scenario-1"></a>Запустите сценарий 1

После нажатия кнопки **Запуск сценария 1**надстройки выполняет следующее.

1. Создание библиотеки документов.
    
2. Создание удаленного приемника событий для событий ItemAdding.
    
    > [!NOTE] 
    > В этой статье обсуждаются тип приемника событий ItemAdding. Как правило тип приемника событий ItemAdding работает лучше, чем тип приемника событий ItemAdded. ECM. Пример Autotagging предоставляет код для событий ItemAdding и ItemAdded типов получателя.

3. Добавление приемника удаленных событий в библиотеку документов.
    
Следующий код в метод **btnScenario1_Click** Default.aspx.cs страницы в ECM. Эти шаги показаны на AutoTaggingWeb проекта.

> [!NOTE] 
> Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.

```C#
protected void btnScenario1_Click(object sender, EventArgs e)
        {
            var _libraryToCreate = this.GetLibaryInformationItemAdding();
 
            var spContext = SharePointContextProvider.Current.GetSharePointContext(Context);
            using (var ctx = spContext.CreateUserClientContextForSPHost())
            {
                try 
                { 
                    if(!ctx.Web.ListExists(_libraryToCreate.Title))
                    {
                        ScenarioHandler _scenario = new ScenarioHandler();
                        _scenario.CreateContosoDocumentLibrary(ctx, _libraryToCreate);
                    }
                    List _list = ctx.Web.Lists.GetByTitle(_libraryToCreate.Title);
                    EventReceiverDefinitionCreationInformation _rec = ReceiverHelper.CreateEventReciever(ScenarioHandler.AUTOTAGGING_ITEM_ADDING_RERNAME, EventReceiverType.ItemAdding);
                    ReceiverHelper.AddEventReceiver(ctx, _list, _rec);
                }
                catch(Exception _ex)
                {

                }
            }
        }  
```

Вызов метода **CreateContosoDocumentLibrary** . Следующий код в файле ScenarioHandler.cs использует методы из OfficeDevPnP.Core для создания библиотеки настраиваемых областей с помощью настраиваемого типа контента. Тип контента по умолчанию в библиотеке документов, будет удален.

```C#
public void CreateContosoDocumentLibrary(ClientContext ctx, Library library)
        {
            // Check the fields.
            if (!ctx.Web.FieldExistsById(FLD_CLASSIFICATION_ID))
            {
                ctx.Web.CreateTaxonomyField(FLD_CLASSIFICATION_ID,
                                            FLD_CLASSIFICATION_INTERNAL_NAME,
                                            FLD_CLASSIFICATION_DISPLAY_NAME,
                                            FIELDS_GROUP_NAME,
                                            TAXONOMY_GROUP,
                                            TAXONOMY_TERMSET_CLASSIFICATION_NAME);
            }

            // Check the content type.
            if (!ctx.Web.ContentTypeExistsById(CONTOSODOCUMENT_CT_ID))
            {
                ctx.Web.CreateContentType(CONTOSODOCUMENT_CT_NAME,
                                          CT_DESC, CONTOSODOCUMENT_CT_ID,
                                          CT_GROUP);
            }

            // Associate fields to content types.
            if (!ctx.Web.FieldExistsByNameInContentType(CONTOSODOCUMENT_CT_NAME, FLD_CLASSIFICATION_INTERNAL_NAME))
            {
                ctx.Web.AddFieldToContentTypeById(CONTOSODOCUMENT_CT_ID,
                                                  FLD_CLASSIFICATION_ID.ToString(),
                                                  false);
            }

            
            CreateLibrary(ctx, library, CONTOSODOCUMENT_CT_ID);
        }

private void CreateLibrary(ClientContext ctx, Library library, string associateContentTypeID)
        {
            if (!ctx.Web.ListExists(library.Title))
            {
                ctx.Web.AddList(ListTemplateType.DocumentLibrary, library.Title, false);
                List _list = ctx.Web.GetListByTitle(library.Title);
                if (!string.IsNullOrEmpty(library.Description))
                {
                    _list.Description = library.Description;
                }

                if (library.VerisioningEnabled)
                {
                    _list.EnableVersioning = true;
                }

                _list.ContentTypesEnabled = true;
                _list.RemoveContentTypeByName("Document");
                _list.Update();
                
     
                ctx.Web.AddContentTypeToListById(library.Title, associateContentTypeID, true);
                ctx.Web.Context.ExecuteQuery();
               
            }
            else
            {
                throw new Exception("A list, survey, discussion board, or document library with the specified title already exists in this Web site.  Please choose another title.");
            }
        }
```

После выполнения этого кода библиотеки документов AutoTaggingSampleItemAdding будет создан в контент сайта, как показано на рисунке 4.

**На рисунке 4. Библиотека документов AutoTaggingSampleItemAdding**

![Снимок экрана shwoing странице контент сайта с помощью новой библиотеки документов AutoTaggingSampleItemAdd.](media/8820a44f-8df8-4c80-aeaa-e50c37b8912c.png)

В ECM. Проект AutoTaggingWeb в файле ReceiverHelper.cs метод **CreateEventReciever** создает определение приемника событий ItemAdding. В ECM. Проект AutoTaggingWeb папка служб включает в себя веб-службы, называется AutoTaggingService.svc. При публикации ECM. Также развертывания проекта AutoTaggingWeb для Azure веб-узла, данной веб-службы для веб-узла. Метод **CreateEventReciever** назначает данной веб-службы удаленного приемника событий в библиотеке документов. Следующий код в метод **CreateEventReciever** показано, как назначить веб-службы удаленного приемника событий.

```C#
public static EventReceiverDefinitionCreationInformation CreateEventReciever(string receiverName, EventReceiverType type)
        {

            EventReceiverDefinitionCreationInformation _rer = new EventReceiverDefinitionCreationInformation();
            _rer.EventType = type;
            _rer.ReceiverName = receiverName;
            _rer.ReceiverClass = "ECM.AutoTaggingWeb.Services.AutoTaggingService";
            _rer.ReceiverUrl = "https://<Your domain>.azurewebsites.net/Services/AutoTaggingService.svc";
            _rer.Synchronization = EventReceiverSynchronization.Synchronous;
            return _rer;
        }

```

Следующий код в метод **AddEventReceiver** назначает приемника удаленных событий в библиотеку документов.

```C#
public static void AddEventReceiver(ClientContext ctx, List list, EventReceiverDefinitionCreationInformation eventReceiverInfo)
        {
            if (!DoesEventReceiverExistByName(ctx, list, eventReceiverInfo.ReceiverName))
            {
                list.EventReceivers.Add(eventReceiverInfo);
                ctx.ExecuteQuery();
            }
        }

```

Теперь в удаленный приемник событий добавляется в библиотеку документов. При отправке документа в библиотеку документов **AutoTaggingSampleItemAdding** документ будет помечен со значением свойства профиля пользователя классификации для этого пользователя. На рисунке 5 показано, как для просмотра свойств в документе. На рисунке 6 показан документ метаданных с полем классификации.


**На рисунке 5. Просмотр свойств документа**

![Снимок экрана с тестовый документ в библиотеке со свойствами были развернуты. ](media/991dc064-1855-4897-a012-c56c0079131e.png)
 **На рисунке 6. Поля классификации в метаданных документа**

![Снимок экрана, показывающий метаданных в тестовый документ с HBI в поле классификации.](media/9dc5be77-70b3-400a-a636-f5fc2face335.png)

Метод **HandleAutoTaggingItemAdding** в файле AutoTaggingService.svc.cs **GetProfilePropertyFor** метод используется для извлечения значения свойства профиля пользователя классификации.

```C#
public void HandleAutoTaggingItemAdding(SPRemoteEventProperties properties,SPRemoteEventResult result)
        {
            using (ClientContext ctx = TokenHelper.CreateRemoteEventReceiverClientContext(properties))
            {
                if (ctx != null)
                {
                    var itemProperties = properties.ItemEventProperties;
                    var _userLoginName = properties.ItemEventProperties.UserLoginName;
                    var _afterProperites = itemProperties.AfterProperties;
                    if(!_afterProperites.ContainsKey(ScenarioHandler.FLD_CLASSIFICATION_INTERNAL_NAME))
                    {
                        string _classficationToSet = ProfileHelper.GetProfilePropertyFor(ctx, _userLoginName, Constants.UPA_CLASSIFICATION_PROPERTY);
                        if(!string.IsNullOrEmpty(_classficationToSet))
                        { 
                            var _formatTaxonomy = AutoTaggingHelper.GetTaxonomyFormat(ctx, _classficationToSet);
                            result.ChangedItemProperties.Add(ScenarioHandler.FLD_CLASSIFICATION_INTERNAL_NAME, _formatTaxonomy);
                        }
                    }
                }
            }
        }

```
    
**Важные**  Могут храниться в виде метаданных в документе после получения значения **классификации** из метода **GetProfilePropertyFor** , определенным образом должен иметь формат значения **классификации** . Метод **GetTaxonomyFormat** в файле AutoTaggingHelper.cs показано, как для форматирования значения **классификации** .

```C#
public static string GetTaxonomyFormat(ClientContext ctx, string term)
        { 
            if(string.IsNullOrEmpty(term))
            {
                throw new ArgumentException(string.Format(EXCEPTION_MSG_INVALID_ARG, "term"));
            }
            string _result = string.Empty;
            var _list = ctx.Web.Lists.GetByTitle(TAXONOMY_HIDDEN_LIST_NAME);
            CamlQuery _caml = new CamlQuery();

            _caml.ViewXml = string.Format(TAXONOMY_CAML_QRY, term);
            var _listItemCollection = _list.GetItems(_caml);

            ctx.Load(_listItemCollection,
                eachItem => eachItem.Include(
                    item => item,
                    item => item.Id,
                    item => item[TAXONOMY_FIELDS_IDFORTERM]));
            ctx.ExecuteQuery();

            if (_listItemCollection.Count > 0)
            {
                var _item = _listItemCollection.FirstOrDefault();
                var _wssId = _item.Id;
                var _termId = _item[TAXONOMY_FIELDS_IDFORTERM].ToString(); ;
                _result = string.Format(TAXONOMY_FORMATED_STRING, _wssId, term, _termId);
            }

            return _result;
        }

```

### <a name="remove-event-scenario-1"></a>Удалить сценарий событие 1

При нажатии кнопки **Удалить сценарий событие 1**, следующий код выполняется удаление приемника событий из библиотеки документов.

```C#
public static void RemoveEventReceiver(ClientContext ctx, List list, string receiverName)
        {
            ctx.Load(list, lib => lib.EventReceivers);
            ctx.ExecuteQuery();

            var _rer = list.EventReceivers.Where(e => e.ReceiverName == receiverName).FirstOrDefault();
            if(_rer != null)
            {
                _rer.DeleteObject();
                ctx.ExecuteQuery();
            }
        }

```

## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>

-  [Управление корпоративным информационным содержимым решений для SharePoint 2013 и SharePoint Online](Enterprise-Content-Management-solutions-for-SharePoint-2013-and-SharePoint-Online.md)
    
-  [Пример OfficeDevPnP.Core](https://github.com/SharePoint/PnP-Sites-Core/tree/master/Core)
    
