# <a name="known-issues-and-frequently-asked-questions"></a><span data-ttu-id="14fff-101">Известные проблемы и часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="14fff-101">Known issues and frequently asked questions</span></span>

<span data-ttu-id="14fff-102">На этой странице представлены известные проблемы и ответы на часто задаваемые вопросы о SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="14fff-102">This page is for listing any known issues or to answer any frequently asked questions around SharePoint Framework.</span></span> 

## <a name="known-issues"></a><span data-ttu-id="14fff-103">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="14fff-103">Known issues</span></span>

<span data-ttu-id="14fff-104">**Проблема с сертификатом разработчика в Chrome (версии 58 и новее)**</span><span class="sxs-lookup"><span data-stu-id="14fff-104">**Dev certificate issue with Chrome (v58-)**</span></span>

- <span data-ttu-id="14fff-105">*Дата: 28 апреля*</span><span class="sxs-lookup"><span data-stu-id="14fff-105">*Date - 28th of April*</span></span>
- <span data-ttu-id="14fff-106">*Обновление: 2 мая*</span><span class="sxs-lookup"><span data-stu-id="14fff-106">*Updated - 2nd of May*</span></span>

<span data-ttu-id="14fff-p101">Если вы используете браузер Chrome для разработки, у вас могут возникнуть проблемы с сертификатом разработчика независимо от того, выполняется ли команда `gulp trust-dev-cert`. В Chrome 58 изменилась модель проверки сертификатов, и во время доступа к локальной рабочей области может появиться такое сообщение: "Ваше подключение не защищено".</span><span class="sxs-lookup"><span data-stu-id="14fff-p101">If you are using Chrome as your development browser, you might have challenges with the developer certificate regardless of executing `gulp trust-dev-cert` command. Chrome has changed its model for certificate validation starting from version 58 and you might see "Your connection is not private" warning when you are accessing the local workbench.</span></span>

<span data-ttu-id="14fff-p102">Следует обновить пакеты шаблонов Yeoman. Мы обновили логику создания сертификатов в пакете *@microsoft/gulp-core-build-serve*. Для существующих решений вы можете просто удалить эту папку и выполнить `npm install`, чтобы получить обновленный пакет. Кроме того, вам понадобится выполнить команды `untrust-dev-cert` и `trust-dev-cert` на компьютере, чтобы устранить проблему с логикой создания сертификатов.</span><span class="sxs-lookup"><span data-stu-id="14fff-p102">You should update your Yeoman template packages. We have updated certification creation logic in the *@microsoft/gulp-core-build-serve* package. In existing solutions, you can simply delete this folder and run `npm install` to get the updated package. You will also need to execute `untrust-dev-cert` and `trust-dev-cert` commands in your machine to address the certification creation logic issue.</span></span> 

## <a name="frequently-asked-questions"></a><span data-ttu-id="14fff-113">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="14fff-113">Frequently asked questions</span></span>

<span data-ttu-id="14fff-114">**Когда в SharePoint Framework будут доступны дополнительные действия и JSLink?**</span><span class="sxs-lookup"><span data-stu-id="14fff-114">**When will custom actions and JSLink be available in the SharePoint Framework?**</span></span>

- <span data-ttu-id="14fff-115">*Дата: 6 июня.*</span><span class="sxs-lookup"><span data-stu-id="14fff-115">*Date - 6th of June*</span></span>

<span data-ttu-id="14fff-116">Расширения SharePoint с дополнительными возможностями настройки для SharePoint Online теперь доступны в виде релиза-кандидата.</span><span class="sxs-lookup"><span data-stu-id="14fff-116">SharePoint Extensions with additional customizations capabilities for the SharePoint Online is now available as Release Candiate release.</span></span> <span data-ttu-id="14fff-117">В настоящий момент дата общей доступности неизвестна.</span><span class="sxs-lookup"><span data-stu-id="14fff-117">We do not have public GA date currently.</span></span> <span data-ttu-id="14fff-118">Чтобы узнать, как создавать эти расширения, прочитайте следующие руководства.</span><span class="sxs-lookup"><span data-stu-id="14fff-118">You can start learning how to build these extensions reading following tutorials.</span></span>

* [<span data-ttu-id="14fff-119">Начало работы с расширениями SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="14fff-119">Getting started with SharePoint Framework Extensions</span></span>](http://aka.ms/spfx-extensions)

<span data-ttu-id="14fff-120">**Будет ли платформа SharePoint Framework доступна локально?**</span><span class="sxs-lookup"><span data-stu-id="14fff-120">**Will SharePoint Framework be available in on-premises?**</span></span>

- <span data-ttu-id="14fff-121">*Дата: 6 июня.*</span><span class="sxs-lookup"><span data-stu-id="14fff-121">*Date - 6th of June*</span></span>
- <span data-ttu-id="14fff-122">*Обновлено: 12 сентября*</span><span class="sxs-lookup"><span data-stu-id="14fff-122">*Updated - 12th of September*</span></span>

<span data-ttu-id="14fff-123">Клиентские веб-части SharePoint Framework теперь доступны в составе SharePoint 2016 с пакетом дополнительных компонентов 2 (FP2).</span><span class="sxs-lookup"><span data-stu-id="14fff-123">SharePoint Framework client-side web parts will be released to SharePoint 2016 as part of the Feature Pack 2 (FP2).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="14fff-124">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="14fff-124">Additional resources</span></span>
<span data-ttu-id="14fff-125">Используйте указанные ниже ресурсы, чтобы отправлять отзывы, комментарии и вопросы, касающиеся разработки решений для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="14fff-125">Please use following resources to provide feedback, comments and questions towards SharePoint engineering.</span></span> 

* [<span data-ttu-id="14fff-126">Список проблем в репозитории sp-dev-docs на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="14fff-126">sp-dev-docs GitHub issue list</span></span>](https://github.com/SharePoint/sp-dev-docs/issues)
* [<span data-ttu-id="14fff-127">Раздел, посвященный разработке решений для SharePoint, на сайте Microsoft Tech Community</span><span class="sxs-lookup"><span data-stu-id="14fff-127">SharePoint Developer MS Tech Community space</span></span>](https://aka.ms/sppnp-community)
