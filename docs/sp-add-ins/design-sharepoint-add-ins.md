# <a name="design-sharepoint-add-ins"></a><span data-ttu-id="9c0f8-101">Разработка надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="9c0f8-101">Design SharePoint Add-ins</span></span>
<span data-ttu-id="9c0f8-102">Получите общее представление о вариантах проектирования и архитектуры, доступных для надстроек SharePoint, и научитесь принимать правильные решения, которые упростят разработку надстройки в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9c0f8-102">Get an overview of the design and architecture options that are available in spappplural, and learn how to make the right decisions to ease the development of your app in sp15allshort.</span></span>
 

 <span data-ttu-id="9c0f8-p101">**Примечание.** Название "приложения для SharePoint" меняется на "надстройки SharePoint". Пока изменения не будут внесены полностью, в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio по-прежнему может встречаться термин "приложение". Дополнительные сведения см. в разделе [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="9c0f8-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

<span data-ttu-id="9c0f8-p102">Предположим, у вас появилась замечательная идея для надстройки. Из этого раздела вы узнаете, какие решения, связанные с проектированием, следует принять, и получите рекомендации по созданию приложения. Например, что представляет собой хороший пользовательский интерфейс? Какие формы приложений доступны? Почему следует использовать одни элементы, а не другие? Какие у вас есть возможности доступа к данным?</span><span class="sxs-lookup"><span data-stu-id="9c0f8-p102">Let's say you have a killer idea for an app. In this section, we'll guide you through the design decisions you need to make and offer best practices to build your app. For example, what makes a good user interface? What are the app "shapes" available? When should I use one instead of another? What options do I have for data access?</span></span> 
 

## <a name="start-designing-sharepoint-add-ins"></a><span data-ttu-id="9c0f8-112">Начало разработки надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="9c0f8-112">Start designing SharePoint Add-ins</span></span>
<span data-ttu-id="9c0f8-113"><a name="SP15Design_Startdesigning"> </a></span><span class="sxs-lookup"><span data-stu-id="9c0f8-113"></span></span>

<span data-ttu-id="9c0f8-p103">Поскольку модель Cloud App Model в SharePoint предоставляет широкие возможности для разработки, Надстройки SharePoint могут быть очень разнообразными. Этот раздел содержит полезные рекомендации для некоторых из наиболее важных решений, которые необходимо принять при планировании и проектировании архитектуры и интерфейса пользователя для надстройки, в том числе, рекомендации по размещению надстройки, эффективному и безопасному доступу надстройки к данным и по созданию качественного интерфейса пользователя.</span><span class="sxs-lookup"><span data-stu-id="9c0f8-p103">Because the Cloud Add-in Model in SharePoint makes so many design options possible, SharePoint Add-ins can come in many shapes and sizes. This section contains helpful guidance for some of the most important decisions that you need to make as you are planning and designing the architecture and user experience of your add-in—including how you will host your add-in, how your add-in will efficiently and securely access data, and what the user experience will be.</span></span>
 

 
<span data-ttu-id="9c0f8-p104">Общие сведения о возможностях проектирования и архитектуры, которые доступны в надстройках для SharePoint, см. в статье  [Существует три способа рассмотрения возможностей проектирования надстроек SharePoint](three-ways-to-think-about-design-options-for-sharepoint-add-ins). Общие сведения о Надстройки SharePoint, см. в статье  [Надстройки SharePoint](sharepoint-add-ins).</span><span class="sxs-lookup"><span data-stu-id="9c0f8-p104">For an overview of the design and architecture options that are available with SharePoint Add-ins, see  [Three ways to think about design options for SharePoint Add-ins](three-ways-to-think-about-design-options-for-sharepoint-add-ins). For an overview of what SharePoint Add-ins are, see  [SharePoint Add-ins](sharepoint-add-ins).</span></span>
 

 

## <a name="choose-the-right-hosting-model-for-your-add-in"></a><span data-ttu-id="9c0f8-118">Выбор подходящей модели размещения надстройки</span><span class="sxs-lookup"><span data-stu-id="9c0f8-118">Choose the right hosting model for your add-in</span></span>
<span data-ttu-id="9c0f8-119"><a name="SP15Design_Hostingmodel"> </a></span><span class="sxs-lookup"><span data-stu-id="9c0f8-119"></span></span>

<span data-ttu-id="9c0f8-p105">Надстройки SharePoint поддерживает несколько вариантов размещения. Можно выбрать собственный веб-стек, либо предоставляемые Microsoft Microsoft Azure и SQL Azure, либо разместить надстройку в SharePoint. Таблица 1 содержит ресурсы, которые помогут вам выбрать правильную модель размещения для вашей надстройки.</span><span class="sxs-lookup"><span data-stu-id="9c0f8-p105">SharePoint Add-ins support multiple hosting options. You can choose your own web stack, have Microsoft provision Microsoft Azure and SQL Azure, or have the add-in hosted on SharePoint. Table 1 contains resources that can help you choose the right hosting model for your add-in.</span></span>
 

 

<span data-ttu-id="9c0f8-123">**Таблица 1. Ресурсы и рекомендации по выбору подходящей модели размещения для надстроек SharePoint**</span><span class="sxs-lookup"><span data-stu-id="9c0f8-123">**Table 1. Resources and guidance for choosing the right hosting model for SharePoint Add-ins**</span></span>


|<span data-ttu-id="9c0f8-124">**Статья**</span><span class="sxs-lookup"><span data-stu-id="9c0f8-124">**Article**</span></span>|<span data-ttu-id="9c0f8-125">**Описание**</span><span class="sxs-lookup"><span data-stu-id="9c0f8-125">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="9c0f8-126">Выбор шаблонов для разработки и размещения надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="9c0f8-126">Choose patterns for developing and hosting your SharePoint Add-in</span></span>](choose-patterns-for-developing-and-hosting-your-sharepoint-add-in)|<span data-ttu-id="9c0f8-127">Узнайте о различных способах размещения компонентов надстроек SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9c0f8-127">Learn about the different ways that you can host the components of SharePoint Add-ins.</span></span>|

## <a name="choose-the-right-data-access-technologies-for-your-add-in"></a><span data-ttu-id="9c0f8-128">Выбор подходящих технологий доступа к данным для надстройки</span><span class="sxs-lookup"><span data-stu-id="9c0f8-128">Choose the right data access technologies for your add-in</span></span>
<span data-ttu-id="9c0f8-129"><a name="SP15Design_Dataaccess"> </a></span><span class="sxs-lookup"><span data-stu-id="9c0f8-129"></span></span>

<span data-ttu-id="9c0f8-p106">Вы должны быть уверены, что ваша надстройка обращается к данным эффективно и безопасно. Для SharePoint существуют различные технологии доступа к данным и работы с данными в надстройке. Таблица 2 содержит ресурсы, которые помогут выбрать подходящий для вашей надстройки механизм доступа к данным.</span><span class="sxs-lookup"><span data-stu-id="9c0f8-p106">You must ensure that your add-in accesses data efficiently and securely. Various data access technologies are available for accessing SharePoint and working with data in your add-in. Table 2 provides resources to help you learn about your options and choose the one that is right for your add-in.</span></span> 
 

 

<span data-ttu-id="9c0f8-133">**Таблица 2. Ресурсы и рекомендации по выборе технологий доступа к данным для использования в надстройках SharePoint**</span><span class="sxs-lookup"><span data-stu-id="9c0f8-133">**Table 2. Resources and guidance for choosing the data access technologies to use in SharePoint Add-ins**</span></span>


|<span data-ttu-id="9c0f8-134">**Статья**</span><span class="sxs-lookup"><span data-stu-id="9c0f8-134">**Article**</span></span>|<span data-ttu-id="9c0f8-135">**Описание**</span><span class="sxs-lookup"><span data-stu-id="9c0f8-135">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="9c0f8-136">Безопасный доступ к данным и клиентские объектные модели для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="9c0f8-136">Secure data access and client object models for SharePoint Add-ins</span></span>](secure-data-access-and-client-object-models-for-sharepoint-add-ins)| <span data-ttu-id="9c0f8-137">Информация о возможностях доступа к данным при разработке приложений для SharePoint, включая возможности подключения для входящих и исходящих сценариев передачи данных, а также API-интерфейсы, доступные при получении доступа к данным SharePoint из вашей надстройки.</span><span class="sxs-lookup"><span data-stu-id="9c0f8-137">Learn about data access options you have when you build SharePoint Add-ins, including data connectivity options for inbound and outbound data scenarios, and the APIs that are available when you want to access SharePoint data from your add-in.</span></span>|

## <a name="design-the-ux-for-your-add-in"></a><span data-ttu-id="9c0f8-138">Проектирование пользовательского интерфейса надстройки</span><span class="sxs-lookup"><span data-stu-id="9c0f8-138">Design the UX for your add-in</span></span>
<span data-ttu-id="9c0f8-139"><a name="SP15Design_UX"> </a></span><span class="sxs-lookup"><span data-stu-id="9c0f8-139"></span></span>

<span data-ttu-id="9c0f8-p107">При разработке надстройки реальная цель должна заключаться в создании интерфейса, который позволит пользователям выполнять сценарии, которые вы намерены для них создать. В таблице 3 представлены ресурсы и рекомендации по проектированию, необходимые для создания надстроек на основе наилучших практик проектирования интерфейсов пользователя, имеющие узнаваемый внешний вид и поведениеSharePoint.</span><span class="sxs-lookup"><span data-stu-id="9c0f8-p107">As you design your add-in, your real goal should be to create an experience that enables users to complete the scenarios that you intend for them to accomplish. In Table 3, discover the resources and design guidance that you need to build great add-ins that follow best practices for user experience design and have the familiar appearance and behavior of SharePoint.</span></span>
 

 

<span data-ttu-id="9c0f8-142">**Таблица 3. Ресурсы и рекомендации по проектированию качественного пользовательского интерфейса для надстроек SharePoint**</span><span class="sxs-lookup"><span data-stu-id="9c0f8-142">**Table 3. Resources and guidance for designing a great user experience for SharePoint Add-ins**</span></span>


|<span data-ttu-id="9c0f8-143">**Статья**</span><span class="sxs-lookup"><span data-stu-id="9c0f8-143">**Article**</span></span>|<span data-ttu-id="9c0f8-144">**Описание**</span><span class="sxs-lookup"><span data-stu-id="9c0f8-144">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="9c0f8-145">Дизайн пользовательского интерфейса надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="9c0f8-145">UX design for SharePoint Add-ins</span></span>](ux-design-for-sharepoint-add-ins)|<span data-ttu-id="9c0f8-146">Узнайте, какие варианты пользовательского интерфейса доступны вам при создании надстроек SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9c0f8-146">Learn about the user experience options that you have when you build SharePoint Add-ins.</span></span>|

## <a name="design-with-update-in-mind"></a><span data-ttu-id="9c0f8-147">Проектирование с расчетом на обновление</span><span class="sxs-lookup"><span data-stu-id="9c0f8-147">Design with update in mind</span></span>
<span data-ttu-id="9c0f8-148"><a name="Upgrade"> </a></span><span class="sxs-lookup"><span data-stu-id="9c0f8-148"></span></span>

<span data-ttu-id="9c0f8-p108">Когда-нибудь вам потребуется сделать обновление для вашей надстройки и загрузить его в Магазин Office или в каталог надстроек организации. Будет намного проще выполнить эту задачу, если при проектировании первой версии подумать о том, как будет обновляться надстройка. Перед началом проектирования мы рекомендуем ознакомиться со статьями  [Процедура обновления надстроек для SharePoint](sharepoint-add-ins-update-process) и [Обновление надстроек для SharePoint](update-sharepoint-add-ins).</span><span class="sxs-lookup"><span data-stu-id="9c0f8-p108">Someday you may want to produce an update of your add-in and upload it to the Office Store or an organization's add-in catalog. That task will be a lot easier if you think about how you would update the add-in while you are designing the first version. We recommend that you read the following articles early in the design phase:  [SharePoint Add-ins update process](sharepoint-add-ins-update-process) and [Update SharePoint Add-ins](update-sharepoint-add-ins).</span></span> 
 

 

## <a name="next-steps-develop-and-publish-your-add-in"></a><span data-ttu-id="9c0f8-152">Дальнейшие действия: разработка и публикация надстройки</span><span class="sxs-lookup"><span data-stu-id="9c0f8-152">Next steps: Develop and publish your add-in</span></span>
<span data-ttu-id="9c0f8-153"><a name="SP15Design_Next"> </a></span><span class="sxs-lookup"><span data-stu-id="9c0f8-153"></span></span>

<span data-ttu-id="9c0f8-p109">Детальный проект для вашей надстройки готов? Будьте готовы создать надстройку и опубликовать ее. Ресурсы, представленные в таблице 4, помогут вам начать работу.</span><span class="sxs-lookup"><span data-stu-id="9c0f8-p109">Have a solid design for your add-in? Get ready to build your add-in and publish it. The resources provided in Table 4 can help you get started.</span></span>
 

 

<span data-ttu-id="9c0f8-157">**Таблица 4. Ресурсы и рекомендации по разработке и публикации надстроек SharePoint**</span><span class="sxs-lookup"><span data-stu-id="9c0f8-157">**Table 4. Resources and guidance for developing and publishing SharePoint Add-ins**</span></span>


|<span data-ttu-id="9c0f8-158">**Статья**</span><span class="sxs-lookup"><span data-stu-id="9c0f8-158">**Article**</span></span>|<span data-ttu-id="9c0f8-159">**Описание**</span><span class="sxs-lookup"><span data-stu-id="9c0f8-159">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="9c0f8-160">Разработка надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="9c0f8-160">Develop SharePoint Add-ins</span></span>](develop-sharepoint-add-ins)|<span data-ttu-id="9c0f8-161">В этой статье рассматриваются сложные понятия и дополнительные возможности, связанные с моделью данных.</span><span class="sxs-lookup"><span data-stu-id="9c0f8-161">Discusses advanced concepts and capabilities of the add-in model.</span></span>|
| [<span data-ttu-id="9c0f8-162">Публикация надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="9c0f8-162">Publish SharePoint Add-ins</span></span>](publish-sharepoint-add-ins)|<span data-ttu-id="9c0f8-163">Описание процесса и требований для публикации надстроек SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9c0f8-163">Describes the process and requirements for publishing SharePoint Add-ins.</span></span>|

## <a name="additional-resources"></a><span data-ttu-id="9c0f8-164">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="9c0f8-164">Additional resources</span></span>
<span data-ttu-id="9c0f8-165"><a name="SP15Design_AddRes"> </a></span><span class="sxs-lookup"><span data-stu-id="9c0f8-165"></span></span>


-  [<span data-ttu-id="9c0f8-166">Пример пакета надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="9c0f8-166">SharePoint Add-ins sample pack</span></span>](http://code.msdn.microsoft.com/office/Apps-for-SharePoint-sample-64c80184)
    
 
-  [<span data-ttu-id="9c0f8-167">Переосмысление разработки для SharePoint</span><span class="sxs-lookup"><span data-stu-id="9c0f8-167">Reimagine SharePoint development</span></span>](http://msdn.microsoft.com/en-US/office/apps/dn133840)
    
 
-  [<span data-ttu-id="9c0f8-168">Надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="9c0f8-168">SharePoint Add-ins</span></span>](sharepoint-add-ins)
    
 
-  [<span data-ttu-id="9c0f8-169">Разработка надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="9c0f8-169">Develop SharePoint Add-ins</span></span>](develop-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="9c0f8-170">Блог, посвященный надстройкам</span><span class="sxs-lookup"><span data-stu-id="9c0f8-170">Blog for add-ins</span></span>](http://blogs.msdn.com/b/spoffapps)
    
 

