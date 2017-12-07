---
title: "План развития SharePoint Framework"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: a5097e0f7d465ab00c5c7a76a8ee78e10f737d7d
ms.sourcegitcommit: 11d9185437fc819ab41421c0f4fe06aa300b9d28
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/25/2017
---
# <a name="sharepoint-framework-roadmap"></a><span data-ttu-id="0679c-102">План развития SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="0679c-102">SharePoint Framework roadmap</span></span>

<span data-ttu-id="0679c-103">Первый выпуск SharePoint Framework поддерживал только клиентские веб-части.</span><span class="sxs-lookup"><span data-stu-id="0679c-103">First release of the SharePoint Framework contained only support for client-side web parts.</span></span> <span data-ttu-id="0679c-104">В дальнейшем современные возможности настройки SharePoint будут расширяться.</span><span class="sxs-lookup"><span data-stu-id="0679c-104">This was however just a start on the journey for providing additional modern customization capabilities to SharePoint.</span></span> <span data-ttu-id="0679c-105">Есть список основных возможностей, выпущенных после выхода общедоступной версии.</span><span class="sxs-lookup"><span data-stu-id="0679c-105">Here is a list of key capabilities released after initial General Availability.</span></span>

- [<span data-ttu-id="0679c-106">Поддержка развертывания на уровне клиента</span><span class="sxs-lookup"><span data-stu-id="0679c-106">Tenant scoped deployment support</span></span>](./tenant-scoped-deployment.md)
- [<span data-ttu-id="0679c-107">Поддержка локальной среды для SharePoint 2016 (пакет дополнительных компонентов 2)</span><span class="sxs-lookup"><span data-stu-id="0679c-107">On-premises support for SharePoint 2016 (Feature Pack 2)</span></span>](./sharepoint-2016-support.md)
- [<span data-ttu-id="0679c-108">Расширения SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="0679c-108">Getting started with SharePoint Framework Extensions</span></span>](./extensions/overview-extensions.md)
- [<span data-ttu-id="0679c-109">Свойства клиента</span><span class="sxs-lookup"><span data-stu-id="0679c-109">Tenant properties</span></span>](./tenant-properties.md)


> [!NOTE]
> <span data-ttu-id="0679c-110">Это список областей, над которыми работают инженеры SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0679c-110">This is a list of areas which SharePoint engineering is having in the backlog and are looking into.</span></span> <span data-ttu-id="0679c-111">Элементы и разделы из этого списка будут постепенно находить воплощение в будущих выпусках SharePoint Framework (**необязательно** все идеи будут реализованы).</span><span class="sxs-lookup"><span data-stu-id="0679c-111">Notice. This is a list of areas which SharePoint engineering is having in the backlog and are looking into. This does **NOT** mean that all of them will be necessarily delivered, but we are looking for getting items and topics from this list gradually released with the future releases of SharePoint Framework.</span></span>

## <a name="general-improvements"></a><span data-ttu-id="0679c-112">Общие улучшения</span><span class="sxs-lookup"><span data-stu-id="0679c-112">General improvements</span></span>

- <span data-ttu-id="0679c-113">Удобство вызова API Graph для доступа к данным пользователей (GraphHttpClient в предварительной версии)</span><span class="sxs-lookup"><span data-stu-id="0679c-113">Easy access to Graph API to access user specific information (GraphHttpClient in dev preview)</span></span>
- <span data-ttu-id="0679c-114">Каталог приложений семейства веб-сайтов с управлением на уровне клиента для обеспечения более простого развертывания решений к концу 2017 года</span><span class="sxs-lookup"><span data-stu-id="0679c-114">Site collection app catalog with tenant level control for enabling easier solution deployed</span></span>
- <span data-ttu-id="0679c-115">Веб-перехватчики уровня сайта</span><span class="sxs-lookup"><span data-stu-id="0679c-115">Site level WebHooks</span></span>
- <span data-ttu-id="0679c-116">Поддержка Office UI Fabric Core</span><span class="sxs-lookup"><span data-stu-id="0679c-116">Office UI Fabric Core</span></span>

## <a name="client-side-web-parts-and-add-ins"></a><span data-ttu-id="0679c-117">Клиентские веб-части++ и надстройки</span><span class="sxs-lookup"><span data-stu-id="0679c-117">Client-side web parts++ and add-ins</span></span>

- <span data-ttu-id="0679c-118">Поддержка более сложных сценариев и взаимодействий с веб-частями</span><span class="sxs-lookup"><span data-stu-id="0679c-118">Supporting more complex scenarios and interactions with web parts</span></span>
    - <span data-ttu-id="0679c-119">Обмен данными между веб-частями</span><span class="sxs-lookup"><span data-stu-id="0679c-119">Part-to-part communication</span></span>
    - <span data-ttu-id="0679c-120">Изоляция платформы JS</span><span class="sxs-lookup"><span data-stu-id="0679c-120">JS Framework isolation</span></span>
    - <span data-ttu-id="0679c-121">Модель "разработчик-любитель" для простых задач разработки</span><span class="sxs-lookup"><span data-stu-id="0679c-121">"citizen developer" model for lightweight development</span></span>

- <span data-ttu-id="0679c-122">Реализация современных технологий оформления веб-частей.</span><span class="sxs-lookup"><span data-stu-id="0679c-122">Bring add-ins to the modern world: Let’s make them play nicer with the new UX.</span></span> 
    - <span data-ttu-id="0679c-123">Регистрация в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0679c-123">Azure AD Registration</span></span>
    - <span data-ttu-id="0679c-124">Встроенная поддержка адаптивного дизайна</span><span class="sxs-lookup"><span data-stu-id="0679c-124">Native responsive support</span></span>
    - <span data-ttu-id="0679c-125">Создание надстроек с помощью SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="0679c-125">Build Add-Ins with SharePoint Framework</span></span>


## <a name="application-lifecycle-management"></a><span data-ttu-id="0679c-126">Управление жизненным циклом приложений</span><span class="sxs-lookup"><span data-stu-id="0679c-126">Application Lifecycle Management</span></span>

- <span data-ttu-id="0679c-127">Упрощенная процедура утверждения: больше не нужно знать администратора клиента.</span><span class="sxs-lookup"><span data-stu-id="0679c-127">Streamlined approval experience: no need to know who your tenant admin is anymore</span></span>
    - <span data-ttu-id="0679c-128">Владелец инициирует процедуру утверждения.</span><span class="sxs-lookup"><span data-stu-id="0679c-128">Owner initiate the approval process</span></span>
    - <span data-ttu-id="0679c-129">Администратор клиента автоматически получает уведомление.</span><span class="sxs-lookup"><span data-stu-id="0679c-129">Tenant admin gets automatically notified</span></span> 
    - <span data-ttu-id="0679c-130">Параметры управления процедурой утверждения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="0679c-130">Settings to control the default experience around approval process</span></span>

- <span data-ttu-id="0679c-131">ALM REST API — развертывание, активация, удаление и обновление приложений и надстроек.</span><span class="sxs-lookup"><span data-stu-id="0679c-131">ALM REST APIs - Deploy, activate, delete and upgrade apps and add-ins</span></span>
- <span data-ttu-id="0679c-132">Предполагается, что ALM REST API будут поддерживать *все* объекты в каталоге приложений, в том числе надстройки.</span><span class="sxs-lookup"><span data-stu-id="0679c-132">ALM REST APIs targeted to support *everything* in the App Catalog, including add-ins</span></span>
- <span data-ttu-id="0679c-133">Автоматическое размещение кода в CDN.</span><span class="sxs-lookup"><span data-stu-id="0679c-133">Automatic CDN hosting for code</span></span>
    - <span data-ttu-id="0679c-134">Добавление пакета JavaScript в пакет приложения, который затем автоматически развертывается в библиотеке, размещаемой в сети CDN Office 365 клиента.</span><span class="sxs-lookup"><span data-stu-id="0679c-134">Package JavaScript bundle into app package, which is automatically then deployed to a library that gets hosted on your tenant Office 365 CDN</span></span>


## <a name="developer-experience"></a><span data-ttu-id="0679c-135">Удобство для разработчиков</span><span class="sxs-lookup"><span data-stu-id="0679c-135">Developer Experience</span></span>
- <span data-ttu-id="0679c-136">SharePoint Framework Workbench 2.0: сведения о развертывании касательно расширений SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="0679c-136">SharePoint Framework Workbench 2.0: Development story for SharePoint Framework Extensions</span></span>
- <span data-ttu-id="0679c-137">Компоненты цепочки инструментов.</span><span class="sxs-lookup"><span data-stu-id="0679c-137">Tool Chain Components</span></span>
- <span data-ttu-id="0679c-138">Дополнительные шаблоны Yeoman.</span><span class="sxs-lookup"><span data-stu-id="0679c-138">Additional Yeoman Templates</span></span>

## <a name="already-shipped-capabilities"></a><span data-ttu-id="0679c-139">Возможности, которые уже обеспечены</span><span class="sxs-lookup"><span data-stu-id="0679c-139">Already shipped capabilities</span></span>

<span data-ttu-id="0679c-140">В приведенных ниже разделах указаны более старые элементы страницы с планом развития, которые уже доступны.</span><span class="sxs-lookup"><span data-stu-id="0679c-140">Following chapters are listing older items in the roadmap page, which have been already shipped.</span></span>

### <a name="javascript-embedding-support-jslink-user-custom-actions"></a><span data-ttu-id="0679c-141">Поддержка внедрения JavaScript (JSLink, дополнительные действия пользователей)</span><span class="sxs-lookup"><span data-stu-id="0679c-141">JavaScript embedding support (JSLink, User Custom Actions)</span></span> 

- <span data-ttu-id="0679c-142">Те же цепочка инструментов и модель развертывания, что и для клиентских веб-частей.</span><span class="sxs-lookup"><span data-stu-id="0679c-142">The same tool chain and deployment model as client-side web parts</span></span>
- <span data-ttu-id="0679c-143">Наследование от строго типизированного базового класса везде, где это возможно, вместо прямого управления моделью DOM страницы.</span><span class="sxs-lookup"><span data-stu-id="0679c-143">Derive from a strongly typed base class wherever possible rather than manipulating the page DOM directly.</span></span>
- <span data-ttu-id="0679c-144">Обеспечение использования современных расширений и возможностей, подобных дополнительным действиям и JSLink, в случае классического варианта.</span><span class="sxs-lookup"><span data-stu-id="0679c-144">Enable modern extension usage with modern experiences similar as Custom Actions and JS Link in classic experience</span></span>
- <span data-ttu-id="0679c-145">Работа с NoScript через каталог приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="0679c-145">Work with NoScript via tenant app catalog</span></span>

### <a name="on-premises-support---sharepoint-2016-feature-pack-2"></a><span data-ttu-id="0679c-146">SharePoint 2016 с пакетом дополнительных компонентов 2: поддержка локальной среды</span><span class="sxs-lookup"><span data-stu-id="0679c-146">On-premises support - Sharepoint 2016 Feature Pack 2</span></span>

- <span data-ttu-id="0679c-147">Предоставление в составе пакета дополнительных компонентов 2 для SharePoint 2016.</span><span class="sxs-lookup"><span data-stu-id="0679c-147">Shipping as part of Feature Pack 2 for SharePoint 2016</span></span>
- <span data-ttu-id="0679c-148">Те же возможности, что и в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="0679c-148">Similar feature capabilities as in SharePoint Online</span></span>
- <span data-ttu-id="0679c-149">Предоставление общей платформы разработки в локальной среде и облаке.</span><span class="sxs-lookup"><span data-stu-id="0679c-149">Target is to provide common development platform across on-premises and the cloud</span></span>
- <span data-ttu-id="0679c-150">Использование современной цепочки инструментов и открытого кода в локальных средах.</span><span class="sxs-lookup"><span data-stu-id="0679c-150">Leveraging modern toolchain and open source on on-premises environments</span></span>
- <span data-ttu-id="0679c-151">Ориентация на версию SharePoint 2016 в 2017 г.</span><span class="sxs-lookup"><span data-stu-id="0679c-151">Targeting SharePoint 2016 version during calendar year 2017</span></span>


## <a name="additional-resources"></a><span data-ttu-id="0679c-152">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="0679c-152">Additional resources</span></span>
<span data-ttu-id="0679c-153">Узнавайте о новых выпусках и возможностях SharePoint Framework из следующих ресурсов.</span><span class="sxs-lookup"><span data-stu-id="0679c-153">Please use following resources to stay up to date on the new releases and capabilities being released for SharePoint Framework.</span></span>

* [<span data-ttu-id="0679c-154">dev.office.com blog</span><span class="sxs-lookup"><span data-stu-id="0679c-154">dev.office.com blog</span></span>](https://dev.office.com/blogs)
* [<span data-ttu-id="0679c-155">Учетная запись OfficeDev в Твиттере</span><span class="sxs-lookup"><span data-stu-id="0679c-155">OfficeDev Twitter account</span></span>](https://twitter.com/officedev)
