---
title: "Autotagging пример надстройки для SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 6b210688ddd9082a1199cacf0c75cc2401137ccc
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="autotagging-sample-add-in-for-sharepoint"></a><span data-ttu-id="3bae0-102">Autotagging пример надстройки для SharePoint</span><span class="sxs-lookup"><span data-stu-id="3bae0-102">Autotagging sample add-in for SharePoint</span></span>

<span data-ttu-id="3bae0-103">В рамках стратегии Enterprise Content Management (ECM) можно автоматически установить метку документы с помощью метаданных при создании или выгрузить в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3bae0-103">As part of your Enterprise Content Management (ECM) strategy, you can automatically tag documents with metadata when they are created or uploaded to SharePoint.</span></span> 
    
<span data-ttu-id="3bae0-104">_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="3bae0-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="3bae0-105">[ECM. AutoTagging](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.AutoTagging) примере показано, как использовать у поставщика надстройки с автоматически тег контента добавляется в библиотеку SharePoint с привязкой из свойства профиля в пользовательских данных.</span><span class="sxs-lookup"><span data-stu-id="3bae0-105">The [ECM.AutoTagging](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.AutoTagging) sample shows you how to use a provider-hosted add-in to automatically tag content added to a SharePoint library with data sourced from a custom user profile property.</span></span> <span data-ttu-id="3bae0-106">Эта надстройка используется удаленных приемников событий, размещенных на нужный Azure веб-сайт, чтобы:</span><span class="sxs-lookup"><span data-stu-id="3bae0-106">This add-in uses remote event receivers, hosted on an Azure Web Site, to:</span></span>   

- <span data-ttu-id="3bae0-107">Создание поля, типы контента и библиотек документов.</span><span class="sxs-lookup"><span data-stu-id="3bae0-107">Create fields, content types, and document libraries.</span></span>
    
- <span data-ttu-id="3bae0-108">Извлечение значения свойства профиля пользователя.</span><span class="sxs-lookup"><span data-stu-id="3bae0-108">Retrieve the value of a custom user profile property.</span></span>
    
- <span data-ttu-id="3bae0-109">Установить поля таксономии.</span><span class="sxs-lookup"><span data-stu-id="3bae0-109">Set taxonomy fields.</span></span>
    
<span data-ttu-id="3bae0-110">Если вы хотите используйте этого решения:</span><span class="sxs-lookup"><span data-stu-id="3bae0-110">Use this solution if you want to:</span></span>

- <span data-ttu-id="3bae0-111">Реализация приемников событий в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="3bae0-111">Implement event receivers in SharePoint Online.</span></span> 
    
- <span data-ttu-id="3bae0-112">Улучшение результатов поиска с помощью присоединения дополнительных метаданных для содержимого при его создании.</span><span class="sxs-lookup"><span data-stu-id="3bae0-112">Improve search results by attaching additional metadata to content when it's created.</span></span>
    
- <span data-ttu-id="3bae0-113">Классификации контента.</span><span class="sxs-lookup"><span data-stu-id="3bae0-113">Classify your content.</span></span>
    
- <span data-ttu-id="3bae0-114">Модернизация кода до миграции в новой версии SharePoint и использовании приемников событий в прошлом.</span><span class="sxs-lookup"><span data-stu-id="3bae0-114">Modernize your code before migrating to a newer version of SharePoint, and you've used event receivers in the past.</span></span>
    
## <a name="before-you-begin"></a><span data-ttu-id="3bae0-115">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="3bae0-115">Before you begin</span></span>
<span data-ttu-id="3bae0-116"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="3bae0-116"></span></span>

<span data-ttu-id="3bae0-117">Чтобы начать работу, загрузите [ECM. AutoTagging](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.AutoTagging) пример надстройки из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.</span><span class="sxs-lookup"><span data-stu-id="3bae0-117">To get started, download the  [ECM.AutoTagging](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.AutoTagging) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

<span data-ttu-id="3bae0-118">Прежде чем запускать эта надстройка, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="3bae0-118">Before you run this add-in , do the following:</span></span>

1. <span data-ttu-id="3bae0-119">Создание веб-сайта Azure и развертывание ECM. Проект AutoTaggingWeb на него.</span><span class="sxs-lookup"><span data-stu-id="3bae0-119">Create an Azure Web Site and deploy the ECM.AutoTaggingWeb project to it.</span></span>
    
2. <span data-ttu-id="3bae0-120">Регистрация надстройки на странице Appregnew.aspx в Office 365.</span><span class="sxs-lookup"><span data-stu-id="3bae0-120">Register your add-in using the Appregnew.aspx page in Office 365.</span></span> 
    
3. <span data-ttu-id="3bae0-121">Эта надстройка используется только для приложений разрешения.</span><span class="sxs-lookup"><span data-stu-id="3bae0-121">This add-in uses app-only permissions.</span></span> <span data-ttu-id="3bae0-122">Им необходимо назначить разрешения только для приложений, на странице AppInv.aspx в Office 365.</span><span class="sxs-lookup"><span data-stu-id="3bae0-122">You need to assign app-only permissions using the AppInv.aspx page in Office 365.</span></span> <span data-ttu-id="3bae0-123">Скопируйте следующий XML-код из файла AppManifest.xml в текстовом поле XML запрашивать разрешения на странице AppInv.aspx как показано на рисунке 1.</span><span class="sxs-lookup"><span data-stu-id="3bae0-123">Copy the following XML from the AppManifest.xml file to the Permission Request XML textbox on the AppInv.aspx page, as shown in Figure 1.</span></span> 

    ``` 
      <AppPermissionRequests AllowAppOnlyPolicy="true">
        <AppPermissionRequest Scope="http://sharepoint/content/tenant" Right="FullControl" />
        <AppPermissionRequest Scope="http://sharepoint/taxonomy" Right="Read" />
        <AppPermissionRequest Scope="http://sharepoint/social/tenant" Right="Read" />
      </AppPermissionRequests>
    ```

    <span data-ttu-id="3bae0-124">**На рисунке 1. Назначение разрешений только для приложений с помощью страницы AppInv.aspx в Office 365**</span><span class="sxs-lookup"><span data-stu-id="3bae0-124">**Figure 1. Assigning app-only permissions by using the AppInv.aspx page in Office 365**</span></span>

    ![Снимок экрана, на странице AppInv.aspx с выделенными полями идентификатор приложения и разрешение запрос XML](media/d733e2b0-55f3-4aee-872b-49e7e2baf470.png)

4. <span data-ttu-id="3bae0-126">В ECM. AutoTaggingWeb проекта, в файле ReceiverHelper.cs в методе **CreateEventReciever** обновите свойство **ReceiverUrl** , указав URL-адрес вашего веб-сайта Azure.</span><span class="sxs-lookup"><span data-stu-id="3bae0-126">In the ECM.AutoTaggingWeb project, in the ReceiverHelper.cs file, in the  **CreateEventReciever** method, update the **ReceiverUrl** property with the URL of your Azure Web Site.</span></span>

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
5. <span data-ttu-id="3bae0-127">Упаковка и развертывание надстройки.</span><span class="sxs-lookup"><span data-stu-id="3bae0-127">Package and deploy your add-in .</span></span> 
    
<span data-ttu-id="3bae0-128">При запуске надстройки, начальной странице документа Autotagging размещением у поставщика надстройка дисплеев, как показано на рисунке 2.</span><span class="sxs-lookup"><span data-stu-id="3bae0-128">When you start the add-in , the start page of the Document Autotagging provider-hosted add-in displays, as shown in Figure 2.</span></span> <span data-ttu-id="3bae0-129">Начальная страница показаны некоторые дополнительных действий по настройке, которые необходимо выполнить перед назначение и удаление приемников событий.</span><span class="sxs-lookup"><span data-stu-id="3bae0-129">The start page shows some additional configuration steps you need to perform before you assign or remove the event receivers.</span></span> 

<span data-ttu-id="3bae0-130">**На рисунке 2. Дополнительных действий по настройке выполняется на странице надстройка Пуск в SharePoint**</span><span class="sxs-lookup"><span data-stu-id="3bae0-130">**Figure 2. Additional configuration steps to be performed on the add-in start page in SharePoint**</span></span>

![Снимок экрана с autotagging добавьте в начало страницы, с три этапа установки с выделением.](media/eb0521b2-11e2-4c57-8026-d7e838c21eae.png)

## <a name="using-the-ecmautotagging-sample-add-in"></a><span data-ttu-id="3bae0-132">С помощью ECM. Autotagging пример надстройки</span><span class="sxs-lookup"><span data-stu-id="3bae0-132">Using the ECM.Autotagging sample add-in</span></span> 
<span data-ttu-id="3bae0-133"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="3bae0-133"></span></span>

<span data-ttu-id="3bae0-134">В этом примере с помощью удаленного приемника событий автоматически тег (Добавление метаданных в) свойство документы, которые были добавлены в библиотеку документов с данными из настраиваемого пользовательского профиля.</span><span class="sxs-lookup"><span data-stu-id="3bae0-134">This sample uses a remote event receiver to automatically tag (add metadata to) documents that are added to a document library, with data from a custom user profile property.</span></span> <span data-ttu-id="3bae0-135">На рисунке 3 показана схема процесса autotagging документов с помощью удаленного приемника событий.</span><span class="sxs-lookup"><span data-stu-id="3bae0-135">The process flow for autotagging documents using the remote event receiver is shown in Figure 3.</span></span>

<span data-ttu-id="3bae0-136">**На рисунке 3. Технологическая схема для добавления тегов к работе с документами в библиотеке документов с помощью удаленного приемника событий**</span><span class="sxs-lookup"><span data-stu-id="3bae0-136">**Figure 3. Process flow for tagging documents in a document library by using a remote event receiver**</span></span>

![Иллюстрация процесса для добавления тегов документа в библиотеке.](media/430eee99-5ab9-49d8-8021-71d7cee79a73.png)

<span data-ttu-id="3bae0-139">Назначение метаданных для только что созданного документа в библиотеке документов с помощью удаленного приемника событий:</span><span class="sxs-lookup"><span data-stu-id="3bae0-139">To assign metadata to the newly created document in the document library by using a remote event receiver:</span></span>

1. <span data-ttu-id="3bae0-140">Пользователь создает или отправляет новое содержимое в библиотеке документов.</span><span class="sxs-lookup"><span data-stu-id="3bae0-140">A user creates or uploads new content to a document library.</span></span> <span data-ttu-id="3bae0-141">Удаленный приемник событий назначается для обработки событий **ItemAdding** или **ItemAdded** в эту библиотеку документов.</span><span class="sxs-lookup"><span data-stu-id="3bae0-141">A remote event receiver is assigned to handle  **ItemAdding** or **ItemAdded** events on this document library.</span></span>
    
2. <span data-ttu-id="3bae0-142">Метод **ItemAdding** или **ItemAdded** выполняется вызов приемника событий remove.</span><span class="sxs-lookup"><span data-stu-id="3bae0-142">The  **ItemAdding** or **ItemAdded** method makes a call to the remove event receiver.</span></span>
    
3. <span data-ttu-id="3bae0-143">Надстройка размещением у поставщика извлекает значение свойства профиля пользователя, настраиваемых в пользовательского профиля службы SharePoint для этого пользователя.</span><span class="sxs-lookup"><span data-stu-id="3bae0-143">The provider-hosted add-in fetches the value of a custom user profile property in the User Profile Service of SharePoint for that user.</span></span> <span data-ttu-id="3bae0-144">В этот образец надстройки извлекается свойство классификации настраиваемого пользовательского профиля, который был добавлен ранее.</span><span class="sxs-lookup"><span data-stu-id="3bae0-144">In this sample add-in , the Classification custom user profile property that was added previously is retrieved.</span></span>
    
4. <span data-ttu-id="3bae0-145">В удаленный приемник событий обновление метаданных на новый документ со значением свойства профиля пользователя для этого пользователя.</span><span class="sxs-lookup"><span data-stu-id="3bae0-145">The remote event receiver updates the metadata on the new document with the value of the custom user profile property for that user.</span></span> 

### <a name="run-scenario-1"></a><span data-ttu-id="3bae0-146">Запустите сценарий 1</span><span class="sxs-lookup"><span data-stu-id="3bae0-146">Run Scenario 1</span></span>

<span data-ttu-id="3bae0-147">После нажатия кнопки **Запуск сценария 1**надстройки выполняет следующее.</span><span class="sxs-lookup"><span data-stu-id="3bae0-147">When you choose the button  **Run Scenario 1**, the add-in does the following:</span></span>

1. <span data-ttu-id="3bae0-148">Создание библиотеки документов.</span><span class="sxs-lookup"><span data-stu-id="3bae0-148">Creates a document library.</span></span>
    
2. <span data-ttu-id="3bae0-149">Создание удаленного приемника событий для событий ItemAdding.</span><span class="sxs-lookup"><span data-stu-id="3bae0-149">Creates the remote event receiver for the ItemAdding event.</span></span>
    
    <span data-ttu-id="3bae0-150">**Примечание**  В этой статье обсуждаются тип приемника событий ItemAdding.</span><span class="sxs-lookup"><span data-stu-id="3bae0-150">**Note**  This article discusses the ItemAdding event receiver type.</span></span> <span data-ttu-id="3bae0-151">Как правило тип приемника событий ItemAdding работает лучше, чем тип приемника событий ItemAdded.</span><span class="sxs-lookup"><span data-stu-id="3bae0-151">Generally, the ItemAdding event receiver type performs better than the ItemAdded event receiver type.</span></span> <span data-ttu-id="3bae0-152">ECM. Пример Autotagging предоставляет код для событий ItemAdding и ItemAdded типов получателя.</span><span class="sxs-lookup"><span data-stu-id="3bae0-152">The ECM.Autotagging sample provides code for both the ItemAdding and ItemAdded event receiver types.</span></span>

3. <span data-ttu-id="3bae0-153">Добавление приемника удаленных событий в библиотеку документов.</span><span class="sxs-lookup"><span data-stu-id="3bae0-153">Adds the remote event receiver to the document library.</span></span>
    
<span data-ttu-id="3bae0-154">Следующий код в метод **btnScenario1_Click** Default.aspx.cs страницы в ECM. Эти шаги показаны на AutoTaggingWeb проекта.</span><span class="sxs-lookup"><span data-stu-id="3bae0-154">The following code, in the  **btnScenario1_Click** method of the Default.aspx.cs page in the ECM.AutoTaggingWeb project, shows these steps.</span></span>

<span data-ttu-id="3bae0-155">**Примечание**  Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.</span><span class="sxs-lookup"><span data-stu-id="3bae0-155">**Note**  The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

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

<span data-ttu-id="3bae0-156">Вызов метода **CreateContosoDocumentLibrary** .</span><span class="sxs-lookup"><span data-stu-id="3bae0-156">A call is made to the  **CreateContosoDocumentLibrary** method.</span></span> <span data-ttu-id="3bae0-157">Следующий код в файле ScenarioHandler.cs использует методы из OfficeDevPnP.Core для создания библиотеки настраиваемых областей с помощью настраиваемого типа контента.</span><span class="sxs-lookup"><span data-stu-id="3bae0-157">The following code in the ScenarioHandler.cs file uses methods from OfficeDevPnP.Core to create a custom document library with a custom content type.</span></span> <span data-ttu-id="3bae0-158">Тип контента по умолчанию в библиотеке документов, будет удален.</span><span class="sxs-lookup"><span data-stu-id="3bae0-158">The default content type in the document library is removed.</span></span>

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

<span data-ttu-id="3bae0-159">После выполнения этого кода библиотеки документов AutoTaggingSampleItemAdding будет создан в контент сайта, как показано на рисунке 4.</span><span class="sxs-lookup"><span data-stu-id="3bae0-159">After this code runs, the AutoTaggingSampleItemAdding document library is created in Site Contents, as shown in Figure 4.</span></span>

<span data-ttu-id="3bae0-160">**На рисунке 4. Библиотека документов AutoTaggingSampleItemAdding**</span><span class="sxs-lookup"><span data-stu-id="3bae0-160">**Figure 4. AutoTaggingSampleItemAdding document library**</span></span>

![Снимок экрана shwoing странице контент сайта с помощью новой библиотеки документов AutoTaggingSampleItemAdd.](media/8820a44f-8df8-4c80-aeaa-e50c37b8912c.png)

<span data-ttu-id="3bae0-162">В ECM. Проект AutoTaggingWeb в файле ReceiverHelper.cs метод **CreateEventReciever** создает определение приемника событий ItemAdding.</span><span class="sxs-lookup"><span data-stu-id="3bae0-162">In the ECM.AutoTaggingWeb project, in the ReceiverHelper.cs file, the  **CreateEventReciever** method creates the ItemAdding event receiver definition.</span></span> <span data-ttu-id="3bae0-163">В ECM. Проект AutoTaggingWeb папка служб включает в себя веб-службы, называется AutoTaggingService.svc.</span><span class="sxs-lookup"><span data-stu-id="3bae0-163">In the ECM.AutoTaggingWeb project, the Services folder includes a web service called AutoTaggingService.svc.</span></span> <span data-ttu-id="3bae0-164">При публикации ECM. Также развертывания проекта AutoTaggingWeb для Azure веб-узла, данной веб-службы для веб-узла.</span><span class="sxs-lookup"><span data-stu-id="3bae0-164">When you published the ECM.AutoTaggingWeb project to your Azure Web Site, this web service was also deployed to your site.</span></span> <span data-ttu-id="3bae0-165">Метод **CreateEventReciever** назначает данной веб-службы удаленного приемника событий в библиотеке документов.</span><span class="sxs-lookup"><span data-stu-id="3bae0-165">The **CreateEventReciever** method assigns this web service as the remote event receiver on the document library.</span></span> <span data-ttu-id="3bae0-166">Следующий код в метод **CreateEventReciever** показано, как назначить веб-службы удаленного приемника событий.</span><span class="sxs-lookup"><span data-stu-id="3bae0-166">The following code from the **CreateEventReciever** method shows how to assign the web service to the remote event receiver.</span></span>

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

<span data-ttu-id="3bae0-167">Следующий код в метод **AddEventReceiver** назначает приемника удаленных событий в библиотеку документов.</span><span class="sxs-lookup"><span data-stu-id="3bae0-167">The following code from the  **AddEventReceiver** method assigns the remote event receiver to the document library.</span></span>

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

<span data-ttu-id="3bae0-168">Теперь в удаленный приемник событий добавляется в библиотеку документов.</span><span class="sxs-lookup"><span data-stu-id="3bae0-168">Now, the remote event receiver is added to the document library.</span></span> <span data-ttu-id="3bae0-169">При отправке документа в библиотеку документов **AutoTaggingSampleItemAdding** документ будет помечен со значением свойства профиля пользователя классификации для этого пользователя.</span><span class="sxs-lookup"><span data-stu-id="3bae0-169">When you upload a document to the  **AutoTaggingSampleItemAdding** document library, the document will be tagged with the value of the Classification custom user profile property for that user.</span></span> <span data-ttu-id="3bae0-170">На рисунке 5 показано, как для просмотра свойств в документе.</span><span class="sxs-lookup"><span data-stu-id="3bae0-170">Figure 5 shows how to view the properties on a document.</span></span> <span data-ttu-id="3bae0-171">На рисунке 6 показан документ метаданных с полем классификации.</span><span class="sxs-lookup"><span data-stu-id="3bae0-171">Figure 6 shows the document's metadata with the Classification field.</span></span>


<span data-ttu-id="3bae0-172">**На рисунке 5. Просмотр свойств документа**</span><span class="sxs-lookup"><span data-stu-id="3bae0-172">**Figure 5. Viewing document properties**</span></span>

<span data-ttu-id="3bae0-173">![Снимок экрана с тестовый документ в библиотеке со свойствами были развернуты. ](media/991dc064-1855-4897-a012-c56c0079131e.png)
 **На рисунке 6. Поля классификации в метаданных документа**</span><span class="sxs-lookup"><span data-stu-id="3bae0-173">![Screenshot of a test document in the library with the properties expanded.](media/991dc064-1855-4897-a012-c56c0079131e.png)
**Figure 6. Classification field in the document metadata**</span></span>

![Снимок экрана, показывающий метаданных в тестовый документ с HBI в поле классификации.](media/9dc5be77-70b3-400a-a636-f5fc2face335.png)

<span data-ttu-id="3bae0-175">Метод **HandleAutoTaggingItemAdding** в файле AutoTaggingService.svc.cs **GetProfilePropertyFor** метод используется для извлечения значения свойства профиля пользователя классификации.</span><span class="sxs-lookup"><span data-stu-id="3bae0-175">The  **HandleAutoTaggingItemAdding** method, in the AutoTaggingService.svc.cs file, uses the **GetProfilePropertyFor** method to retrieve the value of the Classification user profile property.</span></span>

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
    
<span data-ttu-id="3bae0-176">**Важные**  Могут храниться в виде метаданных в документе после получения значения **классификации** из метода **GetProfilePropertyFor** , определенным образом должен иметь формат значения **классификации** .</span><span class="sxs-lookup"><span data-stu-id="3bae0-176">**Important**  After retrieving the  **Classification** value from the **GetProfilePropertyFor** method, the **Classification** value must be formatted in a certain way before it can be stored as metadata on the document.</span></span> <span data-ttu-id="3bae0-177">Метод **GetTaxonomyFormat** в файле AutoTaggingHelper.cs показано, как для форматирования значения **классификации** .</span><span class="sxs-lookup"><span data-stu-id="3bae0-177">The **GetTaxonomyFormat** method in the AutoTaggingHelper.cs file shows how to format the **Classification** value.</span></span>

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

### <a name="remove-event-scenario-1"></a><span data-ttu-id="3bae0-178">Удалить сценарий событие 1</span><span class="sxs-lookup"><span data-stu-id="3bae0-178">Remove Event Scenario 1</span></span>

<span data-ttu-id="3bae0-179">При нажатии кнопки **Удалить сценарий событие 1**, следующий код выполняется удаление приемника событий из библиотеки документов.</span><span class="sxs-lookup"><span data-stu-id="3bae0-179">When you choose the button  **Remove Event Scenario 1**, the following code runs to remove the event receiver from the document library.</span></span>

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

## <a name="additional-resources"></a><span data-ttu-id="3bae0-180">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="3bae0-180">Additional resources</span></span>
<span data-ttu-id="3bae0-181"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="3bae0-181"></span></span>

-  [<span data-ttu-id="3bae0-182">Управление корпоративным информационным содержимым решений для SharePoint 2013 и SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="3bae0-182">Enterprise Content Management solutions for SharePoint 2013 and SharePoint Online</span></span>](Enterprise-Content-Management-solutions-for-SharePoint-2013-and-SharePoint-Online.md)
    
-  [<span data-ttu-id="3bae0-183">Пример OfficeDevPnP.Core</span><span class="sxs-lookup"><span data-stu-id="3bae0-183">OfficeDevPnP.Core sample</span></span>](https://github.com/SharePoint/PnP-Sites-Core/tree/master/Core)
    
