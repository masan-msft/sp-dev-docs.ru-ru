---
title: "План развития SharePoint Framework"
ms.date: 12/15/2017
ms.prod: sharepoint
ms.openlocfilehash: e467c80920855fabcd7e76f174073127139f9795
ms.sourcegitcommit: d24c7dd063a417382e8d0efa83238f08dc349c2c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/22/2018
---
# <a name="sharepoint-framework-roadmap"></a><span data-ttu-id="bd822-102">План развития SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="bd822-102">SharePoint Framework roadmap</span></span>

<span data-ttu-id="bd822-103">Первый выпуск SharePoint Framework поддерживал только клиентские веб-части.</span><span class="sxs-lookup"><span data-stu-id="bd822-103">First release of the SharePoint Framework contained only support for client-side web parts.</span></span> <span data-ttu-id="bd822-104">В дальнейшем современные возможности настройки SharePoint будут расширяться.</span><span class="sxs-lookup"><span data-stu-id="bd822-104">This was however just a start on the journey for providing additional modern customization capabilities to SharePoint.</span></span> <span data-ttu-id="bd822-105">Есть список основных возможностей, выпущенных после выхода общедоступной версии.</span><span class="sxs-lookup"><span data-stu-id="bd822-105">Here is a list of key capabilities released after initial General Availability.</span></span>

- [<span data-ttu-id="bd822-106">Поддержка развертывания на уровне клиента</span><span class="sxs-lookup"><span data-stu-id="bd822-106">Tenant scoped deployment support</span></span>](./tenant-scoped-deployment.md)
- [<span data-ttu-id="bd822-107">Поддержка локальной среды для SharePoint 2016 (пакет дополнительных компонентов 2)</span><span class="sxs-lookup"><span data-stu-id="bd822-107">On-premises support for SharePoint 2016 (Feature Pack 2)</span></span>](./sharepoint-2016-support.md)
- [<span data-ttu-id="bd822-108">Расширения SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="bd822-108">SharePoint Framework Extensions</span></span>](./extensions/overview-extensions.md)
- [<span data-ttu-id="bd822-109">Свойства клиента</span><span class="sxs-lookup"><span data-stu-id="bd822-109">Tenant properties</span></span>](./tenant-properties.md)
- [<span data-ttu-id="bd822-110">API ALM для решений и надстроек SPFx</span><span class="sxs-lookup"><span data-stu-id="bd822-110">ALM APIs for SPFx solutions and add-ins</span></span>](../apis/alm-api-for-spfx-add-ins.md)
- [<span data-ttu-id="bd822-111">Поддержка Office UI Fabric Core</span><span class="sxs-lookup"><span data-stu-id="bd822-111">Office UI Fabric Core support</span></span>](https://dev.office.com/blogs/improved-support-for-office-ui-fabric-core)
- [<span data-ttu-id="bd822-112">Каталог приложений семейства веб-сайтов и упаковка ресурсов</span><span class="sxs-lookup"><span data-stu-id="bd822-112">Asset packaging and site collection app catalog</span></span>](../general-development/site-collection-app-catalog.md)


> [!NOTE]
> <span data-ttu-id="bd822-113">Это список задач, над которыми работают инженеры SharePoint.</span><span class="sxs-lookup"><span data-stu-id="bd822-113">This is a list of areas which SharePoint engineering is having in the backlog and are looking into.</span></span> <span data-ttu-id="bd822-114">Элементы и разделы из этого списка будут постепенно находить воплощение в будущих выпусках SharePoint Framework (**необязательно** все идеи будут реализованы).</span><span class="sxs-lookup"><span data-stu-id="bd822-114">This does **NOT** mean that all of them will be necessarily delivered, but we are looking for getting items and topics from this list gradually released with the future releases of SharePoint Framework.</span></span>

## <a name="general-improvements"></a><span data-ttu-id="bd822-115">Общие улучшения</span><span class="sxs-lookup"><span data-stu-id="bd822-115">General improvements</span></span>

- <span data-ttu-id="bd822-116">Удобство вызова API Graph для доступа к данным пользователей (GraphHttpClient в предварительной версии).</span><span class="sxs-lookup"><span data-stu-id="bd822-116">Easy access to Graph API to access user specific information (GraphHttpClient in preview)</span></span>
- <span data-ttu-id="bd822-117">Веб-перехватчики уровня сайта</span><span class="sxs-lookup"><span data-stu-id="bd822-117">Site level WebHooks</span></span>
- <span data-ttu-id="bd822-118">Обновленные сведения о хранении при поддержке SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="bd822-118">Updated 'store' story with SharePoint Framework support</span></span>
- <span data-ttu-id="bd822-119">Отдел в магазине для решений SharePoint Framework с простым каналом распространения для независимых поставщиков ПО</span><span class="sxs-lookup"><span data-stu-id="bd822-119">'Store' story for SharePoint Framework solutions with easy distribution channel for ISVs</span></span> 

## <a name="client-side-web-parts-and-add-ins"></a><span data-ttu-id="bd822-120">Клиентские веб-части++ и надстройки</span><span class="sxs-lookup"><span data-stu-id="bd822-120">Client-side web parts++ and add-ins</span></span>

- <span data-ttu-id="bd822-121">Поддержка более сложных сценариев и взаимодействий с веб-частями.</span><span class="sxs-lookup"><span data-stu-id="bd822-121">Supporting more complex scenarios and interactions with web parts</span></span>
    - <span data-ttu-id="bd822-122">Обмен данными между веб-частями.</span><span class="sxs-lookup"><span data-stu-id="bd822-122">Part-to-part communication</span></span>
    - <span data-ttu-id="bd822-123">Изоляция платформы JS.</span><span class="sxs-lookup"><span data-stu-id="bd822-123">JS Framework isolation</span></span>
    - <span data-ttu-id="bd822-124">Модель "разработчик-любитель" для простых задач разработки.</span><span class="sxs-lookup"><span data-stu-id="bd822-124">"citizen developer" model for lightweight development</span></span>

- <span data-ttu-id="bd822-125">Реализация современных технологий оформления веб-частей.</span><span class="sxs-lookup"><span data-stu-id="bd822-125">Bring add-ins to the modern world: Let’s make them play nicer with the new UX.</span></span> 
    - <span data-ttu-id="bd822-126">Регистрация в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bd822-126">Azure AD Registration</span></span>
    - <span data-ttu-id="bd822-127">Встроенная поддержка адаптивного дизайна.</span><span class="sxs-lookup"><span data-stu-id="bd822-127">Native responsive support</span></span>
    - <span data-ttu-id="bd822-128">Создание надстроек с помощью SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="bd822-128">Build Add-Ins with SharePoint Framework</span></span>


## <a name="application-lifecycle-management"></a><span data-ttu-id="bd822-129">Управление жизненным циклом приложений</span><span class="sxs-lookup"><span data-stu-id="bd822-129">Application Lifecycle Management</span></span>

- <span data-ttu-id="bd822-130">Упрощенная процедура утверждения: больше не нужно знать администратора клиента.</span><span class="sxs-lookup"><span data-stu-id="bd822-130">Streamlined approval experience: no need to know who your tenant admin is anymore</span></span>
    - <span data-ttu-id="bd822-131">Владелец инициирует процедуру утверждения.</span><span class="sxs-lookup"><span data-stu-id="bd822-131">Owner initiates the approval process</span></span>
    - <span data-ttu-id="bd822-132">Администратор клиента автоматически получает уведомление.</span><span class="sxs-lookup"><span data-stu-id="bd822-132">Tenant admin gets automatically notified</span></span> 
    - <span data-ttu-id="bd822-133">Параметры для управления процедурой утверждения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="bd822-133">Settings to control the default experience around approval process</span></span>


## <a name="developer-experience"></a><span data-ttu-id="bd822-134">Удобство для разработчиков</span><span class="sxs-lookup"><span data-stu-id="bd822-134">Developer Experience</span></span>
- <span data-ttu-id="bd822-135">SharePoint Framework Workbench 2.0: сведения о развертывании касательно расширений SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="bd822-135">SharePoint Framework Workbench 2.0: Development story for SharePoint Framework Extensions</span></span>
- <span data-ttu-id="bd822-136">Компоненты цепочки инструментов.</span><span class="sxs-lookup"><span data-stu-id="bd822-136">Tool Chain Components</span></span>
- <span data-ttu-id="bd822-137">Дополнительные шаблоны Yeoman.</span><span class="sxs-lookup"><span data-stu-id="bd822-137">Additional Yeoman Templates</span></span>

## <a name="already-shipped-capabilities"></a><span data-ttu-id="bd822-138">Возможности, которые уже обеспечены</span><span class="sxs-lookup"><span data-stu-id="bd822-138">Already shipped capabilities</span></span>

<span data-ttu-id="bd822-139">Ниже перечислены возможности, которые уже реализованы.</span><span class="sxs-lookup"><span data-stu-id="bd822-139">Following chapters are listing older items in the roadmap page, which have been already shipped.</span></span>

### <a name="asset-packaging"></a><span data-ttu-id="bd822-140">Упаковка ресурсов</span><span class="sxs-lookup"><span data-stu-id="bd822-140">Asset packaging</span></span>

- <span data-ttu-id="bd822-141">Автоматическое размещение кода в CDN. Добавление пакета JavaScript в пакет приложения, который затем автоматически развертывается в библиотеке, размещаемой в сети CDN Office 365 клиента.</span><span class="sxs-lookup"><span data-stu-id="bd822-141">Automatic CDN hosting for code - Package JavaScript bundle into app package, which is automatically then deployed to a library that gets hosted on your tenant Office 365 CDN</span></span>

### <a name="alm-rest-apis"></a><span data-ttu-id="bd822-142">REST API ALM</span><span class="sxs-lookup"><span data-stu-id="bd822-142">ALM REST APIs</span></span>

- <span data-ttu-id="bd822-143">REST API ALM — развертывание, активация, удаление и обновление приложений и надстроек.</span><span class="sxs-lookup"><span data-stu-id="bd822-143">ALM REST APIs - Deploy, activate, delete and upgrade apps and add-ins</span></span>
- <span data-ttu-id="bd822-144">REST API ALM, поддерживающие *все* объекты в каталоге приложений, в том числе надстройки.</span><span class="sxs-lookup"><span data-stu-id="bd822-144">ALM REST APIs targeted to support *everything* in the App Catalog, including add-ins</span></span>
- <span data-ttu-id="bd822-145">CSOM и командлеты PowerShell, выпущенные по инициативе сообщества разработчиков ПО с открытым исходным кодом.</span><span class="sxs-lookup"><span data-stu-id="bd822-145">CSOM and PowerShell cmdlets released as an open source community initiative</span></span>

### <a name="javascript-embedding-support-jslink-user-custom-actions"></a><span data-ttu-id="bd822-146">Поддержка внедрения JavaScript (JSLink, дополнительные действия пользователей)</span><span class="sxs-lookup"><span data-stu-id="bd822-146">JavaScript embedding support (JSLink, User Custom Actions)</span></span> 

- <span data-ttu-id="bd822-147">Те же цепочка инструментов и модель развертывания, что и для клиентских веб-частей.</span><span class="sxs-lookup"><span data-stu-id="bd822-147">The same tool chain and deployment model as client-side web parts</span></span>
- <span data-ttu-id="bd822-148">Наследование от строго типизированного базового класса везде, где это возможно, вместо прямого управления моделью DOM страницы.</span><span class="sxs-lookup"><span data-stu-id="bd822-148">Derive from a strongly typed base class wherever possible rather than manipulating the page DOM directly.</span></span>
- <span data-ttu-id="bd822-149">Обеспечение использования современных расширений и возможностей, подобных дополнительным действиям и JSLink, в случае классического варианта.</span><span class="sxs-lookup"><span data-stu-id="bd822-149">Enable modern extension usage with modern experiences similar as Custom Actions and JS Link in classic experience</span></span>
- <span data-ttu-id="bd822-150">Работа с NoScript через каталог приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="bd822-150">Work with NoScript via tenant app catalog</span></span>

### <a name="on-premises-support---sharepoint-2016-feature-pack-2"></a><span data-ttu-id="bd822-151">SharePoint 2016 с пакетом дополнительных компонентов 2: поддержка локальной среды</span><span class="sxs-lookup"><span data-stu-id="bd822-151">On-premises support - Sharepoint 2016 Feature Pack 2</span></span>

- <span data-ttu-id="bd822-152">Предоставление в составе пакета дополнительных компонентов 2 для SharePoint 2016.</span><span class="sxs-lookup"><span data-stu-id="bd822-152">Shipping as part of Feature Pack 2 for SharePoint 2016</span></span>
- <span data-ttu-id="bd822-153">Те же возможности, что и в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="bd822-153">Similar feature capabilities as in SharePoint Online</span></span>
- <span data-ttu-id="bd822-154">Предоставление общей платформы разработки в локальной среде и облаке.</span><span class="sxs-lookup"><span data-stu-id="bd822-154">Target is to provide common development platform across on-premises and the cloud</span></span>
- <span data-ttu-id="bd822-155">Использование современной цепочки инструментов и открытого кода в локальных средах.</span><span class="sxs-lookup"><span data-stu-id="bd822-155">Leveraging modern toolchain and open source on on-premises environments</span></span>
- <span data-ttu-id="bd822-156">Ориентация на версию SharePoint 2016 в 2017 г.</span><span class="sxs-lookup"><span data-stu-id="bd822-156">Targeting SharePoint 2016 version during calendar year 2017</span></span>


## <a name="see-also"></a><span data-ttu-id="bd822-157">См. также</span><span class="sxs-lookup"><span data-stu-id="bd822-157">See also</span></span>
<span data-ttu-id="bd822-158">Узнавайте о новых выпусках и возможностях SharePoint Framework из следующих ресурсов.</span><span class="sxs-lookup"><span data-stu-id="bd822-158">Please use following resources to stay up to date on the new releases and capabilities being released for SharePoint Framework.</span></span>

* [<span data-ttu-id="bd822-159">dev.office.com blog</span><span class="sxs-lookup"><span data-stu-id="bd822-159">dev.office.com blog</span></span>](https://dev.office.com/blogs)
* [<span data-ttu-id="bd822-160">Учетная запись OfficeDev в Твиттере</span><span class="sxs-lookup"><span data-stu-id="bd822-160">OfficeDev Twitter account</span></span>](https://twitter.com/officedev)
